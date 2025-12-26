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

- [GCP 准备工作](<gcp.md#准备工作>)已完成
- [Terraform 安装](<terraform-cli.md#Install>)已完成
- GCP 项目已创建并关联结算账号

## 创建和销毁 GCP 资源

参考 [Terraform Quick Start](<terraform.md#Quick Start>)

```bash
cd /d/projects/0000-tests/terraform-test
touch terraform.tf provider.tf gcp-project.tf variable.tf output.tf
```

# GSA

[**GSA**](<gcp-iam.md#GSA>)（Google Cloud Service Accout）是 Google 提供的 SA 功能。

## Quick Start<a id="GSA Quick Start"></a>

```hcl
# 获取当前 Project ID
data "google_project" "project" {}

# 创建 GSA
resource "google_service_account" "workload_identity" {
  account_id   = var.service_account_id
  display_name = "GSA for Workload Identity"
}

# 防止因 namespace 不存在而导致创建 IAM 失败
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = var.app_namespace
  }
}

# 向 KSA 进行 GSA 授权
resource "google_service_account_iam_member" "workload_identity_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[${var.app_namespace}/${var.app_ksa}]"
}

# 为 Pod 创建 KSA 并绑定 GSA
resource "kubernetes_service_account_v1" "my_app_ksa" {
  metadata {
    name      = var.app_ksa
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
    }
  }
}
```

## `google_service_account`

[`google_service_account`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_service_account) type 用于创建谷歌服务账号 ([GSA](gcp-iam.md#GSA))。

完整功能详见 [Terraform GCP | GSA | Quick Start](<terraform-gcp.md#GSA Quick Start>)

```hcl
resource "google_service_account" "$LABEL" {
  account_id   = "$ID"
  display_name = "Service Account"
}
```

```hcl
# 创建 GSA
resource "google_service_account" "workload_identity" {
  account_id   = var.service_account_id
  display_name = "GSA for Workload Identity"
}
```

## `google_service_account_iam_member`

[`google_service_account_iam_member`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_service_account_iam#google_service_account_iam_member-1) 用于向特定成员授权，管理或使用 GSA。

完整功能详见 [Terraform GCP | GSA | Quick Start](<terraform-gcp.md#GSA Quick Start>)

```hcl
resource "google_service_account_iam_member" "$LABEL" {
  service_account_id = $SERVICE_ACCOUNT_ID
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:$PROJECT_ID.svc.id.goog[$NAMESPACE/$KSA_NAME]""
}
```

```hcl
# 获取当前 Project ID
data "google_project" "project" {}

# 防止因 namespace 不存在而导致创建 IAM 失败
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = var.app_namespace
  }
}

# 向 KSA 进行 GSA 授权
resource "google_service_account_iam_member" "workload_identity_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[${var.app_namespace}/${var.app_ksa}]"
}
```

# Provider

## Provider 准备工作

[Terraform GCP 准备工作](<terraform-gcp.md#准备工作>)已完成

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

## `variable.tf`

```hcl
# --- GCP Provider ---
variable "gcp_region" {
  type        = string
  description = "GCP Region"
  default     = "asia-east2"
}

variable "gcp_zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east2-a"
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
```

# Project

> [`google_project`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_project)

尽量在 GCP 控制台创建项目，否则会遇到如下问题：

- API 依赖
- API 等待
- 每个 billing account 链接到 project 的次数是有上限的，学习时要注意节约，尽量少创建项目。
- ...

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
  default     = "asia-east2"
}

variable "gcp_zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east2-a"
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

## 准备工作

- [Terraform-GCP 准备工作](<terraform-gcp.md#准备工作>)已完成
- [Kubectl 已安装并完成配置](<gcp-gke.md#Quick Start>)

## 普通方法

### `terraform.tf`

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

### `provider.tf`

```hcl
provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
  zone    = var.gcp_zone
}
```

### `api.tf`

```hcl
# Compute Engine API
resource "google_project_service" "compute" {
  service = "compute.googleapis.com"
  disable_on_destroy = false
}

# Kubernetes Engine API
resource "google_project_service" "container" {
  service = "container.googleapis.com"
  disable_on_destroy = false
}
```

### `iam.tf`

```hcl
# Service Account
resource "google_service_account" "default" {
  account_id   = var.service_account_id
  display_name = "Service Account"
}
```

### `gke.tf`

```hcl
# GKE
resource "google_container_cluster" "primary" {
  name                     = var.gke_name
  location                 = var.region
  remove_default_node_pool = true
  initial_node_count       = 1
  depends_on = [
    google_project_service.compute,
    google_project_service.container
  ]

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# Node pool
resource "google_container_node_pool" "primary_preemptible_nodes" {
  name       = var.node_pool_name
  location   = var.region
  cluster    = google_container_cluster.primary.name
  node_count = 1

  autoscaling {
    min_node_count = 1
    max_node_count = 5
  }

  node_config {
    machine_type    = "e2-medium"
    service_account = google_service_account.default.email
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

### `variable.tf`

```hcl
# --- GCP Provider ---
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

variable "zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east2-a"
}

# --- GKE ---
variable "gke_name" {
  type        = string
  description = "GKE name"
  default     = "my-cluster"
}

variable "node_pool_name" {
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

### `output.tf`

```hcl
output "gke_cluster_name" {
  description = "GKE name"
  value       = google_container_cluster.my_cluster.name
}
```

## 启用 Workload Identity (推荐)

### `terraform.tf`

```
terraform {
  required_providers {
    google = {
      version = ">= 5.0.0"
      source  = "hashicorp/google"
    }
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = ">= 2.0.0"
    }
  }
}
```

### `provider.tf`

```hcl
provider "google" {
  project = var.project_id
  region  = var.region
  zone    = var.zone
}

data "google_client_config" "default" {}
provider "kubernetes" {
  host                   = "https://${google_container_cluster.primary.endpoint}"
  token                  = data.google_client_config.default.access_token
  cluster_ca_certificate = base64decode(google_container_cluster.primary.master_auth[0].cluster_ca_certificate)
}
```

### `api.tf`

```hcl
locals {
  services = [
    "compute.googleapis.com",        # Compute Engine API
    "container.googleapis.com",      # Kubernetes Engine API
    "iam.googleapis.com",            # IAM API
    "iamcredentials.googleapis.com", # Workload Identity API
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
# 获取当前 Project ID
data "google_project" "project" {}

# 创建 GSA
resource "google_service_account" "workload_identity" {
  account_id   = var.service_account_id
  display_name = "GSA for Workload Identity"
}

# 防止因 namespace 不存在而导致创建 IAM 失败
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = var.app_namespace
  }
}

# 向 KSA 进行 GSA 授权
resource "google_service_account_iam_member" "workload_identity_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[${var.app_namespace}/${var.app_ksa}]"
}

# 为 Pod 创建 KSA 并绑定 GSA
resource "kubernetes_service_account_v1" "my_app_ksa" {
  metadata {
    name      = var.app_ksa
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
    }
  }
}
```

### `gke.tf`

```hcl
# --- GKE ---
resource "google_container_cluster" "primary" {
  name                     = var.gke_name
  location                 = var.region
  remove_default_node_pool = true
  initial_node_count       = 1
  depends_on = [google_project_service.project_services]

  # 启用 Workload Identity
  workload_identity_config {
    workload_pool = "${data.google_project.project.project_id}.svc.id.goog"
  }

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# --- GKE Node Pool ---
resource "google_container_node_pool" "primary_preemptible_nodes" {
  name       = var.node_pool_name
  location   = var.region
  cluster    = google_container_cluster.primary.name
  node_count = 1

  autoscaling {
    min_node_count = 1
    max_node_count = 5
  }

  node_config {
    machine_type    = "e2-medium"
    service_account = google_service_account.workload_identity.email
    oauth_scopes = [
      "https://www.googleapis.com/auth/cloud-platform"
    ]
    
    # 使用 Workload Identity 暴露元数据
    workload_metadata_config {
      mode = "GKE_METADATA"
    }
  }
}
```

- `deletion_protection`：关闭误删保护（生产环境不应设置此参数）
- [`remove_default_node_pool`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#remove_default_node_pool-1)：删除默认节点池
  - [官方建议](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#example-usage---with-a-separately-managed-node-pool-recommended)，将节点池作为独立的资源创建和管理。
  - 直接在 `google_container_cluster ` 资源中定义的节点池无法在不重新创建集群的情况下移除。
- [`initial_node_count`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#initial_node_count-1)：要在此集群的默认节点池中创建的节点数。
- [`autoscaling`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_node_pool#autoscaling-1)：自动伸缩

### `variable.tf`

```hcl
# --- GCP Provider ---
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

variable "zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east2-a"
}

# --- GKE ---
variable "gke_name" {
  type        = string
  description = "GKE name"
  default     = "my-cluster"
}

variable "node_pool_name" {
  type        = string
  description = "GKE Node Pool name"
  default     = "my-node-pool"
}

# --- IAM ---
variable "service_account_id" {
  type        = string
  description = "Service Account ID"
  default     = "my-service-account-id"
}

variable "app_namespace" {
  type        = string
  description = "Kubernetes namespace for the application"
  default     = "my-namespace"
}

variable "app_ksa" {
  type        = string
  description = "Kubernetes Service Account name for the application"
  default     = "my-app-ksa"
}
```

### `output.tf`

```hcl
output "gke_name" {
  description = "GKE name"
  value       = google_container_cluster.primary.name
}
```

# Gcloud SQL

1. 启用 `"sqladmin.googleapis.com"` API

2. 在创建 GKE 时[启用 Workload Identity](<terraform-gcp.md#启用 Workload Identity (推荐)>)

3. 在 `iam.tf` 中加入以下内容：

   ```hcl
   # 授予 GSA 访问 Cloud SQL 的客户端权限
   resource "google_project_iam_member" "cloudsql_client" {
     project = var.project_id
     role    = "roles/cloudsql.client"
     member  = "serviceAccount:${google_service_account.default.email}"
   }
   ```

4. 需在 Chart 模板中创建一个名为 `my-k8s-sa` 的 ServiceAccount，并且要在它的 **Annotations（注解）** 里写上对应的 GCP 账号：（或者使用 Terraform 创建这个资源）

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

5. 在后端 Chart 模板中添加一个 Cloud SQL Auth Proxy 容器

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
         - {{ include "todo-chart.sqlInstanceConnectionName" . | quote }}
       securityContext:
         runAsNonRoot: true
   ```

