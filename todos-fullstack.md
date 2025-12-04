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
  - docker
  - docker-compose
  - k8s
  - argo-cd
  - nginx
  - vite
---

# 项目概述

这是一个使用 React + Flask + MySQL 构建的全栈 TODO 应用，支持 Docker 容器化和 Kubernetes 部署。

![image-20251128210905428](assets/image-20251128210905428.png)

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
│   ├── index.html         # 前端入口 HTML 文件
│   ├── vite.config.js     # 前端请求代理（本地环境）
│   ├── package.json       # 前端依赖配置
│   ├── nginx.conf         # 前端请求代理（容器化环境）
│   └── Dockerfile         # 前端 Docker 镜像构建文件
│
├── assets/                # README 资源文件
│
├── k8s/                   # Kubernetes 部署文件
│   ├── namespace.yaml     # 命名空间定义
│   ├── mysql.yaml         # MySQL 部署和服务
│   ├── backend.yaml       # 后端部署和服务
│   ├── frontend.yaml      # 前端部署和服务
│   └── application.yaml   # Argo CD 应用定义
│
├── todo-chart/                  # Helm Chart 目录
│   ├── Chart.yaml               # Chart 元数据
│   ├── values.yaml              # 模板文件参数配置
│   ├── .helmignore              # 忽略不需要打包的文件
│   └── templates/               # Kubernetes 资源模板目录
│       ├── namespace.yaml       # 命名空间
│       ├── _helpers.tpl         # 模板函数
│       ├── mysql.yaml           # 数据库模板
│       ├── backend.yaml         # 后端模板
│       └── frontend.yaml        # 前端模板
│
├── .env                   # 环境变量（未推送至代码仓库）
├── .env.example           # 环境变量示例文件
├── .gitignore             # Git 忽略文件配置
├── .gitlab-ci.yml         # GitLab CI/CD 配置
├── docker-compose.yml     # Docker Compose 配置
└── README.md              # 项目说明文档
```

## 项目存储

- **项目仓库**
  - GitLab: https://gitlab.com/jerrybai/todos-fullstack
  - GitHub: https://github.com/Jerrybaijy/todos-fullstack

- **镜像仓库**
  - 后端：https://hub.docker.com/repository/docker/jerrybaijy/todos-fullstack-backend
  - 前端：https://hub.docker.com/repository/docker/jerrybaijy/todos-fullstack-frontend

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

# 数据库迁移, flask db init 中的 flask 对应 FLASK_APP
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=change_this_to_a_very_long_random_string
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
    SECRET_KEY = os.environ.get("SECRET_KEY") or "your-secret-key"

    # 获取数据库连接信息
    DB_USER = os.environ.get("MYSQL_USER") or "root"
    DB_PASS = os.environ.get("MYSQL_PASSWORD") or "password"
    DB_HOST = os.environ.get("DB_HOST") or "localhost"
    DB_NAME = os.environ.get("MYSQL_DATABASE") or "todos_db"

    # SQLAlchemy 配置
    SQLALCHEMY_DATABASE_URI = (
        f"mysql+pymysql://{DB_USER}:{DB_PASS}@{DB_HOST}/{DB_NAME}?charset=utf8mb4"
    )
    SQLALCHEMY_TRACK_MODIFICATIONS = False
```

## `__init__.py`

后端应用初始化文件 `app/__init__.py`

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from flask_cors import CORS
from config import Config

# 创建数据库实例
db = SQLAlchemy()
# 创建迁移实例
migrate = Migrate()
# 创建 CORS 实例，使用 flask-cors 库启用了跨域资源共享，允许前端跨域请求
cors = CORS()

def create_app(config_class=Config):
    # 创建 Flask 应用
    app = Flask(__name__)
    # 加载配置
    app.config.from_object(config_class)

    # 初始化数据库
    db.init_app(app)
    # 初始化迁移
    migrate.init_app(app, db)
    # 初始化CORS
    cors.init_app(app)

    # 导入模型，确保SQLAlchemy知道所有模型
    from app import models

    # 注册蓝图
    from app.api import bp as api_bp

    app.register_blueprint(api_bp, url_prefix="/api")

    return app
```

## `models.py`

创建数据库模型文件 `app/models.py`

```python
from app import db

