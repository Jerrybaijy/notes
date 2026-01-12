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

# Quickstart

## 准备工作

- [注册 HCP](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-sign-up)

- [创建组织](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started/cloud-sign-up#create-an-organization)

- [Terraform 安装](<terraform-cli.md#Install>)已完成

- [设置 GCP](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/google-cloud-platform-build#set-up-gcp)：
  
  - 完成 [GCP 准备工作](gcp.md#准备工作)
  
  - [创建 GCP Project](<gcp-project.md#创建 GCP 项目>)
  
  - [为 Terraform 授权](gcp-gcloud-cli.md#为其它应用授权)
  
    ```bash
    gcloud auth application-default login
    ```


## 创建 Terraform 目录

```bash
DIR=/d/projects/my-project/terraform && mkdir -p $DIR && cd $DIR
touch main.tf providers.tf variables.tf variables.tfvars variables.tfvars.example
```

### `main.tf`

根模块主文件 `terraform/main.tf`

```hcl
# 调用 moudle-a 模块
module "moudle-a" {
  # ...
}

# 调用 moudle-b 模块
module "moudle-b" {
  # 其它配置

  # 传递其它模块的输出
  variable-a = module.moudle-a.variable-a

  # 传递根模块的变量
  prefix = var.prefix
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
  default     = "todo"
}

# --- 其它变量 ---
```

### `variables.tfvars`

根模块敏感变量赋值文件 `terraform/variables.tfvars`

```hcl
# GitLab repo token
gitlab_personal_access_token_api      = "gitlab_personal_access_token_api"
gitlab_personal_access_token_read_api = "gitlab_personal_access_token_read_api"
```

### `variables.tfvars.example`

根模块敏感变量赋值文件模板 `terraform/variables.tfvars.example`

```hcl
# GitLab repo token
gitlab_personal_access_token_api      = ""
gitlab_personal_access_token_read_api = ""
```

## 子模块

将 `terraform-module` Git 仓库的子模块复制到 `terraform` 目录下

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

## `.gitignore`

Git 忽略文件 `my-project/.gitignore` 中添加[忽略内容](terraform-configuration-language.md#`.gitignore`)：

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

## 初始化 Terraform

```bash
cd d:/projects/my-project/terraform
terraform init
```

## 应用部署

```bash
cd /d/projects/my-project/terraform
terraform apply
```

## 更新 `kubectl` 配置

使用 Terraform 部署 GKE 资源后要[更新 `kubectl` 配置](<gcp-gke.md#更新 `kubectl` 配置>)。

```bash
gcloud container clusters get-credentials todo-cluster \
    --location asia-east2-a \
    --project project-60addf72-be9c-4c26-8db
```

## 销毁资源

```bash
cd /d/projects/my-project/terraform
terraform destroy
```

