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
├── .env.example           # 环境变量示例文件
├── .gitignore             # Git 忽略文件配置
├── .gitlab-ci.yml         # GitLab CI/CD 配置
├── README.md              # 项目说明文档
├── argocd/                # Argo CD 配置文件
│   ├── application.yaml   # Argo CD 应用配置
│   └── ingress.yaml       # Ingress 配置（可选）
├── assets/                # README 资源文件
├── dev/                   # 开发环境 Kubernetes 配置
│   ├── backend.yaml       # 后端服务部署配置
│   ├── frontend.yaml      # 前端服务部署配置
│   └── mysql-db.yaml      # MySQL 数据库部署配置
├── docker-compose.yml     # Docker Compose 配置
├── backend/               # 后端代码目录
│   ├── Dockerfile         # 后端 Docker 镜像构建文件
│   ├── app/               # 后端应用代码
│   ├── boot.sh            # 后端启动脚本
│   ├── config.py          # 后端配置文件
│   ├── migrations/        # 数据库迁移文件
│   ├── requirements.txt   # 后端依赖列表
│   └── run.py             # 后端入口文件
└── frontend/              # 前端代码目录
    ├── Dockerfile         # 前端 Docker 镜像构建文件
    ├── nginx.conf         # Nginx 配置（用于前端静态文件服务）
    ├── package.json       # 前端依赖配置
    ├── public/            # 前端静态资源
    └── src/               # 前端应用代码
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

# 在 Docker 网络内部，数据库服务的名字叫 'db'
DB_HOST=db

# Flask 配置
FLASK_APP=run.py
FLASK_ENV=production
SECRET_KEY=change_this_to_a_very_long_random_string

# 项目名称
BACKEND_NAME=todos-react-flask-mysql-backend
FRONTEND_NAME=todos-react-flask-mysql-frontend
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

# 后端

## 目录结构

```bash
mkdir -p backend/app/api
```

## 虚拟环境

```bash
cd backend
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
pymysql==1.1.0
cryptography==41.0.7
gunicorn==21.2.0
python-dotenv==1.0.0
```

```bash
pip install -r requirements.txt
```

## `config.py`

创建后端配置文件 `backend/config.py`

```python
import os
from dotenv import load_dotenv

# 加载环境变量
load_dotenv()

class Config:
    # Flask 配置
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'your-secret-key'

    # 数据库配置
    DB_USER = os.environ.get('MYSQL_USER') or 'root'
    DB_PASS = os.environ.get('MYSQL_PASSWORD') or 'password'
    DB_HOST = os.environ.get('DB_HOST') or 'localhost'
    DB_NAME = os.environ.get('MYSQL_DATABASE') or 'todos_db'

    # SQLAlchemy 配置
    SQLALCHEMY_DATABASE_URI = f'mysql+pymysql://{DB_USER}:{DB_PASS}@{DB_HOST}/{DB_NAME}?charset=utf8mb4'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
```

## `__init__.py`

创建后端应用初始化文件 `__init__.py`

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

    # 注册蓝图
    from app.api import bp as api_bp
    app.register_blueprint(api_bp, url_prefix='/api')

    return app
```

## `models.py`

创建数据库模型文件 `app/models.py`

```python
from app import db

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

创建 API 路由文件 `app/api/routes.py`

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

创建后端入口文件 `backend/run.py`

```python
from app import create_app

app = create_app()

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

## `boot.sh`

创建后端启动脚本 `backend/boot.sh`

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

给脚本添加执行权限：

```bash
chmod +x boot.sh
```

## `Dockerfile`

创建 `backend/Dockerfile`

```dockerfile
# 使用 Python 3.10 作为基础镜像
FROM python:3.10-slim

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

## 初始化数据库迁移

```bash
# 确保虚拟环境已激活
flask db init
flask db migrate -m "Initial migration"
flask db upgrade
```

# 前端

## 创建前端项目

```bash
# 返回项目根目录
cd ..
# 使用 Vite 创建 React 项目
npm create vite@latest frontend -- --template react
cd frontend
```

## 安装前端依赖

```bash
npm install
# 安装 axios 用于 API 请求
npm install axios
```

## 修改前端应用代码

