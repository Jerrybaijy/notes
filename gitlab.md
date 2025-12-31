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

# Repo

## 创建远程 GitLab 仓库

GitLab 网页创建 Remote Repo

- 仓库名填写本地项目目录名称 `FOLDER_NAME`，保证本地文件夹和远程仓库同名，便于管理；
- `Project name` 和 `Project slug` 都填写小写连字符文件名；
- `Visibility Level` 选 `Public`；
- 不要在这里创建 `README.md`，否则本地无法直接 `push`；

## 存储库限制

- [GitLab 官方关于存储库大小的限制](https://docs.gitlab.com/ee/user/gitlab_com/#account-and-limit-settings)

# GitLab CI/CD

[**GitLab CI/CD**](https://docs.gitlab.com/topics/build_your_application/) 是 GitLab 提供的**一体化工具**，在代码提交时根据 `.gitlab-ci.yml` 文件触发 **Pipeline**，自动执行 CI/CD 流程。

> [CI/CD YAML 语法（个人）](<gitlab-ci-cd-yaml.md>)
>
> [CI/CD YAML syntax reference](https://docs.gitlab.com/ci/yaml/)
>
> [CI/CD YAML 语法参考（极狐）](https://docs.gitlab.cn/docs/jh/ci/yaml/)

## Pipeline

[**Pipeline**](https://docs.gitlab.com/ci/pipelines/)（流水线）是 GitLab CI/CD 的基础组件，由一系列 Stages 和 Jobs 组成，通过 YAML 关键字在 `.gitlab-ci.yml` 文件中进行配置。

**Pipeline 运行流程**：

- 代码提交
- GitLab 触发 Pipeline
- Runner 拉取代码并执行 Job
- 每个阶段按顺序执行
- 生成构建产物或部署代码

## Stage

**Stage**（阶段）是 Pipeline 的逻辑分组点，它按顺序（从上到下）执行，包含一组 Job。

## Job

[**Job**](https://docs.gitlab.com/ci/jobs/)（作业）是 Pipeline 的基础组成部分，用于完成构建、测试或部署代码等任务，通过 YAML 关键字在 `.gitlab-ci.yml` 文件中进行配置。

- 每个 Stage 包含多个 Job，代表具体的任务。
- 默认情况下，同一个 Stage 内的多个 Job 同时执行。
- Job 有三种执行结果：
  - Passed
  - Failed
  - Skipped


## `.gitlab-ci.yml`

`.gitlab-ci.yml` 用于定义 Pipeline 的所有**阶段**、**作业**及其执行逻辑。GitLab CI/CD 系统会默认在仓库的根目录查找这个文件，并将其作为 CI/CD 流水线的配置文件。

```yaml
# 定义变量
variables:
  # <Variable_NAME>: <Variable_VALUE>
  DOCKER_VERSION: 24.0.5

# 定义阶段（stages）
stages:
  # 阶段1
  - build
  # 阶段2
  - chart-publish

# 定义作业（jobs）
build_backend:
  # 当前作业所属阶段
  stage: build
  
  # 当前作业执行的脚本
  script:
    # 脚本内容

# 定义作业（jobs）
build_frontend:
  stage: build
  script:
    # 脚本内容

# 定义作业（jobs）
publish_chart:
  stage: chart-publish
  script:
    # 脚本内容
```

## Variable

[**Variable**](https://docs.gitlab.com/ci/variables/)

- [预定义变量](https://docs.gitlab.com/ci/variables/predefined_variables/)
- [自定义变量](https://docs.gitlab.com/ci/yaml/#variables)：详见 [variables](#variables)

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
  - DOCKER_HUB_TOKEN: Docker Hub 的 **Access Token**

- 推送至 GitLab
  - 将项目文件推送至 GitLab 仓库
  - GitLab 在 Pipeline 中自动生成 Image 并推送至 Docker Hub

- 推送至 Docker Hub 的 `.gitlab-ci.yml` 模板文件：

  >  此 `.gitlab-ci.yml` 模板文件源自于 [Todo Fullstack GitOps](todos-fullstack-gitops.md) 项目

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
    
    # 项目名称
    PROJECT_NAME: todo-fullstack-gitops
  
    # 后端和前端名称
    BACKEND_NAME: backend
    FRONTEND_NAME: frontend
    
    # 后端和前端目录
    BACKEND_DIR: backend
    FRONTEND_DIR: frontend
  
  # 定义阶段
  stages:
    - build
  
  # 使用 Docker-in-Docker 服务，允许在容器里运行 docker 命令
  services:
    - docker:$DOCKER_VERSION-dind
  
  # 登录 Docker Hub
  before_script:
    # 使用 stdin 输入密码，更加安全
    - echo "$DOCKER_HUB_TOKEN" | docker login -u "$DOCKER_HUB_USER" --password-stdin
  
  # 构建后端镜像
  build_backend:
    stage: build
    image: docker:$DOCKER_VERSION
    script:
      # 进入后端目录
      - cd $BACKEND_DIR
      
      # 使用双标签构建：既有版本号（用于回溯），也有 latest（用于生产）
      - docker build -t $IMAGE_PREFIX/$PROJECT_NAME-$BACKEND_NAME:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/$PROJECT_NAME-$BACKEND_NAME:latest .
      
      # 推送到 Docker Hub
      - docker push $IMAGE_PREFIX/$PROJECT_NAME-$BACKEND_NAME:$CI_COMMIT_SHORT_SHA
      - docker push $IMAGE_PREFIX/$PROJECT_NAME-$BACKEND_NAME:latest
    rules:
      # 只有当 $BACKEND_NAME 目录下有文件变化时，才运行此 Job
      - changes:
          - $BACKEND_DIR/**/*
  
  # 构建前端镜像
  build_frontend:
    stage: build
    image: docker:$DOCKER_VERSION
    script:
      - cd $FRONTEND_DIR
      - docker build -t $IMAGE_PREFIX/$PROJECT_NAME-$FRONTEND_NAME:$CI_COMMIT_SHORT_SHA -t $IMAGE_PREFIX/$PROJECT_NAME-$FRONTEND_NAME:latest .
      - docker push $IMAGE_PREFIX/$PROJECT_NAME-$FRONTEND_NAME:$CI_COMMIT_SHORT_SHA
      - docker push $IMAGE_PREFIX/$PROJECT_NAME-$FRONTEND_NAME:latest
    rules:
      - changes:
          - $FRONTEND_DIR/**/*
  ```

- 相关项目

  - [Todo Fullstack GitOps](todos-fullstack-gitops.md)
  - GitLab CI Image

# GitLab Personal Access Tokens

这是用户级别的 Token，用于在系统内登录账户：

- 右上角个人头像 > `Edit profile` > 左侧边栏 `Personal access tokens` > `Add new token`
- 名称随意
- 尽可能给予最大权限
- 日期尽可能调整到最长（一年）
- Generate 生成 token
- 请务必保存生成的 token，它只显示一次！
- 用户名为 `jerrybai`

# Project Access Tokens

这是项目级别的 Token，用于将各类资源（如 OCI 制品）推送至 GitLab Container Registry：

- 进入项目 > 左侧边栏 `Settings | Access tokens` > `Add new token`
- 名称随意（尽可能写项目名称）
- 按需勾选权限，如 OCI 制品，就勾选 `read_registry` 和 `write_registry` 权限
- 日期尽可能调整到最长（一年）
- `Create project access token`
- 请务必保存生成的 token，它只显示一次！
- 用户名为 `jerrybai`

# GitLab Container Registry

**GitLab Container Registry** 是 GitLab 的镜像仓库，兼容 OCI 标准。每个项目有各自的项目级仓库。

- **公共 GitLab.com：** `registry.gitlab.com`
- **自建/私有 GitLab：** 您的实例地址，例如 `gitlab.example.com:4567`

**如何查看**：进入项目 > 左侧边栏 > `Deploy` > `Container registry`

`<oci-registry>` 格式：比[标准 `<oci-registry>`](it-basics.md#oci-registry) 多了 `<project-name>`

```
oci://<registry>/<namespace>/<project-name>
oci://registry.gitlab.com/jerrybai/todo-fullstack-gitops
```

# 解决办法

## 远程仓库改名

- **改名**：右上角三个点 > `Project settings` > `Project name`
- **改地址**：`Advanced` > `Change path`
- **本地仓库**：移除旧仓库，重新添加远程地址，重新关联 `main` 分支。