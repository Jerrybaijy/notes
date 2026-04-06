---
title: green-assistant
author: Jerry.Baijy
tags:
  - it
  - projects
  - react
  - fastapi
---

# 项目概述

# Docker Compose

## `backend/Dockerfile`

```dockerfile
FROM python:3.11-slim

# 设置工作目录
WORKDIR /app

# 安装系统依赖 (如果后续需要编译某些 python 包)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# 拷贝并安装 Python 依赖
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 拷贝项目文件
COPY . .

# 暴露端口
EXPOSE 8000

# 启动命令
# 注意：使用 0.0.0.0 才能在容器外访问
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## `dashboard/nginx.conf`

```nginx
server {
    listen 80;
    server_name localhost;

    # 静态资源根目录 (Dashboard 编译产物)
    root /usr/share/nginx/html;
    index index.html;

    # 处理单页应用 (SPA) 的路由
    location / {
        try_files $uri $uri/ /index.html;
    }

    # API 代理 (转发到后端容器)
    location /api/ {
        proxy_pass http://backend:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # 允许下载插件 ZIP 文件
    location ~* \.zip$ {
        add_header Content-Disposition 'attachment';
        expires off;
    }

    # 错误页面处理
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }
}
```

## `dashboard/Dockerfile`

```dockerfile
# ==========================================
# 第一阶段：编译并打包浏览器扩展 (Extension)
# ==========================================
FROM node:20-alpine AS extension-builder
WORKDIR /app/extension

# 这里的路径相对于构建上下文 (建议在项目根目录下构建)
COPY ./extension/package*.json ./
RUN npm install

COPY ./extension .
RUN npm run build

# 安装 zip 工具并将 dist 目录打包
RUN apk add --no-cache zip && \
    cd dist && \
    zip -r ../green-assistant.zip .

# ==========================================
# 第二阶段：编译控制台前端 (Dashboard)
# ==========================================
FROM node:20-alpine AS dashboard-builder
WORKDIR /app/dashboard

COPY ./dashboard/package*.json ./
RUN npm install

COPY ./dashboard .
RUN npm run build

# ==========================================
# 第三阶段：最终服务容器 (Nginx)
# ==========================================
FROM nginx:alpine

# 1. 拷贝 Dashboard 静态文件
COPY --from=dashboard-builder /app/dashboard/dist /usr/share/nginx/html

# 2. 拷贝 插件 ZIP 包到同一目录下，方便通过 /green-assistant.zip 下载
COPY --from=extension-builder /app/extension/green-assistant.zip /usr/share/nginx/html/green-assistant.zip

# 3. 拷贝 Nginx 配置文件
COPY ./dashboard/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

## `docker-compose.yml`

```yaml
version: '3.8'

services:
  # 后端服务
  backend:
    build:
      context: ./backend
    container_name: ga-backend
    ports:
      - "8000:8000"
    volumes:
      - ./backend/green_assistant.db:/app/green_assistant.db  # 数据持久化
    restart: always

  # 控制台前端 (包含插件下载和 API 代理)
  dashboard:
    build:
      context: .
      dockerfile: ./dashboard/Dockerfile
    container_name: ga-dashboard
    ports:
      - "8081:80"
    depends_on:
      - backend
    restart: always
```

