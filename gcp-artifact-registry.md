---
title: gcp-artifact-registry
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
  - registry
  - cloud-computing
  - gcp
  - artifact-registry
---

# Overview

[**Artifact Registry**](https://console.cloud.google.com/artifacts) 是 GCP 的制品仓库，是一个私有仓库。

> [Artifact Registry Docs](https://docs.cloud.google.com/artifact-registry/docs)
>
> [`gcloud artifacts`](https://docs.cloud.google.com/sdk/gcloud/reference/artifacts): CLI Reference

每个项目有自己的 Artifact Registry，Artifact Registry 中创建各种类型的 Repostory 以存储制品。

```
Project
└── Artifact Registry  # 制品注册表
    └── Repostories    # 具体制品仓库
```

[`<oci-registry>` 格式](<dev-ops.md#OCI 地址格式>)：

```
oci://<docker-repo-region>-docker.pkg.dev/<project-id>/<docker-repo-name>
oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo
```

其中：

- `<docker-repo-region>`：Docker Repository 位置
- `<docker-repo-region>-docker.pkg.dev>`：Docker Repository 主机名
- `<project-id>`：GCP 项目 ID
- `<docker-repo-name>`：Docker Repository 名称

# Quickstart

## 准备工作

- 完成 [GCP 准备工作](gcp.md#准备工作)
- [创建 GCP Project](<gcp-project.md#创建 GCP 项目>)
- [选择项目](https://console.cloud.google.com/projectselector2/home/dashboard)
- 开启 [Artifact Registry API](https://console.cloud.google.com/marketplace/product/google/artifactregistry.googleapis.com)
- 打开 [Artifact Registry](https://console.cloud.google.com/artifacts) 页面
- 以 Docker Repository 为例

## 创建 Docker Repository

点击 `Create repository`
- **Name**：Docker Repository 名称
- **Format**：Docker Repository 类型
- **Region**：Docker Repository 区域

## 为 Docker 配置身份验证

如需为区域 `asia-east2` 中的 Docker 代码库设置身份验证：

```bash
gcloud auth configure-docker asia-east2-docker.pkg.dev
```

该命令将更新 Docker 配置，允许 Docker 向 Artifact Registry 推送 Image。

## 拉取镜像

随意拉取一个 image，以备使用：

```bash
docker pull us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
```

## 标记镜像

```bash
docker tag us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0 \
asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-image:tag1
```

其中：

- `$DOCKER_REPO_REGION`：Docker Repository 位置
- `$DOCKER_REPO_REGION-docker.pkg.dev`：Docker Repository 主机名
- `$PROJECT_ID`：GCP 项目 ID
- `$DOCKER_REPO_NAME`：Docker Repository 名称

## 向 Docker Repository 推送镜像

```bash
docker push asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-image:tag1
```

## 从 Docker Repository 拉取镜像

```bash
docker pull asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-image:tag1
```

## 删除 Docker Repository

```bash
gcloud artifacts repositories delete my-docker-repo --location=asia-east2
```

# 创建 Docker Repository

> [容器概念](https://docs.cloud.google.com/artifact-registry/docs/container-concepts)
>
> [快速入门：在 Artifact Registry 中存储 Docker 容器映像](https://docs.cloud.google.com/artifact-registry/docs/docker/store-docker-container-images)

## 使用 Gcloud Console 创建 Docker Repository

### 准备工作

- [选择项目](https://console.cloud.google.com/projectselector2/home/dashboard)
- 开启 [Artifact Registry API](https://console.cloud.google.com/marketplace/product/google/artifactregistry.googleapis.com)
- 打开 [Artifact Registry](https://console.cloud.google.com/artifacts) 页面

### 创建 Docker Repository

点击 `Create repository`

- **Name**：my-docker-repo
- **Format**：Docker
- **Region**：asia-east2

## 使用 CLI 创建 Docker Repository

### 启用 Artifact Registry API

```bash
gcloud services enable artifactregistry.googleapis.com
```

### 创建 Docker Repository

```bash
gcloud artifacts repositories create $DOCKER_REPO_NAME \
    --repository-format=docker \
    --location=$DOCKER_REPO_REGION \
```

```bash
gcloud artifacts repositories create my-docker-repo \
    --repository-format=docker \
    --location=asia-east2 \
```

### 为 Docker 配置身份验证

如需为区域 `asia-east2` 中的 Docker 代码库设置身份验证：

```bash
gcloud auth configure-docker asia-east2-docker.pkg.dev
```

该命令将更新 Docker 配置，允许 Docker 向 Artifact Registry 推送 Image。

### 拉取镜像

随意拉取一个 image，以备使用：

```bash
docker pull us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
```

### 标记镜像

```bash
docker tag us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0 \
asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-image:tag1
```

其中：

- `$DOCKER_REPO_REGION`：Docker Repository 位置
- `$DOCKER_REPO_REGION-docker.pkg.dev`：Docker Repository 主机名
- `$PROJECT_ID`：GCP 项目 ID
- `$DOCKER_REPO_NAME`：Docker Repository 名称

### 向 Docker Repository 推送镜像

```bash
docker push asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-image:tag1
```

### 从 Docker Repository 拉取镜像

```bash
docker pull asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-image:tag1
```

## 使用 Terraform 创建 Docker Repository

> [GCP：使用 Terraform 预配 Artifact Registry 资源](https://docs.cloud.google.com/artifact-registry/docs/repositories/terraform)
>
> [Terraform：google_artifact_registry_repository](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/artifact_registry_repository)

### 创建 Terraform 目录

```bash
DIR=/d/projects/my-project/terraform && mkdir -p $DIR && cd $DIR
touch main.tf providers.tf variables.tf
```

### 创建 `gar-docker-repo` 模块目录

```bash
DIR=/d/projects/my-project/terraform/gar-docker-repo && mkdir -p $DIR && cd $DIR
touch api.tf gar-docker-repo.tf terraform.tf variables.tf
```

### `main.tf`

根模块主文件 `terraform/main.tf`

```hcl
# 调用 gar-docker-repo 模块
module "gar-docker-repo" {
  source = "./gar-docker-repo"

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

`gar-docker-repo` 模块 API 文件 `gar-docker-repo/api.tf`

```hcl
locals {
  services = [
    "artifactregistry.googleapis.com" # Artifact Registry API
  ]
}

resource "google_project_service" "project_services" {
  for_each           = toset(local.services)
  service            = each.key
  disable_on_destroy = false
}
```

### `gar-docker-repo.tf`

`gar-docker-repo` 模块主文件 `gar-docker-repo/gar-docker-repo.tf`

```hcl
# 创建 Docker 仓库
resource "google_artifact_registry_repository" "docker_repo" {
  repository_id = local.chart_repo
  format        = "DOCKER"
  depends_on    = [google_project_service.project_services]
}
```

### `terraform.tf`

`gar-docker-repo` 模块 provider version 文件 `gar-docker-repo/terraform.tf`

```
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 7.14.0"
    }
  }
}
```

### `variables.tf`

`gar-docker-repo` 模块变量文件 `gar-docker-repo/variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
}

locals {
  chart_repo = "${var.prefix}-docker-repo"
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

### 创建 Docker Repository

```bash
cd d:/projects/my-project/terraform
terraform apply
```

# Helm

> [快速入门：在 Artifact Registry 中存储 Helm 图表](https://docs.cloud.google.com/artifact-registry/docs/helm/store-helm-charts)

## 启用 Artifact Registry API

```bash
gcloud services enable artifactregistry.googleapis.com
```

## 创建 Docker Repository

Artifact Registry 使用 Docker Repository 存储 Helm Chart，同属 OCI 标准。

```bash
gcloud artifacts repositories create $DOCKER_REPO_NAME \
    --repository-format=docker \
    --location=$DOCKER_REPO_REGION \
```

```bash
gcloud artifacts repositories create my-docker-repo \
    --repository-format=docker \
    --location=asia-east2 \
```

## 为 Helm 配置身份验证

如果 Docker 已经配置身份验证，则 Helm 可以使用 Docker 的身份验证向 Artifact Registry 推送 Chart。

否则，可以按以下方式为 Helm 获取身份验证。

```bash
gcloud auth print-access-token | helm registry login -u oauth2accesstoken \
    --password-stdin $DOCKER_REPO_REGION-docker.pkg.dev
```

```bash
gcloud auth print-access-token | helm registry login -u oauth2accesstoken \
    --password-stdin asia-east2-docker.pkg.dev
```

- 官方文档未更新，应去掉 `https://`。
- `$DOCKER_REPO_REGION`：Docker Repository 位置

## 创建 Chart

```bash
# 创建
cd /d/projects/my-project
helm create my-chart

# 封装
helm package my-chart
```

## 推送 Chart

```bash
helm push my-chart-0.1.0.tgz oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo
```

## 部署 Release

```bash
helm install my-chart \
    oci://asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/my-docker-repo/my-chart \
    --version 0.1.0

# 卸载 Release
helm uninstall my-chart
```

## 删除 Docker Repository

```bash
gcloud artifacts repositories delete my-docker-repo --location=asia-east2
```

