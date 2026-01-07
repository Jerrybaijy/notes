---
title: todo-gcp
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
  - helm
  - argo-cd
  - nginx
  - vite
  - flask-migrate
  - cloud-computing
  - gcp
  - gke
  - cloud-build
  - cloud-sql
  - artifact-registry
  - gcp-repositories
  - terraform
---

# 项目概述

## 项目概述

Todo GCP 是一个完整的全栈 Web 应用原型，采用 GitOps 理念设计和部署，展示了如何使用现代 DevOps 工具链构建、部署和管理一个完整的 Web 应用，涵盖了从开发到生产环境的全流程。



## 项目特点

- **模块化设计**：前后端分离，便于独立开发和部署
- **容器化实现**：所有组件均容器化，确保环境一致性
- **GitOps 实践**：代码即基础设施，自动化部署和同步
- **多环境支持**：支持开发、测试和生产环境的部署
- **支持多种部署方式**：Docker Compose、Kubernetes、Helm Chart、Argo CD
- **可扩展性**：使用 Kubernetes 和 Helm 实现应用的水平扩展

## 技术栈

### 前端技术栈

- **框架**：React
- **构建工具**：Vite
- **样式**：CSS
- **容器化**：Docker + Nginx

### 后端技术栈

- **框架**：Flask (Python)
- **数据库**：MySQL
- **ORM**：SQLAlchemy
- **迁移工具**：Flask-Migrate (Alembic)
- **API**：RESTful API
- **容器化**：Docker

### 部署技术栈

- **容器编排**：Docker Compose, Kubernetes
- **GitOps**：Argo CD
- **包管理**：Helm
- **CI/CD**：Cloud Build
- **Cloud**：GCP, Cloud SQL, Terraform

## 项目结构

```
todo-gcp/
│
├── argo-cd/                # Argo CD 部署配置
│   ├── chart-app.yaml      # Helm Chart Argo CD 应用配置
│   └── k8s-app.yaml        # Kubernetes Argo CD 应用配置
│
├── backend/                # 后端代码目录
│   ├── app/                # 后端应用目录
│   │   ├── api/            # API 路由目录
│   │   │   ├── __init__.py # API 蓝图文件
│   │   │   └── rutes.py    # API 路由文件
│   │   ├── __init__.py     # 后端应用初始化文件
│   │   └── models.py       # 数据库模型文件
│   ├── migrations/         # 数据库迁移目录
│   ├── boot.sh             # 后端启动脚本
│   ├── config.py           # 后端配置文件
│   ├── Dockerfile          # 后端 Docker 镜像构建文件
│   ├── requirements.txt    # 后端依赖列表
│   └── run.py              # 后端入口文件
│
├── frontend/               # 前端代码目录
│   ├── src/                # 前端应用代码
│   │   ├── App.css         # 主组件样式表
│   │   ├── App.jsx         # 主组件
│   │   └── main.jsx        # 前端入口文件
│   ├── Dockerfile          # 前端 Docker 镜像构建文件
│   ├── index.html          # 前端入口 HTML 文件
│   ├── nginx.conf          # 前端请求反向代理（容器化环境）
│   ├── package.json        # npm 依赖
│   └── vite.config.js      # 前端请求代理（本地环境）
│
├── k8s/                    # Kubernetes 部署文件
│   ├── backend.yaml        # 后端部署配置
│   ├── frontend.yaml       # 前端部署配置
│   ├── mysql.yaml          # MySQL 部署配置
│   └── namespace.yaml      # 命名空间配置
│
├── terraform/              # GCP 的 Terraform 部署文件
│   ├── .terraform.lock.hcl # 依赖锁定文件
│   ├── api.tf              # GCP API
│   ├── argo-cd.tf          # Argo CD 配置文件
│   ├── cloud-sql.tf        # Cloud SQL 配置文件
│   ├── cloudbuild-trigger.tf # Cloud Build Trigger 配置文件
│   ├── docker-repo.tf      # Artifact Repository 配置文件
│   ├── gitlab-repo.tf      # 链接到 GitLab 配置文件
│   ├── gke.tf              # GKE 配置文件
│   ├── iam.tf              # GCP 权限配置文件
│   ├── terraform.tf        # Provider 版本配置文件
│   ├── todo-app.tf         # Argo CD CR 配置文件
│   └── variables.tf        # Terraform 变量
│
├── helm-chart/             # Helm Chart 目录
│   ├── templates/          # Kubernetes 资源模板目录
│   │   ├── namespace.yaml  # 命名空间配置模板
│   │   ├── _helpers.tpl    # 模板函数
│   │   ├── mysql.yaml      # MySQL 部署配置模板
│   │   ├── backend.yaml    # 后端部署配置模板
│   │   └── frontend.yaml   # 前端部署配置模板
│   ├── Chart.yaml          # Chart 元数据
│   └── values.yaml         # 模板文件参数配置
│
├── .env                    # 环境变量（未推送至代码仓库）
├── .env.example            # 环境变量示例文件
├── .gitignore              # Git 忽略文件配置
├── .gitlab-ci.yml          # GitLab CI/CD 配置
├── docker-compose.yml      # Docker Compose 配置
└── README.md               # 项目说明文档
```