# 数据库模型
class Todo(db.Model):
    # 表名
    __tablename__ = "todos"

    # 主键
    id = db.Column(db.Integer, primary_key=True)
    # TODO 内容
    content = db.Column(db.String(200), nullable=False)
    # 完成状态
    completed = db.Column(db.Boolean, default=False)

    def to_dict(self):
        # 转换为字典格式，用于 API 返回
        return {"id": self.id, "content": self.content, "completed": self.completed}
```

## `__init__.py`

创建 API 蓝图文件 `app/api/__init__.py`

```python
from flask import Blueprint

# 创建 API 蓝图
# 注册了 /api 前缀，即 routes.py 中的 /todos 实际路径为 /api/todos
bp = Blueprint("api", __name__)

# 导入路由
from app.api import routes
```

## `routes.py`

后端 API 路由文件 `app/api/routes.py`

- 在 `__init__.py` 创建 API 蓝图时添加了 `/api` 前缀
- 后端的路由 `/todos` 实际上对应的完整相对路径是 `/api/todos`

```python
from flask import jsonify, request
from app import db
from app.models import Todo
from app.api import bp

# 获取所有 TODOs
# 在 __init__.py 中注册了 /api 前缀，此处实际路径为 /api/todos
@bp.route("/todos", methods=["GET"])
def get_todos():
    todos = Todo.query.all()
    return jsonify([todo.to_dict() for todo in todos])

# 创建新 TODO
@bp.route("/todos", methods=["POST"])
def create_todo():
    data = request.get_json() or {}
    if "content" not in data:
        return jsonify({"error": "Content is required"}), 400

    todo = Todo(content=data["content"])
    db.session.add(todo)
    db.session.commit()
    return jsonify(todo.to_dict()), 201

# 更新 TODO
@bp.route("/todos/<int:id>", methods=["PUT"])
def update_todo(id):
    todo = Todo.query.get_or_404(id)
    data = request.get_json() or {}

    if "content" in data:
        todo.content = data["content"]
    if "completed" in data:
        todo.completed = data["completed"]

    db.session.commit()
    return jsonify(todo.to_dict())

# 删除 TODO
@bp.route("/todos/<int:id>", methods=["DELETE"])
def delete_todo(id):
    todo = Todo.query.get_or_404(id)
    db.session.delete(todo)
    db.session.commit()
    return jsonify({"message": "Todo deleted successfully"}), 200
```

## `run.py`

后端入口文件 `backend/run.py`

```python
from app import create_app

app = create_app()

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000, debug=True)
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
# 确保全新数据库已正常运行

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

## `App.jsx`

主组件 `src/App.jsx`

```jsx
import { useState, useEffect } from "react";
import "./App.css";

// 允许使用环境变量管理 API 地址，默认值为"/api"
const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || "/api";

/**
 * Todo列表应用的主组件
 * 实现了Todo的增删改查功能
 */
function App() {
  // todos状态：存储所有Todo项的数据
  const [todos, setTodos] = useState([]);
  // input状态：存储用户输入的新Todo内容
  const [input, setInput] = useState("");

  // 组件挂载时，从API获取初始Todo列表
  useEffect(() => {
    // 在effect中直接定义异步函数并执行
    const fetchInitialTodos = async () => {
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

    fetchInitialTodos();
  }, []);

  // 添加新的Todo项
  const handleAdd = async () => {
    // 验证输入不为空
    if (!input.trim()) return;

    // 发送POST请求添加Todo
    const res = await fetch(`${API_BASE_URL}/todos`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ content: input }),
    });

    // 添加成功后更新状态
    if (res.ok) {
      const newTodo = await res.json();
      setTodos([...todos, newTodo]);
      setInput(""); // 清空输入框
    }
  };

  // 切换Todo项的完成状态
  const handleToggle = async (id) => {
    // 发送PUT请求切换完成状态
    const res = await fetch(`${API_BASE_URL}/todos/${id}`, { method: "PUT" });

    // 更新成功后更新状态
    if (res.ok) {
      const updated = await res.json();
      setTodos(todos.map((t) => (t.id === id ? updated : t)));
    }
  };

  // 删除指定ID的Todo项
  const handleDelete = async (id) => {
    // 发送DELETE请求删除Todo
    const res = await fetch(`${API_BASE_URL}/todos/${id}`, {
      method: "DELETE",
    });

    // 删除成功后更新状态
    if (res.ok) {
      setTodos(todos.filter((t) => t.id !== id));
    }
  };

  return (
    <div className="container">
      <h1>My Todo List</h1>

      {/* 输入区域：添加新Todo */}
      <div className="input-group">
        <input
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="What needs to be done?"
          onKeyPress={(e) => e.key === "Enter" && handleAdd()}
        />
        <button onClick={handleAdd}>Add</button>
      </div>

      {/* Todo列表展示 */}
      <ul>
        {todos.map((todo) => (
          <li key={todo.id} className={todo.completed ? "completed" : ""}>
            {/* Todo内容，点击可切换完成状态 */}
            <span
              onClick={() => handleToggle(todo.id)}
              style={{ cursor: "pointer", flex: 1 }}
            >
              {todo.content}
            </span>
            {/* 删除按钮 */}
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

Vite 跨域代理 `frontend/vite.config.js`，用于直接本地运行（**非容器化部署**）时的前后端通信，将前端 `/api` 开头的请求转发到 http://localhost:5000 后端服务。

1. 前端请求: `/api/todos`
2. Vite 代理匹配到 `/api` 前缀
3. 转发到: http://localhost:5000/api/todos

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

- 后端已启动

  ```bash
  cd backend
  python run.py
  ```

- 启动前端

  ```bash
  cd frontend
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

