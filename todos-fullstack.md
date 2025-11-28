---
title: todos-fullstack
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - projects
  - react
  - flask
  - mysql
  - fullstack
---

# 项目概述

这是一个使用 React + Flask + MySQL 构建的全栈 TODO 应用，支持 Docker 容器化和 Kubernetes 部署。

## 技术栈

- **前端**: React 18 + Vite + Axios
- **后端**: Flask 3.0 + SQLAlchemy + Flask-Migrate
- **数据库**: MySQL 8.0
- **容器化**: Docker + Docker Compose
- **编排工具**: Kubernetes
- **GitOps 工具**: Argo CD

## 项目结构

```
todos-fullstack/
│
├── backend/               # 后端代码目录
│   ├── app/               # 后端应用代码
│   │   ├── api/           # api 代码
│   │   │   ├── __init__.py   # API 蓝图文件
│   │   │   └── rutes.py      # API 路由文件
│   │   ├── __init__.py    # 后端应用初始化文件
│   │   └── models.py      # 数据库模型文件
│   │
│   ├── migrations/        # 数据库迁移文件夹
│   │
│   ├── config.py          # 后端配置文件
│   ├── run.py             # 后端入口文件
│   ├── requirements.txt   # 后端依赖列表
│   ├── boot.sh            # 后端启动脚本
│   └── Dockerfile         # 后端 Docker 镜像构建文件
│
├── frontend/              # 前端代码目录
│   ├── node_modules/      # 前端依赖存储
│   ├── public/            # 前端静态资源
│   ├── src/               # 前端应用代码
│   │   ├── App.jsx        # 主组件
│   │   ├── App.css        # 主组件样式表
│   │   └── main.jsx       # 数据库模型文件
│   │
│   ├── .env               # 前端环境变量(未推送至代码仓库)
│   ├── index.html         # 前端入口HTML文件
│   ├── vite.config.js     # 开发环境跨域代理
│   ├── package.json       # 前端依赖配置
│   ├── nginx.conf         # Nginx 配置（用于前端静态文件服务）
│   └── Dockerfile         # 前端 Docker 镜像构建文件
│
├── assets/                # README 资源文件
│
├── dev/                   # 开发环境 Kubernetes 配置
│   ├── backend.yaml       # 后端服务部署配置
│   ├── frontend.yaml      # 前端服务部署配置
│   └── mysql-db.yaml      # MySQL 数据库部署配置
│
├── argocd/                # Argo CD 配置文件
│   ├── application.yaml   # Argo CD 应用配置
│   └── ingress.yaml       # Ingress 配置（可选）
│
├── .env                   # 环境变量(未推送至代码仓库)
├── .env.example           # 环境变量示例文件
├── .gitignore             # Git 忽略文件配置
├── .gitlab-ci.yml         # GitLab CI/CD 配置
├── docker-compose.yml     # Docker Compose 配置
└── README.md              # 项目说明文档
```

## 项目存储

# 项目准备

## 创建项目根目录

```bash
cd projects
mkdir todos-fullstack
```

## 初始化 Git 仓库

```bash
cd todos-fullstack
git init --initial-branch=main
touch .gitignore
```

```
# Dependencies
node_modules/
venv/
.venv/

# Python bytecode
__pycache__/
*.pyc
*.pyo
*.pyd

# Build outputs
dist/
build/

# Environment variables
.env

# Logs
logs/
*.log

# IDE files
.vscode/
.idea/
*.swp
*.swo
*~

# Docker
.dockerignore

# Kubernetes
*.kubeconfig
```

## 配置环境变量

配置环境变量：`todos-fullstack/.env`

```bash
cd todos-fullstack
touch .env
```

```toml
# MySQL 数据库配置
MYSQL_ROOT_PASSWORD=123456
MYSQL_DATABASE=todos_db
MYSQL_USER=jerry
MYSQL_PASSWORD=000000

DB_HOST=localhost

# 数据库迁移
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=change_this_to_a_very_long_random_string

# 项目名称
BACKEND_NAME=todos-backend
FRONTEND_NAME=todos-frontend
```

