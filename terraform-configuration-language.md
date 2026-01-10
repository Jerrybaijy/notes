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

## `variables.tfvars`

`variables.tfvars` 是敏感变量的赋值文件。

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

## Terraform Module 结构

```
terraform/
├── main.tf                  # 根模块主文件：调用 module
├── providers.tf             # 根模块 Provider 文件
├── variables.tf             # 根模块变量文件
├── variables.tfvars         # 根模块敏感变量赋值文件
├── variables.tfvars.example # 根模块敏感变量赋值文件模板
│
├── module-a/                # module-a 模块目录
│   ├── api.tf               # 子模块 API 文件
│   ├── iam.tf               # 子模块 IAM 文件
│   ├── module-a.tf          # 子模块主文件
│   ├── terraform.tf         # 子模块 Provider Version 文件
│   ├── outputs.tf           # 子模块输出文件
│   └── variables.tf         # 子模块变量文件
│
└── module-b/                # module-a 模块目录
    └── 同 module-a
```

## GCP Repositories 连接到 GitLab 示例

关于变量的管理：

- 全局变量的传递
  - 在根模块中声明并赋值全局变量
  - 在子模块中声明局部变量
  - 在 `module` block 中向子模块传入全局变量的值
  - 敏感变量必须在根模块中进行声明和赋值
- 子模块可以独立声明并赋值局部变量

示例详见[通过 Terraform 连接到 GitLab](<gcp-repositories.md#通过 Terraform 连接到 GitLab>)

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

## `variables.tfvars`

`variables.tfvars` 是 `variables.tf` 中敏感变量的赋值文件。

- 在 `.gitignore` 中添加忽略 `*.tfvars`。
- 同时创建敏感变量的赋值文件的模板文件 `variables.tfvars.example`

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
# variables.tfvars

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