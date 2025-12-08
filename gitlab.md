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

> [GitLab Docs](https://docs.gitlab.com/)
>
> [GitLab 文档（极狐）](https://docs.gitlab.cn/docs/jh/user/get_started/)

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

**GitLab CI/CD** 是 GitLab 提供的**一体化工具**，在代码提交时根据 `.gitlab-ci.yml` 文件触发 **Pipeline**，自动执行 CI/CD 流程。

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

# CI/CD YAML 语法

> [CI/CD YAML syntax reference](https://docs.gitlab.com/ci/yaml/)
>
> [CI/CD YAML 语法参考（极狐）](https://docs.gitlab.cn/docs/jh/ci/yaml/)

## Keywords

[**Keywords**](https://docs.gitlab.com/ci/yaml/#keywords) 用于配置 Pipeline，包括：

- [Global keywords](https://docs.gitlab.com/ci/yaml/#global-keywords): 如 `stages`
- [Header keywords](https://docs.gitlab.com/ci/yaml/#header-keywords): 如 `spec`
- [Job keywords](https://docs.gitlab.com/ci/yaml/#job-keywords): 如 `script`

## `stages`

[`stages`](https://docs.gitlab.com/ci/yaml/#stages) 关键字用于包含一组 `jobs`，所有定义的 `stage` 按顺序依次执行。常见的阶段有：

- `build`：代码构建。
- `test`：运行测试。
- `deploy`：部署到指定环境。

## `needs`

[`needs`](https://docs.gitlab.com/ci/yaml/#needs) 关键字可以为当前作业指定依赖作业，是依赖条件。

- 指定作业顺序
- 指定作业结果依赖

### 基本实现

```yaml
publish_chart:
  needs:
    # 依赖作业
    - job: build_backend
  # 其它关键字
```

**在以上示例中**：

- 如果 build_backend 作业的结果为 **Passed**，可以执行 publish_chart 作业。
- 如果 build_backend 作业的结果为 **Failed** 或 **Skipped**，会直接跳过 publish_chart 作业，即结果为 **Skipped**。
- 同一个 `needs` 下的所有 `job` 在逻辑上是 `AND` 关系。

### `needs:optional`

[`needs:optional`](https://docs.gitlab.com/ci/yaml/#needsoptional) 描述用于指定是否允许依赖作业的结果为 **Skipped**。

```yaml
publish_chart:
  needs:
    # 依赖作业
    - job: build_backend
      # 可选描述
      optional: true
  # 其它关键字
```

**在以上示例中**：

- 如果 build_backend 作业的结果为 **Passed** 或 **Skipped**，都可以执行 publish_chart 作业。
- 如果 build_backend 作业的结果为 **Failed**，会直接跳过 publish_chart 作业，即结果为 **Skipped**。

## `rules`

[`rules`](https://docs.gitlab.com/ci/yaml/#rules) 关键字用于在 Pipeline 中包含或排除该作业，是触发条件。

### `rules:changes`

[`rules:changes`](https://docs.gitlab.com/ci/yaml/#ruleschanges) 关键字通过检查特定文件的更改来指定是否将改作业添加到管道。

```yaml
rules:
  - changes:
      - $CHART_DIR/**/*
  - changes:
      - $BACKEND_DIR/**/*
  - changes:
      - $FRONTEND_DIR/**/*
```

**在以上示例中**：

- 三个目录中的任一个有变化，都将该作业添加到管道。
- 同一个 `rules` 下的所有 `changes` 在逻辑上是 `OR` 关系。
- 如果当前作业有 `needs`，需同时满足

## `variables`

[`variables`](https://docs.gitlab.com/ci/yaml/#variables) **自定义变量**，用于存储**非敏感信息**。**敏感信息**应存储在 [受保护变量](https://docs.gitlab.cn/docs/jh/ci/variables/_index#protect-a-cicd-variable) 或 [CI/CD 密钥](https://docs.gitlab.cn/docs/jh/ci/secrets/_index) 中。

- [**Default variables**](https://docs.gitlab.com/ci/yaml/#default-variables)：即当前文档的全局变量
- [**Job variables**](https://docs.gitlab.com/ci/yaml/#job-variables)：即当前 Job 的变量

### 基本实现

**Default variables**:

```yaml
variables:
  # 完整写法
  BACKEND_NAME: 
    value: "backend"

  # 简洁写法
  FRONTEND_NAME: frontend
```

**Job variables**:

```yaml
script:
  - LATEST_VERSION="99.99.99-latest"
```

### 变量名和变量值

- 名称只能使用数字、字母和下划线。在某些 shell 中，第一个字符必须是字母。
- 值必须是字符串。

### 引用变量

在多数情况下，以下两种写法通用：

- `$VARIABLE_NAME`
- `${VARIABLE_NAME}`

```yaml
script:
  - cd $FRONTEND_DIR
```

```yaml
script:
  - cd ${FRONTEND_DIR}
```

特殊情况时，应该使用大括号形式：`${VARIABLE_NAME}`

- 字符串拼接
- 包含特殊字符

```yaml
script:
  - helm push ${CHART_NAME}-${SHA_VERSION}.tgz oci://${OCI_REGISTRY}
```

# GitLab Personal Access Tokens

- 右上角个人头像 > `Edit profile` > 左侧边栏 `Personal access tokens` > `Add new token`
- 名称随意（尽可能写项目名称）
- 勾选 `read_registry` 和 `write_registry` 权限
- 日期尽可能调整到最长（一年）
- Generate 生成 token
- 请务必保存生成的 Token，它只显示一次！
- 用户名为 `jerrybai`

# GitLab Registry

**GitLab Registry** 是 GitLab 的镜像仓库，可以存储 Docker Image, Helm Chart ...

- **公共 GitLab.com：** `registry.gitlab.com`
- **自建/私有 GitLab：** 您的实例地址，例如 `gitlab.example.com:4567`

**如何查看**：进入项目 > 左侧边栏 > `Deploy` > `Container registry`

**OCI 仓库地址：**

```bash
oci://<Registry_Host>/<Namespace>/<Repository_Name>
oci://registry.gitlab.com/jerrybai/todo-fullstack-gitops
```

- **`<Registry_Host>`**: **注册中心的主机名**，每个仓库平台固定，GitLab 是 `registry.gitlab.com`。
- **`<Namespace>`**: **命名空间**，通常是组织名、用户名或项目名。
- **`<Repository Name>`**: **仓库名称**，无需设置，在推送时自动生成，但最好和项目名保持一致。

# 解决办法

## 远程仓库改名

- **改名**：右上角三个点 > `Project settings` > `Project name`
- **改地址**：`Advanced` > `Change path`
- **本地仓库**：移除旧仓库，重新添加远程地址，重新关联 `main` 分支。