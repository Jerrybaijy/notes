---
title: alembic
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - python
  - database-migration-tools
---

# Overview

[Alembic](https://alembic.sqlalchemy.org/) 是一个 Python 数据库迁移工具，通常与 SQLAlchemy 一起使用，用于管理数据库架构的版本控制。

> [Docs](https://alembic.sqlalchemy.org/)

# Install

使用 pip 或 pdm 安装 Alembic

# Quickstart

## 安装

```bash
# 使用 pdm 安装
pdm add alembic
```

## 初始化

在后端目录运行：

```bash
alembic init migrations
```

初始化成功后，你的项目目录结构应该是：

```
backend/
├── migrations/         # 迁移脚本目录
│   ├── versions/       # 版本迁移文件
│   └── env.py          # 迁移环境配置
├── alembic.ini         # Alembic 配置文件
├── pyproject.toml      # PDM 配置文件
└── ...其他文件
```