同时，为了让协作者知道需要配什么，创建一个 `todos-fullstack/.env.example` (不含真实密码)：

```bash
cd todos-fullstack
touch .env.example
```

```toml
# MySQL 数据库配置
MYSQL_ROOT_PASSWORD=
MYSQL_DATABASE=todos_db
MYSQL_USER=
MYSQL_PASSWORD=

# 在 Docker 网络内部，数据库服务的名字叫 'db'
DB_HOST=db

# Flask 配置
FLASK_APP=run.py
FLASK_ENV=production

# change_this_to_a_very_long_random_string
SECRET_KEY=

# 项目名称
BACKEND_NAME=todos-react-flask-mysql-backend
FRONTEND_NAME=todos-react-flask-mysql-frontend
```

# 后端开发

## 目录结构

```bash
mkdir -p todos-fullstack/backend/app/api
```

## 虚拟环境

```bash
cd todos-fullstack/backend

# 提前复制 python-env 脚本到 backend 目录
source python-env
```

## 安装依赖

```bash
cd backend
touch requirements.txt
```

```
# requirements.txt

flask==3.0.0
flask-sqlalchemy==3.1.1
flask-migrate==4.0.5
flask-cors==4.0.1
pymysql==1.1.0
cryptography==41.0.7
gunicorn==21.2.0
python-dotenv==1.0.0
```

```bash
pip install -r requirements.txt
```

## `config.py`

后端配置文件 `backend/config.py`

```python
import os
from dotenv import load_dotenv

# 加载环境变量
load_dotenv()

class Config:
    # Flask 配置
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'your-secret-key'  

    # 获取数据库连接信息
    DB_USER = os.environ.get('MYSQL_USER') or 'root'
    DB_PASS = os.environ.get('MYSQL_PASSWORD') or 'password'        
    DB_HOST = os.environ.get('DB_HOST') or 'localhost'
    DB_NAME = os.environ.get('MYSQL_DATABASE') or 'todos_db'        

    # SQLAlchemy 配置
    SQLALCHEMY_DATABASE_URI = f'mysql+pymysql://{DB_USER}:{DB_PASS}@{DB_HOST}/{DB_NAME}?charset=utf8mb4'
    SQLALCHEMY_TRACK_MODIFICATIONS = False

```

## `__init__.py`

后端应用初始化文件 `app/__init__.py`

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from config import Config

# 创建数据库实例
db = SQLAlchemy()
# 创建迁移实例
migrate = Migrate()

def create_app(config_class=Config):
    # 创建 Flask 应用
    app = Flask(__name__)
    # 加载配置
    app.config.from_object(config_class)

    # 初始化数据库
    db.init_app(app)
    # 初始化迁移
    migrate.init_app(app, db)

    # 导入模型，确保SQLAlchemy知道所有模型
    from app import models
    
    # 注册蓝图
    from app.api import bp as api_bp
    app.register_blueprint(api_bp, url_prefix='/api')

    return app
```

## `models.py`

创建数据库模型文件 `app/models.py`

```python
from app import db

# 数据库模型
class Todo(db.Model):
    # 表名
    __tablename__ = 'todos'

    # 主键
    id = db.Column(db.Integer, primary_key=True)
    # TODO 内容
    content = db.Column(db.String(200), nullable=False)
    # 完成状态
    completed = db.Column(db.Boolean, default=False)

    def to_dict(self):
        # 转换为字典格式，用于 API 返回
        return {
            'id': self.id,
            'content': self.content,
            'completed': self.completed
        }
```

## `__init__.py`

创建 API 蓝图文件 `app/api/__init__.py`

```python
from flask import Blueprint

# 创建 API 蓝图
bp = Blueprint('api', __name__)

# 导入路由
from app.api import routes
```

## `routes.py`

后端 API 路由文件 `app/api/routes.py`

```python
from flask import jsonify, request
from app import db
from app.models import Todo
from app.api import bp

# 获取所有 TODOs
@bp.route('/todos', methods=['GET'])
def get_todos():
    todos = Todo.query.all()
    return jsonify([todo.to_dict() for todo in todos])