Nginx 反向代理 `frontend/nginx.conf`，用于**容器化部署**时的前后端通信，将前端 `/api` 开头的请求转发到 http://backend:5000 后端服务。

1. 前端请求: `/api/todos`
2. Nginx 反向代理匹配到 `/api` 前缀
3. 转发到: http://backend:5000/api/todos
4. 通过 Docker 网络访问后端容器

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
# 指定 Docker Compose 文件版本
version: "3.8"

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

## Docker Compose 构建和部署

- 停止开发环境的 MySQL

- 使用 Docker Compose 构建前端、后端镜像，并启动前端、后端和数据库容器。

  ```bash
  cd todos-fullstack
  docker-compose up -d
  ```

- 外部访问 ：

  - 前端： http://localhost:80
  - 后端：http://localhost:5000/api/todos
  - 数据库： http://localhost:3306

- 停止项目

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

- Docker Compose 测试已完成
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

# CD

此项目实验了三种部署方式，使用其中一个即可：

- Docker Compose
- K8s + Argo CD
- Helm + Argo CD

# Docker Compose 部署

## 创建目录

先创建 `todos-remote` 目录，在此目录分别创建：

- `todos-remote/docker-compose.yml`
- `todos-remote/.env`

## `docker-compose.yml`

```yaml
# 指定 Docker Compose 文件版本
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
    # 指定镜像名称
    image: jerrybaijy/todos-fullstack-backend:latest
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
    # 指定镜像名称
    image: jerrybaijy/todos-fullstack-frontend:latest
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

## `.env`

```toml
# MySQL 数据库配置
MYSQL_ROOT_PASSWORD=123456
MYSQL_DATABASE=todos_db
MYSQL_USER=jerry
MYSQL_PASSWORD=000000

# 在 Docker 网络内部，数据库服务的名字叫 'db'
DB_HOST=db

# Flask 配置
FLASK_APP=run.py
FLASK_ENV=production
SECRET_KEY=change_this_to_a_very_long_random_string
```

## 启动

- 删除 **Docker Compose 测试**时的 Image、Container 和 Volumes，余下操作相同。

- 使用 Docker Compose 拉取前端、后端镜像，并启动前端、后端和数据库容器。

  ```bash
  cd todos-remote
  docker-compose up -d
  ```

- 访问应用

  - 前端应用：http://localhost
  - 后端 API：http://localhost:5000/api/todos

- 停止项目

  ```bash
  cd todos-remote
  docker-compose down
  ```

# K8s + Argo CD 部署

## 准备

- Minikube、Kubectl、Argo CD 已安装

- 创建开发环境目录

  ```bash
  cd todos-fullstack
  mkdir k8s
  ```

## `namespace.yaml`

命名空间 `k8s/namespace.yaml`

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: todos
  labels:
    name: todos
```

## `application.yaml`

