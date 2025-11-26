---
title: todos-react-flask-mysql-fullstack
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

![image-20251126075702455](assets/image-20251126075702455.png)

- **概述**：这是一个全栈应用的原型项目。

- **来源**：自己搭建

- **功能**：Todo list

- **技术栈**：
  - 前端：React
  - 后端：Flask
  - 数据库：容器化 MySQL
  - CI：GitLab CI
  - CD：Docker Compose
  
- **项目仓库**
  - GitLab: https://gitlab.com/jerrybai/todos-react-flask-mysql-fullstack
  - GitHub: https://github.com/Jerrybaijy/todos-react-flask-mysql-fullstack
  
- **镜像仓库**
  - 后端：https://hub.docker.com/repository/docker/jerrybaijy/todos-react-flask-mysql-backend
  - 前端：https://hub.docker.com/repository/docker/jerrybaijy/todos-react-flask-mysql-frontend/general
  
- **项目结构**

  ```
  todos-react-flask-mysql-fullstack/
  ├── todos-react-flask-mysql-backend/
  ├── todos-react-flask-mysql-frontend/
  │
  ├── dev/
  ├── application.yaml
  │   └── blog.html
  │   └── chat_widget.html
  │
  └── 其它
  ```

# 项目准备

## 开发工具

- **Node.js (版本 18+)**：React 运行环境。
- **Python**：Flask 运行环境
- **Docker Desktop**：容器运行环境。
- **Git**：版本控制。

## 创建项目根目录与 Git 初始化

打开你的终端（Terminal 或 PowerShell），执行以下命令：

```bash
# 1. 创建总项目目录
mkdir todos-react-flask-mysql-fullstack
cd todos-react-flask-mysql-fullstack

# 2. 初始化 Git
git init --initial-branch=main

# 3. 创建 .gitignore 文件
# 下面是创建该文件的命令，你也可以手动新建一个 .gitignore 文件，填入以下内容
echo "venv/" >> .gitignore
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
echo "__pycache__/" >> .gitignore
echo ".pytest_cache/" >> .gitignore
echo "dist/" >> .gitignore
echo ".DS_Store" >> .gitignore
```

## 配置环境变量

配置环境变量：`todos-react-flask-mysql-fullstack/.env`

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

同时，为了让协作者知道需要配什么，创建一个 `.env.example` (不含真实密码)：

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

## 依赖文件

创建后端目录：`todos-react-flask-mysql-fullstack/todos-react-flask-mysql-backend`

```bash
cd todos-react-flask-mysql-fullstack
mkdir todos-react-flask-mysql-backend
```

依赖文件：`todos-react-flask-mysql-backend/requirements.txt`

```txt
flask==3.0.0
flask-sqlalchemy==3.1.1
flask-migrate==4.0.5
pymysql==1.1.0
cryptography==41.0.7
gunicorn==21.2.0
python-dotenv==1.0.0
```

## 配置加载器

配置加载器：`todos-react-flask-mysql-backend/config.py`

```python
import os

class Config:
    # 如果环境变量里没有 SECRET_KEY，就报错或者用默认值（生产环境必须有）
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-key-please-change'
    
    # 获取数据库连接信息
    DB_USER = os.environ.get('MYSQL_USER')
    DB_PASS = os.environ.get('MYSQL_PASSWORD')
    DB_HOST = os.environ.get('DB_HOST')
    DB_NAME = os.environ.get('MYSQL_DATABASE')
    
    # 拼接连接字符串
    # 格式: mysql+pymysql://user:pass@host/dbname
    if DB_USER and DB_PASS and DB_HOST and DB_NAME:
        SQLALCHEMY_DATABASE_URI = f'mysql+pymysql://{DB_USER}:{DB_PASS}@{DB_HOST}/{DB_NAME}'
    else:
        # 这是一个防错机制，防止构建镜像时因为没有环境变量而报错
        SQLALCHEMY_DATABASE_URI = 'sqlite:///:memory:'

    SQLALCHEMY_TRACK_MODIFICATIONS = False
```

