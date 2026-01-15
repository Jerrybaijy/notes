---
title: gcp-gce
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - cloud-computing
  - gcp
---

# Overview

[**GCE**](https://docs.cloud.google.com/compute/docs/overview) (Google Compute Engine)，是一种计算和托管服务，可让您在 Google 基础架构上创建并运行虚拟机。

> [GCE Docs](https://docs.cloud.google.com/compute/docs)
>
> [GCE Instance](https://console.cloud.google.com/comput)

# Quickstart

## 准备工作

- [GCP 准备工作](<gcp.md#准备工作>)已完成
- [GCP project](<gcp-project.md#Quickstart>) 已创建

## 创建 GCE

```bash
gcloud compute instances create my-gce \
  --machine-type=e2-medium \
  --image-project=ubuntu-os-cloud \
  --image-family=ubuntu-2404-lts-amd64 \
  --metadata=ssh-keys='Ubuntu:${PUBLIC_KEY}'
```

## 连接 GCE

使用 [OpenSSH](openssh.md#quickstart) 连接 GCE

```bash
ssh -i ~/.ssh/my_secret_key Jerry@34.92.115.81
```

## 删除 GCE

```bash
gcloud compute instances delete my-gce
```

# 创建 GCE

## 使用 Gcloud CLI 创建 GCE

- [准备工作](<#准备工作>)已完成

- 开启 GCE 必需 API

  ```bash
  gcloud services enable $APIs
  gcloud services enable compute.googleapis.com
  ```

- 创建 GCE

  ```bash
  # 创建基础 GCE 实例
  gcloud compute instances create $GCE_NAME \
    --machine-type=e2-medium \
    --image-project=ubuntu-os-cloud \
    --image-family=ubuntu-2404-lts-amd64 \
    --metadata=ssh-keys='${SYSTEM_USERNAME}:${PUBLIC_KEY}'
   
  gcloud compute instances create my-gce \
    --machine-type=e2-medium \
    --image-project=ubuntu-os-cloud \
    --image-family=ubuntu-2404-lts-amd64 \
    --metadata=ssh-keys='Ubuntu:${PUBLIC_KEY}'
  
  # 查看 GCE 实例
  gcloud compute instances list
  ```

  **在以上代码中**：

  - [`ssh-keys`](openssh.md#Quickstart)：
    - 传入 SSH 连接的公钥
    - 同时会创建一个 `SYSTEM_USER_NAME` 用户，可通过 SSH 连接，使用这个账户与 GCE 实例交互。
  - 生成的实例命令提示符为：`Ubuntu@my-gce`

## 使用 Terraform 创建 GCE

