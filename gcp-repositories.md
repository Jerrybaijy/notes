---
title: gcp-repositories
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
  - cloud-computing
  - gcp
  - repo
---

# Overview

[**Repositories**](https://console.cloud.google.com/cloud-build/repositories) 用于链接到其它代码托管平台（如 GitHub）。

[Cloud Build Repositories (2nd gen)](https://docs.cloud.google.com/build/docs/repositories?hl=zh-cn#2nd-gen-repos) 是 Google Cloud Build 目前推荐的源代码连接方式。

> [Repositories Docs](https://docs.cloud.google.com/build/docs/repositories)

链接到源代码仓库的两种方式：

- [Developer Connect](https://docs.cloud.google.com/build/docs/repositories?hl=zh-cn#dc-repo)
- [Cloud Build repositories (2nd gen)](https://docs.cloud.google.com/build/docs/repositories?hl=zh-cn#2nd-gen-repos)（推荐）

# Quick Start

# Connect to GitLab

分三步连接到 GitLab：

1. [Connect to a GitLab Host](#Connect to a GitLab Host)
2. [Connect to a GitLab Repository](#Connect to a GitLab Repository)
3. [Build Repositories from GitLab](#Build Repositories from GitLab)

## Connect to a GitLab Host

> [Connect to a GitLab host](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/connect-host-gitlab)

- [启用相关 APIs](https://console.cloud.google.com/apis/enableflow;apiid=cloudbuild.googleapis.com,secretmanager.googleapis.com;redirect=https:%2F%2Fcloud.google.com%2Fbuild%2Fdocs%2Fautomating-builds%2Fgitlab%2Fconnect-host-gitlab)

  - Cloud Build API
  - Secret Manager API

- 创建两个 GitLab [Personal Access Tokens](https://gitlab.com/-/user_settings/personal_access_tokens)

  - 具有 `api` 范围的访问令牌，用于与代码库建立连接和断开连接。
  - 具有 `read_api` 范围的访问令牌，Cloud Build 触发器使用此令牌访问代码库中的源代码。

- 打开 [Repositories](https://console.cloud.google.com/cloud-build/repositories/2nd-gen) 页面

- 在顶部栏的项目选择器中，选择您的 Google Cloud 项目。

- 选择 `2nd gen` 标签页。

- `Create host connection` > `GitLab`

  - **Region**：项目区域
  - **Name**：连接名称
  - **Host details**：`GitLab.com`
  - **Personal access tokens**：分别对应填写此前创建的两个令牌

- 点击 `Connect`

  点击 `Connect` 按钮后，您的个人访问令牌会安全地存储在 [Secret Manager](https://docs.cloud.google.com/secret-manager/docs/overview?hl=zh-cn) 中。建立主机连接后，Cloud Build 还会代表您创建网络钩子密钥。您可以在 [Secret Manager 页面](https://console.cloud.google.com/security/secret-manager?hl=zh-cn)上查看和管理 Secret。

- [轮换旧的或过期的 GitLab 访问令牌](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/connect-host-gitlab?hl=zh-cn#rotate-token)

## Connect to a GitLab Repository

> [Connect to a GitLab Repository](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/connect-repo-gitlab)

- [启用相关 APIs](https://console.cloud.google.com/apis/enableflow;apiid=cloudbuild.googleapis.com,secretmanager.googleapis.com;redirect=https:%2F%2Fcloud.google.com%2Fbuild%2Fdocs%2Fautomating-builds%2Fgitlab%2Fconnect-host-gitlab)
  - Cloud Build API
  - Secret Manager API
- 打开 [Repositories](https://console.cloud.google.com/cloud-build/repositories/2nd-gen) 页面
- 在顶部栏的项目选择器中，选择您的 Google Cloud 项目。
- 选择 `2nd gen` 标签页。
- 点击 `Link repository`
  - **Connection**：连接的 GitLab host
  - **Repositories**：GitLab 的代码仓库
  - **Repositories name**：可选择 `Generated` 自动生成
- 点击 `Link`，将代码库与连接相关联。

## Build Repositories from GitLab

> [Build Repositories from GitLab](https://docs.cloud.google.com/build/docs/automating-builds/gitlab/build-repos-from-gitlab)

- [启用相关 APIs](https://console.cloud.google.com/apis/enableflow;apiid=cloudbuild.googleapis.com,secretmanager.googleapis.com;redirect=https:%2F%2Fcloud.google.com%2Fbuild%2Fdocs%2Fautomating-builds%2Fgitlab%2Fconnect-host-gitlab)
  - Cloud Build API
  - Secret Manager API
- 打开 [Repositories](https://console.cloud.google.com/cloud-build/repositories/2nd-gen) 页面