# 创建新 TODO
@bp.route('/todos', methods=['POST'])
def create_todo():
    data = request.get_json() or {}
    if 'content' not in data:
        return jsonify({'error': 'Content is required'}), 400

    todo = Todo(content=data['content'])
    db.session.add(todo)
    db.session.commit()
    return jsonify(todo.to_dict()), 201

# 更新 TODO
@bp.route('/todos/<int:id>', methods=['PUT'])
def update_todo(id):
    todo = Todo.query.get_or_404(id)
    data = request.get_json() or {}

    if 'content' in data:
        todo.content = data['content']
    if 'completed' in data:
        todo.completed = data['completed']

    db.session.commit()
    return jsonify(todo.to_dict())

# 删除 TODO
@bp.route('/todos/<int:id>', methods=['DELETE'])
def delete_todo(id):
    todo = Todo.query.get_or_404(id)
    db.session.delete(todo)
    db.session.commit()
    return jsonify({'message': 'Todo deleted successfully'}), 200
```

## `run.py`

后端入口文件 `backend/run.py`

```python
from app import create_app

app = create_app()

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

## MySQL

创建容器化 MySQL 用于开发环境测试，详见 [MySQL 笔记](mysql.md#容器化-mysql)。

```bash
docker run --name mysql-container \
-e MYSQL_ROOT_PASSWORD=123456 \
-e MYSQL_USER=jerry \
-e MYSQL_PASSWORD=000000 \
-e MYSQL_DATABASE=todos_db \
-p 3306:3306 \
-d mysql:8.0
```

## 初始化数据库迁移

在开发环境中初始化数据库迁移

```bash
# 确保虚拟环境已激活
# 确保数据库已正常运行

cd backend

# 初始化迁移仓库（仅首次需要）,这会在 backend 目录下创建 migrations 文件夹
flask db init

# 创建迁移脚本：根据 models.py 中的模型定义生成迁移脚本
flask db migrate -m "Initial migration"

# 应用迁移（创建表）：执行迁移脚本，在数据库中创建表结构
flask db upgrade
```

## 后端测试

- 确保 MySQL 已正常运行，初始化数据库迁移已完成。
- 启动后端

  ```bash
  cd backend
  python run.py
  ```

- 使用 Postman 模仿前端向后端发送请求，详见 [Postman  笔记](postman.md#使用方法)。

  - 请求方法：POST
  - 请求地址：http://localhost:5000/api/todos
  - 请求体

    ```json
    {
      "content": "111"
    }
    ```

# 前端开发

## 创建前端项目

```bash
# 使用 Vite 创建 React 项目
cd todos-fullstack
npm create vite@latest frontend -- --template react

# 安装依赖
cd frontend
npm install
# 安装 axios 用于 API 请求
npm install axios
```

## `.env`

前端环境变量 `frontend/.env`

```toml
VITE_API_BASE_URL=http://localhost:5000/api
```

## `App.jsx`

主组件 `src/App.jsx`

```jsx
import { useState, useEffect } from "react";
import "./App.css";

// 使用环境变量管理API地址
const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || "/api";

function App() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState("");

  useEffect(() => {
    fetchTodos();
  }, []);

  const fetchTodos = async () => {
    try {
      const res = await fetch(`${API_BASE_URL}/todos`);
      if (res.ok) {
        const data = await res.json();
        setTodos(data);
      }
    } catch (error) {
      console.error("Failed to fetch todos", error);
    }
  };

  const handleAdd = async () => {
    if (!input.trim()) return;
    const res = await fetch(`${API_BASE_URL}/todos`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ content: input }),
    });
    if (res.ok) {
      const newTodo = await res.json();
      setTodos([...todos, newTodo]);
      setInput("");
    }
  };

  const handleToggle = async (id) => {
    const res = await fetch(`${API_BASE_URL}/todos/${id}`, { method: "PUT" });
    if (res.ok) {
      const updated = await res.json();
      setTodos(todos.map((t) => (t.id === id ? updated : t)));
    }
  };

  const handleDelete = async (id) => {
    const res = await fetch(`${API_BASE_URL}/todos/${id}`, {
      method: "DELETE",
    });
    if (res.ok) {
      setTodos(todos.filter((t) => t.id !== id));
    }
  };

  return (
    <div className="container">
      <h1>My Todo List</h1>
      <div className="input-group">
        <input
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="What needs to be done?"
          onKeyPress={(e) => e.key === "Enter" && handleAdd()}
        />
        <button onClick={handleAdd}>Add</button>
      </div>
      <ul>
        {todos.map((todo) => (
          <li key={todo.id} className={todo.completed ? "completed" : ""}>
            <span
              onClick={() => handleToggle(todo.id)}
              style={{ cursor: "pointer", flex: 1 }}
            >
              {todo.content}
            </span>
            <button
              className="delete-btn"
              onClick={() => handleDelete(todo.id)}
            >
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;

```

## `App.css`

主组件样式表 `src/App.css`

```css
.container {
  max-width: 500px;
  margin: 50px auto;
  font-family: Arial, sans-serif;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
h1 {
  text-align: center;
  color: #333;
}
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
}
button {
  padding: 10px 20px;
  cursor: pointer;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
}
button:hover {
  background: #0056b3;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}
li.completed span {
  text-decoration: line-through;
  color: #888;
}
.delete-btn {
  background: #dc3545;
  margin-left: 10px;
}
.delete-btn:hover {
  background: #a71d2a;
}
```

## `main.jsx`

前端入口文件 `main.jsx`

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

## `index.html`

`frontend/index.html`

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Todo List</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

## `vite.config.js`

跨域代理 `frontend/vite.config.js`，用于开发环境前后端通信。

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:5000',
        changeOrigin: true
      }
    }
  }
})
```

## 前端测试

- 确保 MySQL 已正常运行，初始化数据库迁移已完成。

- 启动后端

  ```bash
  cd backend
  python run.py
  ```

- 启动前端

  ```bash
  npm run dev
  ```

- 访问前端： http://localhost:5173/

- 前后端通信正常，MySQL 数据变化正常。

# 多容器集成测试

## `boot.sh`

后端启动脚本 `backend/boot.sh`

```bash
#!/bin/bash

