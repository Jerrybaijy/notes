---
title: gcp-gke
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud-computing
  - gcp
  - gke
---

# Overview

[**GKE**](https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview?hl=zh-cn) (Google Kubernetes Engine)，是由 Google 开发的代管式 Kubernetes 服务，可以使用 Google 的基础架构大规模部署和运营容器化应用。

# Quick Start

## 准备工作

- [GCP 准备工作](<gcp.md#准备工作>)已完成
- [本地 kubectl](<kubernetes.md#kubectl>) 已安装
- [GCP project](<gcp-project.md#Quick Start>) 已创建

## 创建 GKE

```bash
# 创建标准集群
gcloud container clusters create $CLUSTER_NAME --region=$REGION
# e.g.
gcloud container clusters create my-cluster \
    --region=asia-east2 \
    --node-locations=asia-east2-a \
    --num-nodes=2 \
    --machine-type=e2-medium \
    --disk-size=40 \
    --disk-type=pd-standard \
    --enable-autoscaling \
    --min-nodes=1 \
    --max-nodes=5 \
    --scopes=cloud-platform
# 查看集群
gcloud container clusters list
```

## 安装 `gke-gcloud-auth-plugin` 插件

否则无法使用 `kubectl` 命令管理集群

```bash
# 安装
gcloud components install gke-gcloud-auth-plugin
# 验证
gke-gcloud-auth-plugin --version
```

## 更新 `kubectl` 配置

用以使用 `gke-gcloud-auth-plugin` 插件交互集群

```bash
gcloud container clusters get-credentials $CLUSTER_NAME \
    --location=$CONTROL_PLANE_LOCATION

# 更新配置
gcloud container clusters get-credentials my-cluster \
    --location asia-east2 \
    --project project-60addf72-be9c-4c26-8db
```

## 交互 GKE

[将 kubectl cnotext 切换至 GKE](<kubernetes.md#`kubectl config`>)

```bash
# 显示当前上下文
kubectl config current-context

# 显示所有上下文
kubectl config get-contexts

# 设置当前上下文
kubectl config use-context $CONTEXT_NAME

# 验证配置
kubectl get ns
```

## 删除 GKE

```bash
gcloud container clusters delete $CLUSTER_NAME --region=$REGION
gcloud container clusters delete my-cluster --region=asia-east2
```

# 创建 GKE 集群

## 使用 `gcloud projects create` 创建 GKE 集群

- [准备工作](<#准备工作>)已完成

- 开启 GKE 必需 API

  ```bash
  gcloud services enable compute.googleapis.com container.googleapis.com \
      --project $PROJECT_ID
  
  gcloud services enable compute.googleapis.com container.googleapis.com \
      --project project-60addf72-be9c-4c26-8db
  ```

- 创建集群

  ```bash
  gcloud container clusters create my-cluster \
      --region=asia-east2 \
      --node-locations=asia-east2-a \
      --num-nodes=2 \
      --machine-type=e2-medium \
      --disk-size=40 \
      --disk-type=pd-standard \
      --enable-autoscaling \
      --min-nodes=1 \
      --max-nodes=5 \
      --scopes=cloud-platform
  # 查看集群
  gcloud container clusters list
  ```

## 使用 Terraform 创建 GKE 集群

### 准备工作

- [Terraform 安装](<terraform-cli.md#Install>)已完成
- GCP 项目已创建并关联结算账号
- [安装和配置 Google Cloud CLI](<gcp.md#Install>)
- [Kubectl 已安装并完成配置](<gcp-gke.md#Quick Start>)

### 创建 Terraform 目录

```bash
DIR=/d/projects/my-project/terraform && mkdir -p $DIR && cd $DIR
touch main.tf providers.tf variables.tf
```

### 创建 `gke` 模块目录

```bash
DIR=/d/projects/my-project/terraform/gke && mkdir -p $DIR && cd $DIR
touch api.tf iam.tf gke.tf outputs.tf terraform.tf variables.tf
```

### `main.tf`

根模块主文件 `terraform/main.tf`

```hcl
# 调用 gke 模块
module "gke" {
  source = "./gke"

  # 传递根模块的变量
  prefix     = var.prefix
  project_id = var.project_id
  region     = var.region
}
```

### `providers.tf`

根模块 provider 文件 `terraform/providers.tf`

```hcl
provider "google" {
  project = var.project_id
  region  = var.region
}

# 定义 GKE 客户端配置数据源（使根模块可直接访问）
data "google_client_config" "default" {}

provider "kubernetes" {
  host                   = "https://${module.gke.cluster_endpoint}"
  token                  = data.google_client_config.default.access_token
  cluster_ca_certificate = base64decode(module.gke.cluster_ca_certificate)
}
```

### `variables.tf`

根模块变量文件 `terraform/variables.tf`

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
```

### `.gitignore`

Git 忽略文件 `my-project/.gitignore` 中添加[忽略内容](terraform-configuration-language.md#`.gitignore`)

### `api.tf`

`gke` 模块 API 文件 `gke/api.tf`

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

### `gke.tf`

`gke` 模块主文件 `gke/gke.tf`

```hcl
# 创建 GKE 集群
resource "google_container_cluster" "my_cluster" {
  name                     = local.gke_name
  location                 = var.region
  remove_default_node_pool = true
  initial_node_count       = 1
  depends_on               = [google_project_service.project_services]

  # 启用 Workload Identity
  workload_identity_config {
    workload_pool = "${data.google_project.project.project_id}.svc.id.goog"
  }

  # 关闭误删保护（生产环境不应设置此参数）
  deletion_protection = false
}

# 创建 Node Pool
resource "google_container_node_pool" "my_node_pool" {
  name       = local.node_pool_name
  location   = var.region
  cluster    = google_container_cluster.my_cluster.name
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

### `iam.tf`

`gke` 模块 IAM 文件 `gke/iam.tf`

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
    "roles/cloudsql.client", # Cloud SQL Client
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

### `outputs.tf`

`gke` 模块输出文件 `gke/outputs.tf`

以下三个 `output ` block 用于根模块 `kubernetes` provider 调用，不可省略：

- cluster_endpoint
- cluster_endpoint
- workload_identity_gsa_email

```hcl
output "cluster_endpoint" {
  value = google_container_cluster.my_cluster.endpoint
}

output "cluster_ca_certificate" {
  value = google_container_cluster.my_cluster.master_auth[0].cluster_ca_certificate
}

# 用于传递给 argocd 模块
output "workload_identity_gsa_email" {
  description = "Workload Identity GSA email"
  value       = google_service_account.workload_identity.email
  sensitive   = false
}

# 用于传递给 argocd 模块
output "app_ns" {
  description = "Kubernetes Namespace Name"
  value       = kubernetes_namespace_v1.app_ns.metadata[0].name
}

output "ksa_name" {
  description = "Kubernetes Service Account Name"
  value       = kubernetes_service_account_v1.my_ksa.metadata[0].name
}

output "gke_name" {
  description = "GKE name"
  value       = google_container_cluster.my_cluster.name
}
```

### `terraform.tf`

`gke` 模块 provider version 文件 `gke/terraform.tf`

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 7.14.0"
    }
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = "~> 3.0.0"
    }
  }
}
```

### `variables.tf`

`gke` 模块变量文件 `gke/variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
}

locals {
  gke_name          = "${var.prefix}-cluster"
  node_pool_name    = "${var.prefix}-node-pool"
  app_ns            = "${var.prefix}-ns"
  workload_identity = "${var.prefix}-workload-identity"
  ksa_name          = "${var.prefix}-ksa"
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
```

### 初始化 Terraform

```bash
cd d:/projects/my-project/terraform
terraform init
```

### 创建 GKE

```bash
cd d:/projects/my-project/terraform
terraform apply
```

### 更新 kubectl 配置

```bash
gcloud container clusters get-credentials my-cluster \
    --location asia-east2 \
    --project project-60addf72-be9c-4c26-8db
```

```bash
# 查看当前上下文
kubectl config current-context

# 切换上下文
kubectl config use-context gke_project-60addf72-be9c-4c26-8db_asia-east2_my-cluster
```

# GKE Reference

> [GKE Reference](https://docs.cloud.google.com/sdk/gcloud/reference/container/clusters)

```bash
# 创建标准集群
gcloud container clusters create $CLUSTER_NAME [Flags]
# e.g.
gcloud container clusters create my-cluster \
    --region=asia-east2 \
    --node-locations=asia-east2-a \
    --num-nodes=2 \
    --machine-type=e2-medium \
    --disk-size=40 \
    --disk-type=pd-standard \
    --enable-autoscaling \
    --min-nodes=1 \
    --max-nodes=5 \
    --scopes=cloud-platform
# 列出所有集群
gcloud container clusters list
# 删除集群
gcloud container clusters delete $CLUSTER_NAME [Flags]
# 停止集群
gcloud container clusters resize $CLUSTER_NAME [Flags]
```



# 手动部署

- 来源：[部署容器化应用](https://cloud.google.com/kubernetes-engine/docs/deploy-app-cluster)

- 这是一个 GKE 练习，将一个简单的容器化 Web Server 部署到 GKE 集群，并可以在互联网访问。

- 此练习没有使用 Yaml 文件部署

- **准备**

  - Google Cloud CLI 环境搭建完成，详见 《Google Cloud》

  - 在 Google Cloud 中启用 API

  - 设置默认项目

    ```bash
    gcloud config set project opportune-study-413101
    ```

- **创建集群**

  - 创建集群

    ```bash
    gcloud container clusters create-auto jerry-cluster --region=asia-east2
    ```

  - 获取用于集群的身份验证凭据

    ```bash
    gcloud container clusters get-credentials jerry-cluster --region asia-east2
    ```

- **部署应用**

  - 手动部署应用

    ```bash
    kubectl create deployment hello-server --image=us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
    ```

  - 可替换为自己创建的镜像

- **公开端口**

  ```bash
  kubectl expose deployment hello-server --type LoadBalancer --port 80 --target-port 8080
  ```

- **获取外部 IP**

  ```bash
  kubectl get service hello-server
  ```

- **访问应用**

  ```bash
  curl http://EXTERNAL-IP
  ```

- **清理**

  - 删除 Service

    ```bash
    kubectl delete service hello-server
    ```

  - 删除集群

    ```bash
    gcloud container clusters delete hello-cluster --region us-central1
    ```

# Yaml 部署

- 来源：[部署特定语言应用](https://cloud.google.com/kubernetes-engine/docs/quickstarts/deploy-app-container-image?hl=zh-cn#go)
- 这是一个 GKE 练习，将一个简单的容器化 Web Server 部署到 GKE 集群，并可以在互联网访问
- 此练习使用 Yaml 文件部署

### 准备

- Google Cloud CLI 已安装

- 在 Google Cloud 中启用 API

- 设置默认项目

  ```bash
  gcloud config set project opportune-study-413101
  ```

- 安装 Go 语言环境

  ```bash
  sudo apt-get install golang
  go version
  ```

### 编写应用

- 如果使用自己的镜像，可以跳过此步。

- 创建工作目录 `helloworld-gke` 并进入

- 创建名为 `example.com/helloworld` 的新模块

  ```bash
  go mod init example.com/helloworld
  ```

- 创建名为 `helloworld.go` 的新文件

  ```go
  package main
  
  import (
          "fmt"
          "log"
          "net/http"
          "os"
  )
  
  func main() {
          http.HandleFunc("/", handler)
  
          port := os.Getenv("PORT")
          if port == "" {
                  port = "8080"
          }
  
          log.Printf("Listening on localhost:%s", port)
          log.Fatal(http.ListenAndServe(fmt.Sprintf(":%s", port), nil))
  }
  
  func handler(w http.ResponseWriter, r *http.Request) {
          log.Print("Hello world received a request.")
          target := os.Getenv("TARGET")
          if target == "" {
                  target = "World"
          }
          fmt.Fprintf(w, "Hello %s!\n", target)
  }
  ```

### 创建镜像

- 如果使用自己的镜像，可以跳过此步

- 创建 Dockerfile

  ```dockerfile
  FROM golang:1.21.0 as builder
  WORKDIR /app
  RUN go mod init quickstart-go
  COPY *.go ./
  RUN CGO_ENABLED=0 GOOS=linux go build -o /quickstart-go
  
  # 使用 Docker 多阶段构建来创建精简的生产镜像
  # https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
  # 原文件不是这个image，导致容器无法启动
  FROM debian
  WORKDIR /
  COPY --from=builder /quickstart-go /quickstart-go
  
  # 原文件没有这句，导致找不到nonroot用户，容器无法启动
  RUN groupadd -r nonroot && useradd -r -g nonroot nonroot
  
  USER nonroot:nonroot
  ENTRYPOINT ["/quickstart-go"]
  ```

- 获取 Google Cloud 项目 ID

  ```bash
  gcloud config get-value project
  ```

- 在集群所在的位置创建名为 `hello-repo` 的仓库

  ```bash
  gcloud artifacts repositories create hello-repo --project=opportune-study-413101 --repository-format=docker --region=us-central1 --description="Docker repository"
  ```

- 创建镜像

  ```bash
  gcloud builds submit --tag us-central1-docker.pkg.dev/opportune-study-413101/hello-repo/helloworld-gke .
  ```

### 创建集群

- 创建集群

  ```sh
  gcloud container clusters create-auto helloworld-gke --region us-central1
  ```

- 验证有权访问该集群

  ```
  kubectl get nodes
  ```

### 创建 Deployment

- 创建 `deployment.yaml` 文件

  `$GCLOUD_PROJECT` 是您的 Google Cloud 项目 ID，$LOCATION 是代码库位置，例如 us-central1

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: helloworld-gke
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: hello
    template:
      metadata:
        labels:
          app: hello
      spec:
        containers:
          - name: hello-app
            # Replace $LOCATION with your Artifact Registry location (e.g., us-west1).
            # Replace $GCLOUD_PROJECT with your project ID.
            image: $LOCATION-docker.pkg.dev/$GCLOUD_PROJECT/hello-repo/helloworld-gke:latest
            # This app listens on port 8080 for web traffic by default.
            ports:
              - containerPort: 8080
            env:
              - name: PORT
                value: "8080"
            resources:
              requests:
                memory: "1Gi"
                cpu: "500m"
                ephemeral-storage: "1Gi"
              limits:
                memory: "1Gi"
                cpu: "500m"
                ephemeral-storage: "1Gi"
  ```

- 部署应用

  ```bash
  kubectl apply -f deployment.yaml
  ```

- 查看应用

  如果所有 `AVAILABLE` 部署都为 `READY`，则表示 Deployment 已完成。否则再次运行 `kubectl apply -f deployment.yaml`，更新 Deployment 以纳入任何更改

  ```bash
  kubectl get deployments
  ```

- 查看 Pod

  ```bash
  kubectl get pods
  ```

### 创建 Service

- 创建 `service.yaml` 文件

  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: hello
  spec:
    type: LoadBalancer
    selector:
      app: hello
    ports:
      - port: 80
        targetPort: 8080
  ```

- 部署 Service

  ```sh
  kubectl apply -f service.yaml
  ```

### 访问应用

- 获取外部 IP

  输出结果的 `EXTERNAL-IP` 列中，复制 Service 的外部 IP 地址

  ```bash
  kubectl get service
  ```

- 访问应用

  ```bash
  http://EXTERNAL-IP
  ```

### 清理

- Delete service

  ```bash
  kubectl delete service hello
  ```

- Delete cluster

  ```bash
  gcloud container clusters delete helloworld-gke --region us-central1
  ```

- Delete repo

  ```bash
  gcloud artifacts repositories delete hello-repo --region=us-central1 --project=opportune-study-413101
  ```
