---
title: cloud-sql
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud-computing
  - gcp
  - cloud-sql
---

# Overview

Cloud SQL 是 Google Cloud 提供的数据库服务。

# Quick Start

## 创建 Cloud SQL 实例

```bash
gcloud sql instances create todo-db-instance \
  --database-version=MYSQL_8_0 \
  --tier=db-n1-standard-2 \
  --region=asia-east2 \
  --storage-auto-increase \
  --storage-size=10GB
```

## 设置根密码

```bash
gcloud sql users set-password root \
  --host=% \
  --instance=todo-db-instance \
  --password=123456
```

## 创建应用数据库和用户

在 [Google Cloud Shell](https://console.cloud.google.com/) 中执行以下命令：（或者本地电脑安装 MySQL 客户端）

```bash
gcloud sql connect todo-db-instance --user=root
```

```sql
CREATE DATABASE todo_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'jerry'@'%' IDENTIFIED BY '000000';
GRANT ALL PRIVILEGES ON todo_db.* TO 'jerry'@'%';
FLUSH PRIVILEGES;
EXIT;
```

## 连接 Cloud SQL

### 获取 Cloud SQL 实例的公网 IP

在 [Google Cloud Shell](https://console.cloud.google.com/) 中执行以下命令：

```bash
gcloud sql instances describe $INSTANCE_NAME --format='value(ipAddresses.ipAddress)'
gcloud sql instances describe todo-db-instance --format='value(ipAddresses.ipAddress)'
# 上次公网 IP：35.220.229.85
```

仅仅拿到公共 IP 是无法直接连接的，出于安全考虑，Google Cloud 默认会拦截所有外部连接。

### 获取本地电脑和 GKE 节点公网 IP

```bash
# 获取本地公网 IP
curl ifconfig.me
# 本地公网 IP：5.181.21.188

# 获取 GKE 节点公网 IP（EXTERNAL-IP）
kubectl get nodes -o wide
# 上次公网 IP：
# 34.150.83.115
# 34.96.197.161
```

### 添加授权网络

如果想从本地电脑和 GKE 节点连接，需要把相应的公网 IP 加入到白名单。

**注意**：要一次性加入多个，如果分次加入，后加入的会覆盖之前的。

```bash
gcloud sql instances patch $INSTANCE_NAME \
  --authorized-networks=[本地公网IP]/32,[GKE 节点1公网IP]/32,[GKE 节点2公网IP]/32
gcloud sql instances patch todo-db-instance \
    --authorized-networks=5.181.21.188/32,34.150.83.115/32,34.96.197.161/32
```

在 [Google Cloud Shell](https://console.cloud.google.com/) 中执行以下命令验证本地公网 IP 是否加入到白名单：

```bash
gcloud sql instances describe todo-db-instance \
    --format="value(settings.ipConfiguration.authorizedNetworks)"
```

本地公网 IP 加入到白名单以后，即可使用本地客户端（如 Navicate）通过 Cloud SQL 的公网 IP 连接它。

GKE 节点公网 IP 加入到白名单以后，GKE 中的 Pod 可通过 Cloud SQL 的公网 IP 连接它。

## 删除 Cloud SQL 实例

```bash
# 删除
gcloud sql instances delete todo-db-instance
# 验证
gcloud sql instances list
```

# Reference

## 语法

> [Gcloud SQL Reference](https://docs.cloud.google.com/sdk/gcloud/reference/sql)

gcloud sql [GROUP](https://docs.cloud.google.com/sdk/gcloud/reference/sql#GROUP) | [COMMAND](https://docs.cloud.google.com/sdk/gcloud/reference/sql#COMMAND) [[GCLOUD_WIDE_FLAG …](https://docs.cloud.google.com/sdk/gcloud/reference/sql#GCLOUD-WIDE-FLAGS)]
