---
title: postgresql
author: Jerry.Baijy
tags:
  - it
  - software
  - databese
---

# Overview

[**PostgreSQL**](https://www.postgresql.org/) 是一个[关系型数据库](it-basics.md#数据库类型)管理系统。

# 备份与恢复

新旧数据库都是容器化应用，命令中的各参数根据实际情况而定、

```bash
# 导出本地数据库为 sql 文件
docker exec ga-postgres-local pg_dump -U postgres green_assistant > green_assistant_backup.sql

# 停止云服务器后端服务（避免导入时有程序在连接数据库）
docker compose stop backend

# 先停止并删除服务器原有的数据库卷，以确保是一个干净的导入
docker compose down -v
docker compose up -d db

# 执行导入（直接将本地导出的 SQL 灌入服务器容器）
cat green_assistant_backup.sql | docker exec -i ga-postgres psql -U postgres -d green_assistant

# 重新启动后端
docker compose up -d
```





本地docker

```bash
# 导出
docker exec ga-postgres-local pg_dump -U postgres green_assistant > processed_backup_candidates_1.sql

docker compose -f docker-compose-local.yml down -v
docker compose -f docker-compose-local.yml up -d db

cat processed_backup_candidates_1.sql | docker exec -i ga-postgres-local psql -U postgres -d green_assistant

docker compose -f docker-compose-local.yml up -d
```

```
cat green_assistant_backup.sql | docker exec -i ga-postgres-local psql -U postgres -d green_assistant
```

云

```
cat processed_backup_candidates_1.sql | docker exec -i ga-postgres psql -U postgres -d green_assistant
```