ArgoCD 应用定义 `k8s/application.yaml`

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: todos-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/Jerrybaijy/todos-fullstack.git
    targetRevision: HEAD
    path: k8s
  destination:
    server: https://kubernetes.default.svc
    namespace: todos
  syncPolicy:
    automated:
      selfHeal: true
      prune: true
    syncOptions:
      - CreateNamespace=true
      - ApplyOutOfSyncOnly=true
    retry:
      limit: 5
      backoff:
        duration: 5s
        factor: 2
        maxDuration: 3m
```

## `mysql.yaml`

数据库部署和服务 `k8s/mysql.yaml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config
  namespace: todos

data:
  MYSQL_DATABASE: todos_db
  DB_HOST: mysql
---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: todos
type: Opaque
stringData:
  MYSQL_ROOT_PASSWORD: "123456"
  MYSQL_USER: jerry
  MYSQL_PASSWORD: "000000"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  namespace: todos
  labels:
    app: mysql
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
          envFrom:
            - configMapRef:
                name: mysql-config
            - secretRef:
                name: mysql-secret
          ports:
            - containerPort: 3306
          volumeMounts:
            - name: mysql-data
              mountPath: /var/lib/mysql
          args:
            - --default-authentication-plugin=mysql_native_password
          readinessProbe:
            exec:
              command:
                - mysqladmin
                - ping
                - -h
                - localhost
            initialDelaySeconds: 30
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
          livenessProbe:
            exec:
              command:
                - mysqladmin
                - ping
                - -h
                - localhost
            initialDelaySeconds: 60
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
      volumes:
        - name: mysql-data
          emptyDir: {}
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
  namespace: todos
  labels:
    app: mysql
spec:
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
  clusterIP: None
```

## `backend.yaml`

后端部署和服务 `k8s/backend.yaml`

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: backend-secret
  namespace: todos
type: Opaque
stringData:
  SECRET_KEY: your-secret-key
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
  namespace: todos
  labels:
    app: backend
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
          image: jerrybaijy/todos-fullstack-backend:latest
          envFrom:
            - secretRef:
                name: backend-secret
            - configMapRef:
                name: mysql-config
            - secretRef:
                name: mysql-secret
          ports:
            - containerPort: 5000
          readinessProbe:
            httpGet:
              path: /api/todos
              port: 5000
            initialDelaySeconds: 30
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
          livenessProbe:
            httpGet:
              path: /api/todos
              port: 5000
            initialDelaySeconds: 60
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
      initContainers:
        - name: wait-for-mysql
          image: busybox:1.31
          command:
            [
              "sh",
              "-c",
              "until nslookup mysql.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for mysql; sleep 2; done;",
            ]
---
apiVersion: v1
kind: Service
metadata:
  name: backend
  namespace: todos
  labels:
    app: backend
spec:
  selector:
    app: backend
  ports:
    - port: 5000
      targetPort: 5000
```

## `frontend.yaml`

前端部署和服务 `k8s/frontend.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  namespace: todos
  labels:
    app: frontend
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
          image: jerrybaijy/todos-fullstack-frontend:latest
          ports:
            - containerPort: 80
          readinessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 10
            periodSeconds: 5
            timeoutSeconds: 3
            failureThreshold: 3
          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 20
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
  namespace: todos
  labels:
    app: frontend
spec:
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 80
  # 如果公网访问，应将服务类型改为 LoadBalancer
  type: ClusterIP
```

## 部署

- 将源代码推送至代码仓库

- 部署

  ```bash
  cd k8s
  kubectl apply -f application.yaml
  ```

- 外部访问 ：

  - 前端：通过 NodePort、LoadBalancer 或端口转发访问
  - 后端：仅集群内部访问，或通过端口转发临时访问
  - 数据库：仅集群内部访问，或通过端口转发临时访问
  
- 端口转发

  ```bash
  # 前端
  kubectl port-forward svc/frontend 8081:80 -n todos
  ```

- 访问前端：http://localhost:8081/

- 如有调试需要，也可将后端和数据库进行端口转发

  ```bash
  # 数据库
  kubectl port-forward svc/mysql 3306:3306 -n todos
  # 后端
  kubectl port-forward svc/backend 5000:5000 -n todos
  ```

# Helm + Argo CD 部署

此步骤是部署方式的其中一种，现在需要将其打包为 Helm Chart 并部署到 Kubernetes 集群，同时实现 CI/CD 自动化流程。

## 准备

- Helm 已安装

