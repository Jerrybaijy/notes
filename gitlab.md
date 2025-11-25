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

# GitLab CI/CD

**GitLab CI/CD** 是 GitLab 内置的 **CI/CD** 工具。

## 配置环境变量

在配置文件中可能需要某些敏感信息（如密码），可在文件中使用 `$VARIABLE_NAME` 代替，在托管平台中设置这个变量信息，然后在 Pipeline 执行配置文件时，平台会自动处理。

- 进入**项目设置**页面
- 左下角 `Settings` > `CI/CD`
- 选择 `Variables` > `Add variables`
  - 不要选择 `Protect variable` 选项，否则在非 main 分支无法完成 CI。
  - 添加敏感变量（如密码）注意一定要选择 `Masked variable` 选项，否则在 log 日志时会打印出来。

## 推送至 Docker Hub

- 目的是在将文件 push 到 Gitlab 时，通过 Pipeline 自动生成 Image 并推送到 Dockerhub。

- 创建 `Dockerfile` 和 `.gitlab-ci.yml` 文件。

  - 项目根目录创建 `.gitlab-ci.yml` 文件。
  - 前/后端目录创建 `Dockerfile` 文件。

- 在 Docker Hub 创建 Access Token，详见 Docker Hub 笔记。

- 在 GitLab 配置环境变量。
  - DOCKER_HUB_USER: jerrybaijy
  - DOCKER_HUB_PASS: Docker Hub 的 **Access Token**

- 推送至 GitLab
  - 将项目文件推送至 GitLab 仓库
  - GitLab 在 Pipeline 中自动生成 Image 并推送至 Docker Hub

- 推送至 Docker Hub 的 `.gitlab-ci.yml` 模板文件：

  >  此 `.gitlab-ci.yml` 模板文件源自于 [Todos React Flask MySQL Fullstack](todos-react-flask-mysql-fullstack.md) 项目

  ```yaml
  # 定义变量
  variables:
    # Docker 版本号
    DOCKER_VERSION: 24.0.5
  
    # 告诉 Docker 使用 overlay2 驱动，性能更好
    DOCKER_DRIVER: overlay2
  
    # 禁用 TLS 证书生成，防止 dind 连接报错
    DOCKER_TLS_CERTDIR: ""
    
    # 镜像名称前缀，$DOCKER_HUB_USER 是 GitLab 里配置的环境变量
    IMAGE_PREFIX: $DOCKER_HUB_USER
    
    # 后端和前端名称
    BACKEND_NAME: todos-react-flask-mysql-backend
    FRONTEND_NAME: todos-react-flask-mysql-frontend
  
  # 定义阶段
  stages:
    - build
  
  # 使用 Docker-in-Docker 服务，允许在容器里运行 docker 命令
  services:
    - docker:$DOCKER_VERSION-dind
  
  # 登录 Docker Hub
  before_script:
    # 使用 stdin 输入密码，更加安全
    - echo "$DOCKER_HUB_PASS" | docker login -u "$DOCKER_HUB_USER" --password-stdin
  
  build_backend:
    stage: build
    image: docker:$DOCKER_VERSION
    script:
      # 进入后端目录
      - cd $BACKEND_NAME
      
      # 使用双标签构建：既有版本号（用于回溯），也有 latest（用于生产）
      - docker build -t $IMAGE_PREFIX/$BACKEND_NAME:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/$BACKEND_NAME:latest .
      
      # 推送到 Docker Hub
      - docker push $IMAGE_PREFIX/$BACKEND_NAME:$CI_COMMIT_SHORT_SHA
      - docker push $IMAGE_PREFIX/$BACKEND_NAME:latest
    rules:
      # 只有当 $BACKEND_NAME 目录下有文件变化时，才运行此 Job
      - changes:
          - $BACKEND_NAME/**/*
  
  build_frontend:
    stage: build
    image: docker:$DOCKER_VERSION
    script:
      - cd $FRONTEND_NAME
      - docker build -t $IMAGE_PREFIX/$FRONTEND_NAME:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/$FRONTEND_NAME:latest .
      - docker push $IMAGE_PREFIX/$FRONTEND_NAME:$CI_COMMIT_SHORT_SHA
      - docker push $IMAGE_PREFIX/$FRONTEND_NAME:latest
    rules:
      - changes:
          - $FRONTEND_NAME/**/*
  ```

- 相关项目

  - [Todo React Flask MySQL Fullstack](todos-react-flask-mysql-fullstack.md)
  - GitLab CI Image


## `.gitlab-ci.yml`

- 核心配置文件，位于项目的根目录。
- 用于定义 CI/CD 流程，包括构建、测试、部署等步骤。

## Pipeline

- 一个完整的 CI/CD 流程，包含多个 **阶段（stages）**，如 `build`、`test`、`deploy`。
- 每次代码提交或合并请求时，GitLab 会自动触发 Pipeline。

## Pipeline 运行流程

- 代码提交
- GitLab 触发 Pipeline
- Runner 拉取代码并执行 Job
- 每个阶段按顺序执行
- 生成构建产物或部署代码

## Stages

- Pipeline 中的阶段，按顺序依次执行。常见的阶段有：
  - `build`：代码构建。
  - `test`：运行测试。
  - `deploy`：部署到指定环境。

## Jobs

- 每个阶段包含多个 Job，代表具体的任务。
- 每个 Job 都在独立的环境中执行（如 Docker 容器）。

## Runner

- 执行 CI/CD 任务的代理。
- 两种类型
  - **Shared Runner**：由 GitLab 提供，适合公共项目。
  - **Specific Runner**：自建 Runner，适合私有项目或自定义环境。

# 解决办法

## 远程仓库改名

- **改名**：右上角三个点 > `Project settings` > `Project name`
- **改地址**：`Advanced` > `Change path`
- **本地仓库**：移除旧仓库，重新添加远程地址，重新关联 `main` 分支。