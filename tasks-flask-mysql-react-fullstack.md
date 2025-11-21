---
title: tasks-flask-mysql-react-fullstack
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - projects
  - flask
  - mysql
  - react
  - fullstack
---

# Tasks Flask MySQL React Fullstack

## 概述

## 后端

### 环境和依赖

- 创建虚拟环境

- 安装依赖

  ```bash
  pip install Flask Flask-CORS Flask-SQLAlchemy pymysql
  ```

### 代码

```python
from flask import Flask, request, jsonify
from flask_cors import CORS
from flask_sqlalchemy import SQLAlchemy
from sqlalchemy import exc

# --- 1. 初始化 Flask 应用和配置 ---
app = Flask(__name__)
# 允许跨域请求
CORS(app) 

# MySQL 数据库配置：连接到 Docker 容器
# 格式: mysql+pymysql://<user>:<password>@<host>:<port>/<db_name>
app.config['SQLALCHEMY_DATABASE_URI'] = \
    'mysql+pymysql://root:000000@localhost:3306/todo_db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

# --- 2. 定义数据库模型 (Task) ---
class Task(db.Model):
    __tablename__ = 'tasks'
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100), nullable=False)
    done = db.Column(db.Boolean, default=False)

    def to_dict(self):
        # 转换为字典，方便 JSON 序列化
        return {
            'id': self.id,
            'title': self.title,
            'done': self.done
        }

# --- 3. 定义 API 路由 ---

# 获取所有任务 (GET /api/tasks)
@app.route('/api/tasks', methods=['GET'])
def get_tasks():
    tasks = Task.query.all()
    # 使用列表推导式将所有 Task 对象转换为字典列表
    return jsonify([task.to_dict() for task in tasks])

# 创建新任务 (POST /api/tasks)
@app.route('/api/tasks', methods=['POST'])
def add_task():
    if not request.json or 'title' not in request.json:
        return jsonify({'message': 'Missing title'}), 400
    
    new_task = Task(title=request.json['title'])
    db.session.add(new_task)
    db.session.commit()
    return jsonify(new_task.to_dict()), 201 # 201 Created

# 更新任务状态 (PUT /api/tasks/<id>)
@app.route('/api/tasks/<int:task_id>', methods=['PUT'])
def update_task(task_id):
    task = Task.query.get_or_404(task_id)
    
    if 'title' in request.json:
        task.title = request.json['title']
    if 'done' in request.json:
        task.done = request.json['done']
    
    db.session.commit()
    return jsonify(task.to_dict())

# 删除任务 (DELETE /api/tasks/<id>)
@app.route('/api/tasks/<int:task_id>', methods=['DELETE'])
def delete_task(task_id):
    task = Task.query.get_or_404(task_id)
    db.session.delete(task)
    db.session.commit()
    return jsonify({'message': 'Task deleted'}), 204 # 204 No Content

# --- 4. 启动应用 (包含数据库初始化) ---
if __name__ == '__main__':
    # 解决 @app.before_first_request 废弃的问题：在应用上下文中创建数据库表
    try:
        with app.app_context():
            db.create_all()
        print("Database tables created or already exist.")
    except exc.OperationalError as e:
        print(f"Error connecting to database. Is the Docker MySQL container running? Error: {e}")
        # 即使连接失败，应用也可能继续运行，但 API 调用会失败
    
    # 默认运行在 http://127.0.0.1:5000/
    app.run(debug=True)
```

## 数据库

### 创建容器化 MySQL

```bash
docker run --name mysql-app-db \
-e MYSQL_ROOT_PASSWORD=000000 \
-e MYSQL_DATABASE=tasks_flask_react_db \
-p 3306:3306 \
-d mysql:8.0
```

## 前端

