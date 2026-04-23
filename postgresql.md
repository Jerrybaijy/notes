---
title: postgresql
author: Jerry.Baijy
tags:
  - dev
  - software
  - databese
---

# Overview

[**PostgreSQL**](https://www.postgresql.org/) 是一个[关系型数据库](it-basics.md#数据库类型)管理系统。

# 备份与恢复

新旧数据库都是容器化应用，命令中的各参数根据实际情况而定、

```bash
# 导出数据库为 sql 文件
docker exec <container_name> pg_dump -U <username> <db_name> > <backup_file>
docker exec ga-postgres pg_dump -U postgres green_assistant > ga_backup.sql

# 停止云服务器后端服务（避免导入时有程序在连接数据库）
docker compose stop backend

# 先停止并删除服务器原有的数据库卷，以确保是一个干净的导入
docker compose rm -s -v db
docker compose up -d db
# 如果想删除所有容器和数据库挂载卷
# docker compose -v
# docker compose up -d db

# 执行导入（直接将导出的 SQL 灌入服务器容器）
cat <backup_file> | docker exec -i <container_name> psql -U <username> -d <db_name>
cat ga_backup.sql | docker exec -i ga-postgres psql -U postgres -d green_assistant

# 重新启动后端
docker compose up -d
```