## 项目存储

- **代码仓库**
  - **GitLab:** https://gitlab.com/jerrybai/todo-gcp
  - **GitHub:** https://github.com/Jerrybaijy/todo-gcp

- **镜像仓库**
  - **后端 Image:** oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/todo-docker-repo/todo-gcp-backend
  - **前端 Image:** oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/todo-docker-repo/todo-gcp-frontend
  - **项目 Chart:** oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/todo-docker-repo/todo-chart

# 项目准备

## 创建项目根目录

```bash
mkdir -p d:/projects/todo-gcp
```

## 初始化 Git 仓库

```bash
cd d:/projects/todo-gcp
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

配置环境变量：`todo-gcp/.env`

```bash
cd d:/projects/todo-gcp
touch .env
```

```toml
# MySQL 数据库配置
DB_HOST=localhost
MYSQL_DATABASE=todo_db
MYSQL_ROOT_PASSWORD=123456
MYSQL_USER=jerry
MYSQL_PASSWORD=000000

# 数据库迁移, flask db init 中的 flask 对应 FLASK_APP
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=change_this_to_a_very_long_random_string
```

同时，为了让协作者知道需要配什么，创建一个 `todo-gcp/.env.example` (不含真实密码)：

```bash
cd d:/projects/todo-gcp
touch .env.example
```

```toml
# MySQL 数据库配置
DB_HOST=
MYSQL_DATABASE=todo_db
MYSQL_ROOT_PASSWORD=
MYSQL_USER=
MYSQL_PASSWORD=

# Flask 配置
FLASK_APP=run.py
FLASK_ENV=production

# change_this_to_a_very_long_random_string
SECRET_KEY=
```

# 后端开发

## 创建后端目录结构

```bash
cd d:/projects/todo-gcp
mkdir -p backend/app/api
```

## 虚拟环境

```bash
cd d:/projects/todo-gcp/backend

# 提前复制 python-env 脚本到 backend 目录
source python-env
```

## 安装依赖

```bash
cd d:/projects/todo-gcp/backend
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
    DB_HOST = os.environ.get("DB_HOST") or "localhost"
    DB_NAME = os.environ.get("MYSQL_DATABASE") or "todo_db"
    DB_USER = os.environ.get("MYSQL_USER") or "root"
    DB_PASS = os.environ.get("MYSQL_PASSWORD") or "password"

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
docker run --name todo-mysql-local \
    -e MYSQL_DATABASE=todo_db \
    -e MYSQL_ROOT_PASSWORD=123456 \
    -e MYSQL_USER=jerry \
    -e MYSQL_PASSWORD=000000 \
    -p 3306:3306 \
    -d mysql:8.0
```

## 初始化数据库迁移

在开发环境中初始化数据库迁移

```bash
# 确保虚拟环境已激活
# 确保全新数据库已正常运行

cd d:/projects/todo-gcp/backend

# 初始化迁移仓库（仅首次需要）,这会在 backend 目录下创建 migrations 目录
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
  cd d:/projects/todo-gcp/backend
  source venv/Scripts/activate
  
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
cd d:/projects/todo-gcp
npm create vite@latest frontend -- --template react

# 安装依赖
cd d:/projects/todo-gcp/frontend
npm install
# 安装 axios 用于 API 请求
npm install axios

# 删除 frontend/src 目录中的 assets 目录和 index.css 文件
```

## `App.jsx`

修改主组件 `src/App.jsx`

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

修改主组件样式表 `src/App.css`

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

修改前端入口文件 `main.jsx`

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

修改前端入口 HTML 文件 `frontend/index.html`

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
  cd d:/projects/todo-gcp/backend
  source venv/Scripts/activate
  python run.py
  ```

- 启动前端

  ```bash
  cd d:/projects/todo-gcp/frontend
  npm run dev
  ```

- 访问前端： http://localhost:5173/

- 前后端通信正常，MySQL 数据变化正常。

# Docker Compose

## `boot.sh`

后端启动脚本 `backend/boot.sh`，首先进行数据库迁移。

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

## `.env`

修改环境变量：`todo-gcp/.env`

由于 `docker-compose.yml` 中 MySQL 的服务名变更为 `db`，所以要将 `.env` 中的 `DB_HOST` 由 `localhost` 改为 `db`。

```toml
# MySQL 数据库配置
DB_HOST=db
MYSQL_DATABASE=todo_db
MYSQL_ROOT_PASSWORD=123456
MYSQL_USER=jerry
MYSQL_PASSWORD=000000

# 数据库迁移, flask db init 中的 flask 对应 FLASK_APP
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=change_this_to_a_very_long_random_string
```

## `docker-compose.yml`

容器编排文件 `todo-gcp/docker-compose.yml`，环境变量获取自 `todo-gcp/.env`。

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
      DB_HOST: ${DB_HOST}
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

## 多容器集成测试

- 停止开发环境的 MySQL

- 使用 Docker Compose 构建前端、后端镜像，并启动前端、后端和数据库容器。

  ```bash
  cd d:/projects/todo-gcp
  docker-compose up -d
  ```