# 等待数据库可用
echo "Waiting for database..."
while ! nc -z $DB_HOST 3306; do
  sleep 1
done
echo "Database is ready!"

# 执行数据库迁移
flask db upgrade

# 启动应用
gunicorn -b 0.0.0.0:5000 run:app
```

## `backend/Dockerfile`

后端镜像构建文件 `backend/Dockerfile`

```dockerfile
# 使用 Python 3.10 作为基础镜像
FROM python:3.10-slim

# 安装必要的系统依赖，包括 nc
RUN apt-get update && apt-get install -y --no-install-recommends \
    netcat-traditional \
    && rm -rf /var/lib/apt/lists/*

# 设置工作目录
WORKDIR /app

# 复制依赖文件
COPY requirements.txt .

# 安装依赖
RUN pip install --no-cache-dir -r requirements.txt

# 复制应用代码
COPY . .

# 复制启动脚本
COPY boot.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/boot.sh

# 暴露端口
EXPOSE 5000

# 启动应用
CMD ["boot.sh"]
```

## `nginx.conf`

前端 Nginx 配置文件 `frontend/nginx.conf`

```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
    }

    # 反向代理 API 请求到后端容器
    location /api {
        proxy_pass http://backend:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

## `frontend/Dockerfile`

前端镜像构建文件 `frontend/Dockerfile`

```dockerfile
# 第一阶段：构建 React 应用
FROM node:18-alpine as build

# 设置工作目录
WORKDIR /app

# 复制 package.json 和 package-lock.json
COPY package*.json ./

# 安装依赖
RUN npm install

# 复制应用代码
COPY . .

# 构建应用
RUN npm run build

# 第二阶段：使用 Nginx 提供静态文件
FROM nginx:alpine

# 复制构建产物到 Nginx 静态目录
COPY --from=build /app/dist /usr/share/nginx/html

# 复制自定义 Nginx 配置
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 暴露端口
EXPOSE 80

# 启动 Nginx
CMD ["nginx", "-g", "daemon off;"]
```

## `docker-compose.yml`

容器编排文件 `todos-fullstack/docker-compose.yml`

- 环境变量获取自 `todos-fullstack/.env`
- 但 DB_HOST 在 `docker-compose.yml` 中硬编码

```yaml
version: '3.8'

services:
  # MySQL 数据库服务
  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    volumes:
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"
    command: --default-authentication-plugin=mysql_native_password  
    networks:
      - todo-network
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]        
      timeout: 20s
      retries: 10

  # 后端服务
  backend:
    build:
      context: ./backend
    restart: always
    environment:
      SECRET_KEY: ${SECRET_KEY}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      DB_HOST: db
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      FLASK_APP: ${FLASK_APP}
      FLASK_ENV: ${FLASK_ENV}
    depends_on:
      db:
        condition: service_healthy
    ports:
      - "5000:5000"
    networks:
      - todo-network

  # 前端服务
  frontend:
    build:
      context: ./frontend
    restart: always
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - todo-network

# 数据库挂载卷
volumes:
  mysql_data:
    driver: local

# 定义网络
networks:
  todo-network:
    driver: bridge

```

## 容器编排

- 停止开发环境的 MySQL
- 使用 Docker Compose 构建前端、后端镜像，并启动前端、后端和数据库容器。

  ```bash
  cd todos-fullstack
  docker-compose up -d
  ```

- 访问应用

  - 前端应用：http://localhost
  - 后端 API：http://localhost:5000/api/todos

- 查看日志

  ```bash
  # 查看所有服务日志
  docker-compose logs -f

  # 查看特定服务日志
  docker-compose logs -f frontend
  docker-compose logs -f backend
  docker-compose logs -f db
  ```

- 停止项目

  这会删除 `docker-compose.yml` 中定义的 Containers 和 Networks，但不会移除 Images、Volumes、Configs，可手动删除。

  ```bash
  cd todos-fullstack
  docker-compose down
  ```

# CI

## `.gitlab-ci.yml`

GitLab CI `todos-fullstack/.gitlab-ci.yml`

```yaml
# 定义变量
variables:
  # Docker 版本号
  DOCKER_VERSION: 24.0.5

  # 告诉 Docker 使用 overlay2 驱动，性能更好
  DOCKER_DRIVER: overlay2

  # 禁用 TLS 证书生成，防止 dind 连接报错
  DOCKER_TLS_CERTDIR: ""
  
  # 镜像名称前缀，$DOCKER_HUB_USER 是 GitLab 里配置的环境变量
  IMAGE_PREFIX: $DOCKER_HUB_USER
  
  # 后端和前端名称
  BACKEND_NAME: backend
  FRONTEND_NAME: frontend

# 定义阶段
stages:
  - build

# 使用 Docker-in-Docker 服务，允许在容器里运行 docker 命令
services:
  - docker:$DOCKER_VERSION-dind

# 登录 Docker Hub
before_script:
  # 使用 stdin 输入密码，更加安全
  - echo "$DOCKER_HUB_PASS" | docker login -u "$DOCKER_HUB_USER" --password-stdin

# 构建后端镜像
build_backend:
  stage: build
  image: docker:$DOCKER_VERSION
  script:
    # 进入后端目录
    - cd $BACKEND_NAME
    
    # 使用双标签构建：既有版本号（用于回溯），也有 latest（用于生产）
    - docker build -t $IMAGE_PREFIX/$BACKEND_NAME:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/$BACKEND_NAME:latest .
    
    # 推送到 Docker Hub
    - docker push $IMAGE_PREFIX/$BACKEND_NAME:$CI_COMMIT_SHORT_SHA
    - docker push $IMAGE_PREFIX/$BACKEND_NAME:latest
  rules:
    # 只有当 $BACKEND_NAME 目录下有文件变化时，才运行此 Job
    - changes:
        - $BACKEND_NAME/**/*

