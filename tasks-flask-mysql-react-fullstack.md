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

  ```
  # requirements.txt
  
  Flask
  Flask-SQLAlchemy
  Flask-CORS
  pymysql
  ```
  
  ```bash
  pip install -r requirements.txt
  ```

### `app.py`

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
    'mysql+pymysql://root:000000@localhost:3306/tasks_db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

# 创建 Flask-SQLAlchemy 实例
db = SQLAlchemy(app)

# --- 2. 定义数据库模型 (Task) ---
class Task(db.Model):
    __tablename__ = 'tasks_tb' # table 名称
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

**创建容器化 MySQL：**

```bash
docker run --name tasks-flask-mysql-react-fullstack \
-e MYSQL_ROOT_PASSWORD=000000 \
-e MYSQL_DATABASE=tasks_db \
-p 3306:3306 \
-d mysql:8.0
```

**启动后端：**

```python
python app.py
```

## 前端

### 创建项目及安装依赖

创建前端项目文件夹：

```bash
npx create-react-app tasks-flask-mysql-react-frontend
```

进入前端项目目录，安装依赖：

```bash
cd tasks-flask-mysql-react-frontend
npm install
```

### `src/App.js`

```javascript
import React, { useState, useEffect } from 'react';
import './App.css'; // 稍后您可以在 App.css 中添加样式

const API_URL = 'http://localhost:5000/api/tasks'; // 指向您的 Flask 后端地址

function App() {
  const [tasks, setTasks] = useState([]);
  const [newTaskTitle, setNewTaskTitle] = useState('');

  // --- 1. 获取任务列表 ---
  const fetchTasks = async () => {
    try {
      const response = await fetch(API_URL);
      const data = await response.json();
      setTasks(data);
    } catch (error) {
      console.error('获取任务失败:', error);
    }
  };

  // 组件首次加载时调用
  useEffect(() => {
    fetchTasks();
  }, []);

  // --- 2. 添加新任务 ---
  const handleAddTask = async (e) => {
    e.preventDefault();
    if (!newTaskTitle.trim()) return;

    try {
      await fetch(API_URL, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ title: newTaskTitle }),
      });
      setNewTaskTitle(''); // 清空输入框
      fetchTasks(); // 重新加载任务列表
    } catch (error) {
      console.error('添加任务失败:', error);
    }
  };

  // --- 3. 切换任务完成状态 ---
  const handleToggleDone = async (task) => {
    try {
      await fetch(`${API_URL}/${task.id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ done: !task.done }),
      });
      fetchTasks(); // 重新加载任务列表
    } catch (error) {
      console.error('更新任务状态失败:', error);
    }
  };

  // --- 4. 删除任务 ---
  const handleDeleteTask = async (id) => {
    try {
      await fetch(`${API_URL}/${id}`, {
        method: 'DELETE',
      });
      // 优化：直接从前端状态中移除，避免完全重新加载
      setTasks(tasks.filter(task => task.id !== id));
    } catch (error) {
      console.error('删除任务失败:', error);
    }
  };

  return (
    <div className="App">
      <h1>任务管理 (React + Flask + MySQL)</h1>

      {/* 添加任务表单 */}
      <form onSubmit={handleAddTask}>
        <input
          type="text"
          value={newTaskTitle}
          onChange={(e) => setNewTaskTitle(e.target.value)}
          placeholder="输入新任务..."
        />
        <button type="submit">添加任务</button>
      </form>

      {/* 任务列表 */}
      <ul>
        {tasks.map((task) => (
          <li key={task.id} style={{ textDecoration: task.done ? 'line-through' : 'none' }}>
            <input
              type="checkbox"
              checked={task.done}
              onChange={() => handleToggleDone(task)}
            />
            {task.title}
            <button onClick={() => handleDeleteTask(task.id)} style={{ marginLeft: '10px' }}>
              删除
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```

### `src/index.js`

### `src/reportWebVitals.js`

### 启动前端

```bash
npm run dev
```



