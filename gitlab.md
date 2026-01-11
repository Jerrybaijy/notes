---
title: gitlab
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - git
  - ci-cd
---

# Overview

> [GitLab Docs](https://docs.gitlab.com/)
>
> [GitLab 文档（极狐）](https://docs.gitlab.cn/docs/jh/user/get_started/)
>
> [CI/CD YAML syntax reference](https://docs.gitlab.com/ci/yaml/)
>
> [CI/CD YAML 语法参考（极狐）](https://docs.gitlab.cn/docs/jh/ci/yaml/)

# Code Repo

## 创建远程 GitLab 仓库

GitLab 网页创建 Code Repo

- 仓库名填写本地项目目录名称 `FOLDER_NAME`，保证本地文件夹和远程仓库同名，便于管理；
- `Project name` 和 `Project slug` 都填写小写连字符文件名；
- `Visibility Level` 选 `Public`；
- 不要在这里创建 `README.md`，否则本地无法直接 `push`；

## 存储库限制

- [GitLab 官方关于存储库大小的限制](https://docs.gitlab.com/ee/user/gitlab_com/#account-and-limit-settings)

## 远程仓库改名

- **改名**：右上角三个点 > `Project settings` > `Project name`
- **改地址**：`Advanced` > `Change path`
- **本地仓库**：移除旧仓库，重新添加远程地址，重新关联 `main` 分支。

# GitLab Tokens

## Personal Access Tokens

这是用户级别的 Token，用于在系统内登录账户：

- 右上角个人头像 > `Edit profile` > 左侧边栏 `Personal access tokens` > `Add new token`
- 名称随意
- 尽可能给予最大权限
- 日期尽可能调整到最长（一年）
- Generate 生成 token
- 请务必保存生成的 token，它只显示一次！
- 用户名为 `jerrybai`

## Project Access Tokens

这是项目级别的 Token，用于将各类资源（如 OCI 制品）推送至 GitLab Container Registry：

- 进入项目 > 左侧边栏 `Settings | Access tokens` > `Add new token`
- 名称随意（尽可能写项目名称）
- 按需勾选权限，如 OCI 制品，就勾选 `read_registry` 和 `write_registry` 权限
- 日期尽可能调整到最长（一年）
- `Create project access token`
- 请务必保存生成的 token，它只显示一次！
- 用户名为 `jerrybai`