# 构建前端镜像
build_frontend:
  stage: build
  image: docker:$DOCKER_VERSION
  script:
    - cd $FRONTEND_NAME
    - docker build -t $IMAGE_PREFIX/$FRONTEND_NAME:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/$FRONTEND_NAME:latest .
    - docker push $IMAGE_PREFIX/$FRONTEND_NAME:$CI_COMMIT_SHORT_SHA
    - docker push $IMAGE_PREFIX/$FRONTEND_NAME:latest
  rules:
    - changes:
        - $FRONTEND_NAME/**/*
```

## GitLab CI

- 多容器集成测试已完成
- 确认以下文件已创建
  - 后端启动脚本 `backend/boot.sh`
  - 后端镜像构建文件 `backend/Dockerfile`
  - 前端 Nginx 配置文件 `frontend/nginx.conf`
  - 前端镜像构建文件 `frontend/Dockerfile`
  - 容器编排文件 `todos-fullstack/docker-compose.yml`
  - GitLab CI `todos-fullstack/.gitlab-ci.yml`
- 配置 GitLab 环境变量
  - `DOCKER_HUB_USER`
  - `DOCKER_HUB_PASS`
- 推送代码至仓库，Pipeline 完成以后查看 Docker Hub。

# 创建 Kubernetes 部署配置

## 创建开发环境目录

```bash
mkdir -p dev argocd
```

## 创建 MySQL 数据库 Kubernetes 配置 dev/mysql-db.yaml

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
type: Opaque
data:
  root-password: cm9vdF9wYXNzd29yZA== # base64 encoded "root_password"
  mysql-user: dG9kb191c2Vy # base64 encoded "todo_user"
  mysql-password: dG9kb19wYXNzd29yZA== # base64 encoded "todo_password"
  mysql-database: dG9kb3NfZGI= # base64 encoded "todos_db"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:8.0
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: root-password
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: mysql-database
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: mysql-user
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: mysql-password
          ports:
            - containerPort: 3306
          volumeMounts:
            - name: mysql-persistent-storage
              mountPath: /var/lib/mysql
      volumes:
        - name: mysql-persistent-storage
          persistentVolumeClaim:
            claimName: mysql-pvc
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
```