- 外部访问 ：

  - 前端： http://localhost:80
  - 后端：http://localhost:5000/api/todos
  - 数据库： http://localhost:3306

- 停止项目

  停止以后，需在 Docker Desktop 中删除相应的 Image 和 Volume。

  ```bash
  cd d:/projects/todo-gcp
  docker-compose down
  ```

# Helm Chart

## 创建 Chart 目录

- 创建 Chart 目录

  ```bash
  cd d:/projects/todo-gcp
  helm create helm-chart
  ```

- 删除 `templates` 目录下的全部默认文件

- 保留并修改以下必要文件：

  - `Chart.yaml`：Chart 元数据
  - `values.yaml`：模板文件的参数值
  - `.helmignore`：忽略不需要打包的文件
  - `templates/`：模板文件目录

- 在 `templates` 目录创建以下文件

  ```bash
  cd d:/projects/todo-gcp/todo-chart/templates/
  touch namespace.yaml _helpers.tpl mysql.yaml backend.yaml frontend.yaml
  ```

## `Chart.yaml`

Chart 的元数据 `helm-chart/Chart.yaml`

```yaml
apiVersion: v2
name: todo-chart
description: A Helm chart for Todo application
version: 0.1.0
type: application
appVersion: "1.0.0"
```

## `values.yaml`

模板文件的参数值 `helm-chart/values.yaml`

```yaml
# 全局配置
global:
  namespace: todo

# 1. 关键：用于模板函数中生成 Cloud SQL 实例连接名称
gcp:
  projectId: "project-60addf72-be9c-4c26-8db"
  region: "asia-east2"
  sqlInstanceName: "todo-db-instance"

# Backend 配置
backend:
  # 2. 关键：添加 ksa 名称
  ksaName: todo-ksa
  replicaCount: 2
  image:
    repository: jerrybaijy/todo-gcp-backend
    tag: latest
    pullPolicy: Always
  service:
    type: ClusterIP
    port: 5000
  env:
    SECRET_KEY: your_secret_key_here
    # 3. 关键：添加 Cloud SQL 的环境变量
    # 由于 Cloud SQL 实例已配置 Cloud SQL Auth Proxy，
    # 因此数据库主机地址指向本地回环地址和默认端
    DB_HOST: "127.0.0.1"        # 本地回环地址
    MYSQL_PORT: "3306"          # MySQL 端口
    MYSQL_DATABASE: "todo_db"   # 数据库名称
    MYSQL_USER: "jerry"         # 数据库用户名
    MYSQL_PASSWORD: "000000"    # 数据库密码

# Frontend 配置
frontend:
  replicaCount: 2
  image:
    repository: jerrybaijy/todo-gcp-frontend
    tag: latest
    pullPolicy: Always
  service:
    # 4. 关键：前端服务类型改为 LoadBalancer 以支持公网访问
    type: LoadBalancer
    port: 80
```

## `namespace.yaml`

命名空间 `templates/namespace.yaml`

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: {{ .Values.global.namespace }}
  labels:
    name: {{ .Values.global.namespace }}
```

## `_helpers.tpl`

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

{{/* 生成 Cloud SQL 实例连接名称 */}}
{{- define "todo-chart.sqlInstanceConnectionName" -}}
{{- printf "%s:%s:%s" .Values.gcp.projectId .Values.gcp.region .Values.gcp.sqlInstanceName -}}
{{- end -}}

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

## `backend.yaml`

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
  # 1. 关键：添加数据库连接相关的环境变量
  DB_HOST: {{ .Values.backend.env.DB_HOST | quote }}
  MYSQL_PORT: {{ .Values.backend.env.MYSQL_PORT | quote }}
  MYSQL_DATABASE: {{ .Values.backend.env.MYSQL_DATABASE | quote }}
  MYSQL_USER: {{ .Values.backend.env.MYSQL_USER | quote }}
  MYSQL_PASSWORD: {{ .Values.backend.env.MYSQL_PASSWORD | quote }}
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
      # 2. 关键：指定 ksa 以支持 Workload Identity
      serviceAccountName: {{ .Values.backend.ksaName }}
      containers:
        - name: backend
          image: "{{ .Values.backend.image.repository }}:{{ .Values.backend.image.tag }}"
          imagePullPolicy: {{ .Values.backend.image.pullPolicy }}
          envFrom:
            - secretRef:
                name: {{ include "todo-chart.backend.fullname" . }}-secret
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
        # 3. 关键：添加 cloud-sql-proxy 容器，连接到 Cloud SQL 实例
        - name: cloud-sql-proxy
          image: gcr.io/cloud-sql-connectors/cloud-sql-proxy:2.14.1
          args:
            - "--port=3306"
            - {{ include "todo-chart.sqlInstanceConnectionName" . | quote }}
          securityContext:
            runAsNonRoot: true
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

## `frontend.yaml`

前端模板文件 `templates/frontend.yaml`

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

# Terraform

## 创建 Terraform 目录和配置文件

```bash
mkdir -p d:/projects/todo-gcp/terraform
cd d:/projects/todo-gcp/terraform
touch terraform.tf api.tf iam.tf gke.tf docker-repo.tf cloud-sql.tf variables.tf terraform.tfvars
```

## `terraform.tf`

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 7.14.0"
    }
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = "~> 3.0.0"
    }
    helm = {
      source  = "hashicorp/helm"
      version = "~> 3.1.0"
    }
    time = {
      source  = "hashicorp/time"
      version = "~> 0.11.1"
    }
  }
}
```

