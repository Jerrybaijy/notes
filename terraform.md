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

> [Terraform Docs](http://developer.hashicorp.com/terraform/docs)
>
> [Terraform CLI Docs](https://developer.hashicorp.com/terraform/cli)
>
> [Terraform Configuration Language Docs](https://developer.hashicorp.com/terraform/language)
>
> [Terraform Registry](https://registry.terraform.io/)

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
mkdir -p /d/projects/my-project/terraform
cd /d/projects/my-project/terraform
touch providers.tf variables.tf vpc.tf output.tf
```

## `terraform.tf`

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

## `providers.tf`

```hcl
provider "google" {
  project = var.gcp_project_id
  region  = var.gcp_region
  zone    = var.gcp_zone
}
```

## `variables.tf`

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

## `vpc.tf`

```hcl
resource "google_compute_network" "vpc_network" {
  name = var.vpc_network_name
}
```

## `output.tf`

## 初始化 Terraform

[初始化目录](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#initialize-the-directory)

```bash
cd /d/projects/my-project/terraform
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
cd /d/projects/my-project/terraform
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

## 修改 Terraform 配置

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

**注意**：如果有通过 CLI 部署的资源，应先通过 CLI 清理，然后再进行销毁。

如清理失败，详见 [Terraform CLI 笔记](<terraform-cli#通过 `kubectl` 安装 Argo CD 并部署应用的特殊说明>)。

```bash
cd /d/projects/my-project/terraform
terraform destroy
```