## 创建后端 Kubernetes 配置 dev/backend.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
        - name: backend
          image: registry.gitlab.com/<your-namespace>/todos-fullstack/backend:latest
          env:
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: mysql-user
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: mysql-password
            - name: DB_HOST
              value: mysql
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  name: mysql-secret
                  key: mysql-database
            - name: SECRET_KEY
              value: your-secret-key
          ports:
            - containerPort: 5000
          command: ["/bin/sh", "-c"]
          args:
            - |
              # 等待数据库可用
              echo "Waiting for database..."
              while ! nc -z $DB_HOST 3306; do
                sleep 1
              done
              echo "Database is ready!"

              # 执行数据库迁移
              flask db upgrade

              # 启动应用
              gunicorn -b 0.0.0.0:5000 run:app
---
apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  selector:
    app: backend
  ports:
    - port: 5000
      targetPort: 5000
```

## 创建前端 Kubernetes 配置 dev/frontend.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
        - name: frontend
          image: registry.gitlab.com/<your-namespace>/todos-fullstack/frontend:latest
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  type: NodePort
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

## 创建 Argo CD 应用配置 argocd/application.yaml

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: todos-fullstack
  namespace: argocd
spec:
  project: default
  source:
    repoURL: "https://gitlab.com/<your-namespace>/todos-fullstack.git"
    targetRevision: HEAD
    path: dev
  destination:
    server: "https://kubernetes.default.svc"
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```

## 创建 Ingress 配置（可选） argocd/ingress.yaml

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: todos-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: todos.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: frontend
                port:
                  number: 80
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: backend
                port:
                  number: 5000
```

# 使用 Argo CD 部署到 Kubernetes

## 前提条件

- Kubernetes 集群已安装 Argo CD
- 已配置好 Argo CD 访问权限
- GitLab 仓库已配置好 CI/CD 权限

## 安装 Argo CD（如果尚未安装）

```bash
# 创建 Argo CD 命名空间
kubectl create namespace argocd

# 安装 Argo CD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# 获取 Argo CD 初始密码
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# 访问 Argo CD UI
# 首先将 Argo CD 服务暴露为 NodePort
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