## `api.tf`

```hcl
locals {
  services = [
    "compute.googleapis.com",          # Compute Engine API
    "container.googleapis.com",        # Kubernetes Engine API
    "iam.googleapis.com",              # IAM API
    "iamcredentials.googleapis.com",   # Workload Identity API
    "sqladmin.googleapis.com",         # Cloud SQL API
    "artifactregistry.googleapis.com", # Artifact Registry API
    "cloudbuild.googleapis.com",       # Cloud Build API
    "secretmanager.googleapis.com"     # Secret Manager API
  ]
}

resource "google_project_service" "project_services" {
  for_each           = toset(local.services)
  service            = each.key
  disable_on_destroy = false
}
```

## `iam.tf`

GCP IAM 配置文件 `terraform/iam.tf`

```hcl
# 获取当前 Project ID
data "google_project" "project" {}

# 创建 GSA
resource "google_service_account" "workload_identity" {
  account_id   = local.sa_id
  display_name = "GSA for Workload Identity"
}

# 为 GSA 分配多个角色
resource "google_project_iam_member" "gsa_roles" {
  for_each = toset([
    "roles/cloudsql.client",         # Cloud SQL Client
    "roles/artifactregistry.writer", # Artifact Registry Writer
    "roles/artifactregistry.reader", # Artifact Registry Reader
    "roles/logging.logWriter",       # Logs Writer
  ])

  project = var.project_id
  role    = each.key
  member  = "serviceAccount:${google_service_account.workload_identity.email}"
}

# 创建 app_ns，防止因 app_ns 不存在而导致创建 KSA 失败
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = local.app_ns
    annotations = {
      # 加注解，防止 Argo CD 删除该 Namespace
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
  lifecycle {
    ignore_changes = [
      metadata[0].labels # 忽略标签变化
    ]
  }
}

# 创建 KSA，并绑定到 GSA
resource "kubernetes_service_account_v1" "my_ksa" {
  metadata {
    name      = local.ksa_name
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
      # 加注解，防止 Argo CD 删除该 KSA
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
}

# 允许 KSA 以 GSA 身份运行
resource "google_service_account_iam_member" "workload_identity_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[${local.app_ns}/${local.ksa_name}]"
}

# 允许 argocd-repo-server SA 以 GSA 身份运行
resource "google_service_account_iam_member" "argocd_repo_server_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[argocd/argocd-repo-server]"
}

output "app_namespace" {
  description = "Kubernetes Namespace Name"
  value       = kubernetes_namespace_v1.app_ns.metadata[0].name
}

output "ksa_name" {
  description = "Kubernetes Service Account Name"
  value       = kubernetes_service_account_v1.my_ksa.metadata[0].name
}

# 创建 Cloud Build 的 GSA
resource "google_service_account" "cloudbuild_worker" {
  account_id   = "${var.prefix}-cloudbuild-worker"
  display_name = "Cloud Build Worker Service Account"
}

# 为 GSA 分配角色
resource "google_project_iam_member" "cloudbuild_worker_roles" {
  for_each = toset([
    "roles/logging.logWriter",       # Logs Writer
    "roles/artifactregistry.writer", # Artifact Registry Writer
    "roles/artifactregistry.reader"  # Artifact Registry Reader
  ])

  project = var.project_id
  role    = each.key
  member  = "serviceAccount:${google_service_account.cloudbuild_worker.email}"
}

# 允许 Cloud Build 服务代理访问 Secret Manager 中的 Secrets
resource "google_secret_manager_secret_iam_member" "cloudbuild_secret_accessor" {
  for_each = {
    api     = google_secret_manager_secret.gitlab_api_token.id
    read    = google_secret_manager_secret.gitlab_read_api_token.id
    webhook = google_secret_manager_secret.webhook_secret.id
  }
  secret_id = each.value
  role      = "roles/secretmanager.secretAccessor"
  # 必须使用 Cloud Build 的 Service Agent 账号
  member = "serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloudbuild.iam.gserviceaccount.com"
}

# 允许 Cloud Build 服务代理以 GSA 身份运行
# 否则 Cloud Build 服务代理无法代表 GSA 执行构建任务
resource "google_service_account_iam_member" "cloudbuild_worker_binding" {
  service_account_id = google_service_account.cloudbuild_worker.name
  role               = "roles/iam.serviceAccountUser"
  member             = "serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloudbuild.iam.gserviceaccount.com"
}
```

## `gke.tf`

GKE 配置文件 `terraform/gke.tf`

