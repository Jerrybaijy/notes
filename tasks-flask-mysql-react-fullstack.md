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

## 后端及数据库

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

### 数据库

**创建容器化 MySQL：**

```bash
docker run --name tasks-flask-mysql-react-db \
-e MYSQL_ROOT_PASSWORD=000000 \
-e MYSQL_DATABASE=tasks_db \
-p 3306:3306 \
-d mysql:8.0
```

**启动后端：**

```python
python app.py
```

### `Dockerfile`

```dockerfile
# 使用官方的 Python 瘦身版作为基础镜像
FROM python:3.10-slim

# 设置工作目录
WORKDIR /app

# 复制 requirements.txt 并安装依赖
# 这一步优先执行，可以利用 Docker 缓存
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 复制所有的源代码
COPY . .

# 暴露 Flask 应用的默认端口
EXPOSE 5000

# 运行 Gunicorn 或其他生产级 WSGI 服务器是最佳实践，
# 但为了保持简单性，我们使用您代码中的开发模式启动方式
# 假设您的主文件是 app.py
CMD ["python", "app.py"]
```

### `.gitlab-ci.yml`

```yaml
variables:
  # 您的 Docker Hub 用户名
  DOCKER_USER: $DOCKER_HUB_USERNAME 
  # 您的 Docker Hub 密码/令牌
  DOCKER_PASSWORD: $DOCKER_HUB_PASSWORD 
  # 镜像名称（例如：jerrybaijy/tasks-backend-image）
  IMAGE_NAME: $DOCKER_IMAGE_NAME 
  # 使用动态标签：[分支名]-[短提交SHA]，确保版本唯一性
  IMAGE_TAG: $CI_COMMIT_REF_SLUG-$CI_COMMIT_SHORT_SHA 
  # DIND 必要的配置
  DOCKER_TLS_CERTDIR: ""

stages:
  - build_and_push

build_backend_image:
  stage: build_and_push
  # 沿用您指定的 Docker 镜像版本
  image: docker:20.10.20
  services:
    - docker:20.10.20-dind
  
  # 仅在主分支或打 Tag 时运行
  only:
    - main
    - master
    - tags

  before_script:
    # 1. 安全登录 Docker Hub（将密码通过标准输入传递）
    - echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USER" --password-stdin
  
  script:
    # 2. 构建 Docker 镜像
    - docker build -t $IMAGE_NAME:$IMAGE_TAG .
    
    # 3. 推送带版本号的镜像
    - docker push $IMAGE_NAME:$IMAGE_TAG
    
    # 4. 额外步骤：如果是在 main/master 分支，推送 :latest 标签
    - |
      if [ "$CI_COMMIT_REF_NAME" = "main" ] || [ "$CI_COMMIT_REF_NAME" = "master" ]; then
        LATEST_TAG=$IMAGE_NAME:latest
        docker tag $IMAGE_NAME:$IMAGE_TAG $LATEST_TAG
        echo "Pushing latest tag..."
        docker push $LATEST_TAG
      fi

  after_script:
    # 安全登出
    - docker logout
```

### GitLab CI

根据 `Dockerfile` 和 `.gitlab-ci.yml` 进行 CI，构建镜像并推送至 Docker Hub。

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

主组件 `src/App.js`

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

### `src/main.jsx`

入口文件 `src/main.jsx`

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

reportWebVitals();
```

**在以上代码中：**

- `<App />`：引入主组件

### `src/reportWebVitals.js`

性能报告

```javascript
const reportWebVitals = onPerfEntry => {
  if (onPerfEntry && onPerfEntry instanceof Function) {
    import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
      getCLS(onPerfEntry);
      getFID(onPerfEntry);
      getFCP(onPerfEntry);
      getLCP(onPerfEntry);
      getTTFB(onPerfEntry);
    });
  }
};

export default reportWebVitals;
```

### `vite.config.js`

配置代理 `frontend/vite.config.js`

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    host: true, // 监听所有 IP，Docker 需要
    proxy: {
      // 把 /api 开头的请求转发给后端
      '/api': {
        target: 'http://backend:5000', // Docker 内部服务名
        changeOrigin: true,
        secure: false,
      }
    }
  }
})
```

### 启动前端

```bash
npm run dev
```

### `Dockerfile`