## 扩展插件

先创建 `todos-react-flask-mysql-backend/app` 目录。

扩展插件：`todos-react-flask-mysql-backend/app/extensions.py`

```python
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

# 这里只创建实例，不绑定 app，为了解耦
db = SQLAlchemy()
migrate = Migrate()
```

## 数据库模型

数据库模型：`todos-react-flask-mysql-backend/app/models.py`

```python
from app.extensions import db

class Todo(db.Model):
    __tablename__ = 'todos'
    
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(200), nullable=False)
    completed = db.Column(db.Boolean, default=False)

    def to_dict(self):
        return {
            'id': self.id,
            'content': self.content,
            'completed': self.completed
        }
```

## 业务路由

先创建 `todos-react-flask-mysql-backend/app/api` 目录。 

业务路由：`todos-react-flask-mysql-backend/app/api/todo.py`

```python
from flask import Blueprint, jsonify, request
from app.extensions import db
from app.models import Todo

# 定义蓝图
bp = Blueprint('api', __name__)

@bp.route('/todos', methods=['GET'])
def get_todos():
    todos = Todo.query.all()
    return jsonify([t.to_dict() for t in todos])

@bp.route('/todos', methods=['POST'])
def add_todo():
    data = request.get_json()
    if not data or 'content' not in data:
        return jsonify({'error': 'Content is required'}), 400
    
    new_todo = Todo(content=data['content'])
    db.session.add(new_todo)
    db.session.commit()
    return jsonify(new_todo.to_dict()), 201

@bp.route('/todos/<int:id>', methods=['PUT'])
def update_todo(id):
    todo = Todo.query.get_or_404(id)
    
    # 这里只演示切换完成状态
    todo.completed = not todo.completed
    db.session.commit()
    return jsonify(todo.to_dict())

@bp.route('/todos/<int:id>', methods=['DELETE'])
def delete_todo(id):
    todo = Todo.query.get_or_404(id)
    db.session.delete(todo)
    db.session.commit()
    return jsonify({'message': 'Deleted successfully'})
```

## 蓝图注册

蓝图注册：`todos-react-flask-mysql-backend/app/api/__init__.py`

```python
from app.api.todo import bp
```

## 应用工厂

应用工厂：`todos-react-flask-mysql-backend/app/__init__.py`

```python
from flask import Flask
from config import Config
from app.extensions import db, migrate

def create_app(config_class=Config):
    app = Flask(__name__)
    app.config.from_object(config_class)

    # 1. 初始化插件
    db.init_app(app)
    migrate.init_app(app, db)

    # 2. 注册蓝图
    from app.api import bp as api_bp
    app.register_blueprint(api_bp, url_prefix='/api')

    return app
```

## 启动入口

启动入口：`todos-react-flask-mysql-backend/run.py`

```python
from app import create_app

app = create_app()

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

## 生产环境启动脚本

**解释**：这个脚本非常关键。因为 Docker 启动时，MySQL 可能还没准备好。这个脚本会等待数据库迁移完成后再启动 Web 服务。

生产环境启动脚本：`todos-react-flask-mysql-backend/boot.sh`

```bash
#!/bin/sh

# 只要之前的命令失败，脚本就停止
set -e

# 等待 10 秒，让 MySQL 容器先启动好 (生产环境可以用更高级的 wait-for-it 脚本)
echo "Waiting for MySQL to start..."
sleep 10

# 自动执行数据库迁移 (创建/更新表)
echo "Running database migrations..."
flask db upgrade

# 启动 Gunicorn 服务器
# -w 4: 开启4个工作进程
# -b :5000: 监听 5000 端口
echo "Starting Gunicorn..."
exec gunicorn -b :5000 --access-logfile - --error-logfile - run:app
```

## 后端镜像构建

后端镜像构建：`todos-react-flask-mysql-backend/Dockerfile`

```dockerfile
FROM python:3.9-slim

# 设置容器内的工作目录
WORKDIR /app