- 源代码开发完成，已将镜像推送至镜像仓库。

- 创建 Chart

  ```bash
  cd d:/projects/todos-helm
  helm create todo-chart
  ```

- 删除 `templates` 目录下的全部默认文件

- 保留并修改以下必要文件：

  - `Chart.yaml`：Chart 元数据
  - `values.yaml`：配置值
  - `.helmignore`：忽略不需要打包的文件
  - `templates/`：我们将创建自己的模板文件目录

- 在 `templates` 目录创建以下文件

  ```bash
  cd d:/projects/todos-helm/todo-chart/templates/
  touch namespace.yaml _helpers.tpl mysql.yaml backend.yaml frontend.yaml
  ```

## Chart.yaml

Chart 的元数据 `todos-helm/Chart.yaml`

```yaml
apiVersion: v2
name: todo-chart
description: A Helm chart for Todo application
version: 0.1.0
type: application
appVersion: "1.0.0"
```

## values.yaml

参数配置 `todos-helm/values.yaml`

```yaml
# 全局配置
global:
  namespace: todos-helm

# MySQL配置
mysql:
  image: mysql
  tag: 8.0
  imagePullPolicy: IfNotPresent
  rootPassword: "123456"
  database: todos_db
  user: jerry
  password: "000000"
  replicaCount: 1
  persistence:
    enabled: true
    size: 1Gi
  service:
    type: ClusterIP
    port: 3306

# Backend配置
backend:
  replicaCount: 1
  image:
    repository: jerrybaijy/todos-helm-backend
    tag: latest
    pullPolicy: IfNotPresent
  service:
    type: ClusterIP
    port: 5000
  env:
    SECRET_KEY: your_secret_key_here

# Frontend配置
frontend:
  replicaCount: 1
  image:
    repository: jerrybaijy/todos-helm-frontend
    tag: latest
    pullPolicy: IfNotPresent
  service:
    type: NodePort
    port: 80
    nodePort: 30080
```

## namespace.yaml

命名空间 `templates/namespace.yaml`

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: {{ .Values.global.namespace }}
  labels:
    name: {{ .Values.global.namespace }}
```

## _helpers.tpl

模板函数 `templates/_helpers.tpl`

```tpl
{{/* 定义 Chart 的名称，优先使用 Values.nameOverride，如果不存在则使用 Chart.Name */}}
{{- define "todo-chart.name" }}
{{- default .Chart.Name .Values.nameOverride | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/* 定义 Chart 的完整标识，格式为 Chart.Name-Chart.Version */}}
{{- define "todo-chart.chart" }}
{{- printf "%s-%s" .Chart.Name .Chart.Version | replace "+" "_" | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/* 定义 Chart 的完整发布名称，优先使用 Values.fullnameOverride，如果不存在则根据 Release.Name 和 Chart.Name 生成 */}}
{{- define "todo-chart.fullname" }}
{{- if .Values.fullnameOverride }}
{{- .Values.fullnameOverride | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- $name := default .Chart.Name .Values.nameOverride }}
{{- if contains $name .Release.Name }}
{{- .Release.Name | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- printf "%s-%s" .Release.Name $name | trunc 63 | trimSuffix "-" }}
{{- end }}
{{- end }}
{{- end }}

