---
title: n8n
author: Jerry.Baijy
tags:
  - dev
  - workflow
---

# Overview

[n8n](https://n8n.io/)

> [Docs](https://docs.n8n.io/?_gl=1*ydajv4*_gcl_au*OTQxMTQ3MTMwLjE3NzY1Njk3MjA.*_ga*MTAyNTUzMTgyMy4xNzc2NTY5NzIx*_ga_0SC4FF2FH9*czE3NzY2MTAwMzAkbzMkZzEkdDE3NzY2MTI3NzckajUkbDAkaDA.)

# Install

## 运行方式

有以下运行方式：

- Docker
- npm
- Cloud

## 使用 Docker 安装 n8n

> [Docker Installation](https://docs.n8n.io/hosting/installation/docker/)

- 已安装 Docker

- 创建数据卷

  ```bash
  docker volume create n8n_data
  ```

- 启动 n8n

  ```bash
  docker run -d \
    --name n8n \
    -p 5678:5678 \
    -e GENERIC_TIMEZONE=Asia/Shanghai \
    -e TZ=Asia/Shanghai \
    -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
    -e N8N_RUNNERS_ENABLED=true \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
  ```

  **在以上命令中**：

  - `GENERIC_TIMEZONE`：给 n8n 程序设置时区
  - `TZ`：给容器内部系统设置时区
  - `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS`：强制文件权限安全
  - `N8N_RUNNERS_ENABLED`：开启 n8n 新一代任务执行器

## 使用 docker-compose 安装 n8n