```dockerfile
# === 阶段 1: 构建阶段 (Build Stage) ===
# 使用 Node.js 镜像来构建 React 应用
FROM node:20-alpine AS build

# 设置工作目录
WORKDIR /app

# 复制 package.json 和 package-lock.json
COPY package*.json ./

# 安装依赖
RUN npm install

# 复制所有项目文件
COPY . .

# 执行构建，生成静态文件 (通常是 /build 或 /dist 目录)
RUN npm run build

# === 阶段 2: 运行阶段 (Run Stage) ===
# 使用一个轻量级的 Web 服务器镜像，例如 Nginx
FROM nginx:stable-alpine

# 将构建阶段生成的静态文件复制到 Nginx 的默认静态文件目录
# 确保 'build' 目录的路径与您的 npm run build 输出的路径一致
COPY --from=build /app/build /usr/share/nginx/html

# 暴露端口
EXPOSE 80

# 启动 Nginx
CMD ["nginx", "-g", "daemon off;"]
```

### `.gitlab-ci.yml`

```yaml
# 默认使用 Docker 镜像来执行 CI 任务
image: docker:latest

# 引入 docker:dind (Docker in Docker) 服务，允许 CI/CD 任务内部执行 Docker 命令
services:
  - docker:dind

# 定义阶段
stages:
  - build_and_push

# 定义全局变量
variables:
  # 确保 Docker 容器环境是干净的
  DOCKER_TLS_CERTDIR: ""
  # 定义镜像标签，使用分支名或短的 commit SHA
  IMAGE_TAG: $CI_COMMIT_REF_SLUG-$CI_COMMIT_SHORT_SHA 
  # 完整镜像路径
  FULL_IMAGE_NAME: $DOCKER_HUB_USERNAME/$DOCKER_IMAGE_NAME:$IMAGE_TAG

# 构建并推送任务
docker_build_and_push:
  stage: build_and_push
  
  # 仅在 master/main 分支或打 tag 时运行此任务
  only:
    - main
    - master
    - tags

  before_script:
    # 1. 登录 Docker Hub
    # 使用之前设置的 GitLab CI/CD 变量进行认证
    - echo "$DOCKER_HUB_PASSWORD" | docker login -u "$DOCKER_HUB_USERNAME" --password-stdin

  script:
    # 2. 构建 Docker 镜像
    # -t 用于给镜像打标签
    - docker build -t $FULL_IMAGE_NAME .
    
    # 3. 推送带版本号的镜像到 Docker Hub
    - docker push $FULL_IMAGE_NAME
    
    # --- 额外的步骤: 推送 latest 标签 (仅在 master/main 分支时) ---
    - | # 使用多行脚本语法
      if [ "$CI_COMMIT_REF_NAME" = "main" ] || [ "$CI_COMMIT_REF_NAME" = "master" ]; then
        LATEST_TAG=$DOCKER_HUB_USERNAME/$DOCKER_IMAGE_NAME:latest
        docker tag $FULL_IMAGE_NAME $LATEST_TAG
        echo "Pushing $LATEST_TAG tag..."
        docker push $LATEST_TAG
      fi

  # 清理步骤：确保无论脚本是否成功都退出 Docker Hub 登录
  after_script:
    - docker logout
```

### GitLab CI

根据 `Dockerfile` 和 `.gitlab-ci.yml` 进行 CI，构建镜像并推送至 Docker Hub。

## 前后端通信测试

- 数据库：容器化 MySQL

- 后端：http://127.0.0.1:5000

  ```bash
  python app.py
  ```

- 前端：http://localhost:3000

  ```bash
  npm start
  ```

## 容器化运行

### 加入同一网络

```bash
docker network create tasks-flask-mysql-react-fullstack
```

### 数据库

```bash
docker run --name tasks-flask-mysql-react-db \
-e MYSQL_ROOT_PASSWORD=000000 \
-e MYSQL_DATABASE=tasks_db \
--network tasks-flask-mysql-react-fullstack \
-p 3306:3306 \
-d mysql:8.0
```

### 后端

```bash
docker run --name tasks-flask-mysql-react-backend \
  --network tasks-flask-mysql-react-fullstack \
  -p 5000:5000 \
  -e DATABASE_URI="mysql+pymysql://root:000000@tasks-flask-mysql-react-db:3306/tasks_db" \
  -d jerrybaijy/tasks-react-flask-mysql-backend:latest
```

### 前端

```bash
docker run --name tasks-flask-mysql-react-frontend \
  --network tasks-flask-mysql-react-fullstack \
  -p 3000:80 \
  -e API_HOST="tasks-flask-mysql-react-backend" \
  -d jerrybaijy/tasks-react-flask-mysql-frontend:latest
```

### 访问

前端：http://localhost:3000
