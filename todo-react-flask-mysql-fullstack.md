# todo-react-flask-mysql-fullstack

我是一个初学者，你应该详细完整地告诉我开发步骤，比如：.gitlab-ci.yml 里的环境变量，都代表什么，我应该去哪配置这些环境变量，还有，我应该怎么创建项目，如何安装依赖，从头到尾，都给我详细说一下。另外，每个文件都要完整代码，不要有类似其它同理的说法

------

## 准备

### 准备工作

在开始写代码之前，请确保你安装了以下软件：

1. **Git**: 用于代码版本控制。
2. **Docker Desktop**: 用于运行容器。
3. **Node.js (版本 18+)**: 用于生成前端项目框架。
4. **VS Code**: 推荐的代码编辑器。

### 创建项目根目录与 Git 初始化

打开你的终端（Terminal 或 PowerShell），执行以下命令：

```bash
# 1. 创建总项目文件夹
mkdir todo-react-flask-mysql-fullstack
cd todo-react-flask-mysql-fullstack

# 2. 初始化 Git
git init

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

### 配置环境变量

配置环境变量：`todo-react-flask-mysql-fullstack/.env`

```toml
# MySQL 数据库配置
MYSQL_ROOT_PASSWORD=123456
MYSQL_DATABASE=todo_db
MYSQL_USER=jerry
MYSQL_PASSWORD=000000

# 在 Docker 网络内部，数据库服务的名字叫 'db'
DB_HOST=db

# Flask 配置
FLASK_APP=run.py
FLASK_ENV=production
SECRET_KEY=change_this_to_a_very_long_random_string
```

同时，为了让协作者知道需要配什么，创建一个 `.env.example` (不含真实密码)：

```toml
# MySQL 数据库配置
MYSQL_ROOT_PASSWORD=
MYSQL_DATABASE=todo_db
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

## 后端

### 依赖文件

创建后端目录：`todo-react-flask-mysql-fullstack/backend`

```bash
cd todo-react-flask-mysql-fullstack
mkdir backend
```

依赖文件：`backend/requirements.txt`

```txt
flask==3.0.0
flask-sqlalchemy==3.1.1
flask-migrate==4.0.5
pymysql==1.1.0
cryptography==41.0.7
gunicorn==21.2.0
python-dotenv==1.0.0
```

### 配置加载器

配置加载器：`backend/config.py`

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

### 扩展插件

先创建 `backend/app` 文件夹。

扩展插件：`backend/app/extensions.py`

```python
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

# 这里只创建实例，不绑定 app，为了解耦
db = SQLAlchemy()
migrate = Migrate()
```

### 数据库模型

数据库模型：`backend/app/models.py`

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

### 业务路由

先创建 `backend/app/api` 文件夹。 

业务路由：`backend/app/api/todo.py`

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

### 蓝图注册

蓝图注册：`backend/app/api/__init__.py`

```python
from app.api.todo import bp
```

### 应用工厂

应用工厂：`backend/app/__init__.py`

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

### 启动入口

启动入口：`backend/run.py`

```python
from app import create_app

app = create_app()

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### 生产环境启动脚本

**解释**：这个脚本非常关键。因为 Docker 启动时，MySQL 可能还没准备好。这个脚本会等待数据库迁移完成后再启动 Web 服务。

生产环境启动脚本：`backend/boot.sh`

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

### 后端镜像构建

后端镜像构建：`backend/Dockerfile`

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

### 数据库

在容器编排时，会自动创建容器化 MySQL，并在 `本地测试` 时进行初始化。

## 前端

### 创建 React 项目

```bash
# 创建 React 项目
cd todo-react-flask-mysql-fullstack
npm create vite@latest frontend

# 安装依赖
cd frontend
npm install

