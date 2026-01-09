---
title: terraform-configuration-language
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - iac
  - terraform
  - code-language
  - hcl
---

# Overview

[**Configuration Language**](https://developer.hashicorp.com/terraform/language) 是 Terraform 的配置语言，它基于 [HCL](hcl.md)，适用于 [Terraform CLI](https://developer.hashicorp.com/terraform/cli)、 [HCP Terraform](https://cloud.hashicorp.com/products/terraform) 和 [Terraform Enterprise](https://developer.hashicorp.com/terraform/enterprise)，主要目的是**声明资源**，这些资源代表基础设施对象。

> [Configuration Language Docs](https://developer.hashicorp.com/terraform/language)：适用于 Terraform 的 HCL 语言
>
> [Write Terraform Configuration](https://developer.hashicorp.com/terraform/tutorials/configuration-language)
>
> [Terraform provider for Google Cloud](https://registry.terraform.io/providers/hashicorp/google/latest/docs)

Terraform 语言的语法仅由几个基本元素组成：

```hcl
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}

resource "aws_vpc" "main" {
  cidr_block = var.base_cidr_block
}
```

- `Block`：是其他内容的容器。
- `Argument`：用于为名称赋值。它们出现在 block 中。
- Block 的顺序通常并不重要；Terraform 在确定操作顺序时，只考虑资源之间的隐式和显式关系。

# Code Style

> [Code Style](https://developer.hashicorp.com/terraform/language/style)

# Syntax

> [Syntax](https://developer.hashicorp.com/terraform/language/syntax)

# Files and Configuration Structure

> [Files and Configuration Structure](https://developer.hashicorp.com/terraform/language/files)

## `.terraform`

这是一个**本地缓存目录**，它是 Terraform 运行的“工作间”。

- 会在执行 `terraform init` 后自动生成。
- **存放 Provider 插件**：Terraform 会根据你在 `providers.tf` 中定义的 `google` provider，从官方仓库下载对应的二进制驱动文件并存放在这里 。
- **存放 Module**：如果你在代码中引用了外部模块，它们也会被下载到这里。
- **注意**：这个文件夹通常很大，**绝对不要**将其提交到 Git 仓库。你应该在 `.gitignore` 文件中忽略它。

## `.terraform.lock.hcl`

[**依赖锁定文件**](https://developer.hashicorp.com/terraform/language/files/dependency-lock)（Dependency Lock File），类似于 Node.js 的 `package-lock.json` 或 Python 的 `poetry.lock`。

- 会在执行 `terraform init` 后自动生成。
- **版本锁定**：它记录了你当前使用的 Provider 插件的具体版本号和校验和（Hashes） 。
- **团队一致性**：如果你把这个文件提交到 Git，团队中的其他成员在执行 `terraform init` 时，Terraform 会确保下载完全相同版本的插件，避免因为 Provider 版本升级导致的基础设施变更不一致。
- **建议**：行业最佳实践是**将其提交到 Git**。

## `terraform.tfstate`

这是**状态文件**，是 Terraform 的“记忆库”。

- **原理**：它记录了云端资源的真实状态。
- **消失/变化的原因**：如果你是第一次运行且没有实际创建资源，它可能只是一个临时占位符。正常情况下，执行完 `terraform apply` 后，它会变成一个持久化的文件。
- **注意**：这个文件包含敏感信息，**不要**提交到公共代码仓库。

## `terraform.tfstate.backup`

这是**状态备份文件**，每当执行一次会改变状态的操作（如 `terraform apply` 或 `terraform destroy`）时，Terraform 会遵循以下流程：

1. **读取**当前的 `terraform.tfstate` 文件。
2. **备份**：将这个旧的状态保存为 `terraform.tfstate.backup`。
3. **更新**：将云端最新的真实状态和变更结果写入新的 `terraform.tfstate` 。

如果这次 `apply` 过程中发生了严重错误（比如网络中断导致状态文件损坏），可以通过这个备份文件恢复到上一个稳定的状态。

状态备份文件包含敏感信息，不要提交到 Git。

## `.terraform.tfstate.lock.info`

这是**状态锁文件**，作用是**防止多人同时修改**同一套资源。

- **原理**：当你运行 `terraform plan` 或 `apply` 时，Terraform 会创建一个“锁”。如果此时你的同事也尝试运行命令，Terraform 会报错并阻止他，直到你运行结束。
- **消失的原因**：一旦命令执行完毕（无论成功或失败），锁就会被自动释放，文件随之删除。
- 如果命令意外崩溃导致这个文件没有消失，下次运行会报错。这时通常使用 `terraform force-unlock` 命令，而不是手动删除文件。
- **注意**：这个文件**不要**提交到公共代码仓库。

## `$PLAN_NAME.tfplan`

这个**锁定计划文件**是在执行 `terraform plan -out=$PLAN_NAME.tfplan` 后自动生成，锁定了当前的代码逻辑和云端状态。

稍后可以执行 `terraform apply "todo-infra.tfplan"` 命令以执行锁定计划。

## `terraform.tfvars`

`terraform.tfvars` 是敏感变量的赋值文件。

只能存储在根模块中，否则 Terraform 读取不到。

## `.gitignore`

将以下添加到 `my-project/.gitignore` 文件：

```
# Terraform
.terraform/
*.tfstate
*.tfstate.*
.terraform.tfstate.lock.info
*.tfplan
*.tfvars
*.tfvars.json
```

# Module

[**Module**](https://developer.hashicorp.com/terraform/language/modules) 是Terraform 共同管理的多个资源（即保存在同一个目录中的一组文件）的集合。

> [`module` blcok](#`module`)
>
> [Provider Module](https://registry.terraform.io/browse/modus)

## 模块化编程

```
terraform/
├── main.tf              # 入口文件：调用 module
├── providers.tf         # Provider 文件
├── variables.tf         # 全局变量文件
├── terraform.tfvars     # 敏感变量赋值文件
│
├── module-a/
│   ├── module-a.tf  # 资源文件
│   ├── terraform.tf # Provider 版本号文件
│   ├── api.tf       # API 文件
│   ├── iam.tf       # IAM 文件
│   ├── variables.tf # 局部变量文件
│   └── outputs.tf   # 输出文件
│
└── module-b/
    └── 同 module-a
```

## GCP Repositories 连接到 GitLab 示例

关于变量的管理：

- 全局变量的传递
  - 在根模块中声明并赋值全局变量
  - 在子模块中声明局部变量
  - 在 `module` block 中向子模块传入根模块的值
  - 敏感变量必须在根模块中进行声明和赋值
- 子模块可以声明并赋值局部变量

### 创建 Terraform 配置文件

```bash
mkdir -p /d/projects/my-project/terraform/gitlab-repo

cd /d/projects/my-project/terraform
touch main.tf providers.tf variables.tf terraform.tfvars

cd /d/projects/my-project/terraform/gitlab-repo
touch terraform.tf api.tf iam.tf gitlab-repo.tf variables.tf
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

### `variables.tf`

`terraform/variables.tf`：全局变量

```hcl
# 在根模块中声明并赋值全局变量

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

# 在根模块中声明敏感变量

# --- Secrets ---
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

### `terraform.tfvars`

`terraform/terraform.tfvars`：全局敏感变量赋值

```hcl
# 在根模块中对敏感变量赋值

gitlab_personal_access_token_api      = "gitlab_personal_access_token_api"
gitlab_personal_access_token_read_api = "gitlab_personal_access_token_read_api"
```

### `.gitignore`

`my-project/.gitignore`

添加[忽略内容](terraform-configuration-language.md#`.gitignore`)

### `terraform.tf`

`gitlab-repo/terraform.tf`

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

`gitlab-repo/api.tf`

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

### `iam.tf`

`gitlab-repo/iam.tf`

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

### `gitlab-repo.tf`

Repositories 配置文件 `gitlab-repo/gitlab-repo.tf`：链接到 GitLab

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

### `variables.tf`

`gitlab-repo/variables.tf`

```hcl
# 在子模块中声明局部变量
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

# 在子模块中声明敏感变量
# --- Secrets ---
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

### 创建 Resource

```bash
cd d:/projects/my-project/terraform
terraform apply
```

# Provider

[**Provider**](https://developer.hashicorp.com/terraform/language/providers) 插件用于与云提供商、SaaS 提供商和其他 API 进行交互，从而管理现实世界的基础设施。

> [`provider` block](#`provider`)
>
> [Provider Registry](https://registry.terraform.io/browse/providers)
>
> [Provider Registry Docs](https://developer.hashicorp.com/terraform/registry/providers/docs)
>
> [Terraform provider for Google Cloud Docs](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
>
> [Terraform on Google Cloud](https://docs.cloud.google.com/docs/terraform?hl=zh-cn)

# Resource

[**Resource**](https://developer.hashicorp.com/terraform/language/resources) 是 Terraform 创建和管理的基础设施对象，[Provider](<#Provider>) 是提供资源类型的插件。

# Dependency

## Overview

**Terraform 的外部依赖**：

- [Provider 插件](#Provider)
- [Module 插件](#Module)

[**Terraform 资源和模块之间的依赖**](https://developer.hashicorp.com/terraform/tutorials/configuration-language/dependencies)：

- [隐式依赖](#Implicit Dependencies)
- [显示依赖](#Explicit Dependencies)

在配置文件中资源的声明顺序不会影响 Terraform 创建或销毁它们的顺序。被依赖的资源会被先销毁。

## Implicit Dependencies

### 天然依赖

Terraform 会根据资源的天然依赖顺序创建资源。

例如：先创建 cluster，再创建 node pool。

### 引用依赖

只要一个资源的参数引用了另一个资源的属性，Terraform 就会自动建立依赖。

```hcl
# 创建 GSA
resource "google_service_account" "workload_identity" {
  account_id   = var.service_account_id
  display_name = "GSA for Workload Identity"
}

# 为 Pod 创建 KSA 并绑定 GSA
resource "kubernetes_service_account_v1" "my_app_ksa" {
  metadata {
    name      = var.app_ksa
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      
      # 这里引用了 GSA 的 email
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
    }
  }
}
```

## Explicit Dependencies

通过 [`depends_on`](<terraform-configuration-language.md#`depends_on`>) 参数手动指定的依赖关系。

# Variable

> [`variable` block](<terraform-configuration-language.md#`variable`>)
>
> [管理模块中的值](https://developer.hashicorp.com/terraform/language/values)
>
> [变量](https://developer.hashicorp.com/terraform/tutorials/configuration-language/variables)
>
> [敏感变量](https://developer.hashicorp.com/terraform/tutorials/configuration-language/sensitive-variables)

## `terraform.tfvars`

`terraform.tfvars` 是 `variables.tf` 中敏感变量的赋值文件。

- 在 `.gitignore` 中添加忽略 `*.tfvars`。
- 同时创建敏感变量的赋值文件的模板文件 `terraform.tfvars.example`

`variables.tf` 文件中：

- 声明变量但不赋值
- 标记为敏感

```hcl
# variables.tf

variable "mysql_jerry_password" {
  type        = string
  description = "MySQL jerry user password"
  sensitive   = true # 标记为敏感
}
```

变量赋值文件中添加变量值：

```hcl
# terraform.tfvars

mysql_jerry_password = "000000"
```

资源文件中引用变量：

```hcl
# cloud-sql.tf

resource "google_sql_user" "jerry_user" {
  name     = "jerry"
  instance = google_sql_database_instance.mysql_instance.name
  password = var.mysql_jerry_password
  host     = "%"
}
```

# Blocks

## Block

Block 是 [HCL](hcl.md) 语言的核心概念。

## `data`

[`data`](https://developer.hashicorp.com/terraform/language/block/data) block 用于从 provider 获取 resource 的数据。可以引用数据源属性来配置其他 resource，保持配置动态，防止硬编码。

```hcl
data "<TYPE>" "<LABEL>" {
  # ...
}
```

```hcl
# 获取 google_project.project 资源的数据
data "google_project" "project" {}
```

## `locals`

[`locals`](https://developer.hashicorp.com/terraform/language/block/locals) block 用于在单个 block 中定义多个变量的值，尤其适用于前缀。

定义变量：

```hcl
# --- Prefix ---
variable "prefix" {
  type        = string
  description = "Project prefix"
  default     = "todo"
}

locals {
  app_ns = "${var.prefix}-ns"

  # ... 其它变量 ...
}
```

使用变量：

```hcl
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = local.app_ns
  }
}
```

## `module`

[`module`](https://developer.hashicorp.com/terraform/language/block/module) block 用于指示 Terraform 创建在本地或远程 Module 中定义的资源。

**注意**：以下情况必须运行 `terraform init` 命令，以便 Terraform 可以更新本地代码。

- 新增 Module
- 修改旧 Module 的 `source` 参数



## `output`

[`output`](https://developer.hashicorp.com/terraform/language/block/output) block 用于公开有关基础设施的信息。主要有四个用途：

- 根模块可以在 CLI 输出中显示值。
- 子模块可以向父模块公开资源属性。
- 其他使用[远程状态的](https://developer.hashicorp.com/terraform/language/state/remote)Terraform 配置可以通过数据源访问根模块的输出`terraform_remote_state`。
- 将信息从 Terraform 操作传递到自动化工具。

```hcl
output "<LABEL>" {
  description = "<STRING>"
  value       = <EXPRESSION>
  
  # ...
}
```

**在以上示例中**：

- `<LABEL>`：输出结果中代表 value 的名字
- [官方建议的参数顺序](https://developer.hashicorp.com/terraform/language/style#outputs)

```hcl
output "gcp_project_id" {
  description = "GCP project ID"
  value       = google_project.my_project.project_id
}
```

## `provider`

[`provider`](https://developer.hashicorp.com/terraform/language/block/provider) block 用于声明和配置 [Provider](<#Provider>) 插件。

```hcl
provider "<PROVIDER_NAME>" {
  <PROVIDER_ARGUMENTS>
  
  # ...
}
```

- `<PROVIDER_NAME>`：Provider 名称，如 `google`。
- `<PROVIDER_ARGUMENTS>`：Provider 提供的参数。

```hcl
# terraform.tf

terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 4.0"
    }
  }
}
```

```hcl
# provider.tf

provider "google" {
  project = "my-project-id"
  region  = "asia-east1"
  zone    = "asia-east1-a"
}
```

- 如果在 `provider` 中指定的 `region` 和 `zone`，会被 `resource` 继承。

- 如果在 `resource` 中不想继承 `provider` 中指定的 `region` 和 `zone`，则可进行覆盖：

  ```hcl
  # 以 Regional 集群为例
  resource "google_container_cluster" "primary" {
    name = "my-gke-cluster"
    
    # 覆盖 provider 中指定的 region 和 zone，它会忽略 provider 里的 zone
    # 创建 Regional 集群
    location = "us-central1" 
  
    initial_node_count = 1
    # ...
  }
  ```

## `resource`

> [Resources](https://developer.hashicorp.com/terraform/language/resources)

[`resource`](https://developer.hashicorp.com/terraform/language/block/resource) block 用于定义一段 infrastracture。各个 resource 支持的参数由 Provider 决定。

```hcl
resource "<TYPE>" "<LABEL>" {
  <PROVIDER_ARGUMENTS>

  # ...
}
```

- [`TYPE`](https://developer.hashicorp.com/terraform/language/block/resource#type)：资源类型
- [`LABEL`](https://developer.hashicorp.com/terraform/language/block/resource#label)：资源标签。
  - Terraform 使用此标签在状态文件中跟踪资源。此标签不会影响实际基础设施的名称。
  - 资源标签不能动态化，必须显示指定。
- [`<PROVIDER_ARGUMENTS>`](https://developer.hashicorp.com/terraform/language/block/resource#provider-arguments)：参数。Provider 决定可以为资源定义哪些参数。

```hcl
# aws-instance.tf

resource "aws_instance" "web" {
  ami           = "ami-a1b2c3d4"
  instance_type = "t2.micro"
}
```

引用资源：

```	hcl
<TYPE>.<LABEL>.<ARGUMENT>
aws_instance.web.ami
```

## `terraform`

[`terraform`](https://developer.hashicorp.com/terraform/language/block/terraform) block 用于配置 Terraform 的行为，包括 Terraform 版本、后端、与 HCP Terraform 的集成以及所需的Provider。

```hcl
terraform { 
  required_providers { 
    < PROVIDER > {} 
  } 
  
  # ...
}
```

```hcl
# terraform.tf

terraform {
  required_providers {
    google = {
      version = ">= 5.0.0"
      source  = "hashicorp/google"
    }
  }
}
```

## `variable`

### Overview

[`variable`](https://developer.hashicorp.com/terraform/language/block/variable) block 用于定义 [Variable](<#Variable>)。

```hcl
variable “<LABEL>” { 
  type         = < TYPE >
  description  = "<DESCRIPTION>"
  default      = < DEFAULT_VALUE >
  
  # ...
}
```

**在以上示例中**：

- `<LABEL>`：变量标识
- `type`：类型
- `description`：描述
- `default`：默认值
- [官方建议的参数顺序](https://developer.hashicorp.com/terraform/language/style#variables)

定义变量：

```hcl
# variables.tf

variable "gcp_project_id" {
  type        = string
  description = "GCP Project ID"
  default     = "project-jerry-222222"
}

variable "gcp_region" {
  type        = string
  description = "GCP Region"
  default     = "asia-east2"
}

variable "gcp_zone" {
  type        = string
  description = "GKE Zone"
  default     = "asia-east2-a"
}
```

使用变量：

```hcl
# main.tf

provider "google" {
  project = var.project_id
  region  = var.gcp_region
  zone    = var.gcp_zone
}
```

### 说明

如果声明的变量为空值，在部署时会被要求输入变量值。

# Arguments

## Argument

Argument 是 [HCL](hcl.md) 语言的核心概念。

## `depends_on`

[`depends_on`](https://developer.hashicorp.com/terraform/language/meta-arguments/depends_on) meta-argument 可以处理 Terraform 无法自动推断的 resource 或 block 的依赖关系。

```hcl
depends_on [<TYPE>.<LABEL>]
```

```hcl
# 1. 定义一个 S3 存储桶
resource "aws_s3_bucket" "example" {
  bucket = "my-unique-terraform-demo-bucket"
}

# 2. 定义一个存储桶中的对象
resource "aws_s3_bucket_object" "example_file" {
  bucket = aws_s3_bucket.example.id
  key    = "hello.txt"
  source = "hello.txt"

  # 显式依赖：强制要求在 bucket 资源就绪后再处理此资源
  depends_on = [
    aws_s3_bucket.example
  ]
}
```

# Expressions