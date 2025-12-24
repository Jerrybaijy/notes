---
title: gcp-project
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud-computing
  - gcp
  - gcp-project
---

# Overview

[**Project**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#projects) 资源是 GCP [资源层次结构](<gcp.md#资源层次结构>)中最基础的实体，是所有服务资源的“容器”，是一种 Global 资源。

在 GCP 中，任何服务资源都必须归属于某个项目。除您使用[共享 VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc?hl=zh-cn) 或 [VPC 网络对等互连](https://docs.cloud.google.com/vpc/docs/vpc-peering?hl=zh-cn)，否则一个项目无法访问其他项目的资源。

> [项目概览](https://docs.cloud.google.com/docs/overview?hl=zh-cn)
>
> [项目资源](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#projects)
>
> [创建和管理项目](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects?hl=zh-cn)
>
> [Project Reference](https://docs.cloud.google.com/sdk/gcloud/reference/projects)

- [**项目编号**](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects?hl=zh-cn#before_you_begin)，由 Google Cloud 提供。
- [**项目 ID**](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects?hl=zh-cn#before_you_begin)
  - 您可以提供或 Google Cloud 可以为您提供。
  - 不得使用正在或以前使用过的项目 ID；这包括已删除的项目。
- [**项目名称**](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects?hl=zh-cn#before_you_begin)，由您提供。

# Quick Start

## 准备工作

[GCP 准备工作](<gcp.md#准备工作>)已完成

## 创建项目

```bash
gcloud projects create $PROJECT_ID [FLAGS]

gcloud projects create project-jerry-111111 \
    --name "My Projet" \
    --organization 338307828462
```

## 设置默认项目

```bash
# 查看所有项目
gcloud projects list
# 设置默认项目
gcloud config set project $PROJECT_ID
gcloud config set project project-jerry-111111
# 查看当前项目ID
gcloud config get-value project
```

## 更新配额

将配额项目更新为当前正在使用的项目

```bash
gcloud auth application-default set-quota-project $PROJECT_ID
gcloud auth application-default set-quota-project project-jerry-111111
```

## 关联结算账号

```bash
# 列出所有结算账号
gcloud billing accounts list

# # 关联结算账号
gcloud billing projects link $PROJECT_ID --billing-account=$ACCOUNT_ID
gcloud billing projects link project-jerry-111111 --billing-account=01716E-392C40-6E5B41
```

## 启用 API

新项目默认禁用了大多数 API。如果你要创建虚拟机，需要手动启用 Compute Engine API：

```bash
gcloud services enable $API
gcloud services enable compute.googleapis.com
```

## 创建服务资源

以创建 VM 为例

```bash
# 创建 VM
gcloud compute instances create my-vm \
    --zone=asia-east1-a \
    --machine-type=e2-micro \
    --image-family=debian-11 \
    --image-project=debian-cloud

# 列出所有 VM
gcloud compute instances list

# 停止 VM
gcloud compute instances stop my-vm --zone=asia-east1-a

# 删除 VM
gcloud compute instances delete my-vm --zone=asia-east1-a
```

## 删除项目

```bash
gcloud projects delete $PROJECT_ID
gcloud projects delete project-jerry-111111
```

# Create a Project

## Create a Project with `gcloud projects create`

如果不指定 `--name`，默认会使用项目 ID 作为名称。

```bash
gcloud projects create $PROJECT_ID [FLAGS]

gcloud projects create project-jerry-111111 \
    --name "My Projet" \
    --organization 338307828462
```

## Create a Project with Terraform

详见 [Terraform-GCP 笔记](<terraform-gcp.md#Project>)

# Project Reference

## 语法

> [Project  Reference](https://docs.cloud.google.com/sdk/gcloud/reference/projects)

gcloud projects [$COMMAND](https://docs.cloud.google.com/sdk/gcloud/reference/projects#COMMAND) [[FLAGS](https://docs.cloud.google.com/sdk/gcloud/reference/projects#GCLOUD-WIDE-FLAGS)]

## Commands

```bash
# 列出所有项目
gcloud projects list
# 创建项目
gcloud projects create $PROJECT_ID [FLAGS]
# 删除项目
gcloud projects delete $PROJECT_ID [FLAGS]
```