- **修改 src/App.jsx**

  ```jsx
  import { useState, useEffect } from "react";
  import axios from "axios";
  import "./App.css";

  function App() {
    // TODOs 列表状态
    const [todos, setTodos] = useState([]);
    // 新 TODO 内容状态
    const [content, setContent] = useState("");
    // 加载状态
    const [loading, setLoading] = useState(true);
    // API 基础 URL
    const API_BASE_URL = "http://localhost:5000/api";

    // 获取所有 TODOs
    const fetchTodos = async () => {
      try {
        const response = await axios.get(`${API_BASE_URL}/todos`);
        setTodos(response.data);
      } catch (error) {
        console.error("Error fetching todos:", error);
      } finally {
        setLoading(false);
      }
    };

    // 初始化时获取 TODOs
    useEffect(() => {
      fetchTodos();
    }, []);

    // 创建新 TODO
    const handleSubmit = async (e) => {
      e.preventDefault();
      if (!content.trim()) return;

      try {
        const response = await axios.post(`${API_BASE_URL}/todos`, {
          content,
        });
        setTodos([...todos, response.data]);
        setContent("");
      } catch (error) {
        console.error("Error creating todo:", error);
      }
    };

    // 更新 TODO 状态
    const toggleComplete = async (id, currentStatus) => {
      try {
        const response = await axios.put(`${API_BASE_URL}/todos/${id}`, {
          completed: !currentStatus,
        });
        setTodos(todos.map((todo) => (todo.id === id ? response.data : todo)));
      } catch (error) {
        console.error("Error updating todo:", error);
      }
    };

    // 删除 TODO
    const deleteTodo = async (id) => {
      try {
        await axios.delete(`${API_BASE_URL}/todos/${id}`);
        setTodos(todos.filter((todo) => todo.id !== id));
      } catch (error) {
        console.error("Error deleting todo:", error);
      }
    };

    if (loading) {
      return <div className="container">Loading...</div>;
    }

    return (
      <div className="container">
        <h1>Todo List</h1>

        {/* 添加 TODO 表单 */}
        <form onSubmit={handleSubmit} className="todo-form">
          <input
            type="text"
            placeholder="Add a new todo..."
            value={content}
            onChange={(e) => setContent(e.target.value)}
            className="todo-input"
          />
          <button type="submit" className="add-btn">
            Add
          </button>
        </form>

        {/* TODOs 列表 */}
        <ul className="todo-list">
          {todos.map((todo) => (
            <li
              key={todo.id}
              className={`todo-item ${todo.completed ? "completed" : ""}`}
            >
              <span
                className="todo-content"
                onClick={() => toggleComplete(todo.id, todo.completed)}
              >
                {todo.content}
              </span>
              <button
                className="delete-btn"
                onClick={() => deleteTodo(todo.id)}
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

- **修改 src/App.css**

  ```css
  .container {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  
  h1 {
    text-align: center;
    color: #333;
  }
  
  .todo-form {
    display: flex;
    margin-bottom: 20px;
  }
  
  .todo-input {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ddd;
    border-radius: 4px 0 0 4px;
  }
  
  .add-btn {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 0 4px 4px 0;
    cursor: pointer;
  }
  
  .add-btn:hover {
    background-color: #45a049;
  }
  
  .todo-list {
    list-style-type: none;
    padding: 0;
  }
  
  .todo-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    margin-bottom: 10px;
    background-color: #f9f9f9;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .todo-item.completed {
    background-color: #e8f5e8;
  }
  
  .todo-content {
    flex: 1;
    cursor: pointer;
  }
  
  .todo-item.completed .todo-content {
    text-decoration: line-through;
    color: #888;
  }
  
  .delete-btn {
    padding: 5px 10px;
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .delete-btn:hover {
    background-color: #da190b;
  }
  ```

## 创建前端 Dockerfile

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

## 创建前端 Nginx 配置文件 nginx.conf

```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
    }

    # API 反向代理
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

# 本地测试

# 容器编排

## 创建 docker-compose.yml 文件

```yaml
version: "3.8"

services:
  # MySQL 数据库服务
  db:
    image: mysql:8.0
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: todos_db
      MYSQL_USER: todo_user
      MYSQL_PASSWORD: todo_password
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    networks:
      - todos-network

  # 后端服务
  backend:
    build:
      context: ./backend
    container_name: todos-backend
    restart: always
    environment:
      MYSQL_USER: todo_user
      MYSQL_PASSWORD: todo_password
      DB_HOST: db
      MYSQL_DATABASE: todos_db
      SECRET_KEY: your-secret-key
    ports:
      - "5000:5000"
    depends_on:
      - db
    networks:
      - todos-network

  # 前端服务
  frontend:
    build:
      context: ./frontend
    container_name: todos-frontend
    restart: always
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - todos-network

# 网络配置
networks:
  todos-network:
    driver: bridge

# 卷配置
volumes:
  mysql_data:
```

## 使用 Docker Compose 启动项目

```bash
# 在项目根目录执行
docker-compose up -d
```

## 访问应用

- 前端应用：http://localhost
- 后端 API：http://localhost:5000/api/todos

## 查看日志

```bash
# 查看所有服务日志
docker-compose logs -f

# 查看特定服务日志
docker-compose logs -f frontend
docker-compose logs -f backend
docker-compose logs -f db
```

## 停止项目

```bash
docker-compose down
```

# CI

**创建 `todos-fullstack/.gitlab-ci.yml` 文件**

```yaml
stages:
  - build
  - test
  - deploy

# 变量定义
variables:
  DOCKER_DRIVER: overlay2
  DOCKER_HOST: tcp://docker:2375
  DOCKER_TLS_CERTDIR: ""
  IMAGE_REGISTRY: registry.gitlab.com
  FRONTEND_IMAGE: $IMAGE_REGISTRY/$CI_PROJECT_PATH/frontend:$CI_COMMIT_SHORT_SHA
  BACKEND_IMAGE: $IMAGE_REGISTRY/$CI_PROJECT_PATH/backend:$CI_COMMIT_SHORT_SHA

# 构建前端镜像
build-frontend:
  stage: build
  image: docker:20.10.16
  services:
    - docker:20.10.16-dind
  script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker build -t $FRONTEND_IMAGE ./frontend
    - docker push $FRONTEND_IMAGE
  only:
    - main

# 构建后端镜像
build-backend:
  stage: build
  image: docker:20.10.16
  services:
    - docker:20.10.16-dind
  script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker build -t $BACKEND_IMAGE ./backend
    - docker push $BACKEND_IMAGE
  only:
    - main

# 部署到 Kubernetes (通过 Argo CD)
deploy:
  stage: deploy
  image: alpine:latest
  script:
    - echo "部署触发成功，Argo CD 将自动检测到镜像变更并更新部署"
    - echo "前端镜像: $FRONTEND_IMAGE"
    - echo "后端镜像: $BACKEND_IMAGE"
  only:
    - main
```

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
