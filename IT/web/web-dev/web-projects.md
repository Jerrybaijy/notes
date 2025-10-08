---
title: web-projects
author: Jerry.Baijy
tags:
  - it
  - web
---

# 员工管理系统（web）

- 这是一个训练案例，预先安装 MySQL。
- flask 框架、前端、MySQL

## 创建数据库和表结构

- 使用终端创建

    - 创建数据库：`unicom`
    - 创建数据表：`admin`
    - 按格式先添加几条数据

    ```
    表名：admin
    结构
      id bigint unsigned primary key auto_increment not null,
      username varchar(16) not null,
      password varchar(16) not null,
        mobile char(11) not null
    ```

    ```sql
    create database unicom default charset=utf8;
    
    use unicom;
    
    create table admin(
    id bigint unsigned primary key auto_increment not null,
    username varchar(16) not null,
    password varchar(16) not null,
      mobile char(11) not null
    )default charset=utf8;
    ```

## 创建 Flask 框架

- Flask 框架和 HTML 文件

    ```python
    from flask import Flask, render_template
    app = Flask(__name__)
    @app.route('/home')
    def home():
        return render_template('home.html')
    if __name__ == '__main__':
        app.run()
    ```

## 连接MySQL

- 连接 MySQL 获取数据并以 `n2` 传入 HTML

    ```python
    conn = pymysql.Connect(
        host="localhost",
        port=3306,
        user="root",
        password="123456",
        charset="utf8",
        database="unicom",
    )
    print("MySQL已连接.....")
    cursor = conn.cursor(cursor=DictCursor)
    cursor.execute("select id, username, password, mobile from admin")
    user_list = cursor.fetchall()
    cursor.close()
    conn.close()
    return render_template("home.html", n2=user_list)
    ```

- 同时在 `render_template` 里添加 `n2 = user_list`

## HTML接收数据并渲染

- 使用 `for 循环` 接收数据

    ```html
    <table border="1">
      <thead>
        <tr>
          <th>ID</th>
          <th>姓名</th>
          <th>密码</th>
          <th>手机号</th>
        </tr>
      </thead>
      <tbody>
        {% for item in n2%}
        <tr>
          <td>{{item.id}}</td>
          <td>{{item.username}}</td>
          <td>{{item.password}}</td>
          <td>{{item.mobile}}</td>
        </tr>
        {% endfor %}
      </tbody>
    </table>
    ```

## CSS美化

- 引入 BootStrap

    ```html
    <div class="container">
        <table class="table table-bordered">...</table>
    </div>
    ```

## HTML 添加数据

- 添加数据库以外内容

    ```html
    <td>
      <a class="btn btn-danger btn-xs">删除</a>
    </td>
    ```

## 获取 id 并删除数据行

- 获取 `id` 并删除数据行

    ```html
    <td>
      <a href="/admin/delete?aid={{ item.id }}" class="btn btn-danger btn-xs">删除</a>
    </td>
    ```

    ``` python
    @app.route("/admin/delete")
    def admin_delete():
        # 获取 id
        aid = request.args.get("aid")
      
        # 连接 MySQL
        conn = pymysql.Connect(
            host="localhost",
            port=3306,
            user="root",
            password="123456",
            charset="utf8",
            database="unicom",
        )
        print("MySQL已连接.....")
        cursor = conn.cursor(cursor=DictCursor)
      
        # 删除数据行
        cursor.execute("delete from admin where id=%s", [aid])
        conn.commit()
        return redirect("/home")  # 返回 home
    ```

    **在以上代码中**

    - 同时引入 `request`，`redirect`
    - `aid` 为 HTML 中接收浏览器返回内容的变量 