{{/* 定义 MySQL 组件的完整名称 */}}
{{- define "todo-chart.mysql.fullname" }}
{{- printf "%s-mysql" (include "todo-chart.fullname" .) | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/* 定义 Backend 组件的完整名称 */}}
{{- define "todo-chart.backend.fullname" }}
{{- printf "%s-backend" (include "todo-chart.fullname" .) | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/* 定义 Frontend 组件的完整名称 */}}
{{- define "todo-chart.frontend.fullname" }}
{{- printf "%s-frontend" (include "todo-chart.fullname" .) | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/* 定义基础的标签集合，包含 Chart 信息和 Release 信息 */}}
{{- define "todo-chart.labels" }}
helm.sh/chart: {{ include "todo-chart.chart" . }}
helm.sh/version: {{ .Chart.Version | quote }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/managed-by: {{ .Release.Service }}
{{- if .Values.commonLabels }}
{{- toYaml .Values.commonLabels | nindent 2 }}
{{- end }}
{{- end }}

{{/* 定义 MySQL 组件的标签集合，继承基础标签并添加组件特定标签 */}}
{{- define "todo-chart.mysql.labels" }}
{{- include "todo-chart.labels" . }}
app.kubernetes.io/name: {{ include "todo-chart.name" . }}-mysql
app.kubernetes.io/component: mysql
{{- end }}

{{/* 定义 MySQL 组件的选择器标签，用于 Pod 选择 */}}
{{- define "todo-chart.mysql.selectorLabels" }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/name: {{ include "todo-chart.name" . }}-mysql
app.kubernetes.io/component: mysql
{{- end }}

{{/* 定义 Backend 组件的标签集合，继承基础标签并添加组件特定标签 */}}
{{- define "todo-chart.backend.labels" }}
{{- include "todo-chart.labels" . }}
app.kubernetes.io/name: {{ include "todo-chart.name" . }}-backend
app.kubernetes.io/component: backend
{{- end }}

{{/* 定义 Backend 组件的选择器标签，用于 Pod 选择 */}}
{{- define "todo-chart.backend.selectorLabels" }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/name: {{ include "todo-chart.name" . }}-backend
app.kubernetes.io/component: backend
{{- end }}

{{/* 定义 Frontend 组件的标签集合，继承基础标签并添加组件特定标签 */}}
{{- define "todo-chart.frontend.labels" }}
{{- include "todo-chart.labels" . }}
app.kubernetes.io/name: {{ include "todo-chart.name" . }}-frontend
app.kubernetes.io/component: frontend
{{- end }}

{{/* 定义 Frontend 组件的选择器标签，用于 Pod 选择 */}}
{{- define "todo-chart.frontend.selectorLabels" }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/name: {{ include "todo-chart.name" . }}-frontend
app.kubernetes.io/component: frontend
{{- end }}
```

## mysql.yaml

数据库模板文件 `templates/mysql.yaml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ include "todo-chart.mysql.fullname" . }}-config
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.mysql.labels" . | nindent 4 }}

data:
  MYSQL_DATABASE: {{ .Values.mysql.database | quote }}
  DB_HOST: {{ include "todo-chart.mysql.fullname" . }}
---
apiVersion: v1
kind: Secret
metadata:
  name: {{ include "todo-chart.mysql.fullname" . }}-secret
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.mysql.labels" . | nindent 4 }}

type: Opaque
stringData:
  MYSQL_ROOT_PASSWORD: {{ .Values.mysql.rootPassword | quote }}
  MYSQL_USER: {{ .Values.mysql.user }}
  MYSQL_PASSWORD: {{ .Values.mysql.password | quote }}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "todo-chart.mysql.fullname" . }}
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.mysql.labels" . | nindent 4 }}