# 获取 Argo CD UI 访问地址
kubectl get svc argocd-server -n argocd
```

## 通过 Argo CD UI 创建应用

- 登录 Argo CD UI
- 点击 "NEW APP" 按钮
- 填写应用信息：
  - Application Name: `todos-fullstack`
  - Project: `default`
  - Repository URL: `https://gitlab.com/<your-namespace>/todos-fullstack.git`
  - Path: `dev`
  - Cluster URL: `https://kubernetes.default.svc`
  - Namespace: `default`
- 点击 "CREATE" 按钮创建应用
- 点击 "SYNC" 按钮同步应用

## 通过 Argo CD CLI 创建应用

```bash
# 登录 Argo CD CLI
argocd login <argocd-server-address> --username admin --password <initial-password>

# 创建应用
argocd app create todos-fullstack \
  --repo https://gitlab.com/<your-namespace>/todos-fullstack.git \
  --path dev \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default

# 同步应用
argocd app sync todos-fullstack
```

## 配置自动同步

- 在 Argo CD UI 中，进入应用详情页
- 点击 "APP DETAILS" 标签
- 找到 "SYNC POLICY" 部分，点击 "EDIT"
- 勾选 "Automated" 和 "Self Heal" 选项
- 点击 "SAVE"

这样，当 GitLab 仓库中的代码发生变更时，Argo CD 会自动检测并同步部署。

## 查看部署状态

```bash
# 查看 Argo CD 应用状态
argocd app get todos-fullstack

# 查看 Kubernetes Pod 状态
kubectl get pods

# 查看 Kubernetes Service 状态
kubectl get services

# 查看部署日志
kubectl logs -f deployment/frontend
kubectl logs -f deployment/backend
kubectl logs -f deployment/mysql
```

## 访问部署的应用

```bash
# 获取前端服务的外部 IP 或 NodePort
kubectl get service frontend
```

然后通过 http://<外部 IP>:30080 或 http://<节点 IP>:<NodePort> 访问应用

## 删除部署

```bash
# 通过 Argo CD 删除应用
argocd app delete todos-fullstack
```

```

```

# 常见问题及解决方案

1. **数据库连接失败**

   - 检查环境变量是否正确配置
   - 确保数据库服务已启动
   - 检查数据库用户权限

2. **迁移命令失败**

   - 确保已安装 flask-migrate
   - 确保数据库已创建
   - 检查数据库连接字符串是否正确

3. **前端无法访问后端 API**

   - 检查 CORS 配置（如果有）
   - 确保后端服务已启动
   - 检查 API 地址是否正确

4. **Docker 构建失败**

   - 检查 Dockerfile 语法是否正确
   - 确保依赖文件存在
   - 检查网络连接

5. **Kubernetes 部署失败**
   - 检查 YAML 语法是否正确
   - 确保 Docker 镜像已正确构建
   - 检查资源配额是否足够

# 开发建议

1. **使用 Git 进行版本控制**

   - 定期提交代码
   - 使用分支管理功能
   - 编写有意义的提交信息

2. **编写单元测试**

   - 为后端 API 编写测试
   - 为前端组件编写测试

3. **使用 CI/CD 自动化部署**

   - 配置 GitLab CI 或 GitHub Actions
   - 实现自动构建和部署

4. **监控和日志**

   - 添加日志记录
   - 配置监控系统
   - 设置告警

5. **安全最佳实践**
   - 使用 HTTPS
   - 定期更新依赖
   - 实现身份认证和授权
   - 防止 SQL 注入和 XSS 攻击

# 总结

本项目是一个完整的 React + Flask + MySQL 全栈应用，支持 Docker 容器化和使用 Argo CD 进行 Kubernetes 部署。通过本教程，你可以学习到：

1. 如何创建 React 前端应用
2. 如何创建 Flask 后端 API
3. 如何设计和使用 MySQL 数据库
4. 如何使用 Docker 和 Docker Compose 进行容器化部署
5. 如何使用 GitLab CI/CD 进行自动化构建
6. 如何使用 Argo CD 进行 GitOps 风格的 Kubernetes 部署和管理

希望本教程对你有所帮助，祝你学习愉快！
