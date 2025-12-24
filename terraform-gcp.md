---
title: terraform-gcp
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud
  - gcp
  - iac
  - terraform
---

# Overview

此笔记主要记录 Terraform 创建 GCP 资源的样板。

> [Terraform provider for Google Cloud Docs](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
>
> [Terraform on Google Cloud](https://docs.cloud.google.com/docs/terraform?hl=zh-cn)

# Quick Start

## 准备工作

- [GCP 准备工作](<gcp.md#准备工作>)已完成。
- [本地 kubectl](<kubernetes.md#kubectl>) 已安装（如需部署 GKE 的话）。
- [Terraform](<terraform.md#Install>) 已安装。

## 创建和销毁 GCP 资源

参考 [Terraform Quick Start](<terraform.md#Quick Start>)

```bash
cd /d/projects/0000-tests/terraform-test
touch terraform.tf provider.tf gcp-project.tf variable.tf output.tf
```

# Project

> [`google_project`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_project)

## `terraform.tf`

```
terraform {
  required_providers {
    google = {
      version = ">= 5.0.0"
      source  = "hashicorp/google"
    }
  }
}
```

## `provider.tf`

```hcl
provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
  zone    = var.gcp_zone
}
```

## `gcp-project.tf`

```hcl
# 创建项目
resource "google_project" "my_project" {
  project_id          = var.gcp_project_id
  name                = var.gcp_project_name
  org_id              = var.gcp_org_id
  billing_account     = var.gcp_billing_account_id
  auto_create_network = false
  # 允许删除（生产环境不应设置此参数）
  deletion_policy = "DELETE"
}

# 启用 API，以 Compute Engine 为例
resource "google_project_service" "compute_api" {
  project = google_project.my_project.project_id
  service = "compute.googleapis.com"

  # 依赖项目创建完成
  depends_on = [google_project.my_project]
}
```

- [`billing_account`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_project.html?q=#billing_account-1)：关联账单账号（可选，但推荐）。
- [`auto_create_network`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_project.html?q=#auto_create_network-1)：是否自动创建默认网络（建议设为 false，保持项目整洁）。
- [`deletion_policy`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_project.html?q=#deletion_policy-1)：删除政策，为了方便调试在开发环境可设置为 `DELETE`。

## `variable.tf`

```hcl
# --- GCP Provider ---
variable "gcp_region" {
  type        = string
  description = "GCP Region"
  default     = "asia-east1"
}

variable "gcp_zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east1-a"
}

# --- GCP Project ---
variable "gcp_org_id" {
  type        = string
  description = "GCP Organization ID"
  default     = "338307828462"
}

variable "gcp_project_id" {
  type        = string
  description = "GCP Project ID"
  default     = "project-jerry-555555"
}

variable "gcp_project_name" {
  type        = string
  description = "GCP Project 名称"
  default     = "My Project"
}

variable "gcp_billing_account_id" {
  type        = string
  description = "GCP 账单账号ID"
  default     = "01716E-392C40-6E5B41"
}
```

## `output.tf`

```hcl
output "gcp_project_id" {
  description = "GCP project ID"
  value       = google_project.my_project.project_id
}
```

# GKE

> [`google_container_cluster`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster)
>
> [`google_container_node_pool`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_node_pool)

以下文件详见 [GCP Project](<#GCP Project>) 章节：

- `terraform.tf`
- `provider.tf`
- `gcp-project.tf`

## `gke.tf`

```hcl
# service account
resource "google_service_account" "my_service_account" {
  account_id   = var.service_account_id
  display_name = "Service Account"
}

# cluster
resource "google_container_cluster" "my_cluster" {
  name                     = var.gcp_gke_name
  location                 = var.gcp_region
  remove_default_node_pool = true
  initial_node_count       = 1

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# node pool
resource "google_container_node_pool" "my_node_pool" {
  name       = var.gcp_node_pool_name
  location   = var.gcp_region
  cluster    = google_container_cluster.my_cluster.name
  node_count = 1

  autoscaling {
    min_node_count = 1
    max_node_count = 5
  }

  node_config {
    machine_type = "e2-medium"

    service_account = google_service_account.my_service_account.email
    oauth_scopes = [
      "https://www.googleapis.com/auth/cloud-platform"
    ]
  }
}
```

- `deletion_protection`：关闭误删保护（生产环境不应设置此参数）
- [`remove_default_node_pool`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#remove_default_node_pool-1)：删除默认节点池
  - [官方建议](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#example-usage---with-a-separately-managed-node-pool-recommended)，将节点池作为独立的资源创建和管理。
  - 直接在 `google_container_cluster ` 资源中定义的节点池无法在不重新创建集群的情况下移除。
- [`initial_node_count`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#initial_node_count-1)：要在此集群的默认节点池中创建的节点数。
- [`autoscaling`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_node_pool#autoscaling-1)：自动伸缩

## `variable.tf`

```hcl
# --- GKE ---
variable "gcp_gke_name" {
  type        = string
  description = "GKE name"
  default     = "my-cluster"
}

variable "gcp_node_pool_name" {
  type        = string
  description = "GKE Node Pool name"
  default     = "my-node-pool"
}

variable "service_account_id" {
  type        = string
  description = "Service Account ID"
  default     = "my-service-account-id"
}
```

## `output.tf`

```hcl
output "gcp_project_id" {
  description = "GCP project ID"
  value       = google_project.my_project.project_id
}

output "gke_cluster_name" {
  description = "GKE name"
  value       = google_container_cluster.my_cluster.name
}
```

# Gcloud SQL

## `iam.tf`

```hcl
# 创建一个专门给 Pod 用的 GCP 服务账号
resource "google_service_account" "sql_proxy_sa" {
  account_id   = "sql-proxy-sa"
  display_name = "Service Account for SQL Auth Proxy"
}

# 允许 K8s 服务账号使用该 GCP 服务账号
resource "google_service_account_iam_member" "workload_identity_user" {
  service_account_id = google_service_account.sql_proxy_sa.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${var.gcp_project_id}.svc.id.goog[my-namespce/my-k8s-sa]"
}

# 给该账号授予 Cloud SQL Client 权限
resource "google_project_iam_member" "sql_client_role" {
  project = var.gcp_project_id
  role    = "roles/cloudsql.client"
  member  = "serviceAccount:${google_service_account.sql_proxy_sa.email}"
}
```

- `my-namespce`：应用的命名空间
- `my-k8s-sa`：Chart 模板中 ServiceAccount 名称

**为了给该账号授予 Cloud SQL Client 权限**：

1. 需在 `gke.tf` 中启用：

   ```hcl
   resource "google_container_cluster" "my_cluster" {
     workload_identity_config {
       workload_pool = "${var.gcp_project_id}.svc.id.goog"
     }
   
     # ...
   }
   ```

2. 需在 Chart 模板中创建一个名为 `my-k8s-sa` 的 ServiceAccount，并且要在它的 **Annotations（注解）** 里写上对应的 GCP 账号：

   ```yaml
   # serviceaccount.yaml
   
   apiVersion: v1
   kind: ServiceAccount
   metadata:
     name: {{ .Values.global.serviceAccountName }}
     namespace: {{ .Values.global.namespace }}
     annotations:
       iam.gke.io/gcp-service-account: {{ .Values.gcp.sqlProxySaEmail | quote }}
   ```

   ```yaml
   # values.yaml
   
   global:
     namespace: my-namespace
     serviceAccountName: "my-k8s-sa"
   
   gcp:
     projectId: "project-60addf72-be9c-4c26-8db"
     sqlProxySaEmail: "sql-proxy-sa@project-60addf72-be9c-4c26-8db.iam.gserviceaccount.com"
   ```
