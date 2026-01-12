---
title: gcp-repositories
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
  - cloud-computing
  - gcp
  - repo
  - gcp-repositories
---

# Overview

[**Repositories**](https://console.cloud.google.com/cloud-build/repositories) 用于链接到其它源代码仓库（如 GitLab）。

> [Repositories Docs](https://docs.cloud.google.com/build/docs/repositories)

链接到源代码仓库的两种方式：

- [Developer Connect](https://docs.cloud.google.com/build/docs/repositories?hl=zh-cn#dc-repo)
- [Cloud Build repositories (2nd gen)](https://docs.cloud.google.com/build/docs/repositories?hl=zh-cn#2nd-gen-repos)（推荐）

[Cloud Build repositories (2nd gen)](https://docs.cloud.google.com/build/docs/repositories#2nd-gen-repos) 是 Google Cloud Build 推荐的源代码仓库连接方式。

如无特殊说明，此笔记默认使用 Cloud Build repositories (2nd gen) 进行链接。

# GitLab

## 使用 Gcloud Console 连接到 GitLab

分三步连接到 GitLab：

1. [连接到 GitLab 主机](#连接到 GitLab 主机)
2. [链接到 GitLab Repository](#链接到 GitLab Repository)
3. [创建触发器](#创建触发器)

### 连接到 GitLab Host

> [Connect to a GitLab host](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/connect-host-gitlab)

- [启用相关 APIs](https://console.cloud.google.com/apis/enableflow;apiid=cloudbuild.googleapis.com,secretmanager.googleapis.com;redirect=https:%2F%2Fcloud.google.com%2Fbuild%2Fdocs%2Fautomating-builds%2Fgitlab%2Fconnect-host-gitlab)

  - Cloud Build API
  - Secret Manager API

- 创建两个 GitLab [Personal Access Tokens](https://gitlab.com/-/user_settings/personal_access_tokens)

  - 具有 `api` 范围的访问令牌，用于与代码库建立连接和断开连接。
  - 具有 `read_api` 范围的访问令牌，Cloud Build 触发器使用此令牌访问代码库中的源代码。

- 打开 [Repositories](https://console.cloud.google.com/cloud-build/repositories/2nd-gen) 页面

- 在顶部栏的项目选择器中，选择您的 Google Cloud 项目。

- 选择 `2nd gen` 标签页。

- `Create host connection` > `GitLab`

  - **Region**：`my-region`
  - **Name**：`my-gitlab-host`
  - **Host details**：`GitLab.com`
  - **Personal access tokens**：分别对应填写此前创建的两个令牌

- 点击 `Connect`

  点击 `Connect` 按钮后，您的个人访问令牌会安全地存储在 [Secret Manager](https://docs.cloud.google.com/secret-manager/docs/overview) 中。建立主机连接后，Cloud Build 还会代表您创建网络钩子密钥。您可以在 [Secret Manager 页面](https://console.cloud.google.com/security/secret-manager)上查看和管理 Secret。

- [轮换旧的或过期的 GitLab 访问令牌](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/connect-host-gitlab?hl=zh-cn#rotate-token)

### 链接到 GitLab Repository

> [Connect to a GitLab Repository](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/connect-repo-gitlab)

- [启用相关 APIs](https://console.cloud.google.com/apis/enableflow;apiid=cloudbuild.googleapis.com,secretmanager.googleapis.com;redirect=https:%2F%2Fcloud.google.com%2Fbuild%2Fdocs%2Fautomating-builds%2Fgitlab%2Fconnect-host-gitlab)
  - Cloud Build API
  - Secret Manager API
- 打开 [Repositories](https://console.cloud.google.com/cloud-build/repositories/2nd-gen) 页面
- 在顶部栏的项目选择器中，选择您的 Google Cloud 项目。
- 选择 `2nd gen` 标签页。
- 点击 `Link repository`
  - **Connection**：连接的 GitLab host
  - **Repositories**：GitLab 的代码仓库
  - **Repositories name**：可选择 `Generated` 自动生成
- 点击 `Link`，将代码库与连接相关联。

### 创建 Trigger

> [Build Repositories from GitLab](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/build-repos-from-gitlab)

- [启用相关 APIs](https://console.cloud.google.com/apis/enableflow;apiid=cloudbuild.googleapis.com,secretmanager.googleapis.com;redirect=https:%2F%2Fcloud.google.com%2Fbuild%2Fdocs%2Fautomating-builds%2Fgitlab%2Fconnect-host-gitlab)
  - Cloud Build API
  - Secret Manager API
- 打开 [Triggers](https://console.cloud.google.com/cloud-build/triggers) 页面
- 在顶部栏的项目选择器中，选择您的 Google Cloud 项目。
- 点击 `Create trigger`
  - **Name**：`my-trigger`
  - **Region**：`my-region`（**注意**：代码库的区域必须与触发器的区域一致。）
  - **Event**：触发事件，选 `Push to a branch`。
  - **Source**
    - **Repository service**：`Cloud Build respotories`
    - **Repository generation**：`2nd gen`
    - **Repository**：选择[链接到 GitLab Repository](<#链接到 GitLab Repository>) 中链接的仓库
    - **Branch**： 监控的分支名称（通常是 `^main$`，支持正则）。
  - **Configuration**
    - **Type**：`Cloud Build configuration file (yaml/json)`
    - **Service account**：选择当前项目的适当 GSA

## 使用 Terraform 连接到 GitLab

### 创建 Terraform 目录

```bash
DIR=/d/projects/my-project/terraform && mkdir -p $DIR && cd $DIR
touch main.tf providers.tf terraform.tfvars terraform.tfvars.example variables.tf
```

### 创建 `gitlab-repo` 模块目录

```bash
DIR=/d/projects/my-project/terraform/gitlab-repo && mkdir -p $DIR && cd $DIR
touch api.tf iam.tf gitlab-repo.tf terraform.tf variables.tf
```

### `main.tf`

根模块主文件 `terraform/main.tf`

```hcl
# 调用 gitlab-repo 模块
module "gitlab-repo" {
  source = "./gitlab-repo"

  # 传递根模块的变量
  prefix                                = var.prefix
  project_id                            = var.project_id
  region                                = var.region
  gitlab_personal_access_token_api      = var.gitlab_personal_access_token_api
  gitlab_personal_access_token_read_api = var.gitlab_personal_access_token_read_api
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

### `terraform.tfvars`

根模块敏感变量赋值文件 `terraform/terraform.tfvars`

```hcl
# GitLab repo token
gitlab_personal_access_token_api      = "gitlab_personal_access_token_api"
gitlab_personal_access_token_read_api = "gitlab_personal_access_token_read_api"
```

### `terraform.tfvars.example`

根模块敏感变量赋值文件 `terraform/terraform.tfvars`

```hcl
# GitLab repo token
gitlab_personal_access_token_api      = ""
gitlab_personal_access_token_read_api = ""
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

variable "zone" {
  type        = string
  description = "GCP Zone"
  default     = "asia-east2-a"
}

# --- GitLab repo token ---
variable "gitlab_personal_access_token_api" {
  type        = string
  description = "GitLab Personal Access Token for API"
  sensitive   = true
}

variable "gitlab_personal_access_token_read_api" {
  type        = string
  description = "GitLab Personal Access Token for Read"
  sensitive   = true
}
```

### `.gitignore`

Git 忽略文件 `my-project/.gitignore` 中添加[忽略内容](terraform-configuration-language.md#`.gitignore`)

### `api.tf`

`gitlab-repo` 模块 API 文件 `gitlab-repo/api.tf`

```hcl
locals {
  services = [
    "cloudbuild.googleapis.com",    # Cloud Build API
    "secretmanager.googleapis.com", # Secret Manager API
  ]
}

resource "google_project_service" "project_services" {
  for_each           = toset(local.services)
  service            = each.key
  disable_on_destroy = false
}
```

### `gitlab-repo.tf`

`gitlab-repo` 模块主文件 `gitlab-repo/gitlab-repo.tf`

需先创建 GitLab Personal Tokens

```hcl
# 1. 存储 Token 到 Secret Manager

# 创建存储 API Token 的 Secret
resource "google_secret_manager_secret" "gitlab_api_token" {
  secret_id = "${var.code_repo}-api-token"
  replication {
    auto {}
  }
}

# 存入具体的 API Token 值
resource "google_secret_manager_secret_version" "api_token_version" {
  secret      = google_secret_manager_secret.gitlab_api_token.id
  secret_data = var.gitlab_personal_access_token_api
}

# 创建存储 Read API Token 的 Secret
resource "google_secret_manager_secret" "gitlab_read_api_token" {
  secret_id = "${var.code_repo}-read-api-token"
  replication {
    auto {}
  }
}

# 存入具体的 Read API Token 值
resource "google_secret_manager_secret_version" "read_api_token_version" {
  secret      = google_secret_manager_secret.gitlab_read_api_token.id
  secret_data = var.gitlab_personal_access_token_read_api
}

# 随机生成一个 Webhook 密钥
resource "random_password" "webhook_secret_value" {
  length  = 16
  special = false
}

# 创建 Secret Manager 容器
resource "google_secret_manager_secret" "webhook_secret" {
  secret_id = "gitlab-webhook-secret"
  replication {
    auto {}
  }
}

# 存入随机生成的密钥值
resource "google_secret_manager_secret_version" "webhook_secret_version" {
  secret      = google_secret_manager_secret.webhook_secret.id
  secret_data = random_password.webhook_secret_value.result
}

# 2. 连接到 GitLab 主机 (2nd Gen)
resource "google_cloudbuildv2_connection" "my_gitlab_connection" {
  location = var.region
  name     = local.code_repo_host

  gitlab_config {
    # 引用 Secret Manager 中的令牌
    authorizer_credential {
      user_token_secret_version = google_secret_manager_secret_version.api_token_version.id
    }
    read_authorizer_credential {
      user_token_secret_version = google_secret_manager_secret_version.read_api_token_version.id
    }
    webhook_secret_secret_version = google_secret_manager_secret_version.webhook_secret_version.id
  }
}

# 3. 链接具体的代码仓库
resource "google_cloudbuildv2_repository" "my_repo" {
  name              = "${var.repo_username}-${local.project_name}"
  location          = google_cloudbuildv2_connection.my_gitlab_connection.location
  parent_connection = google_cloudbuildv2_connection.my_gitlab_connection.id
  remote_uri        = "https://gitlab.com/${var.repo_username}/${local.project_name}.git"
}

# 4. 为 GitLab 仓库创建 Cloud Build 触发器
resource "google_cloudbuild_trigger" "gitlab_trigger" {
  name            = local.trigger_name
  location        = google_cloudbuildv2_repository.my_repo.location
  service_account = google_service_account.cloudbuild_worker.id

  # 使用第 2 代连接 (v2 repository)
  repository_event_config {
    repository = google_cloudbuildv2_repository.my_repo.id
    push {
      branch = "^main$"
    }
  }

  # 指定构建配置
  filename = "cloudbuild.yaml"

  included_files = [
    "backend/**",
    "frontend/**",
    "helm-chart/**"
  ]

  depends_on = [
    google_cloudbuildv2_repository.my_repo,
    google_secret_manager_secret_iam_member.cloudbuild_secret_accessor,
    google_project_iam_member.cloudbuild_worker_roles,
    google_service_account_iam_member.cloudbuild_worker_binding
  ]
}

```

### `iam.tf`

`gitlab-repo` 模块 IAM 文件 `gitlab-repo/iam.tf`

```hcl
# 创建 Cloud Build 的 GSA
resource "google_service_account" "cloudbuild_worker" {
  account_id   = "${var.prefix}-cloudbuild-worker"
  display_name = "Cloud Build Worker Service Account"
}

# 为 GSA 分配角色
resource "google_project_iam_member" "cloudbuild_worker_roles" {
  for_each = toset([
    "roles/logging.logWriter",       # Logs Writer
    "roles/artifactregistry.writer", # Artifact Registry Writer
    "roles/artifactregistry.reader"  # Artifact Registry Reader
  ])

  project = var.project_id
  role    = each.key
  member  = "serviceAccount:${google_service_account.cloudbuild_worker.email}"
}

# 获取当前 Project ID
data "google_project" "project" {}

# 允许 Cloud Build 服务代理访问 Secret Manager 中的 Secrets
resource "google_secret_manager_secret_iam_member" "cloudbuild_secret_accessor" {
  for_each = {
    api     = google_secret_manager_secret.gitlab_api_token.id
    read    = google_secret_manager_secret.gitlab_read_api_token.id
    webhook = google_secret_manager_secret.webhook_secret.id
  }
  secret_id = each.value
  role      = "roles/secretmanager.secretAccessor"
  # 必须使用 Cloud Build 的 Service Agent 账号
  member = "serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloudbuild.iam.gserviceaccount.com"
}

# 允许 Cloud Build 服务代理以 GSA 身份运行
# 否则 Cloud Build 服务代理无法代表 GSA 执行构建任务
resource "google_service_account_iam_member" "cloudbuild_worker_binding" {
  service_account_id = google_service_account.cloudbuild_worker.name
  role               = "roles/iam.serviceAccountUser"
  member             = "serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloudbuild.iam.gserviceaccount.com"
}
```

### `terraform.tf`

`gitlab-repo` 模块 provider version 文件 `gitlab-repo/terraform.tf`

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

### `variables.tf`

`gitlab-repo` 模块变量文件 `gitlab-repo/variables.tf`

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
}

locals {
  code_repo_host = "${var.prefix}-${var.code_repo}-host"
  project_name   = "${var.prefix}-project"
  trigger_name   = "${var.prefix}-trigger"
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

# --- Repo ---
variable "code_repo" {
  type        = string
  description = "Code repo"
  default     = "gitlab"
}

variable "repo_username" {
  type        = string
  description = "Repo username"
  default     = "jerrybai"
}

# --- GitLab repo token ---
variable "gitlab_personal_access_token_api" {
  type        = string
  description = "GitLab Personal Access Token for API"
  sensitive   = true
}

variable "gitlab_personal_access_token_read_api" {
  type        = string
  description = "GitLab Personal Access Token for Read"
  sensitive   = true
}
```

### 初始化 Terraform

```bash
cd d:/projects/my-project/terraform
terraform init
```

### 创建资源

```bash
cd d:/projects/my-project/terraform
terraform apply
```
