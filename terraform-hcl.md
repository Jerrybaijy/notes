---
title: terraform-hcl
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

[**Terraform HCL**](https://developer.hashicorp.com/terraform/language) 是 Terraform 的配置语言，它基于 HCL，适用于 [Terraform CLI](https://developer.hashicorp.com/terraform/cli)、 [HCP Terraform](https://cloud.hashicorp.com/products/terraform) 和 [Terraform Enterprise](https://developer.hashicorp.com/terraform/enterprise)，主要目的是**声明资源**，这些资源代表基础设施对象。

> [Terraform HCL Docs](https://developer.hashicorp.com/terraform/language)

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

# Blocks

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

Terraform 依赖于 [Provider](https://developer.hashicorp.com/terraform/language/providers)（插件）与云提供商、SaaS 提供商和其他 API 进行交互。

> [Provider Registry](https://registry.terraform.io/browse/providers)
>
> [Terraform provider for Google Cloud Docs](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
>
> [Terraform on Google Cloud](https://docs.cloud.google.com/docs/terraform?hl=zh-cn)

[`provider`](https://developer.hashicorp.com/terraform/language/block/provider) block 用于声明和配置 [Providers](<terraform.md#Providers>)。

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

- 如果在 resource 中不想继承 `provider` 中指定的 `region` 和 `zone`，则可进行覆盖：

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

[`resource`](https://developer.hashicorp.com/terraform/language/block/resource) block 用于定义一段 infrastracture。各个 resource 支持的参数由提供程序决定。

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

[`variable`](https://developer.hashicorp.com/terraform/language/block/variable) block 用于定义 [Variables](<terraform.md#Variables>)。

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