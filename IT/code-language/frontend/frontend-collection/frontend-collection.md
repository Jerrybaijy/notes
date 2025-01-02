# 前端基础

## 概述

- 前端开发是创建 WEB 页面或 APP 等前端界面呈现给用户的过程，通过 HTML、CSS 及 JavaScript 以及衍生出来的各种技术、框架、解决方案，来实现互联网产品的用户界面交互。
- 前端三剑客
  - **HTML**：结构层  从语义角度描述页面结构
  - **CSS**：样式层  从美观角度描述页面样式
  - **JavaScript**：行为层  从交互角度描述页面行为

## 文件处理

1. 创建一个名为 `web-projects` 的新文件夹。这是你所有的网站项目的存放地。
2. 在 `web-projects` 中，创建名为 `test-site` 的文件夹来存放你的第一个网站。
3. 项目结构

   - **`index.html` 文件**
   - **`images` 文件夹**：存图片
   - **`styles` 文件夹**：存 CSS 文件
   - **`scripts` 文件夹**：存 JS 文件
4. 文件名符合规范，详见 `计算机基础` > `文件名`
5. **引用文件**：详见 `计算机基础` > `路径`

# BootStrap 框架

Bootstrap 是一个流行的开源前端框架，用于快速开发响应式和移动优先的网站及应用程序。它由 Twitter 团队开发和维护，提供了一系列预制的 HTML、CSS、JavaScript 和图标，帮助开发者构建具有一致外观和交互功能的网页界面，而无需从头开始编写大量的样式和脚本。

## Bootstrap 核心组成

Bootstrap 包含以下核心部分：

1. **CSS 样式库**：
    - 提供了一整套预定义的样式，如布局、按钮、表格、表单、排版等。
    - 核心文件：`bootstrap.min.css`。
2. **JavaScript 插件**：
    - 提供交互组件，如模态框（Modal）、轮播图（Carousel）、下拉菜单（Dropdown）等。
    - 核心文件：`bootstrap.bundle.min.js`，包含原生 JavaScript 和依赖的 Popper.js。
3. **Icons 图标库**：
    - Bootstrap 提供了独立的图标库，支持数千种矢量图标。
    - 文件：`bootstrap-icons.css`。
4. **工具类（Utility Classes）**：
    - 预定义的工具类帮助快速调整布局和样式，如间距、颜色、显示控制等。

## BootStrap 基础

### Bootstrap 引入方式

#### 使用 CDN 引入