# 启动项目
npm run dev
```

### `frontend/vite.config.js`

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

### `frontend/index.html`

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

### `frontend/src/App.css`

```css
.container {
  max-width: 500px;
  margin: 50px auto;
  font-family: Arial, sans-serif;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
h1 { text-align: center; color: #333; }
.input-group { display: flex; gap: 10px; margin-bottom: 20px; }
input { flex: 1; padding: 10px; font-size: 16px; }
button { padding: 10px 20px; cursor: pointer; background: #007bff; color: white; border: none; border-radius: 4px; }
button:hover { background: #0056b3; }
ul { list-style: none; padding: 0; }
li { display: flex; justify-content: space-between; align-items: center; padding: 10px; border-bottom: 1px solid #eee; }
li.completed span { text-decoration: line-through; color: #888; }
.delete-btn { background: #dc3545; margin-left: 10px; }
.delete-btn:hover { background: #a71d2a; }
```

### `frontend/src/main.jsx`

React 入口：`frontend/src/main.jsx`

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

### `frontend/src/App.jsx`

React 主组件：`frontend/src/App.jsx`

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

### `frontend/nginx.conf`

Nginx 配置：`frontend/nginx.conf`

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

### `frontend/Dockerfile`

前端镜像构建：`frontend/Dockerfile`

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

## 容器编排

Docker Compose: `todo-react-flask-mysql-fullstack/docker-compose.yml`

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
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost"]
      timeout: 20s
      retries: 10

  # === 2. 后端服务 (本地构建) ===
  backend:
    # 注意这里：本地开发用 build，不要用 image
    build: ./backend 
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

  # === 3. 前端服务 (本地构建) ===
  frontend:
    # 注意这里：本地开发用 build，不要用 image
    build: ./frontend
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

## 本地测试

1. **启动项目**：

   ```bash
   cd todo-react-flask-mysql-fullstack
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

## GitLab CI

在 GitLab 配置环境变量：`DOCKER_HUB_USER` 和 `DOCKER_HUB_PASS`

GitLab CI: `todo-react-flask-mysql-fullstack/.gitlab-ci.yml`

**修改逻辑说明**：

- `docker login`: 改为使用上面配置的变量。
- `image name`: Docker Hub 的镜像命名规则是 `用户名/仓库名:标签`。我们将分别构建 `用户名/todo-react-flask-mysql-backend` 和 `用户名/todo-react-flask-mysql-frontend`。

```yaml
# 定义阶段：这里只有构建阶段
stages:
  - build

# 使用 Docker-in-Docker 服务，允许在容器里运行 docker 命令
services:
  - docker:20.10.16-dind

variables:
  # 使用 overlay2 驱动以提高性能
  DOCKER_DRIVER: overlay2
  # 定义你的 Docker Hub 镜像名称前缀
  # 最终会生成: $DOCKER_HUB_USER/todo-react-flask-mysql-backend 和 $DOCKER_HUB_USER/todo-react-flask-mysql-frontend
  # 这里的 $DOCKER_HUB_USER 就是你在 GitLab 里配的变量
  IMAGE_PREFIX: $DOCKER_HUB_USER

# 所有任务执行前的通用步骤：登录 Docker Hub
before_script:
  - echo "Logging in to Docker Hub..."
  # -u 用户名 -p 密码(Token)
  - docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASS

build_backend:
  stage: build
  image: docker:20.10.16
  script:
    - cd backend
    
    # 构建两个标签：一个是具体的 commit hash (用于回滚)，一个是 latest (用于生产)
    - docker build -t $IMAGE_PREFIX/todo-react-flask-mysql-backend:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/todo-react-flask-mysql-backend:latest .
    
    # 推送到 Docker Hub
    - docker push $IMAGE_PREFIX/todo-react-flask-mysql-backend:$CI_COMMIT_SHORT_SHA
    - docker push $IMAGE_PREFIX/todo-react-flask-mysql-backend:latest

build_frontend:
  stage: build
  image: docker:20.10.16
  script:
    - cd frontend
    
    - docker build -t $IMAGE_PREFIX/todo-react-flask-mysql-frontend:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/todo-react-flask-mysql-frontend:latest .

    - docker push $IMAGE_PREFIX/todo-react-flask-mysql-frontend:$CI_COMMIT_SHORT_SHA
    - docker push $IMAGE_PREFIX/todo-react-flask-mysql-frontend:latest
```

## 总结

你现在已经拥有了一个完整的流程：

1. **开发**：在本地修改代码。
2. **测试**：使用 `docker-compose up` 在本地运行查看效果。
3. **发布**：执行 `git add .`, `git commit -m "update"`, `git push`。
4. **自动构建**：GitLab 收到推送后，会根据 `.gitlab-ci.yml` 自动打包出新的 Docker 镜像。

## 如何改到 Docker Hub？

要改到 Docker Hub（全球最大的公共/私有镜像库），我们需要做三件事：

1. **注册/准备**：在 Docker Hub 获取访问令牌（Access Token）。
2. **配置**：在 GitLab 中填入 Docker Hub 的账号密码变量。
3. **修改**：更新 `.gitlab-ci.yml` 指向 Docker Hub。

下面是手把手的详细步骤：

### 第一步：在 Docker Hub 准备账号与令牌

为了安全起见，我们在 CI/CD 中**不要使用你的登录密码**，而是使用 **Access Token**。

1. 登录 [hub.docker.com](https://hub.docker.com/)。
2. 点击右上角头像 -> **Account Settings** (账户设置)。
3. 点击左侧 **Security** (安全)。
4. 点击 **New Access Token** 按钮。
   - **Description**: 随便填，比如 `GitLab CI`。
   - **Access permissions**: 选择 `Read & Write`。
5. **复制生成的 Token**。注意：这个 Token 只显示一次，一定要复制好！

------

### 第二步：在 GitLab 配置环境变量

回到你的 GitLab 项目页面：

1. 点击左侧菜单 **Settings** -> **CI/CD**。
2. 找到 **Variables** 区域，点击 **Expand**。
3. 点击 **Add variable**，我们需要添加两个变量：

**变量 1：用户名**

- **Key**: `DOCKER_HUB_USER`
- **Value**: 你的 Docker Hub 用户名 (比如 `zhangsan`)
- *Type 选 Variable，Flags 都不用勾选*

**变量 2：密码/令牌**

- **Key**: `DOCKER_HUB_PASS`
- **Value**: **刚才复制的那串 Access Token**
- *Type 选 Variable，建议勾选 Mask variable (这样在日志里会显示为 `*****`，不会泄露)*

### 第四步：验证

1. 修改完代码后，执行 `git add .`, `git commit`, `git push`。
2. 去 GitLab 查看 **Build -> Jobs**，观察流水线是否成功。
3. 如果成功，去 [hub.docker.com](https://hub.docker.com/) 查看你的个人主页，你会发现多出了两个仓库：`todo-backend` 和 `todo-frontend`。

## 总结流程

1. 你写代码，推送到 GitLab。
2. GitLab 根据 `.gitlab-ci.yml` 自动打包，利用你在 GitLab 设置的变量登录 Docker Hub，并把镜像推送到 Docker Hub。
3. 你在云服务器上，只需要有 `.env` 和 `docker-compose.yml`，运行 `docker-compose up -d`。
4. Docker 会自动从 Docker Hub 下载刚才打包好的 `latest` 镜像并运行。

## 生产环境

Docker Compose: `todo-react-flask-mysql-fullstack/docker-compose.yml`

```yaml
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
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - prod-net
    healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost"]
      timeout: 20s
      retries: 10

  backend:
    # === 变化在这里 ===
    # 不再是 build，而是 image
    image: jerrybaijy/todo-react-flask-mysql-backend:latest
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
      - prod-net

  frontend:
    # === 变化在这里 ===
    image: jerrybaijy/todo-react-flask-mysql-frontend:latest
    restart: always
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - prod-net

volumes:
  db_data:

networks:
  prod-net:
```

