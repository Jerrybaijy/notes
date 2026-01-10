---
title: argo-cd
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - git-ops
  - ci-cd
  - k8s
  - argo-cd
---

# Overview

[**Argo CD**](https://argo-cd.readthedocs.io/en/stable/) 是一个声明式的、面向 Kubernetes 的 GitOps CD 工具。

![argo-cd](assets/argo-cd.png)

# Quick Start

## 准备工作

- Docker 已安装
- Kubectl 已安装
- 集群已启动

## 安装及初始化

- [安装 Argo CD](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

  ```bash
  # 创建 Argo CD 命名空间
  kubectl create namespace argocd
  
  # 安装 Argo CD
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  ```

- 查看 pod 状态，直到全部运行

  ```bash
  kubectl get pod -n argocd
  ```

- 配置 Argo CD Server

  ```bash
  # 本地：转发端口到本地（临时），访问：127.0.0.1:8080
  kubectl port-forward svc/argocd-server 8080:443 -n argocd
  
  # 公网
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
  
  # 查看网络服务
  kubectl get svc -n argocd
  ```

- 获取密码

  ```bash
  kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
  
  # 用户名：admin
  # 本地上次密码：dAlsKbgZa4FvVT6V
  # GCP 上次密码：BKgY5d5oEQCoMNFx
  ```

- 本地访问

  - 端口转发以后，当前终端要保持打开，否则访问不到。
  - 访问地址：https://127.0.0.1:8080

- 公网访问

  - 需要科学上网
  - 访问地址：http://$EXTERNAL-IP

## 编写配置文件

编写 Chart 配置文件

[编写 CR 配置文件](<#编写 CR 配置文件>)

## 部署应用

```bash
cd d:/projects/my-project/argo-cd
kubectl apply -f my-app.yaml
```

## 访问应用

### 本地

前端端口转发：

```bash
# 查看应用服务
kubectl get svc -n my-ns

# 将前端服务 80 端口到本地 8081 端口
kubectl port-forward svc/frontend 8081:80 -n my-ns
```

如有调试需要，也可将后端和数据库进行端口转发：

```bash
# 数据库
kubectl port-forward svc/mysql 3306:3306 -n my-ns
# 后端
kubectl port-forward svc/backend 5000:5000 -n my-ns
```

访问应用：http://localhost:8081/

### 公网

查看前端公网 IP：

```bash
kubectl get svc -n my-ns
```

访问应用：http://$EXTERNAL-IP

## 删除应用

```bash
cd d:/projects/my-project/argo-cd
kubectl delete -f my-app.yaml
```


## 删除 Argo CD

删除 ArgoCD 自定义资源定义（CRD）

```bash
kubectl delete crd applications.argoproj.io appprojects.argoproj.io argocds.argoproj.io

# 或者（与安装对应）
kubectl delete -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

删除 ArgoCD 的命名空间

```bash
kubectl delete ns argocd
```

# Install

Argo CD 有[多种安装方式](https://argo-cd.readthedocs.io/en/stable/operator-manual/installation/)。

## 使用声明式清单安装 Argo CD

- 准备工作

  - Docker 已安装

  - Kubectl 已安装
  - 集群已启动

- [安装 Argo CD](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

  ```bash
  # 创建 Argo CD 命名空间
  kubectl create namespace argocd
  
  # 安装 Argo CD
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  ```

- 查看 pod 状态，直到全部运行

  ```bash
  kubectl get pod -n argocd
  ```

## 使用 Helm Chart 安装 Argo CD

## 使用 Terraform 安装 Argo CD

### 准备工作

建立在[使用 Terraform 配置 GKE 集群](<gcp-gke.md#使用 Terraform 创建 GKE 集群>)的基础上

### 创建 `argocd` 模块目录

```bash
DIR=/d/projects/my-project/terraform/argocd && mkdir -p $DIR && cd $DIR
touch argocd.tf outputs.tf terraform.tf variables.tf
```

### `main.tf`

根模块主文件 `terraform/main.tf`

```hcl
# 调用 argocd 模块
module "argocd" {
  source     = "./argocd"
  depends_on = [module.gke]

  # 传递其它模块的输出
  workload_identity_gsa_email = module.gke.workload_identity_gsa_email

  # 传递根模块的变量
  prefix         = var.prefix
  project_id     = var.project_id
  region         = var.region
  my_external_ip = var.my_external_ip
}
```

### `providers.tf`

根模块 provider 文件  `terraform/providers.tf`

```hcl
provider "helm" {
  kubernetes = {
    host                   = "https://${module.gke.cluster_endpoint}"
    token                  = data.google_client_config.default.access_token
    cluster_ca_certificate = base64decode(module.gke.cluster_ca_certificate)
  }
}
```

### `terraform.tfvars`

根模块敏感变量赋值文件 `terraform/terraform.tfvars`

```hcl
# # Argo CD management IP
my_external_ip = "5.181.21.188"
```

### `terraform.tfvars.example`

根模块敏感变量赋值文件模板 `terraform/terraform.tfvars.example`

```hcl
# Argo CD management IP
my_external_ip = ""
```

### `variables.tf`

根模块变量文件 `terraform/variables.tf`

```hcl
# --- Argo CD ---
variable "my_external_ip" {
  type        = string
  description = "My external IP access to Argo CD"
  sensitive   = true
}
```

### `.gitignore`

Git 忽略文件 `my-project/.gitignore` 中添加[忽略内容](terraform-configuration-language.md#`.gitignore`)

### `argocd.tf`

`argocd` 模块主文件 `argocd/argocd.tf`

```hcl
# 创建 Argo CD 命名空间
resource "kubernetes_namespace_v1" "argocd_ns" {
  metadata {
    name = "argocd"
  }
}

# 安装 Argo CD
resource "helm_release" "argocd" {
  name       = "argocd"
  repository = "https://argoproj.github.io/argo-helm"
  chart      = "argo-cd"
  namespace  = kubernetes_namespace_v1.argocd_ns.metadata[0].name
  version    = "7.7.1"

  set = [
    # 为 argocd-repo-server KSA 添加注解，绑定到 Workload Identity GSA
    {
      name  = "repoServer.serviceAccount.annotations.iam\\.gke\\.io/gcp-service-account"
      value = var.workload_identity_gsa_email
    },
    # 设置服务类型为 LoadBalancer
    {
      name  = "server.service.type"
      value = "LoadBalancer"
    },
    # 允许 HTTP 访问
    {
      name  = "server.extraArgs"
      value = "{--insecure}"
    },
    # 仅允许自己的 IP 访问
    {
      name  = "server.service.loadBalancerSourceRanges"
      value = "{${var.my_external_ip}/32}"
    }
  ]
}

# 创建 Argo CD 访问 GAR 的 Secret
resource "kubernetes_secret_v1" "gar_repo_secret" {
  metadata {
    name      = "gar-repo-secret"
    namespace = kubernetes_namespace_v1.argocd_ns.metadata[0].name
    labels = {
      "argocd.argoproj.io/secret-type" = "repository"
    }
  }

  data = {
    name      = "${var.prefix}-docker-repo"
    type      = "helm"
    url       = local.chart_repo_url
    enableOCI = "true"
  }
}
```

1

### `outputs.tf`

`argocd` 模块输出文件 `argocd/outputs.tf`

```hcl
output "argocd_ns" {
  description = "ArgoCD 命名空间名称"
  value       = kubernetes_namespace_v1.argocd_ns.metadata[0].name
}

# 获取 Argo CD 服务数据
data "kubernetes_service_v1" "argocd_server" {
  metadata {
    name      = "${helm_release.argocd.name}-server"
    namespace = helm_release.argocd.namespace
  }
  depends_on = [helm_release.argocd]
}

# 输出 Argo CD 公网 IP
output "argocd_loadbalancer_ip" {
  description = "Argo CD UI 的公网访问 IP"
  value       = data.kubernetes_service_v1.argocd_server.status[0].load_balancer[0].ingress[0].ip
}

# 获取初始密码 Secret 数据
data "kubernetes_secret_v1" "argocd_initial_admin_secret" {
  metadata {
    name      = "argocd-initial-admin-secret"
    namespace = helm_release.argocd.namespace
  }
  depends_on = [helm_release.argocd]
}

# 输出初始管理员密码
output "argocd_initial_admin_password" {
  description = "Argo CD 的初始管理员密码 (用户名为 admin)"
  value       = data.kubernetes_secret_v1.argocd_initial_admin_secret.data["password"]
  sensitive   = true
}
```

### `terraform.tf`

`argocd` 模块 provider version 文件 `argocd/terraform.tf`

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 7.14.0"
    }
    helm = {
      source  = "hashicorp/helm"
      version = "~> 3.1.0"
    }
  }
}
```

### `variables.tf`

`argocd` 模块变量文件 `argocd/variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
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

# --- Argo CD ---
variable "my_external_ip" {
  type        = string
  description = "My external IP access to Argo CD"
  sensitive   = true
}

locals {
  chart_repo_url = "${var.region}-docker.pkg.dev/${var.project_id}/${var.prefix}-docker-repo"
}

variable "workload_identity_gsa_email" {
  type        = string
  description = "Workload Identity GSA email"
}
```

### `gke/iam.tf`

在 `gke/iam.tf` 中添加如下配置，以允许 Argo CD 从 GAR 拉取 chart。

```hcl
# 为 Workload Identity GSA 分配角色
resource "google_project_iam_member" "workload_identity_roles" {
  for_each = toset([
    
    # ... 其它角色 ...
    
    "roles/artifactregistry.reader" # Artifact Registry Reader
  ])

  project = var.project_id
  role    = each.key
  member  = "serviceAccount:${google_service_account.workload_identity.email}"
}

# 允许 argocd-repo-server KSA 以 Workload Identity GSA 身份运行
resource "google_service_account_iam_member" "argocd_repo_server_binding" {
  service_account_id = google_service_account.workload_identity.name
  role               = "roles/iam.workloadIdentityUser"
  member             = "serviceAccount:${data.google_project.project.project_id}.svc.id.goog[argocd/argocd-repo-server]"
}
```

### `argocd/iam.tf`

```hcl
# 若想让 Argo CD 从 GKE 集群访问 GAR，则需要:
  
  # Argo CD 侧
    # 在安装 Argo CD 时，为 argocd-repo-server KSA 添加注解，绑定到 Workload Identity GSA。
    # 创建 Argo CD 访问 GAR 的 Secret
  
  # GKE 侧
    # 为集群开启 Workload Identity
    # 创建 Workload Identity GSA 并为其分配 Artifact Registry Reader 角色
    # 允许 argocd-repo-server KSA 以 Workload Identity GSA 身份运行
    # 详见 GKE 模块中的 iam.tf 文件
```

### 初始化 Terraform

```bash
cd d:/projects/my-project/terraform
terraform init
```

### 安装 Argo CD

```bash
cd d:/projects/my-project/terraform
terraform apply
```

# 访问管理页面

## Kubectl 方式创建时访问管理页面

### 本地

端口转发：

```bash
# 查看网络服务
kubectl get svc -n argocd

# 本地：转发端口到本地
kubectl port-forward svc/argocd-server 8080:443 -n argocd
```

本地访问：

- 端口转发以后，当前终端要保持打开，否则访问不到
- 访问地址：https://127.0.0.1:8080

### 公网

改变 `argocd-server` 的类型为 `LoadBalancer`：

```bash
# 查看网络服务
kubectl get svc -n argocd

# 公网
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

公网访问：

- 需要科学上网
- 访问地址：http://$EXTERNAL-IP

## Terraform 方式创建时访问管理页面

### 通过设置 LoadBalancer

在 Argo CD 资源块中添加如下：

- 设置服务类型为 LoadBalancer
- 且仅允许自己的 IP 访问

```hcl
set = [
  # 设置服务类型为 LoadBalancer
  {
    name  = "server.service.type"
    value = "LoadBalancer"
  },
  # 允许 HTTP 访问
  {
    name  = "server.extraArgs"
    value = "{--insecure}"
  },
  # 仅允许自己的 IP 访问
  {
    name  = "server.service.loadBalancerSourceRanges"
    value = "{${var.my_external_ip}/32}"
  }
]
```

**公网访问**：

- 需要科学上网

- 获取 Argo CO 管理页面 IP

  ```bash
  terraform output argocd_loadbalancer_ip
  ```

- 访问地址：http://$EXTERNAL-IP

### GKE Ingress + Identity-Aware Proxy (IAP) (生产级推荐)

这套方案虽然配置复杂，但它利用了 Google 的全球负载均衡和身份验证体系，是目前 GKE 上管理后台最安全的做法。

1.  准备工作：配置 OAuth 同意屏幕
2.  创建 Google 托管证书 (Managed Certificate)
3.  配置 BackendConfig 以启用 IAP
4.  修改 Argo CD 服务 (Service)
5.  创建 Ingress 暴露服务
6.  配置 IAM 权限
7.  域名解析 (DNS)

# 获取初始密码

**注意**：登录以后应在 `User Info` 中及时修改密码！

Kubectl 方式创建时获取初始密码：

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d

# 用户名：admin
# 本地上次密码：dAlsKbgZa4FvVT6V
```

Terraform 方式创建时获取初始密码：

```bash
terraform output -raw argocd_initial_admin_password
```

# 编写 K8s 配置文件

## 准备工作

- Argo CD 已安装并初始化

- 源代码开发完成，已将引用的 Image 推送至镜像仓库。

- 创建 K8s 配置文件和目录

  ```
  cd d:/projects/my-project
  mkdir k8s
  touch namespace.yaml mysql.yaml backend.yaml frontend.yaml
  ```

## `namespace.yaml`

创建命名空间 `k8s/namespace.yaml`

## `mysql.yaml`

创建数据库配置文件 `k8s/mysql.yaml`

## `backend.yaml`

创建后端配置文件 `k8s/backend.yaml`

## `frontend.yaml`

创建前端配置文件 `k8s/frontend.yaml`

# CR 配置文件

## Overview

[`application.yaml`](https://argo-cd.readthedocs.io/en/stable/user-guide/application-specification/) 是 Argo CD 的 [Kubernetes CR](kubernetes.md#CR) 配置文件，它声明式地定义了 Argo CD 如何将**K8s 配置文件**或 **Helm Chart** 中指定的应用配置同步到目标 Kubernetes 集群。

- Argo CD 的安装过程已经在 Kubernetes 集群中配置并部署了 CRD，这个 CRD 就是 `Application` 对象的蓝图。
- 通过 `kubectl apply -f application.yaml` 命令所创建的 YAML 文件，正是该 [CRD](kubernetes.md#CRD) 定义的 [CR](kubernetes.md#CR) 的一个实例。

## 编写 CR 配置文件

在 `argo-cd` 目录创建 Argo CD 的 CR 配置文件 `my-app.yaml`

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-app
  namespace: argocd
  finalizers:
    - resources-finalizer.argocd.argoproj.io
spec:
  project: default
  source:
    # <oci-registry>
    repoURL: registry.gitlab.com/jerrybai/my-project
    targetRevision: "99.99.99-latest"
    chart: my-chart

  destination:
    server: https://kubernetes.default.svc
    namespace: my-ns
  syncPolicy:
    automated:
      selfHeal: true
      prune: true
    syncOptions:
      - CreateNamespace=true
      - ApplyOutOfSyncOnly=true
    retry:
      limit: 5
      backoff:
        duration: 5s
        factor: 2
        maxDuration: 3m
```

## 常规写法

```yaml
apiVersion: argoproj.io/v1alpha1  # Argo CD API 版本
kind: Application                 # 自定义资源类型
metadata:                         # 应用程序元数据
  name: my-app                    # 应用程序名称
  namespace: argocd               # Argo CD 所在命名空间
  finalizers:                     # 终结器
    - resources-finalizer.argocd.argoproj.io # 前台级联删除
spec:                             # 规约
  project: default
  source:                         # 仓库源
    repoURL: registry.gitlab.com/jerrybai/my-project # OCI Registry
    targetRevision: "99.99.99-latest" # Chart 版本号
    chart: my-chart                   # Chart 名称
  destination:
    server: https://kubernetes.default.svc # 目标集群 API 地址
    namespace: my-ns                        # 资源所在命名空间
  syncPolicy:         # 同步策略
    automated:        # 自动同步配置
      selfHeal: true  # 自愈
      prune: true     # 修剪
    syncOptions:                   # 同步选项
      - CreateNamespace=true       # 自动创建命名空间
      - ApplyOutOfSyncOnly=true    # 仅同步未同步的资源，而不是所有资源
```

## 字段

> [官方字段规范](https://argo-cd.readthedocs.io/en/stable/user-guide/application-specification/)

[**Go 结构体**](https://pkg.go.dev/github.com/argoproj/argo-cd/v2/pkg/apis/application/v1alpha1)是 Argo CD Application CRD 字段的定义来源，Go 结构直接对应于 YAML 或 JSON 中的字段。

1. **查找字段：** 您可以在页面上找到名为 **`ApplicationSpec`** 的结构体（Struct）。这就是 `application.yaml` 文件中 **`.spec`** 字段对应的全部内容。
2. **字段名称：** 结构体中的每个字段名称（例如 `Source`、`Destination`、`SyncPolicy`）都对应于 YAML 中的键名（例如 `source`、`destination`、`syncPolicy`）。
3. **类型：** 字段旁边的类型（例如 `ApplicationSource`、`Destination`）表明该字段是一个**嵌套结构**。您需要点击这些类型名称，跳转到下一层结构体，才能看到子字段的完整列表。

## `source`

`source` 用于指定 CR 的仓库源。

```yaml
# K8s 清单源
source:
  # Git 仓库地址
  repoURL: https://gitlab.com/jerrybai/my-project.git
  # 版本指针，HEAD 为当前选定分支的最新提交
  targetRevision: HEAD
  # K8s 配置文件在 Git 仓库中的路径
  path: k8s
```

```yaml
# Helm Chart 源
source:
  # <oci-registry>，不需要加 oci:// 前缀
  repoURL: registry.gitlab.com/jerrybai/my-project
  # Chart 版本号
  targetRevision: "99.99.99-latest"
  # Chart 名称
  chart: my-chart
```

## `finalizers`

[`finalizers`](https://argo-cd.readthedocs.io/en/stable/user-guide/app_deletion/#about-the-deletion-finalizer) 终结器，用于级联删除。

```yaml
metadata:
  finalizers:
    - resources-finalizer.argocd.argoproj.io
```

上述代码在执行 `kubectl delete -f my-app.yaml` 时，会执行前台级联删除，即先删除 my-ns 中的业务资源（如 Pod），再删除 argocd 命名空间中的 app。

注意：如果 `my-ns` 中有 Terraform 部署的 SA 资源，应在 Terraform 中给相应资源加注解，否则会误删 `my-ns` 和 SA 资源。

```hcl
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = local.app_ns
    annotations = {
      # 加注解，防止 Argo CD 删除该 Namespace
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
}

resource "kubernetes_service_account_v1" "my_ksa" {
  metadata {
    name      = local.ksa_name
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account"  = google_service_account.workload_identity.email
      # 加注解，防止 Argo CD 删除该 KSA
      "argocd.argoproj.io/sync-options" = "Delete=false"
    }
  }
}
```

# 同步

Argo CD 允许用户自定义目标集群中所需状态的[**同步方式**](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/)。

# 部署应用

有三种方式部署应用：

- Argo CD UI
- Argo CD CLI
- K8s 原生部署

## K8s 原生部署应用

- 准备工作

  - Argo CD 已安装并初始化
  - 源代码开发完成，已将引用的 Image 推送至镜像仓库。

- 说明：此部分的目录和文件源自 [Todo Fullstack](todo-fullstack.md) 项目

- 创建 K8s 和 Argo CD 目录

  ```
  cd d:/projects/my-project
  mkdir k8s argo-cd
  ```

- 在 `k8s` 目录创建以下 K8s 配置文件：

  - `namespace.yaml`：应用的命名空间
  - `mysql.yaml`：数据库
  - `backend.yaml`：后端
  - `frontend.yaml`：前端
  
- 在 `argo-cd` 目录创建 Argo CD 的 CR 配置文件 `my-app.yaml`

  ```yaml
  apiVersion: argoproj.io/v1alpha1
  kind: Application
  metadata:
    name: my-app
    namespace: argocd
    finalizers:
      - resources-finalizer.argocd.argoproj.io
  spec:
    project: default
    source:
      repoURL: https://gitlab.com/jerrybai/my-project.git
      targetRevision: HEAD
      path: k8s
    destination:
      server: https://kubernetes.default.svc
      namespace: my-ns
    syncPolicy:
      automated:
        selfHeal: true
        prune: true
      syncOptions:
        - CreateNamespace=true
        - ApplyOutOfSyncOnly=true
      retry:
        limit: 5
        backoff:
          duration: 5s
          factor: 2
          maxDuration: 3m
  ```

- 推送至 Git 仓库

- 部署应用

  ```bash
  cd d:/projects/my-project/argo-cd
  kubectl apply -f my-app.yaml
  ```

- 在 Argo CD 页面查看应用已启动

## 使用 Terraform 部署应用

**遗留问题**：由于某些权限问题，Argo CD 无法拉取 GAR 中的 chart。

### 准备工作

建立在以下的基础上：

- [通过 Terraform 连接到 GitLab](<gcp-repositories.md#通过 Terraform 连接到 GitLab>)
- [使用 Terraform 创建 Docker Repository](<gcp-artifact-registry.md#使用 Terraform 创建 Docker Repository>)
- 完成 Cloud Build 将 image 和 chart 推送至 GAR
- [使用 Terraform 配置 GKE 集群](<gcp-gke.md#使用 Terraform 创建 GKE 集群>)
- [使用 Terraform 配置 Cloud SQL](<gcp-cloud-sql.md#使用 Terraform 创建 Cloud SQL>)
- [使用 Terraform 配置 Argo CD](<argo-cd.md#使用 Terraform 安装 Argo CD>)

### 创建 `my-app` 模块目录

```bash
DIR=/d/projects/my-project/terraform/my-app && mkdir -p $DIR && cd $DIR
touch my-app.tf variables.tf
```

### `main.tf`

根模块主文件 `terraform/main.tf`

```hcl
# 调用 my-app 模块
module "my-app" {
  source = "./my-app"
  depends_on = [
    module.argocd,
    module.cloud-sql
  ]

  # 传递其它模块的输出
  argocd_ns = module.argocd.argocd_ns
  app_ns    = module.gke.app_ns

  # 传递根模块的变量
  prefix = var.prefix
}
```

### `my-app.tf`

`my-app` 模块主文件 `my-app/my-app.tf`

与 `my-app.yaml` 对比，由于 Terraform 创建了 `my-ns` 命名空间，所以删除 `CreateNamespace=true`。

```hcl
# 使用 kubernetes_manifest 部署 Argo CD Application
resource "kubernetes_manifest" "my_app" {
  manifest = {
    "apiVersion" = "argoproj.io/v1alpha1"
    "kind"       = "Application"
    "metadata" = {
      "name"      = local.app_name
      "namespace" = var.argocd_ns
      "finalizers" = [
        "resources-finalizer.argocd.argoproj.io"
      ]
    }
    "spec" = {
      "project" = "default"
      "source" = {
        "repoURL"        = local.chart_repo_url
        "targetRevision" = "99.99.99-latest"
        "chart"          = local.chart_name
      }
      "destination" = {
        "server"    = "https://kubernetes.default.svc"
        "namespace" = var.app_ns
      }
      "syncPolicy" = {
        "automated" = {
          "selfHeal" = true
          "prune"    = true
        }
        "syncOptions" = [
          "ApplyOutOfSyncOnly=true"
        ]
        "retry" = {
          "limit" = 5
          "backoff" = {
            "duration"    = "5s"
            "factor"      = 2
            "maxDuration" = "3m"
          }
        }
      }
    }
  }
}
```

### `variables.tf`

`my-app` 模块变量文件 `my-app/variables.tf`

```hcl
variable "prefix" {
  type        = string
  description = "Project prefix"
}

locals {
  project_name   = "${var.prefix}-project"
  app_name       = "${var.prefix}-app"
  chart_name     = "${var.prefix}-chart"
  chart_repo_url = "asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/${var.prefix}-docker-repo"
}

variable "argocd_ns" {
  type        = string
  description = "Argo CD Namespace"
}

variable "app_ns" {
  type        = string
  description = "Kubernetes Namespace for the Application"
}
```

### 部署应用

```
│ Error: Failed to construct REST client
│
│   with kubernetes_manifest.my_app,
│   on todo-app.tf line 8, in resource "kubernetes_manifest" "my_app":
│    8: resource "kubernetes_manifest" "my_app" {
│
│ cannot create REST client: no client config
```

如果使用 `terraform apply` 一次性部署（包括 `my-app.tf`），会因为 Argo CD 还未安装导致上述错误，所以暂时分两步部署。

```bash
# 先安装 Argo CD 及其依赖
terraform apply -target=helm_release.argocd

# 再部署 my-app.tf 及其它资源
terraform apply
```

# FAQ

## OutOfSync

- 当使用 ArgoCD 部署好应用以后，一切运行正常，但 UI 页面一直显示 OutOfSync，即使状态不同步，应用程序实际上也是同步的，但看到它不同步很烦人。若要消除此问题，有一种解决方案是使用资源排除。

  ![image-20240329143514361](assets/image-20240329143514361.png)

- [以下方法由博主提供](https://medium.com/@rojenshrestha100/argo-cd-out-of-sync-due-to-cilium-identity-f9d6188aa056)

- 访问 Argo CD 的 configmap

  ```bash
  kubectl get cm -n argocd
  ```

  ![image-20240329143851461](assets/image-20240329143851461.png)

- 使用 nano 编辑器编辑此配置图

  ```bash
  KUBE_EDITOR="nano" kubectl edit cm argocd-cm -n argocd
  ```

- 文末在第一层级添加以下数据并保存

  ```yaml
  data:
    resource.exclusions: |
      - apiGroups:
        - cilium.io
        kinds:
        - CiliumIdentity
        clusters:
        - "*"
  ```

## 使用 Terraform 创建 Argo CD 的受信任仓库

```hcl
resource "kubernetes_secret_v1" "argocd_gcr_repo" {
  metadata {
    name      = "google-artifact-registry"
    namespace = kubernetes_namespace_v1.argocd_ns.metadata[0].name
    labels = {
      "argocd.argoproj.io/secret-type" = "repository"
    }
  }

  data = {
    type      = "helm"
    url       = "asia-east2-docker.pkg.dev/${data.google_project.project.project_id}/my-docker-repo"
    enableOCI = "true"
    name      = "my-docker-repo"
    project   = "default"
  }
}
```

## 在安装 Argo CD 时为 argocd-repo-server SA 添加注解

```hcl
resource "helm_release" "argocd" {
  # ... 其它配置 ...

  set = [
    # 设置 argocd-repo-server 的 GSA 注解，以启用 Workload Identity
    {
      name  = "repoServer.serviceAccount.annotations.iam\\.gke\\.io/gcp-service-account"
      value = google_service_account.workload_identity.email
    },
    
    # ... 其它配置 ...
  ]
}
```