```hcl
# 添加 Google Provider
provider "google" {
  project = var.project_id
  region  = var.region
  zone    = var.zone
}

# 添加 Kubernetes Provider
data "google_client_config" "default" {}
provider "kubernetes" {
  host                   = "https://${google_container_cluster.my_cluster.endpoint}"
  token                  = data.google_client_config.default.access_token
  cluster_ca_certificate = base64decode(google_container_cluster.my_cluster.master_auth[0].cluster_ca_certificate)
}

# 创建 GKE 集群
resource "google_container_cluster" "my_cluster" {
  name                     = local.gke_name
  location                 = var.region
  remove_default_node_pool = true
  initial_node_count       = 1
  depends_on               = [google_project_service.project_services]

  # 启用 Workload Identity
  workload_identity_config {
    workload_pool = "${data.google_project.project.project_id}.svc.id.goog"
  }

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# 创建 Node Pool
resource "google_container_node_pool" "my_node_pool" {
  name       = local.node_pool_name
  location   = var.region
  cluster    = google_container_cluster.my_cluster.name
  node_count = 1

  autoscaling {
    min_node_count = 1
    max_node_count = 5
  }

  node_config {
    machine_type    = "e2-medium"
    service_account = google_service_account.workload_identity.email
    oauth_scopes = [
      "https://www.googleapis.com/auth/cloud-platform"
    ]

    # 使用 Workload Identity 暴露元数据
    workload_metadata_config {
      mode = "GKE_METADATA"
    }
  }
}

output "gke_name" {
  description = "GKE name"
  value       = google_container_cluster.my_cluster.name
}
```

## `docker-repo.tf`

GAR 配置文件 `terraform/docker-repo.tf`

```hcl
# 创建 Docker 仓库
resource "google_artifact_registry_repository" "docker_repo" {
  repository_id = local.chart_repo_name
  format        = "DOCKER"
  depends_on    = [google_project_service.project_services]
}
```

## `gitlab-repo.tf`

Repositories 配置文件 `terraform/gitlab-repo.tf`：链接到 GitLab

```hcl
# 1. 存储 Token 到 Secret Manager

# 创建存储 API Token 的 Secret
resource "google_secret_manager_secret" "gitlab_api_token" {
  secret_id = "${var.code_repo}-api-token"
  replication {
    auto {}
  }
}

# 存入具体的 API Token 值
resource "google_secret_manager_secret_version" "api_token_version" {
  secret      = google_secret_manager_secret.gitlab_api_token.id
  secret_data = var.gitlab_personal_access_token_api
}

# 创建存储 Read API Token 的 Secret
resource "google_secret_manager_secret" "gitlab_read_api_token" {
  secret_id = "${var.code_repo}-read-api-token"
  replication {
    auto {}
  }
}

# 存入具体的 Read API Token 值
resource "google_secret_manager_secret_version" "read_api_token_version" {
  secret      = google_secret_manager_secret.gitlab_read_api_token.id
  secret_data = var.gitlab_personal_access_token_read_api
}

# 随机生成一个 Webhook 密钥
resource "random_password" "webhook_secret_value" {
  length  = 16
  special = false
}

# 创建 Secret Manager 容器
resource "google_secret_manager_secret" "webhook_secret" {
  secret_id = "gitlab-webhook-secret"
  replication {
    auto {}
  }
}

# 存入随机生成的密钥值
resource "google_secret_manager_secret_version" "webhook_secret_version" {
  secret      = google_secret_manager_secret.webhook_secret.id
  secret_data = random_password.webhook_secret_value.result
}

# 2. 连接到 GitLab 主机 (2nd Gen)
resource "google_cloudbuildv2_connection" "my_gitlab_connection" {
  location = var.region
  name     = local.code_repo_host

  gitlab_config {
    # 引用 Secret Manager 中的令牌
    authorizer_credential {
      user_token_secret_version = google_secret_manager_secret_version.api_token_version.id
    }
    read_authorizer_credential {
      user_token_secret_version = google_secret_manager_secret_version.read_api_token_version.id
    }
    webhook_secret_secret_version = google_secret_manager_secret_version.webhook_secret_version.id
  }
}

# 3. 链接具体的代码仓库
resource "google_cloudbuildv2_repository" "my_repo" {
  name              = "${var.repo_username}-${local.project_name}"
  location          = google_cloudbuildv2_connection.my_gitlab_connection.location
  parent_connection = google_cloudbuildv2_connection.my_gitlab_connection.id
  remote_uri        = "https://gitlab.com/${var.repo_username}/${local.project_name}.git"
}
```

## `cloudbuild-trigger.tf`

Cloud Build Trigger 配置文件 `terraform/cloudbuild-trigger.tf`

```hcl
# 为 GitLab 仓库创建 Cloud Build 触发器
resource "google_cloudbuild_trigger" "gitlab_trigger" {
  name            = local.trigger_name
  location        = google_cloudbuildv2_repository.my_repo.location
  service_account = google_service_account.cloudbuild_worker.id

  # 使用第 2 代连接 (v2 repository)
  repository_event_config {
    repository = google_cloudbuildv2_repository.my_repo.id
    push {
      branch = "^main$"
    }
  }

  # 指定构建配置
  filename = "cloudbuild.yaml"

  included_files = [
    "backend/**",
    "frontend/**",
    "helm-chart/**"
  ]

  depends_on = [
    google_cloudbuildv2_repository.my_repo,
    google_secret_manager_secret_iam_member.cloudbuild_secret_accessor,
    google_project_iam_member.cloudbuild_worker_roles,
    google_service_account_iam_member.cloudbuild_worker_binding
  ]
}
```