# 安装系统依赖 (如果需要编译某些库)
RUN apt-get update && apt-get install -y default-libmysqlclient-dev build-essential && rm -rf /var/lib/apt/lists/*

# 复制依赖清单并安装
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 复制所有代码
COPY . .

# 给启动脚本增加可执行权限
RUN chmod +x boot.sh

# 设置环境变量
ENV FLASK_APP=run.py

# 暴露端口
EXPOSE 5000

# 容器启动时的入口
ENTRYPOINT ["./boot.sh"]
```

## 数据库

在容器编排时，会自动创建容器化 MySQL 及 database，并在 `本地测试` 时进行初始化创建 table。

# 前端

## 创建 React 项目

```bash
# 创建 React 项目
cd todos-react-flask-mysql-fullstack
npm create vite@latest todos-react-flask-mysql-frontend

# 安装依赖
cd todos-react-flask-mysql-frontend
npm install

# 启动项目
npm run dev
```

## `todos-react-flask-mysql-frontend/vite.config.js`

配置开发环境代理。

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

## `todos-react-flask-mysql-frontend/index.html`

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Production Todo App</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

## `todos-react-flask-mysql-frontend/src/App.css`

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

## `todos-react-flask-mysql-frontend/src/main.jsx`

React 入口：`todos-react-flask-mysql-frontend/src/main.jsx`

```javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

## `todos-react-flask-mysql-frontend/src/App.jsx`

React 主组件：`todos-react-flask-mysql-frontend/src/App.jsx`

```javascript
import { useState, useEffect } from 'react'
import './App.css'

function App() {
  const [todos, setTodos] = useState([])
  const [input, setInput] = useState('')

  useEffect(() => {
    fetchTodos()
  }, [])

  const fetchTodos = async () => {
    try {
      const res = await fetch('/api/todos')
      if (res.ok) {
        const data = await res.json()
        setTodos(data)
      }
    } catch (error) {
      console.error("Failed to fetch todos", error)
    }
  }

  const handleAdd = async () => {
    if (!input.trim()) return
    const res = await fetch('/api/todos', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ content: input })
    })
    if (res.ok) {
      const newTodo = await res.json()
      setTodos([...todos, newTodo])
      setInput('')
    }
  }

  const handleToggle = async (id) => {
    const res = await fetch(`/api/todos/${id}`, { method: 'PUT' })
    if (res.ok) {
      const updated = await res.json()
      setTodos(todos.map(t => t.id === id ? updated : t))
    }
  }

  const handleDelete = async (id) => {
    const res = await fetch(`/api/todos/${id}`, { method: 'DELETE' })
    if (res.ok) {
      setTodos(todos.filter(t => t.id !== id))
    }
  }

  return (
    <div className="container">
      <h1>My Todo List</h1>
      <div className="input-group">
        <input 
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="What needs to be done?"
          onKeyPress={(e) => e.key === 'Enter' && handleAdd()}
        />
        <button onClick={handleAdd}>Add</button>
      </div>
      <ul>
        {todos.map(todo => (
          <li key={todo.id} className={todo.completed ? 'completed' : ''}>
            <span 
              onClick={() => handleToggle(todo.id)}
              style={{cursor: 'pointer', flex: 1}}
            >
              {todo.content}
            </span>
            <button className="delete-btn" onClick={() => handleDelete(todo.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  )
}

export default App
```

## `todos-react-flask-mysql-frontend/nginx.conf`

Nginx 配置：`todos-react-flask-mysql-frontend/nginx.conf`

```nginx
server {
    listen 80;
    
    # 处理前端路由，防止刷新 404
    location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
    }

    # 反向代理 API 请求到后端容器
    location /api {
        proxy_pass http://backend:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## `todos-react-flask-mysql-frontend/Dockerfile`

前端镜像构建：`todos-react-flask-mysql-frontend/Dockerfile`

```dockerfile
# 阶段一：构建阶段
FROM node:18-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# 阶段二：生产部署阶段
FROM nginx:stable-alpine
# 删除默认配置
RUN rm /etc/nginx/conf.d/default.conf
# 复制自定义配置
COPY nginx.conf /etc/nginx/conf.d/
# 复制构建产物
COPY --from=build-stage /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

# 容器编排

Docker Compose: `todos-react-flask-mysql-fullstack/docker-compose.yml`

```yaml
services:
  # === 1. 数据库服务 ===
  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    ports:
      - "3306:3306"

    # 使用旧的密码认证方式，防止 Navicat/DBeaver 连接报错
    command: --default-authentication-plugin=mysql_native_password
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost"]
      timeout: 20s
      retries: 10

  # === 2. 后端服务 ===
  backend:
    build: ./${BACKEND_NAME}
    restart: always
    environment:
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      DB_HOST: db
      SECRET_KEY: ${SECRET_KEY}
    depends_on:
      db:
        condition: service_healthy
    networks:
      - app-network

  # === 3. 前端服务 ===
  frontend:
    build: ./${FRONTEND_NAME}
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - app-network

# 数据库挂载卷
volumes:
  db_data:

# 定义网络
networks:
  app-network:
    driver: bridge
```

# 本地测试

1. **启动项目**：

   ```bash
   cd todos-react-flask-mysql-fullstack
   docker-compose up -d --build
   ```

   *(这需要几分钟时间下载镜像和构建)*

2. **初始化数据库迁移** (这是第一次运行必须做的)： 现在容器都启动了，但是数据库是空的，也没有迁移记录。我们需要进入后端容器执行初始化。

   ```bash
   # 进入后端容器
   docker-compose exec backend bash
   
   # 在容器内部执行以下命令
   flask db init
   flask db migrate -m "Initial migration"
   flask db upgrade
   
   # 退出容器
   exit
   ```

   *注意：之后的每次代码更新，`boot.sh` 会自动运行 `flask db upgrade`，不需要你手动搞了，只有第一次初始化需要手动。*

3. **验证**： 打开浏览器访问 http://localhost。你应该能看到 Todo List 页面，并且可以添加、删除数据。

4. 本地测试通过，第一次将源代码推送至代码托管平台。

# GitLab CI

**在 GitLab 配置环境变量：**

- `DOCKER_HUB_USER`
- `DOCKER_HUB_PASS`

GitLab CI: `todos-react-flask-mysql-fullstack/.gitlab-ci.yml`

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
  BACKEND_NAME: todos-react-flask-mysql-backend
  FRONTEND_NAME: todos-react-flask-mysql-frontend

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

# 生产环境

此部分实现在无代码情况下，在本地或云服务器上，只需要有 `.env` 和 `docker-compose.yml`，运行 `docker-compose up -d` 命令，即可启动容器化应用。

## 创建目录

先创建 `todos` 目录，在此目录分别创建：

- `todos/docker-compose.yml`
- `todos/.env`

## `todos/docker-compose.yml`

生产环境的 `docker-compose.yml` 与本地测试时有两处不同：

- 需要指定 Docker Compose 文件版本
- 后端和前端由 build image 变为指定 image 名称

```yaml
# 指定 Docker Compose 文件版本
version: '3.8'

services:
  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    ports:
      - "3306:3306"
    command: --default-authentication-plugin=mysql_native_password
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost"]
      timeout: 20s
      retries: 10

  backend:
    # 指定镜像名称
    image: jerrybaijy/$BACKEND_NAME:latest
    restart: always
    environment:
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      DB_HOST: db
      SECRET_KEY: ${SECRET_KEY}
    depends_on:
      db:
        condition: service_healthy
    networks:
      - app-network

  frontend:
    # 指定前端镜像名称
    image: jerrybaijy/$FRONTEND_NAME:latest
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - app-network

volumes:
  db_data:

networks:
  app-network:
    driver: bridge
```

## `todos/.env`

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

## 启动

1. 删除本地测试时的 Image、Container 和 Volumes，余下操作与 `本地测试` 相同。

3. **启动项目**：

   ```bash
   cd todos
   docker-compose up -d --build
   ```

4. **初始化数据库迁移**

   ```bash
   # 进入后端容器
   docker-compose exec backend bash
   
   # 在容器内部执行以下命令
   flask db init
   flask db migrate -m "Initial migration"
   flask db upgrade
   
   # 退出容器
   exit
   ```

5. **验证**： 打开浏览器访问 http://localhost。你应该能看到 Todo List 页面，并且可以添加、删除数据。

# Argo CD

## 目录结构

```
todos-react-flask-mysql-fullstack/
├── todos-react-flask-mysql-backend/
├── todos-react-flask-mysql-frontend/
│
├── dev/
│   ├── mysql-db.yaml
│   ├── backend.yaml
│   └── frontend.yaml
│
├── application.yaml
│
└── 其它文件
```



## `mysql-config.yaml`

为了保证数据持久化和密码安全，使用 `PVC` 和 `Secret`。

**注意：** 实际操作时，需要使用 Base64 编码 `.env` 文件中的用户名和密码，例如：运行 `echo -n '123456' | base64` 来获取 `MYSQL_ROOT_PASSWORD` 的值。

```yaml
# Secret
apiVersion: v1
kind: Secret
metadata:
  name: todos-mysql-secret
type: Opaque
data:
  # 这里的用户名和密码需要是 Base64 编码后的值
  # MYSQL_ROOT_PASSWORD
  mysql-root-password: MTIzNDU2
  # MYSQL_USER
  mysql-user: amVycnk=
  # MYSQL_PASSWORD
  mysql-password: MDAwMDAw
---
# PVC
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: todos-mysql-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```



## `mysql-deployment.yaml`

Deployment 和 Service

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-db-deployment
  labels:
    app: mysql-db
spec:
  selector:
    matchLabels:
      app: mysql-db
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql-db
    spec:
      containers:
      - name: mysql
        image: mysql:8.0
        ports:
        - containerPort: 3306
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: mysql-root-password
        - name: MYSQL_DATABASE
          # 数据库名直接写死或从 configmap 引用，这里直接写死
          value: todos_db
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
        # 对应 Docker Compose 中的命令
        command: ["--default-authentication-plugin=mysql_native_password"]
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
  name: db  # 这里的名称 'db' 很重要，对应后端服务中的 DB_HOST
spec:
  ports:
  - port: 3306
  selector:
    app: mysql-db
```

## `mysql-pvc.yaml`

持久卷声明

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
```

## `backend-deployment.yaml`

为后端服务 (backend) 创建清单

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-deployment
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
        # ⚠️ 部署到 Minikube 时，通常需要先将镜像构建到 Minikube 的环境中
        # 但为了简化，我们假设您已经有一个可用的 Dockerfile 和上下文
        # 在实际 GitOps 部署中，您可能需要使用公有/私有镜像仓库
        # 这里的 build: ./${BACKEND_NAME} 步骤被 Docker 构建/镜像仓库取代
        image: backend-image:latest # 替换为您实际的镜像名称
        ports:
        - containerPort: 5000 # 假设后端服务在 5000 端口运行
        env:
        - name: DB_HOST
          value: db # 对应 MySQL Service 的名称
        # 从 Secret 引用数据库用户和密码
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
        - name: MYSQL_DATABASE
          value: todos_db
        - name: SECRET_KEY
          value: "change_this_to_a_very_long_random_string" # 建议也放入 Secret
---
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 5000
      targetPort: 5000
```

## `frontend-deployment.yaml`

为前端服务 (frontend) 创建清单

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
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
        # 同样，替换为您实际的镜像名称
        image: frontend-image:latest 
        ports:
        - containerPort: 80 # 前端服务通常是 Nginx，使用 80 端口
---
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
spec:
  selector:
    app: frontend
  # 使用 NodePort/LoadBalancer 以便在 Minikube 外部访问
  type: NodePort 
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      # NodePort 会分配一个 30000-32767 之间的端口
```

