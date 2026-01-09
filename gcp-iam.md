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

# Workload Identity（旧）

[**Workload Identity**](https://docs.cloud.google.com/iam/docs/workload-identity-federation?hl=zh-cn) 是一种“无密钥”认证机制。

> [Workload Identity](https://docs.cloud.google.com/iam/docs/workload-identity-federation?hl=zh-cn)

**Workload Identity 的核心为**：

- 创建一个 GSA
  - 为 GSA 添加角色
- 创建一个 KSA（或者已存在，如 `argocd-repo-server`）
  - 将 KSA 绑定到 GSA
  - 允许 KSA 以 GSA 运行

**通信链条**：

```
Pod
 └─ 使用 KSA：<app_ns>/<ksa_name>
     └─ 通过 Workload Identity
         └─ 绑定到 GSA：<sa_id>@<project>.iam.gserviceaccount.com
             └─ GSA 拥有 roles/cloudsql.client
                 └─ Pod 可以访问 Cloud SQL
```

**为了使 Workload Identity 生效并让后端可以连接到 Cloud SQL**：

- **GCP 侧**
  - `iam.tf`
  - `gke.tf`
- **后端 Helm Chart 侧**
  - `backend.yaml`
  - `_helpers.tpl`
  - `values.yaml`

## Service Account

### `iam.tf`

```hcl
# 获取当前 Project ID
data "google_project" "project" {}

# 创建 Workload Identity GSA
resource "google_service_account" "workload_identity" {
  account_id   = local.workload_identity
  display_name = "GSA for Workload Identity"
}

# 为 Workload Identity GSA 分配角色
resource "google_project_iam_member" "workload_identity_roles" {
  for_each = toset([
    "roles/cloudsql.client",        # Cloud SQL Client
    "roles/artifactregistry.reader" # Artifact Registry Reader
  ])

  project = var.project_id
  role    = each.key
  member  = "serviceAccount:${google_service_account.workload_identity.email}"
}

# 创建 app_ns，防止因 app_ns 不存在而导致创建 App KSA 失败
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = local.app_ns
    annotations = {
      # 加注解，防止 Argo CD 删除该 Namespace
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
  lifecycle {
    ignore_changes = [
      metadata[0].labels # 忽略标签变化，防止 Argo CD 标签变更引起冲突
    ]
  }
}

# 创建 App KSA，并绑定到 Workload Identity GSA
resource "kubernetes_service_account_v1" "my_ksa" {
  metadata {
    name      = local.ksa_name
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
      # 加注解，防止 Argo CD 删除该 KSA
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
}

# 允许 App KSA 以 Workload Identity GSA 身份运行
resource "google_service_account_iam_member" "workload_identity_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[${local.app_ns}/${local.ksa_name}]"
}
```

### 创建 KSA 的两种方式

#### 在 Terraform 中声明 KSA 资源

```hcl
# iam.tf

# 创建 App KSA，并绑定到 Workload Identity GSA
resource "kubernetes_service_account_v1" "my_ksa" {
  metadata {
    name      = local.ksa_name
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
      # 加注解，防止 Argo CD 删除该 KSA
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
}
```

#### 在 Helm Chart 中声明 KSA 资源

需在 Chart 模板中创建一个名为 `my-ksa` 的 ServiceAccount，并且要在它的 **Annotations（注解）** 里写上对应的 GCP serviceAccountName。

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
  namespace: my-ns
  serviceAccountName: "my-ksa"

gcp:
  sqlProxySaEmail: "my-sa-id@project-60addf72-be9c-4c26-8db.iam.gserviceaccount.com"
```

## `gke.tf`

```hcl
# --- GKE ---
resource "google_container_cluster" "my-cluster" {
  # ...

  # 启用 Workload Identity
  workload_identity_config {
    workload_pool = "${data.google_project.project.project_id}.svc.id.goog"
  }
}

# --- GKE Node Pool ---
resource "google_container_node_pool" "my-node-pool" {
  # ...

  node_config {
    # ...
    
    # 配置节点以使用 Workload Identity 暴露元数据
    workload_metadata_config {
      mode = "GKE_METADATA"
    }
  }
}
```

## `backend.yaml`

```yaml
# 1. 关键：指定 ksa 以支持 Workload Identity
serviceAccountName: {{ .Values.global.ksaName }}

containers:
- name: backend
  # ... 后端配置

# 2. 关键：添加 cloud-sql-proxy 容器，连接到 Cloud SQL 实例
- name: cloud-sql-proxy
  image: gcr.io/cloud-sql-connectors/cloud-sql-proxy:2.14.1
  args:
    - "--port=3306"
    - {{ include "my-chart.sqlInstanceConnectionName" . | quote }}
  securityContext:
    runAsNonRoot: true
```

## `values.yaml`

```yaml
# 全局配置
global:
  ksaName: my-ksa

# 用于模板函数中生成 Cloud SQL 实例连接名称
gcp:
  projectId: "project-60addf72-be9c-4c26-8db"
  region: "asia-east2"
  sqlInstanceName: "my-db-instance"
```

## `_helpers.tpl`

```tpl
{{/* 生成 Cloud SQL 实例连接名称 */}}

{{- define "my-chart.sqlInstanceConnectionName" -}}
{{- printf "%s:%s:%s" .Values.gcp.projectId .Values.gcp.region .Values.gcp.sqlInstanceName -}}
{{- end -}}
```

# FAQ

由于 Argo CD 无法拉取 Google Artifat Registry，下面是一些留存验证方法。

```
# 查看 Argo CD 的 argocd-repo-server 是否绑定到 GSA
kubectl get sa argocd-repo-server -n argocd -o yaml

# 查看 GSA 是否给 Argo CD 的 argocd-repo-server 授权
gcloud iam service-accounts get-iam-policy my-workload-identity@project-60addf72-be9c-4c26-8db.iam.gserviceaccount.com

kubectl rollout restart deployment argocd-repo-server -n argocd

kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-repo-server
```

```
kubectl exec -n argocd deploy/argocd-repo-server -it -- sh

helm pull oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-chart --version 99.99.99-latest
```

```
# 检查 cluster 和 node pool 的 Workload Identity 配置

gcloud container clusters describe my-cluster \
    --region asia-east2 \
    --project project-60addf72-be9c-4c26-8db \
    | grep workloadMetadataConfig

gcloud container node-pools describe my-node-pool \
    --cluster my-cluster \
    --region asia-east2 \
    --project project-60addf72-be9c-4c26-8db \
    | grep workloadMetadataConfig
```

