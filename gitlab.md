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

# GitLab

## GitLab 基础

## 创建远程 GitLab 仓库

GitLab 网页创建 Remote Repo

- 仓库名填写本地文件夹名称 `FOLDER_NAME`，保证本地文件夹和远程仓库同名，便于管理；
- `Project name` 和 `Project slug` 都填写小写连字符文件名；
- `Visibility Level` 选 `Public`；
- 不要在这里创建 `README.md`，否则本地无法直接 `push`；

## 存储库限制

- [GitLab 官方关于存储库大小的限制](https://docs.gitlab.com/ee/user/gitlab_com/#account-and-limit-settings)

# GitLab CI

**GitLab CI/CD** 是 GitLab 内置的 **CI/CD** 工具。

## 配置环境变量

在配置文件中可能需要某些敏感信息（如密码），可在文件中使用 `$VARIABLE_NAME` 代替，在托管平台中设置这个变量信息，然后在 Pipeline 执行配置文件时，平台会自动处理。

- 进入项目设置页面
- 左下角 `Settings` > `CI/CD`
- 选择 `Variables` > `添加变量信息`
  - 不要选择 `Protect variable` 选项，否则在非 main 分支无法完成 CI。
  - 注意一定要选择 `Masked variable` 选项，否则在 log 日志时会打印出来。

## 推送至 Docker Hub

- 项目根目录创建 `Dockerfile` 和 `.gitlab-ci.yml` 文件。
- 在 Docker Hub 创建 Access Token，详见 Docker Hub 笔记。
- 在 GitLab 配置环境变量。
  - DOCKER_HUB_USER: jerrybaijy
  - DOCKER_HUB_PASS: Docker Hub 的 **Access Token**
- 推送至 GitLab

  - 将项目文件推送至 GitLab 仓库
  - GitLab 在 Pipeline 中自动生成 Image 并推送至 Docker Hub

## `.gitlab-ci.yml`