spec:
  replicas: {{ .Values.mysql.replicaCount }}
  selector:
    matchLabels:
      {{- include "todo-chart.mysql.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "todo-chart.mysql.labels" . | nindent 8 }}
    spec:
      containers:
        - name: mysql
          image: "{{ .Values.mysql.image }}:{{ .Values.mysql.tag }}"
          envFrom:
            - configMapRef:
                name: {{ include "todo-chart.mysql.fullname" . }}-config
            - secretRef:
                name: {{ include "todo-chart.mysql.fullname" . }}-secret
          ports:
            - containerPort: {{ .Values.mysql.service.port }}
          volumeMounts:
            - name: mysql-data
              mountPath: /var/lib/mysql
          # args:
          #   - --default-authentication-plugin=mysql_native_password
          readinessProbe:
            exec:
              command:
                - mysqladmin
                - ping
                - -h
                - localhost
            initialDelaySeconds: 30
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
          livenessProbe:
            exec:
              command:
                - mysqladmin
                - ping
                - -h
                - localhost
            initialDelaySeconds: 60
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
      volumes:
        - name: mysql-data
          emptyDir: {}
---
apiVersion: v1
kind: Service
metadata:
  name: {{ include "todo-chart.mysql.fullname" . }}
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.mysql.labels" . | nindent 4 }}

spec:
  selector:
    {{- include "todo-chart.mysql.selectorLabels" . | nindent 6 }}
  ports:
    - port: {{ .Values.mysql.service.port }}
      targetPort: {{ .Values.mysql.service.port }}
  clusterIP: None
```

## backend.yaml

后端模板文件 `templates/backend.yaml`

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: {{ include "todo-chart.backend.fullname" . }}-secret
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.backend.labels" . | nindent 4 }}
type: Opaque
stringData:
  SECRET_KEY: {{ .Values.backend.env.SECRET_KEY | quote }}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "todo-chart.backend.fullname" . }}
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.backend.labels" . | nindent 4 }}

spec:
  replicas: {{ .Values.backend.replicaCount }}
  selector:
    matchLabels:
      {{- include "todo-chart.backend.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "todo-chart.backend.labels" . | nindent 8 }}
    spec:
      containers:
        - name: backend
          image: "{{ .Values.backend.image.repository }}:{{ .Values.backend.image.tag }}"
          imagePullPolicy: {{ .Values.backend.image.pullPolicy }}
          envFrom:
            - secretRef:
                name: {{ include "todo-chart.backend.fullname" . }}-secret
            - configMapRef:
                name: {{ include "todo-chart.mysql.fullname" . }}-config
            - secretRef:
                name: {{ include "todo-chart.mysql.fullname" . }}-secret
          ports:
            - containerPort: {{ .Values.backend.service.port }}
          readinessProbe:
            httpGet:
              path: /api/todos
              port: {{ .Values.backend.service.port }}
            initialDelaySeconds: 30
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
          livenessProbe:
            httpGet:
              path: /api/todos
              port: {{ .Values.backend.service.port }}
            initialDelaySeconds: 60
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
      initContainers:
        - name: wait-for-mysql
          image: busybox:1.31
          command:
            [
              "sh",
              "-c",
              "until nslookup {{ include "todo-chart.mysql.fullname" . }}.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for mysql; sleep 2; done;"
            ]
---
apiVersion: v1
kind: Service
metadata:
  name: {{ include "todo-chart.backend.fullname" . }}
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.backend.labels" . | nindent 4 }}

spec:
  selector:
    {{- include "todo-chart.backend.selectorLabels" . | nindent 6 }}
  ports:
    - port: {{ .Values.backend.service.port }}
      targetPort: {{ .Values.backend.service.port }}
```

## frontend.yaml

前端模板文件 `templates/frontend.yaml`

由于前端源码把 Nginx 反向代理的后端服务名写死了，而 Helm 是动态生成的后端服务名，所以此处添加了 Nginx 配置的覆盖。

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ include "todo-chart.frontend.fullname" . }}-nginx-config
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.frontend.labels" . | nindent 4 }}
data:
  default.conf: |
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
            proxy_pass http://{{ include "todo-chart.backend.fullname" . }}:{{ .Values.backend.service.port }};
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "todo-chart.frontend.fullname" . }}
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.frontend.labels" . | nindent 4 }}

