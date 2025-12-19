---
title: terraform
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - iac
  - terraform
---

# Overview

[**Terraform**](https://developer.hashicorp.com/terraform) 是一种由 HashiCorp 公司开发的开源的**基础设施即代码（IaC）工具**。

> [Terraform Docs](http://developer.hashicorp.com/terraform/docs)
>
> [Terraform on Google Cloud](https://docs.cloud.google.com/docs/terraform?hl=zh-cn)

## Workflow

[HCP Terraform](https://cloud.hashicorp.com/products/terraform) 支持以下工作流程：

- [VCS](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-create-vcs-workspace)
- [CLI](https://developer.hashicorp.com/terraform/cloud-docs/workspaces/run/cli)
- [API](https://developer.hashicorp.com/terraform/cloud-docs/api-docs)

## CDK for Terraform

[**CDKTF**](https://developer.hashicorp.com/terraform/cdktf)（Cloud Development Kit for Terraform）允许你使用熟悉的编程语言来定义和配置基础设施。

# Quick Start

此 [Quick Start](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started) 以 GCP 为例

## 注册 HCP

[Sign up for HCP Terraform](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-sign-up)

## 创建组织

[Create an organization](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-sign-up#create-an-organization)

## 安装 Terraform

### 安装 Terraform

以管理员身份启动终端，使用 Chocolatey [安装 Terraform](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/install-cli)，重启终端生效。

```bash
# 安装（安装完成后需重启所有终端）
choco install terraform
# 查看版本
terraform version
```

### 开启命令补全

- 在 `/c/Users/jerry/.bashrc` 文件中添加如下内容，重启终端生效。
- 例：输入 `terrform pl`，然后按 `Tab` 会补全至 `terrform plan`。
- 注：如果有多个子命令符合条件，连按两次 `Tab` 会返回全部可用子命令。

```bash
# Terraform 别名和自动补全
alias terraform='terraform.exe'
complete -C /c/ProgramData/chocolatey/lib/terraform/tools/terraform.exe terraform
```

### VS Code Plugin

在 VS Code 中安装 `HashiCorp Terraform` 插件。

- 语法高亮
- 代码格式化（需在 VS Code 的 `settings.json` 文件中设置）

## 设置 GCP

提前[设置 GCP](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#set-up-gcp)：

- 创建一个项目
- 为此项目启用 [Compute Engine API](https://console.developers.google.com/apis/library/compute.googleapis.com)

## 创建 configuration

### 创建目录和配置文件

```bash
mkdir /d/projects/0000-tests/learn-terraform-gcp
cd /d/projects/0000-tests/learn-terraform-gcp
touch main.tf
```

### `main.tf`

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
  zone    = "asia-east2-b"
}

resource "google_compute_network" "vpc_network" {
  name = "terraform-network"
}
```

### 代码格式化

有两种方法进行格式化：

- VS Code 插件 `HashiCorp Terraform`（需在 VS Code 的 `settings.json` 文件中设置）

- 使用 Terraform 命令

  ```bash
  cd /d/projects/0000-tests/learn-terraform-gcp
  # 格式化
  terraform fmt
  # 验证格式化时有效的
  terraform validate
  ```

## 初始化目录

[初始化目录](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#initialize-the-directory)

```bash
cd /d/projects/0000-tests/learn-terraform-gcp
terraform init
```

- 这一步会下载配置中定义 Google provider，并将其安装在当前工作目录的一个隐藏子目录中，名为 `.terraform`。
- 还创建了一个名为 `.terraform.lock.hcl` 的锁文件，指定了所使用的具体提供者版本，以确保每次 Terraform 运行一致。这也让你能够控制何时升级配置中使用的供应商。

## 部署资源

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

目录多出一个 **`terraform.tfstate`** 文件，这是 Terraform 的状态文件。

- Terraform 会将它管理的资源的 ID 和属性存储在这个文件中，以便未来更新或销毁这些资源。
- 注意这个文件中包含敏感信息。

登录 Google Cloud 控制台，会发现多了一个名为 `terraform-network` 的 VPC。

## 修改配置

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
  zone    = "asia-east2-b"
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

## 清理部署

```bash
cd /d/projects/0000-tests/learn-terraform-gcp
terraform destroy
```

# Command

```bash
# 查看版本
terraform version
# 帮助
terraform -help
# 特定命令帮助
terraform plan -help
terraform $COMMAND -help
```

# Variables

## `variable`

[`variable`](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-variables)：类似环境变量

如果声明的变量为空值，在部署时会被要求输入变量值。

```hcl
# variables.tf

variable "project" {
  default = "project-60addf72-be9c-4c26-8db"
}

variable "region" {
  default = "asia-east2"
}

variable "zone" {
  default = "asia-east2-b"
}
```

```hcl
# main.tf

provider "google" {
  project = var.project
  region  = var.region
  zone    = var.zone
}
```

## `output`

[`output`](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-outputs)：在部署完成后会输出，也可使用 `terraform output` 命令进行查询。

```hcl
output "ip" {
  value = google_compute_instance.vm_instance.network_interface.0.network_ip
}
```



