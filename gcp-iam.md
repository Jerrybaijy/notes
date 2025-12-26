---
title: gcp-iam
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud-computing
  - gcp
---

# Overview

**IAM**（Identity and Access Management，身份与访问管理）是一个安全框架，旨在确保**正确的人员**在**正确的时间**为了**正确的理由**访问**正确的资源**。

> [GCP IAM Docs](https://docs.cloud.google.com/iam/docs?hl=zh-cn)

解决集群权限有三种方式，推荐 **Workload Identity**：

| **方式**              | **说明**                          | **复杂度** |
| --------------------- | --------------------------------- | ---------- |
| **默认服务账号**      | GKE 自动创建                      | 最简单     |
| **自定义服务账号**    | 手动创建，需要单独管理            | 中等       |
| **Workload Identity** | 精细控制 Pod 级别权限，安全性最高 | 复杂       |

# GSA

[**SA**](https://docs.cloud.google.com/iam/docs/service-account-overview?hl=zh-cn)（Service Accout）是一种通常由应用或计算工作负载（例如 Compute Engine 实例）而非真人使用的特殊账号。服务账号由其电子邮件地址（对该账号是唯一的）标识。

[**GSA**](https://docs.cloud.google.com/iam/docs/service-account-overview?hl=zh-cn)（Google Cloud Service Accout）是 Google 提供的 SA 功能。

GCP 有两种账号：

- 用户账号：控制台 > `IAM & Admin` > `IAM`
- GSA：控制台 > `IAM & Admin` > `Service Accounts`
  - 默认服务账号：创建项目时由系统默认创建
  - 自定义服务账号：由用户创建
  - 服务代理

## 自定义 GSA

```hcl
# 创建 GSA
resource "google_service_account" "default" {
  account_id   = var.service_account_id
  display_name = "Service Account"
}

resource "google_container_node_pool" "primary_preemptible_nodes" {
  # ...
  }

  node_config {
    # 使用 GSA
    service_account = google_service_account.default.email
    
    # ...
}
```

# Workload Identity

[**Workload Identity**](https://docs.cloud.google.com/iam/docs/workload-identity-federation?hl=zh-cn) 是一种“无密钥”认证机制。

> [Workload Identity](https://docs.cloud.google.com/iam/docs/workload-identity-federation?hl=zh-cn)

## `iam.tf`

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

## `gke.tf`

```hcl
# --- GKE ---
resource "google_container_cluster" "primary" {
  # ...

  # 启用 Workload Identity
  workload_identity_config {
    workload_pool = "${data.google_project.project.project_id}.svc.id.goog"
  }
}

# --- GKE Node Pool ---
resource "google_container_node_pool" "primary_preemptible_nodes" {
  # ...

  node_config {
    machine_type    = "e2-medium"
    service_account = google_service_account.workload_identity.email
    oauth_scopes = [
      "https://www.googleapis.com/auth/cloud-platform"
    ]
    
    # 配置节点以使用 Workload Identity 暴露元数据
    workload_metadata_config {
      mode = "GKE_METADATA"
    }
  }
}
```