## `cloud-sql.tf`

Cloud SQL 配置文件 `terraform/cloud-sql.tf`

```hcl
# 创建 Cloud SQL 实例
resource "google_sql_database_instance" "mysql_instance" {
  name             = local.db_instance
  database_version = "MYSQL_8_0"
  region           = var.region

  settings {
    tier            = "db-f1-micro" # 测试环境使用的最小规格
    disk_type       = "PD_SSD"
    disk_size       = 10   # 初始 10GB
    disk_autoresize = true # 自动扩容

    # 开启公网 IP，但会通过 IAM 权限锁定访问，仅允许通过授权代理访问
    ip_configuration {
      ipv4_enabled = true
    }
  }

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# 创建 DATABASE
resource "google_sql_database" "my_db" {
  name      = local.db_name
  instance  = google_sql_database_instance.mysql_instance.name
  charset   = "utf8mb4"
  collation = "utf8mb4_unicode_ci"
}

# 创建 root 用户
resource "google_sql_user" "root_user" {
  name     = "root"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_root_password
  host     = "%"
}

# 创建普通账户
resource "google_sql_user" "jerry_user" {
  name     = "jerry"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_jerry_password
  host     = "%"
}

output "cloud_sql_connection_name" {
  description = "Cloud SQL instance connection name"
  value       = google_sql_database_instance.mysql_instance.connection_name
}

output "sql_instance_name" {
  description = "Cloud SQL 实例的名称"
  value       = google_sql_database_instance.mysql_instance.name
}

output "database_name" {
  description = "Cloud SQL database name"
  value       = google_sql_database.my_db.name
}
```

## `argo-cd.tf`

Argo CD 配置文件 `terraform/argo-cd.tf`

- 在安装 Argo CD 时添加 argocd-repo-server 的 GSA 注解
- 创建 Argo CD 访问 GAR 的 Secret

```hcl
# 添加 Helm Provider
provider "helm" {
  kubernetes = {
    host                   = "https://${google_container_cluster.my_cluster.endpoint}"
    token                  = data.google_client_config.default.access_token
    cluster_ca_certificate = base64decode(google_container_cluster.my_cluster.master_auth[0].cluster_ca_certificate)
  }
}

# 创建 Argo CD 命名空间
resource "kubernetes_namespace_v1" "argocd_ns" {
  metadata {
    name = "argocd"
  }
  depends_on = [google_container_node_pool.my_node_pool]
}

# 安装 Argo CD
resource "helm_release" "argocd" {
  name       = "argocd"
  repository = "https://argoproj.github.io/argo-helm"
  chart      = "argo-cd"
  namespace  = kubernetes_namespace_v1.argocd_ns.metadata[0].name
  version    = "7.7.1"

  set = [
    # 添加 argocd-repo-server 的 GSA 注解，以启用 Workload Identity
    {
      name  = "repoServer.serviceAccount.annotations.iam\\.gke\\.io/gcp-service-account"
      value = google_service_account.workload_identity.email
    },
    # 设置服务类型为 LoadBalancer
    {
      name  = "server.service.type"
      value = "LoadBalancer"
    },
    # 允许 HTTP 访问
    {
      name  = "server.extraArgs"
      value = "{--insecure}"
    },
    # 仅允许自己的 IP 访问
    {
      name  = "server.service.loadBalancerSourceRanges"
      value = "{${var.my_external_ip}/32}"
    }
  ]

  depends_on = [
    google_service_account.workload_identity,
    google_service_account_iam_member.argocd_repo_server_binding
  ]
}

# 创建 Argo CD 访问 GAR 的 Secret
resource "kubernetes_secret_v1" "gar_repo_secret" {
  metadata {
    name      = "gar-repo-secret"
    namespace = kubernetes_namespace_v1.argocd_ns.metadata[0].name
    labels = {
      "argocd.argoproj.io/secret-type" = "repository"
    }
  }

  data = {
    name      = "todo-docker-repo"
    type      = "helm"
    url       = local.chart_repo_url
    enableOCI = "true"
  }
}

# 获取 Argo CD 服务数据 (用于 Output)
data "kubernetes_service_v1" "argocd_server" {
  metadata {
    name      = "${helm_release.argocd.name}-server"
    namespace = helm_release.argocd.namespace
  }
  depends_on = [helm_release.argocd]
}

# 获取初始密码 Secret 数据
data "kubernetes_secret_v1" "argocd_initial_admin_secret" {
  metadata {
    name      = "argocd-initial-admin-secret"
    namespace = helm_release.argocd.namespace
  }
  depends_on = [helm_release.argocd]
}

# 输出 Argo CD 公网 IP
output "argocd_loadbalancer_ip" {
  description = "Argo CD UI 的公网访问 IP"
  value       = data.kubernetes_service_v1.argocd_server.status[0].load_balancer[0].ingress[0].ip
}

# 输出初始管理员密码
output "argocd_initial_admin_password" {
  description = "Argo CD 的初始管理员密码 (用户名为 admin)"
  value       = data.kubernetes_secret_v1.argocd_initial_admin_secret.data["password"]
  sensitive   = true
}
```

