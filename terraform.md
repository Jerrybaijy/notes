---
title: terraform
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud
  - iac
  - terraform
---

# Overview

[**Terraform**](https://developer.hashicorp.com/terraform) 是一个由 HashiCorp 公司开发的开源的**基础设施即代码（IaC）工具**。

> [Terraform Docs](http://developer.hashicorp.com/terraform/docs)：Terraform 官方文档
>
> [Terraform CLI Docs](https://developer.hashicorp.com/terraform/cli)：Terraform CLI 官方文档
>
> [Terraform HCL Docs](https://developer.hashicorp.com/terraform/language)：适用于 Terraform 的 HCL 语言
>
> [Terraform Registry](https://registry.terraform.io/)
>
> [Write Terraform Configuration](https://developer.hashicorp.com/terraform/tutorials/configuration-language)
>
> [Terraform provider for Google Cloud](https://registry.terraform.io/providers/hashicorp/google/latest/docs)

## Workflow

[HCP Terraform](https://cloud.hashicorp.com/products/terraform) 支持以下工作流程：

- [VCS](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-create-vcs-workspace)
- [CLI](https://developer.hashicorp.com/terraform/cloud-docs/workspaces/run/cli)
- [API](https://developer.hashicorp.com/terraform/cloud-docs/api-docs)

## CDK for Terraform

[**CDKTF**](https://developer.hashicorp.com/terraform/cdktf)（Cloud Development Kit for Terraform）允许你使用熟悉的编程语言来定义和配置基础设施。

# Quick Start

此 [Quick Start](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started) 以在 GCP 部署一个 VPC 资源为例。

## 准备工作

- [注册 HCP](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-sign-up)
- [创建组织](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-sign-up#create-an-organization)
- [Terraform 安装](<terraform-cli.md#Install>)已完成
- [设置 GCP](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#set-up-gcp)：
  - 创建一个项目
  - 为此项目启用 [Compute Engine API](https://console.developers.google.com/apis/library/compute.googleapis.com)


## 创建 Terraform 目录和配置文件

```bash
mkdir /d/projects/0000-tests/learn-terraform-gcp
cd /d/projects/0000-tests/learn-terraform-gcp
touch providers.tf variables.tf vpc.tf output.tf
```

## 编写 `terraform.tf`

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "6.8.0"
    }
  }
}
```

## 编写 `providers.tf`

```hcl
provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
  zone    = var.gcp_zone
}
```

## 编写 `variables.tf`

```hcl
variable "gcp_project_id" {
  description = "GCP Project ID"
  type        = string
  default     = "project-60addf72-be9c-4c26-8db"
}

variable "gcp_region" {
  description = "GCP Region"
  type        = string
  default     = "asia-east2"
}

variable "gcp_zone" {
  description = "GKE Zone"
  type        = string
  default     = "asia-east2-a"
}

variable "vpc_network_name" {
  description = "VPC 网络的名称"
  type        = string
  default     = "terraform-network"
}
```

## 编写 `vpc.tf`

```hcl
resource "google_compute_network" "vpc_network" {
  name = var.vpc_network_name
}
```

## 编写 `output.tf`

## 初始化 Terraform

[初始化目录](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#initialize-the-directory)

```bash
cd /d/projects/0000-tests/learn-terraform-gcp
terraform init
```

当执行 `terraform init` 后，Terraform 会根据 `.tf` 文件进行初始化工作，会在配置根目录出现：

- `.terraform`：本地缓存目录，详见 [`.terraform`](<#`.terraform`>)。
- `.terraform.lock.hcl`：依赖锁定文件，详见 [`.terraform.lock.hcl`](<#`.terraform.lock.hcl`>)。

## 应用部署

```bash
# 使用 gcloud CLI 授权
gcloud auth application-default login

# 部署
cd /d/projects/0000-tests/learn-terraform-gcp
terraform apply

# 检查状态
terraform show
```

执行 `terraform apply` 命令以后，看到的是 Terraform 的 **Plan**，输入 `yes`（必须完整输入这三个字母）并按回车。

当执行 `terraform apply` 后，会在配置根目录出现：

- `terraform.tfstate`：状态文件，详见 [`terraform.tfstate`](<#`terraform.tfstate`>)。
- `terraform.tfstate.backup`：状态备份文件，详见 [`terraform.tfstate.backup`](<#`terraform.tfstate.backup`>)。

登录 Google Cloud 控制台，可以查看新部署的 GCP 资源。

## 更新 `kubectl` 配置

使用 Terraform 部署 GKE 资源后要[更新 `kubectl` 配置](<gcp-gke.md#更新 `kubectl` 配置>)。

```bash
gcloud container clusters get-credentials todo-cluster \
    --location asia-east2-a \
    --project project-60addf72-be9c-4c26-8db
```

## 修改 Terraform 配置（可选）

向 `main.tf` 中添加一个 Compute Engine 实例，并执行 `terraform apply` 命令部署。

也可修改已存在资源的配置。

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "6.8.0"
    }
  }
}

provider "google" {
  project = "project-60addf72-be9c-4c26-8db"
  region  = "asia-east2"
  zone    = "asia-east2-a"
}

resource "google_compute_network" "vpc_network" {
  name = "terraform-network"
}

resource "google_compute_instance" "vm_instance" {
  name         = "terraform-instance"
  machine_type = "e2-micro"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = google_compute_network.vpc_network.name
    access_config {
    }
  }
}
```

## 销毁部署

```bash
cd /d/projects/0000-tests/learn-terraform-gcp
terraform destroy
```

# Dependencies

## Overview

[**Dependencies**](https://developer.hashicorp.com/terraform/tutorials/configuration-language/dependencies)：Terraform 资源和模块之间的依赖关系。

- 显示依赖
- 隐式依赖

在配置文件中资源的声明顺序不会影响 Terraform 创建或销毁它们的顺序。

被依赖的资源会被先销毁。

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

通过 [`depends_on`](<terraform-hcl.md#`depends_on`>) 参数手动指定的依赖关系。

# Providers

Terraform 依赖于 [Provider](https://developer.hashicorp.com/terraform/language/providers)（插件）与云提供商、SaaS 提供商和其他 API 进行交互。

> [Providers](https://developer.hashicorp.com/terraform/language/providers)
>
> [Provider Registry](https://registry.terraform.io/browse/providers)

# Resources

> [Resources](https://developer.hashicorp.com/terraform/language/resources)

# Variables

> [`variable`](<terraform-hcl.md#`variable`>)
>
> [管理模块中的值](https://developer.hashicorp.com/terraform/language/values)
>
> [变量](https://developer.hashicorp.com/terraform/tutorials/configuration-language/variables)
>
> [敏感变量](https://developer.hashicorp.com/terraform/tutorials/configuration-language/sensitive-variables)

# Terraform 文件

## 配置文件

如果资源少，可以将所有配置写入 `main.tf` 文件。

如果资源多，可以将 `main.tf` 拆分重构为多个文件，以 GCP 为例：

- `providers.tf`：Provider 配置文件
- `gke.tf`：GKE 配置文件
- `iam.tf`：GCP 权限配置文件
- `sql.tf`：Cloud SQL 配置文件
- `variables.tf`：输入变量配置文件
- `output.tf`：输出变量配置文件

## Git 忽略

将以下添加到 `.gitignore` 文件：

```
# Terraform
.terraform/
*.tfstate
.terraform.tfstate.lock.info
*.tfplan
*.tfvars
*.tfvars.json
*.tfstate.backup
```

## `.terraform`

这是一个**本地缓存目录**，它是 Terraform 运行的“工作间”。

- 会在执行 `terraform init` 后自动生成。
- **存放 Provider 插件**：Terraform 会根据你在 `providers.tf` 中定义的 `google` provider，从官方仓库下载对应的二进制驱动文件并存放在这里 。
- **存放 Module**：如果你在代码中引用了外部模块，它们也会被下载到这里。
- **注意**：这个文件夹通常很大，**绝对不要**将其提交到 Git 仓库。你应该在 `.gitignore` 文件中忽略它。

## `.terraform.lock.hcl`

这是**依赖锁定文件**（Dependency Lock File），类似于 Node.js 的 `package-lock.json` 或 Python 的 `poetry.lock`。

- 会在执行 `terraform init` 后自动生成。
- **版本锁定**：它记录了你当前使用的 Provider 插件的具体版本号和校验和（Hashes） 。
- **团队一致性**：如果你把这个文件提交到 Git，团队中的其他成员在执行 `terraform init` 时，Terraform 会确保下载完全相同版本的插件，避免因为 Provider 版本升级导致的基础设施变更不一致。
- **建议**：行业最佳实践是**将其提交到 Git**。

## `.terraform.tfstate.lock.info`

这是**状态锁文件**，作用是**防止多人同时修改**同一套资源。

- **原理**：当你运行 `terraform plan` 或 `apply` 时，Terraform 会创建一个“锁”。如果此时你的同事也尝试运行命令，Terraform 会报错并阻止他，直到你运行结束。
- **消失的原因**：一旦命令执行完毕（无论成功或失败），锁就会被自动释放，文件随之删除。
- 如果命令意外崩溃导致这个文件没有消失，下次运行会报错。这时通常使用 `terraform force-unlock` 命令，而不是手动删除文件。
- **注意**：这个文件**不要**提交到公共代码仓库。

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

## `$PLAN_NAME.tfplan`

这个**锁定计划文件**是在执行 `terraform plan -out=$PLAN_NAME.tfplan` 后自动生成，锁定了当前的代码逻辑和云端状态。

稍后可以执行 `terraform apply "todo-infra.tfplan"` 命令以执行锁定计划。

