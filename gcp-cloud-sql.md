---
title: gcp-cloud-sql
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud-computing
  - gcp
  - cloud-sql
---

# Overview

[**Cloud SQL**](https://docs.cloud.google.com/sql/docs?hl=zh-cn) 是由 GCP 提供的、适用于 [MySQL](https://docs.cloud.google.com/sql/docs/mysql?hl=zh-cn)、[PostgreSQL](https://docs.cloud.google.com/sql/docs/postgres?hl=zh-cn) 和 [SQL Server](https://docs.cloud.google.com/sql/docs/sqlserver?hl=zh-cn) 的**全代管式数据库服务**。

> [Cloud SQL Docs](https://docs.cloud.google.com/sql/docs?hl=zh-cn)
>
> [Cloud SQL Reference](https://docs.cloud.google.com/sdk/gcloud/reference/sql)

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

## 设置 Root 密码

```bash
gcloud sql users set-password root \
  --host=% \
  --instance=todo-db-instance \
  --password=123456
```

## 创建 Database 和普通用户

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

使用 [Cloud SQL Auth](<#Cloud SQL Auth>) 机制连接 Cloud SQL。

## 删除 Cloud SQL 实例

```bash
# 删除
gcloud sql instances delete todo-db-instance
# 验证
gcloud sql instances list
```

# 创建 Cloud SQL

## 使用 `gcloud` 创建 Cloud SQL

详见 [Quick Start](<gcp-cloud-sql.md#Quick Start>)

## 使用 Terraform 创建 Cloud SQL（旧）

### 准备工作

[已通过 Terraform 配置 GKE 集群](<gcp-gke.md#使用 Terraform 创建 GKE 集群>)

### `api.tf`

```hcl
locals {
  services = [
    # ...
    
    "sqladmin.googleapis.com" # Cloud SQL API
  ]
}

resource "google_project_service" "project_services" {
  for_each           = toset(local.services)
  service            = each.key
  disable_on_destroy = false
}
```

### `iam.tf`

```hcl
# 允许 GSA 访问 Cloud SQL
resource "google_project_iam_member" "mysql_client" {
  project = var.project_id
  role    = "roles/cloudsql.client"
  member  = "serviceAccount:${google_service_account.workload_identity.email}"
}
```

### `cloud-sql.tf`

```hcl
# 创建 Cloud SQL 实例
resource "google_sql_database_instance" "mysql_instance" {
  name             = local.db_instance
  database_version = "MYSQL_8_0"
  region           = var.region

  settings {
    tier            = "db-f1-micro" # 测试环境使用的最小规格
    disk_type       = "PD_SSD"
    disk_size       = 10   # 初始 10GB
    disk_autoresize = true # 自动扩容

    # 开启公网 IP，但会通过 IAM 权限锁定访问，仅允许通过授权代理访问
    ip_configuration {
      ipv4_enabled = true
    }
  }

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# 创建 DATABASE
resource "google_sql_database" "my_db" {
  name      = local.db_name
  instance  = google_sql_database_instance.mysql_instance.name
  charset   = "utf8mb4"
  collation = "utf8mb4_unicode_ci"
}

# 创建 root 用户
resource "google_sql_user" "root_user" {
  name     = "root"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_root_password
  host     = "%"
}

# 创建普通账户
resource "google_sql_user" "jerry_user" {
  name     = "jerry"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_jerry_password
  host     = "%"
}

output "cloud_sql_connection_name" {
  description = "Cloud SQL instance connection name"
  value       = google_sql_database_instance.mysql_instance.connection_name
}

output "sql_instance_name" {
  description = "Cloud SQL 实例的名称"
  value       = google_sql_database_instance.mysql_instance.name
}

output "database_name" {
  description = "Cloud SQL database name"
  value       = google_sql_database.my_db.name
}
```

### `variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
  default     = "my"
}

locals {
  # ...
  
  db_instance    = "${var.prefix}-db-instance"
  db_name        = "${var.prefix}_db"
}

# --- Cloud SQL ---
variable "mysql_root_password" {
  type        = string
  description = "MySQL root user password"
  sensitive   = true
}

variable "mysql_jerry_password" {
  type        = string
  description = "MySQL jerry user password"
  sensitive   = true
}
```

### `terraform.tfvars`

```hcl
mysql_root_password  = "123456"
mysql_jerry_password = "000000"
```

## 使用 Terraform 创建 Cloud SQL

### 创建 Terraform 目录

```bash
mkdir -p /d/projects/my-project/terraform/cloud-sql

cd /d/projects/my-project/terraform
touch providers.tf main.tf variables.tf terraform.tfvars terraform.tfvars.example

cd /d/projects/my-project/terraform/cloud-sql
touch terraform.tf api.tf iam.tf cloud-sql.tf variables.tf
```

### `providers.tf`

`terraform/providers.tf`

```hcl
provider "google" {
  project = var.project_id
  region  = var.region
}
```

### `main.tf`

`terraform/main.tf`

```hcl
# 调用 cloud-sql 模块
module "cloud-sql" {
  source = "./cloud-sql"

  # 向局部变量传入全局变量的值
  prefix               = var.prefix
  project_id           = var.project_id
  region               = var.region
  mysql_root_password  = var.mysql_root_password
  mysql_jerry_password = var.mysql_jerry_password
}
```

### `variables.tf`

`terraform/variables.tf`：全局变量

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
  default     = "my"
}

# --- GCP ---
variable "project_id" {
  type        = string
  description = "GCP Project ID"
  default     = "project-60addf72-be9c-4c26-8db"
}

variable "region" {
  type        = string
  description = "GCP Region"
  default     = "asia-east2"
}

# --- Cloud SQL ---
variable "mysql_root_password" {
  type        = string
  description = "MySQL root user password"
  sensitive   = true
}

variable "mysql_jerry_password" {
  type        = string
  description = "MySQL jerry user password"
  sensitive   = true
}
```

### `terraform.tfvars`

`terraform/terraform.tfvars`：全局敏感变量赋值

```hcl
mysql_root_password  = "123456"
mysql_jerry_password = "000000"
```

### `terraform.tfvars.example`

`terraform/terraform.tfvars.example`：全局敏感变量赋值模板

```hcl
mysql_root_password = "mysql_root_password"
mysql_jerry_password = "mysql_jerry_password"
```

### `.gitignore`

`my-project/.gitignore`

添加[忽略内容](terraform-configuration-language.md#`.gitignore`)

### `terraform.tf`

`gar-docker-repo/terraform.tf`

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 7.14.0"
    }
  }
}
```

### `api.tf`

`gar-docker-repo/api.tf`

```hcl
locals {
  services = [
    "sqladmin.googleapis.com", # Cloud SQL API
    "iam.googleapis.com",      # IAM API
  ]
}

resource "google_project_service" "project_services" {
  for_each           = toset(local.services)
  service            = each.key
  disable_on_destroy = false
}
```

### `iam.tf`

`gar-docker-repo/iam.tf`

```hcl
# 若想让后端连接 Cloud SQL，则需要:
  # 为集群开启 Workload Identity
  # 创建 Workload Identity GSA 并为其分配 Cloud SQL Client 角色
  # 创建 App KSA 并绑定到 Workload Identity GSA
  # 允许 App KSA 以 Workload Identity GSA 身份运行
  # 详见 GKE 模块中的 iam.tf 文件
```

### `cloud-sql.tf`

`gar-docker-repo/cloud-sql.tf`

```hcl
# 创建 Cloud SQL 实例
resource "google_sql_database_instance" "mysql_instance" {
  name             = local.db_instance
  database_version = "MYSQL_8_0"
  region           = var.region

  settings {
    tier            = "db-f1-micro" # 测试环境使用的最小规格
    disk_type       = "PD_SSD"
    disk_size       = 10   # 初始 10GB
    disk_autoresize = true # 自动扩容

    # 开启公网 IP，但会通过 IAM 权限锁定访问，仅允许通过授权代理访问
    ip_configuration {
      ipv4_enabled = true
    }
  }

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# 创建 DATABASE
resource "google_sql_database" "my_db" {
  name      = local.db_name
  instance  = google_sql_database_instance.mysql_instance.name
  charset   = "utf8mb4"
  collation = "utf8mb4_unicode_ci"
}

# 创建 root 用户
resource "google_sql_user" "root_user" {
  name     = "root"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_root_password
  host     = "%"
}

# 创建普通账户
resource "google_sql_user" "jerry_user" {
  name     = "jerry"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_jerry_password
  host     = "%"
}

output "cloud_sql_connection_name" {
  description = "Cloud SQL instance connection name"
  value       = google_sql_database_instance.mysql_instance.connection_name
}

output "sql_instance_name" {
  description = "Cloud SQL 实例的名称"
  value       = google_sql_database_instance.mysql_instance.name
}

output "database_name" {
  description = "Cloud SQL database name"
  value       = google_sql_database.my_db.name
}
```

### `variables.tf`

`gar-docker-repo/variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
}

locals {
  db_instance    = "${var.prefix}-db-instance"
  db_name        = "${var.prefix}_db"
}

# --- GCP ---
variable "project_id" {
  type        = string
  description = "GCP Project ID"
}

variable "region" {
  type        = string
  description = "GCP Region"
}

# --- Cloud SQL ---
variable "mysql_root_password" {
  type        = string
  description = "MySQL root user password"
  sensitive   = true
}

variable "mysql_jerry_password" {
  type        = string
  description = "MySQL jerry user password"
  sensitive   = true
}
```

### 初始化 Terraform

```bash
cd d:/projects/my-project/terraform
terraform init
```

### 创建 Cloud SQL

```bash
cd d:/projects/my-project/terraform
terraform apply
```

# 连接 Cloud SQL (白名单)

有两种方式连接 Cloud SQL：

- [Cloud SQL Auth](<#Cloud SQL Auth>) (推荐)
- 添加白名单

此处记录如何添加白名单：

## 获取 Cloud SQL 实例的公网 IP

在 [Google Cloud Shell](https://console.cloud.google.com/) 中执行以下命令：

```bash
gcloud sql instances describe $INSTANCE_NAME --format='value(ipAddresses.ipAddress)'
gcloud sql instances describe todo-db-instance --format='value(ipAddresses.ipAddress)'
# 上次公网 IP：35.220.229.85
```

仅仅拿到公共 IP 是无法直接连接的，出于安全考虑，Google Cloud 默认会拦截所有外部连接。

## 获取本地电脑和 GKE 节点公网 IP

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

## 添加授权网络

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

# Cloud SQL Auth

[**Cloud SQL Auth**](https://docs.cloud.google.com/sql/docs/mysql/sql-proxy?hl=zh-cn) 是 Google Cloud 提供的一套安全连接 Cloud SQL 实例的认证机制，在不暴露数据库公网 IP、不使用静态数据库密码的前提下，安全地连接 Cloud SQL。它通过 **IAM 身份认证 + 临时凭证** 来完成数据库访问控制。

## 在本地连接

- [下载 Cloud SQL Auth](https://docs.cloud.google.com/sql/docs/mysql/sql-proxy?hl=zh-cn#install)，将文件重命名为 `cloud-sql-proxy.exe`。

- 在终端执行以下命令（确保已经配置了 `gcloud auth login`）

  ```bash
  cd /d/下载/综合下载
  
  ./cloud-sql-proxy 项目ID:区域:数据库实例名称
  ./cloud-sql-proxy project-60addf72-be9c-4c26-8db:asia-east2:my-db-instance
  ```

  保持终端打开，代理默认会监听本地的 `127.0.0.1:3306`。

- 使用 Navicate 连接 Cloud SQL，`127.0.0.1:3306`。

## 在集群中连接

详见 [Todo Fullstack](<todo-fullstack.md#Chart + Argo CD + GCP + Terraform 部署>) 项目

- 在 GKE 中[启用 Workload Identity](<gcp-iam.md#Workload Identity>)
- 在后端添加 cloud-sql-proxy 容器

### 允许 GSA 访问 Cloud SQL

```hcl
# iam.tf

# 允许 GSA 访问 Cloud SQL
resource "google_project_iam_member" "mysql_client" {
  project = var.project_id
  role    = "roles/cloudsql.client"
  member  = "serviceAccount:${google_service_account.workload_identity.email}"
}
```

### 添加 cloud-sql-proxy 容器

在后端 Chart 模板中添加一个 Cloud SQL Auth Proxy 容器

```yaml
# backend.yaml

containers:
  - name: backend
    # ... 省略其他配置 ...
  # 2. 关键：注入 Sidecar 容器：添加 cloud-sql-proxy 容器。
  - name: cloud-sql-proxy
    image: gcr.io/cloud-sql-connectors/cloud-sql-proxy:2.14.1
    args:
      - "--port=3306"
      - {{ include "my-chart.sqlInstanceConnectionName" . | quote }}
    securityContext:
      runAsNonRoot: true
```

```
# _helpers.tpl

# ... 省略其他配置 ...

{{/* 生成 Cloud SQL 实例连接名称 */}}
{{- define "my-chart.sqlInstanceConnectionName" -}}
{{- printf "%s:%s:%s" .Values.gcp.projectId .Values.gcp.region .Values.gcp.sqlInstanceName -}}
{{- end -}}
```

```yaml
# values.yaml

# ... 省略其他配置 ...

gcp:
  projectId: "project-60addf72-be9c-4c26-8db"
  region: "asia-east2"
  sqlInstanceName: "my-db-instance"
```

# Reference

## 语法

> [Gcloud SQL Reference](https://docs.cloud.google.com/sdk/gcloud/reference/sql)

gcloud sql [GROUP](https://docs.cloud.google.com/sdk/gcloud/reference/sql#GROUP) | [COMMAND](https://docs.cloud.google.com/sdk/gcloud/reference/sql#COMMAND) [[GCLOUD_WIDE_FLAG …](https://docs.cloud.google.com/sdk/gcloud/reference/sql#GCLOUD-WIDE-FLAGS)]