## `todo-app.tf`

Argo CD 的 CR 资源配置文件 `terraform/todo-app.tf`

```hcl
# 增加一个睡眠资源
resource "time_sleep" "wait_for_argocd" {
  depends_on      = [helm_release.argocd]
  create_duration = "30s"
}

# 使用 kubernetes_manifest 部署 Argo CD Application
resource "kubernetes_manifest" "my_app" {
  manifest = {
    "apiVersion" = "argoproj.io/v1alpha1"
    "kind"       = "Application"
    "metadata" = {
      "name"      = local.app_name
      "namespace" = kubernetes_namespace_v1.argocd_ns.metadata[0].name
      "finalizers" = [
        "resources-finalizer.argocd.argoproj.io"
      ]
    }
    "spec" = {
      "project" = "default"
      "source" = {
        "repoURL"        = local.chart_repo_url
        "targetRevision" = "99.99.99-latest"
        "chart"          = local.chart_name
      }
      "destination" = {
        "server"    = "https://kubernetes.default.svc"
        "namespace" = kubernetes_namespace_v1.app_ns.metadata[0].name
      }
      "syncPolicy" = {
        "automated" = {
          "selfHeal" = true
          "prune"    = true
        }
        "syncOptions" = [
          "ApplyOutOfSyncOnly=true"
        ]
        "retry" = {
          "limit" = 5
          "backoff" = {
            "duration"    = "5s"
            "factor"      = 2
            "maxDuration" = "3m"
          }
        }
      }
    }
  }
  depends_on = [
    helm_release.argocd,
    time_sleep.wait_for_argocd,
    google_sql_user.root_user
  ]
}
```

## `variables.tf`

变量配置文件 `terraform/variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
  default     = "todo"
}

locals {
  gke_name        = "${var.prefix}-cluster"
  node_pool_name  = "${var.prefix}-node-pool"
  app_ns          = "${var.prefix}-ns"
  sa_id           = "${var.prefix}-sa-id"
  ksa_name        = "${var.prefix}-ksa"
  db_instance     = "${var.prefix}-db-instance"
  db_name         = "${var.prefix}_db"
  app_name        = "${var.prefix}-app"
  chart_repo_name = "${var.prefix}-docker-repo"
  chart_name      = "${var.prefix}-chart"
  chart_repo_url  = "${var.region}-docker.pkg.dev/${var.project_id}/${local.chart_repo_name}"
  code_repo_host  = "${var.prefix}-${var.code_repo}-host"
  project_name    = "${var.prefix}-gcp"
  trigger_name    = "${var.prefix}-trigger"
}

# --- GCP ---
variable "project_id" {
  type        = string
  description = "GCP Project ID"
  default     = "project-60addf72-be9c-4c26-8db"
}

variable "region" {
  type        = string
  description = "GCP Region"
  default     = "asia-east2"
}

variable "zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east2-a"
}

# --- Cloud SQL ---
variable "mysql_root_password" {
  type        = string
  description = "MySQL root user password"
  sensitive   = true
}

variable "mysql_jerry_password" {
  type        = string
  description = "MySQL jerry user password"
  sensitive   = true
}

# --- Argo CD ---
variable "my_external_ip" {
  type        = string
  description = "My external IP access to Argo CD"
  sensitive   = true
}

# --- Repo ---
variable "code_repo" {
  type        = string
  description = "Code repo"
  default     = "gitlab"
}

variable "repo_username" {
  type        = string
  description = "Repo username"
  default     = "jerrybai"
}

# --- Secrets ---
variable "gitlab_personal_access_token_api" {
  type        = string
  description = "GitLab Personal Access Token for API"
  sensitive   = true
}

variable "gitlab_personal_access_token_read_api" {
  type        = string
  description = "GitLab Personal Access Token for Read"
  sensitive   = true
}
```

## `terraform.tfvars`

敏感变量赋值文件 `terraform/terraform.tfvars`

```hcl
mysql_root_password                   = "123456"
mysql_jerry_password                  = "000000"
my_external_ip                        = "5.181.21.188"
gitlab_personal_access_token_api      = "gitlab_personal_access_token_api"
gitlab_personal_access_token_read_api = "gitlab_personal_access_token_read_api"
```

## `.gitignore`

