---
title: gcp
author: Jerry.Baijy
tags:
  - 应用科学
  - it
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

## 资源范围

[GCP 资源范围](https://docs.cloud.google.com/docs/overview?hl=zh-cn#global_regional_and_zonal_resources)：

- **全球资源**：可以由跨区域和地区的其他任何资源访问的资源，包括预配置的磁盘映像、磁盘快照和网络。
- **区域资源**：只能由同一区域内的资源访问的资源，包括静态外部 IP 地址。
- **地区资源**：只能由同一地区内的资源访问的资源，包括虚拟机实例、机器类型和磁盘。

下图显示了全球范围、地区和区域及其部分资源之间的关系：

![regions-zones](assets/regions-zones.svg)

## 交互方式

Google Cloud 为您提供了三种与服务和资源[交互的基本方式](https://docs.cloud.google.com/docs/overview?hl=zh-cn#ways_to_interact_with_the_services)。

- [Google Cloud console](https://console.cloud.google.com/?hl=zh-cn) 提供基于 Web 的图形界面
- 命令行界面
  - [Google Cloud CLI](https://docs.cloud.google.com/sdk/gcloud)
  - [Cloud Shell](https://docs.cloud.google.com/shell/docs/features?hl=zh-cn)
- [客户端库](https://docs.cloud.google.com/sdk/cloud-client-libraries?hl=zh-cn)

# Google Cloud SDK

[**Google Cloud SDK**](https://docs.cloud.google.com/sdk/docs/overview?hl=zh-cn) 是一套用于与Google Cloud 服务交互的库和工具。它包括命令行工具、特定于语言的客户端库、IDE 扩展程序和模拟器，可帮助您在 Google Cloud上管理资源和自动执行任务。

# Google Cloud CLI

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

# GCP Config

## Config Overview

## Config Preference

> [Config Preference](https://docs.cloud.google.com/sdk/gcloud/reference/config)

[`gcloud config`](https://docs.cloud.google.com/sdk/gcloud/reference/config) 用于查看和编辑 Google Cloud CLI 属性。

### `gcloud config set`

[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) 用于设置 Google Cloud CLI 属性。

```bash
# 设置登录账户
gcloud config set account $YOUR_ACCOUNT
# 设置项目
gcloud config set project $PROJECT_ID
```

### `gcloud config get`

[`gcloud config get`](https://docs.cloud.google.com/sdk/gcloud/reference/config/get) 用于获取一个 Google Cloud CLI 属性值。

```bash
# 查看当前区域
gcloud config get-value compute/region
# 查看当前项目ID
gcloud config get-value project
```

### `gcloud config list`

[`gcloud config list`](https://docs.cloud.google.com/sdk/gcloud/reference/config/list) 列出 Google Cloud CLI 属性的当前活跃配置。

```bash
gcloud config list [SECTION/PROPERTY] [Flags]
# 列出当前项目
gcloud config list project
```

# GCP Projects

## Projects Overview

分配和使用的任何 Google Cloud 资源都必须属于一个[**项目**](https://docs.cloud.google.com/docs/overview?hl=zh-cn#projects)。除您使用[共享 VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc?hl=zh-cn) 或 [VPC 网络对等互连](https://docs.cloud.google.com/vpc/docs/vpc-peering?hl=zh-cn)，否则一个项目无法访问其他项目的资源。

每个 Google Cloud 项目都具有以下内容：

- 项目名称，由您提供。
- 项目 ID，您可以提供或 Google Cloud 可以为您提供。
- 项目编号，由 Google Cloud 提供。

## Projects Preference

> [Projects Preference](https://docs.cloud.google.com/sdk/gcloud/reference/projects)

```bash
# 列出所有项目
gcloud projects list
# 删除项目
gcloud projects delete $PROJECT_ID
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