spec:
  replicas: {{ .Values.frontend.replicaCount }}
  selector:
    matchLabels:
      {{- include "todo-chart.frontend.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "todo-chart.frontend.labels" . | nindent 8 }}
    spec:
      containers:
        - name: frontend
          image: "{{ .Values.frontend.image.repository }}:{{ .Values.frontend.image.tag | default .Chart.AppVersion }}"
          imagePullPolicy: {{ .Values.frontend.image.pullPolicy }}
          ports:
            - containerPort: {{ .Values.frontend.service.port }}
          volumeMounts:
            - name: nginx-config
              mountPath: /etc/nginx/conf.d
          readinessProbe:
            httpGet:
              path: /
              port: {{ .Values.frontend.service.port }}
            initialDelaySeconds: 10
            periodSeconds: 5
            timeoutSeconds: 3
            failureThreshold: 3
          livenessProbe:
            httpGet:
              path: /
              port: {{ .Values.frontend.service.port }}
            initialDelaySeconds: 20
            periodSeconds: 10
            timeoutSeconds: 5
            failureThreshold: 3
      volumes:
        - name: nginx-config
          configMap:
            name: {{ include "todo-chart.frontend.fullname" . }}-nginx-config
---
apiVersion: v1
kind: Service
metadata:
  name: {{ include "todo-chart.frontend.fullname" . }}
  namespace: {{ .Values.global.namespace }}
  labels:
    {{- include "todo-chart.frontend.labels" . | nindent 4 }}

spec:
  selector:
    {{- include "todo-chart.frontend.selectorLabels" . | nindent 6 }}
  ports:
    - port: {{ .Values.frontend.service.port }}
      targetPort: {{ .Values.frontend.service.port }}
  type: {{ .Values.frontend.service.type }}
```

## 本地测试 Chart

- 检查语法

  ```bash
  cd /d/projects/todos-helm
  helm lint ./todo-chart
  ```

- 部署 Helm Release

  ```yaml
  cd /d/projects/todos-helm
  helm install todo-app ./todo-chart
  ```

- 查看，所有资源运行正常

  ```yaml
  kubectl get all -n todos-helm
  ```

- 端口转发

  ```bash
  # 前端
  kubectl port-forward svc/todo-app-todo-chart-frontend 8081:80 -n todos-helm
  ```

- 访问前端：http://localhost:8081/

- 如有调试需要，也可将后端和数据库进行端口转发

  ```bash
  # 数据库
  kubectl port-forward svc/todo-app-todo-chart-mysql 3306:3306 -n todos-helm
  # 后端
  kubectl port-forward svc/todo-app-todo-chart-backend 5000:5000 -n todos-helm
  ```

- 卸载 Helm Release

  ```bash
  helm uninstall todo-app
  ```

## 封装 Chart

# 项目总结

## 通信

### 本地开发阶段
#### 通信流程

前端发送请求 `/api/todos` → Vite 代理 → 后端 (http://localhost:5000) → 容器化 MySQL (端口映射)

#### 前端通信配置

- **运行地址** ：本地 http://localhost:5173/
- **代理配置**：在 `vite.config.js` 中配置了 API 代理
- **通信方式** ：Vite 代理将前端请求 `/api/todos` 转发至 http://localhost:5000/api/todos 直接访问后端。

#### 后端通信配置

- **运行地址** ：本地 http://localhost:5000
- **后端到数据库** ：直接连接本地经端口转发后的容器化 MySQL

#### 数据库通信配置

- **端口转发**：在启动容器化 MySQL 时设置端口转发至本地

### Docker Compose 阶段

#### 通信流程

外部请求 → 前端容器 (80端口) → Nginx 反向代理 → 后端容器 (5000端口)

#### 网络配置

- 所有服务（前端、后端、数据库）都在同一个 Docker 网络 todo-network 中
- 服务间通过服务名进行通信

#### 通信方式

- **前端到后端** ：前端容器内的 Nginx 将 `/api` 请求反向代理到 http://backend:5000/api/todos
- **后端到数据库** ：后端通过 db:3306 访问 MySQL 数据库

### ArgoCD 阶段

#### 通信流程

外部请求 → 前端 Service → 前端 Pod → Nginx 反向代理 → 后端 Service → 后端 Pod

#### 网络配置
- 所有服务（前端、后端、数据库）都在 todos 命名空间中
- 服务间通过 Kubernetes Service 名进行通信
#### 通信方式
- 前端到后端 ：前端容器内的 Nginx 将 `/api` 请求反向代理到 http://backend:5000/api/todos
- 后端到数据库 ：后端通过 mysql 服务名访问 MySQL 数据库

## 环境变量

### 本地开发阶段

环境变量获取自 `todos-fullstack/.env`

### Docker Compose 阶段

- 环境变量获取自 `todos-fullstack/.env`
- 但 DB_HOST 在 `docker-compose.yml` 中硬编码

### ArgoCD 阶段

在 `backend.yaml` 中创建 backend-secret 对象，创建以下环境变量：

- SECRET_KEY

在 `mysql.yaml` 中创建 mysql-config 对象，创建以下环境变量：

- MYSQL_DATABASE
- DB_HOST

在 `mysql.yaml` 中创建 mysql-secret对象，创建以下环境变量：

- MYSQL_ROOT_PASSWORD
- MYSQL_USER
- MYSQL_PASSWORD

## 总结

本项目是一个完整的 React + Flask + MySQL 全栈应用，支持 Docker 容器化和使用 Argo CD 进行 Kubernetes 部署。通过本教程，你可以学习到：

1. 如何创建 React 前端应用
2. 如何创建 Flask 后端 API
3. 如何设计和使用 MySQL 数据库
4. 如何使用 Docker 和 Docker Compose 进行容器化部署
5. 如何使用 GitLab CI/CD 进行自动化构建
6. 如何使用 Argo CD 进行 GitOps 风格的 Kubernetes 部署和管理

希望本教程对你有所帮助，祝你学习愉快！