添加[忽略内容](terraform-configuration-language.md#`.gitignore`)：

```
# Terraform
.terraform/
*.tfstate
*.tfstate.*
.terraform.tfstate.lock.info
*.tfplan
*.tfvars
*.tfvars.json
```

## 初始化 Terraform

```bash
cd d:/projects/todo-gcp/terraform
terraform init
```

# Cloud Build

## 创建 GAR 和链接 GitLab

需先创建 GitLab Personal Tokens

```bash
# 链接到 GitLab 和创建 Trigger
terraform apply -target=google_cloudbuild_trigger.gitlab_trigger

# 创建 Artifact Registry Docker Repositoy
terraform apply -target=google_artifact_registry_repository.docker_repo
```

## `cloudbuild.yaml`

Cloud Build 配置文件 `todo-gcp/cloudbuild.yaml`

```yaml
steps:
  # 获取完整的 Git 历史，确保 HEAD^ 可用
  - name: "gcr.io/cloud-builders/git"
    id: "unshallow"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        git fetch --unshallow || true

  # 1. 构建并推送后端镜像
  - name: "gcr.io/cloud-builders/docker"
    id: "build-backend"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        # 检查 backend 目录在当前 commit 中是否有变动
        if git diff --quiet HEAD^ HEAD -- ${_BACKEND_DIR}; then
          echo "No changes in backend, skipping build."
        else
          echo "Changes detected, starting backend build..."
          cd ${_BACKEND_DIR} && \
          docker build -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:${SHORT_SHA} \
              -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:latest . && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:${SHORT_SHA} && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:latest
        fi

  # 2. 构建并推送前端镜像
  - name: "gcr.io/cloud-builders/docker"
    id: "build-frontend"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        # 检查 frontend 目录在当前 commit 中是否有变动
        if git diff --quiet HEAD^ HEAD -- ${_FRONTEND_DIR}; then
          echo "No changes in frontend, skipping build."
        else
          echo "Changes detected, starting frontend build..."
          cd ${_FRONTEND_DIR} && \
          docker build -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:${SHORT_SHA} \
              -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:latest . && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:${SHORT_SHA} && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:latest
        fi

  # 3. 打包并推送 Helm Chart
  - name: "alpine/helm:3.12.3"
    id: "publish-chart"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        BACKEND_CHANGED=$(git diff --name-only HEAD^ HEAD | grep "^${_BACKEND_DIR}/" || true)
        FRONTEND_CHANGED=$(git diff --name-only HEAD^ HEAD | grep "^${_FRONTEND_DIR}/" || true)
        CHART_CHANGED=$(git diff --name-only HEAD^ HEAD | grep "^${_CHART_DIR}/" || true)

        # 检查 backend || frontend || helm-chart 目录在当前 commit 中是否有变动
        if [ -n "$$BACKEND_CHANGED" ] || [ -n "$$FRONTEND_CHANGED" ] || [ -n "$$CHART_CHANGED" ]; then
          echo "Executing chart publish..."
          curl -L https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -o /workspace/yq && \
          chmod +x /workspace/yq && \
          cd ${_CHART_DIR} && \
          CHART_VERSION=$(/workspace/yq e '.version' Chart.yaml) && \
          SHA_VERSION="$${CHART_VERSION}-${SHORT_SHA}" && \
          LATEST_VERSION="99.99.99-latest" && \
          helm package . --version "$${SHA_VERSION}" && \
          helm package . --version "$${LATEST_VERSION}" && \
          helm push ${_CHART_NAME}-$${SHA_VERSION}.tgz oci://${_OCI_REGISTRY} && \
          helm push ${_CHART_NAME}-$${LATEST_VERSION}.tgz oci://${_OCI_REGISTRY}
        else
          echo "Nothing changed that requires a chart update."
        fi

substitutions:
  _OCI_REGISTRY: asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/todo-docker-repo
  _PROJECT_NAME: todo-gcp
  _BACKEND_NAME: backend
  _FRONTEND_NAME: frontend
  _BACKEND_DIR: backend
  _FRONTEND_DIR: frontend
  _CHART_NAME: todo-chart
  _CHART_DIR: helm-chart

options:
  logging: CLOUD_LOGGING_ONLY
```

## 构建 Image 和 Chart

将源代码推送至代码仓库，触发 Cloud Build 构建并推送 image 和 chart 到 GAR。

# 部署应用

## 部署应用

**遗留问题**：Argo CD 无法拉取 GAR 中的 chart

```bash
cd d:/projects/todo-gcp/terraform

# 先安装 Argo CD 及其依赖
terraform apply -target=helm_release.argocd

# 再部署 my-app.tf 及其它资源
terraform apply
```

## 更新 kubectl 配置

```bash
gcloud container clusters get-credentials todo-cluster \
    --location asia-east2 \
    --project project-60addf72-be9c-4c26-8db
```

```bash
# 查看当前上下文
kubectl config current-context

# 切换上下文
kubectl config use-context gke_project-60addf72-be9c-4c26-8db_asia-east2_todo-cluster
```

## 访问应用

- 获取前端访问地址

  ```bash
  kubectl get svc -n todo-ns
  ```

- 访问前端：http://$EXTERNAL-IP

- 在本地电脑使用 Cloud SQL Auth 代理连接 Cloud SQL，详见 [Cloud SQL 笔记](<gcp-cloud-sql.md#Cloud SQL Auth>)。


## 销毁资源

```bash
cd d:/projects/todo-gcp/terraform
terraform destroy
```