- [Bootstrap 官网](https://v5.bootcss.com/) > `Docs` > `Introduction` > [CDN links](https://v5.bootcss.com/docs/getting-started/introduction/#cdn-links)
- [Bootstrap 官网](https://v5.bootcss.com/) > `Icons` > CDN
- 在 `CDN links` 中复制 Bootstrap 的 CDN 地址，在 HTML 文件 `<head>` 元素中引入 Bootstrap 的 CSS 样式和图标样式，在 `<body>` 底部引入 JS 组件。

    > CSS：https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css
    > 
    > Icons：https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css
    > 
    > JS：https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js
    
    ```html
    <head>
      <!-- 使用 CDN 引入 Bootstrap 的 CSS 样式表 -->
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css">
      
      <!-- 使用 CDN 引入 Bootstrap 的图标样式表 -->
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
    </head>
    
    <body>
      <!-- 其它 body 元素 -->
    
      <!-- 使用 CDN 引入 Bootstrap 的 JS 组件 -->
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
    </body>
    ```
    

#### 本地引入

1. [官网下载 Bootstrap](https://github.com/twbs/bootstrap/releases/download/v5.3.0-alpha1/bootstrap-5.3.0-alpha1-dist.zip)
2. 下载 BootStrap 文件并解压，文件夹名字改为 `bootStrap`，与 HTML 文件放入同级目录。

    ```html
    <head>
      <!-- 本地引入 Bootstrap 的样式表-->
      <link rel="stylesheet" href="bootstrap/css/bootstrap.css">
    </head>
    <body>
      <!-- 其它 body 元素 -->
    
      <!-- 本地引入 Bootstrap 的JS组件 -->
      <script src="bootStrap/js/bootstrap.bundle.min.js"></script>
    </body>
    ```

### jQuery 依赖

- 从 Bootstrap4 开始，移除了对 `JS组件` 对 `jQuery` 的硬性依赖，如果使用的是 Bootstrap4 以前的版本，在引入 `JS组件` 时，应事先引入 jQuery。

- **引入方式**

    ```html
    <body>
      <!-- 其它 body 元素 -->
    
      <script src="js/jquery-3.7.1.min.js"></script>
      <!-- bootstrap.js 需要依赖 jquery，所以要在 jquery 后面引入 -->
      <script src="bootstrap/js/bootstrap.js"></script>
    </body>
    ```

### 基本语法

1. 实际就是去 Bootstrap 官网找喜欢的样式，然后把它们的 HTML 粘贴到自己的代码中；
2. 首先引入 Bootstrap 的 `CSS 样式表` 和 `JS 组件`；
3. 比如想做一个按钮，就去 Bootstrap 官网中文文档找 [Buttons](https://v5.bootcss.com/docs/components/buttons/)；
4. 然后把喜欢的图标的 HTML 代码复制到自己的代码中；

    ```html
	<head>
      <!-- 使用 CDN 引入 Bootstrap 的样式表 -->
	  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css">
	</head>
	
	<body>
	  <!-- 这是从 Bootstrap 复制过来的 -->
	  <button type="button" class="btn btn-primary">Primary</button>
	  
	  <!-- 其它 body 元素 -->
	
	  <!-- 使用 CDN 引入 Bootstrap 的JS组件 -->
	  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
	</body>
	```
	
5. 这样无需自己设置 CSS 和 JavaScript，也能达到 BootStrap 所展示的效果。

## 栅格系统

- **语法**：将父级标签（整行/整块）分成12份，针对12份布局，所有栅格自带 float 属性，以分成3块为例
	
	``` html
  <!--将一整行分3份-->
  <div class="container">
    <div class="row">
      <div class="col - sm - 4">左</div>
      <div class="col - sm - 4">中</div>
      <div class="col - sm - 4">右</div>
    </div>
  </div>
  
  <!--将500px宽度分3份-->
  <div style="width:500px;margin:0 auto;">
    <div class="d-flex" style="flex-basis:100%;">
      <div class="flex-grow-1" style="flex-basis:0;">左</div>
	    <div class="flex-grow-1" style="flex-basis:0;">中</div>
	    <div class="flex-grow-1" style="flex-basis:0;">右</div>
	  </div>
	</div>
	```


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
          host = "localhost",
          port = 3306,
          user = "root",
          password = "123456",
          charset = "utf8",
          database = "unicom"
  )
  print("MySQL已连接.....")
  cursor = conn.cursor(cursor = DictCursor)
  cursor.execute("select id, username, password, mobile from admin")
  user_list = cursor.fetchall()
  cursor.close()
  conn.close()
  return render_template('home.html',n2 = user_list)
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
  @app.route('/admin/delete')
  def admin_delete():
      # 获取 id
      aid = request.args.get("aid")
  
      # 连接 MySQL
      conn = pymysql.Connect(
          host = "localhost",
          port = 3306,
          user = "root",
          password = "123456",
          charset = "utf8",
          database = "unicom"
      )
      print("MySQL已连接.....")
      cursor = conn.cursor(cursor = DictCursor)
  
      # 删除数据行
      cursor.execute("delete from admin where id=%s", [aid])
      conn.commit()
      return redirect('/home')  # 返回 home
  ```

  - 同时引入 `request`，`redirect`
  - `aid` 为 HTML 中接收浏览器返回内容的变量 
