---
title: nginx
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - web
  - nginx
---

# Nginx

## 反向代理

Nginx 反向代理 `nginx.conf`，用于**容器化部署**时的前后端通信。

`todo-fullstack-gitops` 项目中的示例：将前端 `/api` 开头的请求转发到 http://backend:5000 后端服务。

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

