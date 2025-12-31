---
title: gcp
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - cloud-computing
  - gcp
---

# Overview

[**GCP**](https://docs.cloud.google.com/docs/overview?hl=zh-cn) （Google Cloud Platform）是谷歌提供的一套云计算服务。

> [Google Cloud Docs](https://docs.cloud.google.com/docs)
>
> [Gcloud Reference](https://docs.cloud.google.com/sdk/gcloud/reference)
>
> [Google Cloud 使用入门](https://docs.cloud.google.com/docs/get-started)
>
> [Google Cloud 产品](https://cloud.google.com/products?hl=zh-cn&_gl=1*xq66jx*_ga*MTYwMDY0NjE4Ni4xNzYxNTY3Mjky*_ga_WH2QY8WWF5*czE3NjU4MDQ4MDkkbzgkZzEkdDE3NjU4MDc0NTQkajI5JGwwJGgw)

## 交互方式

Google Cloud 为您提供了三种与服务和资源[交互的基本方式](https://docs.cloud.google.com/docs/overview?hl=zh-cn#ways_to_interact_with_the_services)。

- [Google Cloud console](https://console.cloud.google.com/?hl=zh-cn) 提供基于 Web 的图形界面
- 命令行界面
  - [Google Cloud CLI](https://docs.cloud.google.com/sdk/gcloud)
  - [Cloud Shell](https://docs.cloud.google.com/shell/docs/features?hl=zh-cn)
- [客户端库](https://docs.cloud.google.com/sdk/cloud-client-libraries?hl=zh-cn)

# Quick Start

## 准备工作

- 注册 Google 并开通结算
- [安装和配置 Google Cloud CLI](<#Install>)

## 创建 GCP Project

[创建 GCP Project](<gcp-project.md#Create a Project with `gcloud projects create`>)

## 管理 GCP 服务资源

- [使用 Terraform 管理 GCP 服务资源](<terraform.md#Quick Start>)
- 或者使用其它方式（例如 CLI）管理 GCP 服务资源

## 删除 GCP Project

- [使用 Terraform 删除 GCP Project](<gcp-project.md#Quick Start>)
- 或者使用其它方式（例如 CLI）删除 GCP Project

# Google Cloud CLI

[**Google Cloud SDK**](https://docs.cloud.google.com/sdk/docs/overview?hl=zh-cn) 是一套用于与Google Cloud 服务交互的库和工具。它包括命令行工具、特定于语言的客户端库、IDE 扩展程序和模拟器，可帮助您在 Google Cloud上管理资源和自动执行任务。

[**Google Cloud CLI**](https://cloud.google.com/sdk/gcloud?hl=zh-cn) 是 Google Cloud 的命令行工具。

## Install

> [安装 Google Cloud CLI](https://docs.cloud.google.com/sdk/docs/install-sdk?hl=zh-cn)

### Windows

- 下载并安装 [Google Cloud CLI](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe?hl=zh-cn)

  尽量不要选择为所有用户安装

- 安装之后会出现 Google Cloud SDK Shell 应用

- 关闭 SDK Shell 和全部 Terminal，重新打开 Terminal，验证安装：

  ```bash
  gcloud version
  ```

- 初始化 Google Cloud

  ```bash
  gcloud init
  ```

- 根据提示选择选项，最后跳转到浏览器中登录 Google 账号。

- 配置 Google Cloud CLI 的默认选项

  ```bash
  # 设置默认项目
  gcloud config set project $PROJECT_ID
  # 设置默认 region (zone 同理)
  gcloud config set compute/region $REGION
  # 列出默认配置
  gcloud config list
  ```

### Linux

- [根据操作系统选择安装 Google Cloud CLI](https://cloud.google.com/sdk/docs/install?hl=zh-cn)

- 进入 User 目录

- 下载 Linux 归档文件

  ```bash
  curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-469.0.0-linux-x86_64.tar.gz
  ```

- 解压

  ```bash
  tar -xf google-cloud-cli-469.0.0-linux-x86_64.tar.gz
  ```

- 将 gcloud CLI 添加到路径

  ```bash
  ./google-cloud-sdk/install.sh
  ```

- 初始化

  ```bash
  ./google-cloud-sdk/bin/gcloud init
  ```

  - 选择第 2 项：Log in with a new account
  - 点击输出的网址，跳转到网页获取 authorization code，并粘贴回至 bash
  - 选择项目，目前项目为 true-oasis-418914
  - 选择默认区域：上次选 [48] asia-east2-b

- 安装 kubectl

  ```bash
  # 成功过的方法一
  gcloud components install kubectl
  ```

  ```bash
  # 成功过的方法二
  sudo apt-get update
  # 安装 kubectl
  sudo snap install kubectl --classic
  # 添加环境变量
  export PATH=$PATH:/snap/bin
  # 验证安装
  kubectl version --client
  # 安装插件
  sudo apt-get install google-cloud-cli-gke-gcloud-auth-plugin
  ```

## Uninstall

- [卸载 Google Cloud CLI](https://cloud.google.com/sdk/docs/uninstall-cloud-sdk?hl=zh-cn)
- 以下两个命令需要在 **Google Cloud CLI** 或 **CMD** 中执行
- 运行以下命令查找您的安装目录；

  ```bash
gcloud info --format="value(installation.sdk_root)"
  ```

- 手动打开安装目录，点击 `unistall` 卸载；
- 运行以下命令查找您的用户配置目录；

  ```bash
gcloud info --format="value(config.paths.global_config_dir)"
  ```

- 手动删除用户配置目录。

# Resource Manager

Google Cloud 提供组织和项目等容器资源，可对其他 Google Cloud 资源进行分组和分层整理。

> [Resource Manager Docs](https://docs.cloud.google.com/resource-manager/docs?hl=zh-cn)

## 地理架构

[地理架构](https://docs.cloud.google.com/docs/geography-and-regions?hl=zh-cn)：指资源的可用地理范围。资源只能被同范围内的资源访问。

```
Location: 通用

Multi-region(多区域)
└── Region (区域)
    └── Zone (可用区)
```

- **Location (位置)**：一个通用的概念，指部署资源的地理范围。可以是 Multi-region、Region 和 Zone。
- **Multi-region (多区域)**：大洲级别，例如 `ASIA` （台湾），由多个 Region 组成，会跨 Region 备份。
- **Region (区域)**：城市级别，例如 `asia-east1` （台湾），由多个 Zone 组成，会跨 Zone 备份。
- **Zone (可用区)**：机房级别，例如 `asia-east1-a`（台湾 A 区），不备份。

## 资源层次结构

[**资源层次结构**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn)：Google Cloud 资源以分层方式进行整理。

```
Organization
└── Folder (可选)
    └── Project
```

- [**Organization**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#organizations) 资源是Google Cloud 资源层次结构中的**根节点**，通常对应一个公司或域名（如 `yourcompany.com`）。
- [**Folder**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#folders) 资源是 Organization 和 Project 之间的可选层级，可对项目进行分组。
- [**Project**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#projects) 资源是 GCP 最基础的实体，是所有服务资源的“容器”。

# Gcloud Reference

## 语法

> [Gcloud Reference](https://docs.cloud.google.com/sdk/gcloud/reference)

gcloud [$GROUP](https://docs.cloud.google.com/sdk/gcloud/reference#GROUP) | [$COMMAND](https://docs.cloud.google.com/sdk/gcloud/reference#COMMAND) [$FLAGS]

## 其它命令

```bash
gcloud version
# 查看登录账户
gcloud auth list
# 查看项目中的实例
gcloud compute instances list --project=$PROJECT_ID
```

## 镜像

```bash
# 创建镜像
gcloud builds submit --tag us-central1-docker.pkg.dev/PROJECT_ID/REPO_NAME/IMAGE_NAME .
# 查看仓库镜像
gcloud artifacts docker images list LOCATION-docker.pkg.dev/PROJECT_ID/REPO_NAME
```

## 仓库

```bash
# 创建仓库
gcloud artifacts repositories create $REGISTRY_NAME \
    --repository-format=$FORMAT \
    --location=$LOCATION \
    --description="MESSAGE"

gcloud artifacts repositories create todo-docker \
    --repository-format=docker \
    --location=asia-east2 \
    --description="Docker repository for todo app images and charts"

# 查看仓库
gcloud artifacts repositories list
# 删除仓库
gcloud artifacts repositories delete $REPO_NAME --location=$LOACATION
```

# `gcloud config`

[`gcloud config`](https://docs.cloud.google.com/sdk/gcloud/reference/config) 用于查看和编辑 Google Cloud CLI 属性。

## `gcloud config set`

[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) 用于设置 Google Cloud CLI 的默认属性。

```bash
# 设置登录账户
gcloud config set account $YOUR_ACCOUNT
# 设置默认项目
gcloud config set project $PROJECT_ID
# 设置默认 region (zone 同理)
gcloud config set compute/region $REGION
```

## `gcloud config get`

[`gcloud config get`](https://docs.cloud.google.com/sdk/gcloud/reference/config/get) 用于获取一个 Google Cloud CLI 默认属性值。

```bash
# 查看默认 region (zone 同理)
gcloud config get-value compute/region
# 查看默认项目 ID
gcloud config get-value project
```

## `gcloud config list`

[`gcloud config list`](https://docs.cloud.google.com/sdk/gcloud/reference/config/list) 列出 Google Cloud CLI 的默认属性。

```bash
gcloud config list [SECTION/PROPERTY] [Flags]
# 列出当前项目
gcloud config list project
```

# `gcloud services`

[`gcloud services`](https://docs.cloud.google.com/sdk/gcloud/reference/services) 用于管理 API 和服务。

## `gcloud services enable` 

[`gcloud services enable`](https://docs.cloud.google.com/sdk/gcloud/reference/services/enable) 用于为 project 启用 API 和服务。

```bash
gcloud services enable $API

# 为默认项目启用 API（可同时启用多个）
gcloud services enable compute.googleapis.com

# 强制为默认项目停用 API（可同时停用多个）
gcloud services disable compute.googleapis.com container.googleapis.com --force
```

# GCP Bare Metal

[**Bare Metal**](https://cloud.google.com/bare-metal/docs/bms-setup?hl=zh-cn)（裸金属）是指未经虚拟化的物理服务器，即裸机。在裸金属服务器上运行的操作系统直接安装在物理硬件上，而不是在虚拟化层上运行。

## 准备工作

- Google Cloud 控制台中的项目选择器页面上创建项目，并启用 API。

- [创建 VPC 网络](https://cloud.google.com/vpc/docs/create-modify-vpc-networks?hl=zh-cn#gcloud)

  ```bash
  # 创建
  gcloud compute networks create $VPC_NETWORK_NAME \
      --subnet-mode=auto \
      --bgp-routing-mode=$DYNAMIC_ROUTING_MODE \
      --mtu=$MTU
  
  # 删除
  gcloud compute networks delete $VPC_NETWORK_NAME
  ```

  ```bash
  # EG
  gcloud compute networks create my-vpc-network-1 \
      --subnet-mode=auto \
      --bgp-routing-mode=global \
      --mtu=1460
  ```

## 创建 VLAN 连接

- 按照以下步骤为 Cloud Interconnect 连接[创建 VLAN 连接](https://cloud.google.com/bare-metal/docs/bms-setup?hl=zh-cn#bms-vlan-attachments)

- 创建两个 Cloud Router 实例

  ```bash
  gcloud compute routers create $ROUTER_NAME \
      --network $VPC_NETWORK_NAME \
      --asn 16550 \
      --region $REGION
  ```

  ```bash
  # EG
  gcloud compute routers create my-router-1 \
      --network my-vpc-network-1 \
      --asn 16550 \
      --region us-central1
  
  gcloud compute routers create my-router-2 \
      --network my-vpc-network-1 \
      --asn 16550 \
      --region us-central1
  ```

- 创建两个 `InterconnectAttachment`

  ```bash
  # 创建
  gcloud compute interconnects attachments partner create $ATTACHMENT_NAME \
      --region $REGION \
      --router $ROUTER_NAME \
      --edge-availability-domain availability-domain-1 \
      --edge-availability-domain $AVAILABILITY_DOMAIN \
      --admin-enabled
  
  # 删除
  gcloud compute interconnects attachments delete $ATTACHMENT_NAME --region=us-central1
  ```

  ```bash
  # EG
  gcloud compute interconnects attachments partner create my-attachment-1 \
      --region us-central1 \
      --router my-router-1 \
      --edge-availability-domain availability-domain-1 \
      --admin-enabled
  
  gcloud compute interconnects attachments partner create my-attachment-2 \
      --region us-central1 \
      --router my-router-2 \
      --edge-availability-domain availability-domain-2 \
      --admin-enabled
  ```

- 描述连接，以检索其配对密钥。您在打开更改请求以创建与裸金属解决方案环境的连接后，将与 Google Cloud 共享密钥。

  ```bash
  gcloud compute interconnects attachments describe my-attachment-1 \
      --region us-central1
  
  gcloud compute interconnects attachments describe my-attachment-2 \
  	--region us-central1
  ```

- 激活 VLAN 连接

  ```bash
  gcloud compute interconnects attachments partner update $ATTACHMENT_NAME \
      --region $REGION \
      --admin-enabled
  ```

  ```bash
  # EG
  gcloud compute interconnects attachments partner update my-attachment-1 \
      --region us-central1 \
      --admin-enabled
  
  gcloud compute interconnects attachments partner update my-attachment-2 \
      --region us-central1 \
      --admin-enabled
  ```

- 至此仍为：`state: PENDING_PARTNER`，实际应为 `INACTIVE` 或 `ACTIVE`
