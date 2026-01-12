---
title: gcp-gcloud-cli
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - cloud-computing
  - gcp
  - cli
---

# Overview

[**Google Cloud SDK**](https://docs.cloud.google.com/sdk/docs/overview?hl=zh-cn) 是一套用于与Google Cloud 服务交互的库和工具。它包括命令行工具、特定于语言的客户端库、IDE 扩展程序和模拟器，可帮助您在 Google Cloud上管理资源和自动执行任务。

[**Google Cloud CLI**](https://cloud.google.com/sdk/gcloud?hl=zh-cn) 是 Google Cloud 的命令行工具。

# Install

> [安装 Google Cloud CLI](https://docs.cloud.google.com/sdk/docs/install-sdk?hl=zh-cn)

## Windows

- 下载并安装 [Google Cloud CLI](https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe)

  - 保留 `Bundled Python`，否则 Gcloud SDK Shell 会出现警告信息

  - 安装之后会出现 Gcloud SDK Shell 应用

  - 关闭 Gcloud SDK Shell 和全部 Terminal，重新打开 Windows Terminal。

  - 使用 Windows Terminal 执行 `gcloud` 命令

- 验证安装

  ```bash
  gcloud version
  ```

- 初始化 Gcloud CLI

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

## Linux

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

# Uninstall

- [卸载 Google Cloud CLI](https://cloud.google.com/sdk/docs/uninstall-cloud-sdk)

- 以下两个命令需要在 **Gcloud CLI** 或 **CMD** 中执行

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

# Authorize

## 为 Gcloud CLI 授权

[安装 Gcloud CLI](gcp-gcloud-cli.md#Install) 以后，执行 `gcloud init` 命令。

## 为 Kubectl 授权

具体写入的内容包括：

- **集群凭据 (Credentials)：** 包含用于身份验证的访问令牌（Access Token）或证书。
- **集群端点 (Endpoint)：** 集群控制平面的公网或内网 IP 地址。
- **上下文 (Context)：** 将集群、用户和命名空间绑定在一起的一个配置名称。

```bash
gcloud container clusters get-credentials $CLUSTER_NAME \
    --location $LOCATION \
    --project $PROJECT_ID
```

```bash
gcloud container clusters get-credentials my-cluster \
    --location asia-east2 \
    --project project-60addf72-be9c-4c26-8db
```

## 为应用授权

其它应用程序（如 Terraform）交互 GCP 时，需先授权：

```bash
gcloud auth application-default login
```

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

## `gcloud services enable` 

[`gcloud services enable`](https://docs.cloud.google.com/sdk/gcloud/reference/services/enable) 用于为 project 启用 API 和服务。

```bash
gcloud services enable $API

# 为默认项目启用 API（可同时启用多个）
gcloud services enable compute.googleapis.com

# 强制为默认项目停用 API（可同时停用多个）
gcloud services disable compute.googleapis.com container.googleapis.com --force
```
