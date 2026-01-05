---
title: gcp-cloud-build
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
  - cloud-computing
  - gcp
---

# Overview

[**Cloud Build**](https://console.cloud.google.com/cloud-build) 是一项可在 GCP 基础设施上执行构建的服务。

> [Cloud Build Docs](https://docs.cloud.google.com/build/docs)

其它留存：

- [使用 Cloud Build 构建镜像](https://cloud.google.com/build/docs/build-push-docker-image?hl=zh-cn)
- [创建 Cloud Build 配置文件 (`cloudbuild.yaml`)](https://www.google.com/search?q=[https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration%3Fhl%3Dzh-cn](https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration%3Fhl%3Dzh-cn))
- [使用 Cloud Build 部署到 Kubernetes](https://www.google.com/search?q=https://cloud.google.com/build/docs/deploying-builds/deploy-gke%3Fhl%3Dzh-cn)

# Quickstart

- 启用 [Cloud Build API](https://console.cloud.google.com/marketplace/product/google/cloudbuild.googleapis.com?referrer=search&project=project-60addf72-be9c-4c26-8db&returnUrl=%2Fcloud-build%2Fbuilds%3Freferrer%3Dsearch%26project%3Dproject-60addf72-be9c-4c26-8db%26inv%3D%26invt%3DAcFoRQ)

- [将 Repositories 关联到 GitLab](gcp-repositories.md#GitLab)

- [创建 Docker Repository](<gcp-artifact-registry.md#创建 Docker Repository>)

- 给服务账号添加角色

  ```bash
  378042797368-compute@developer.gserviceaccount.com
  Artifact Registry Writer
  Logs Writer
  ```

- 编写 `cloudbuild.yaml`

- 推送源代码至 GitLab，触发 Cloud Build。

# Build 配置文件

>  [创建 Build 配置文件](https://docs.cloud.google.com/build/docs/configuring-builds/create-basic-configuration)

## `cloudbuild.yaml`

>  此文件源自 [Todo GCP](todo-gcp.md#`cloudbuild.yaml`) 项目

```yaml
steps:
  # 获取完整的 Git 历史，确保 HEAD^ 可用
  - name: "gcr.io/cloud-builders/git"
    id: "unshallow"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        git fetch --unshallow || true

  # 1. 构建并推送后端镜像
  - name: "gcr.io/cloud-builders/docker"
    id: "build-backend"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        # 检查 backend 目录在当前 commit 中是否有变动
        if git diff --quiet HEAD^ HEAD -- ${_BACKEND_DIR}; then
          echo "No changes in backend, skipping build."
        else
          echo "Changes detected, starting backend build..."
          cd ${_BACKEND_DIR} && \
          docker build -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:${SHORT_SHA} \
              -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:latest . && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:${SHORT_SHA} && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_BACKEND_NAME}:latest
        fi

  # 2. 构建并推送前端镜像
  - name: "gcr.io/cloud-builders/docker"
    id: "build-frontend"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        # 检查 frontend 目录在当前 commit 中是否有变动
        if git diff --quiet HEAD^ HEAD -- ${_FRONTEND_DIR}; then
          echo "No changes in frontend, skipping build."
        else
          echo "Changes detected, starting frontend build..."
          cd ${_FRONTEND_DIR} && \
          docker build -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:${SHORT_SHA} \
              -t ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:latest . && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:${SHORT_SHA} && \
          docker push ${_OCI_REGISTRY}/${_PROJECT_NAME}-${_FRONTEND_NAME}:latest
        fi

  # 3. 打包并推送 Helm Chart
  - name: "alpine/helm:3.12.3"
    id: "publish-chart"
    entrypoint: "bash"
    args:
      - "-c"
      - |
        BACKEND_CHANGED=$(git diff --name-only HEAD^ HEAD | grep "^${_BACKEND_DIR}/" || true)
        FRONTEND_CHANGED=$(git diff --name-only HEAD^ HEAD | grep "^${_FRONTEND_DIR}/" || true)
        CHART_CHANGED=$(git diff --name-only HEAD^ HEAD | grep "^${_CHART_DIR}/" || true)

        # 检查 backend || frontend || helm-chart 目录在当前 commit 中是否有变动
        if [ -n "$$BACKEND_CHANGED" ] || [ -n "$$FRONTEND_CHANGED" ] || [ -n "$$CHART_CHANGED" ]; then
          echo "Executing chart publish..."
          curl -L https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -o /workspace/yq && \
          chmod +x /workspace/yq && \
          cd ${_CHART_DIR} && \
          CHART_VERSION=$(/workspace/yq e '.version' Chart.yaml) && \
          SHA_VERSION="$${CHART_VERSION}-${SHORT_SHA}" && \
          LATEST_VERSION="99.99.99-latest" && \
          helm package . --version "$${SHA_VERSION}" && \
          helm package . --version "$${LATEST_VERSION}" && \
          helm push ${_CHART_NAME}-$${SHA_VERSION}.tgz oci://${_OCI_REGISTRY} && \
          helm push ${_CHART_NAME}-$${LATEST_VERSION}.tgz oci://${_OCI_REGISTRY}
        else
          echo "Nothing changed that requires a chart update."
        fi

# 定义变量
substitutions:
  _OCI_REGISTRY: asia-east2-docker.pkg.dev/project-60addf72-be9c-4c26-8db/todo-docker-repo
  _PROJECT_NAME: todo-gcp
  _BACKEND_NAME: backend
  _FRONTEND_NAME: frontend
  _BACKEND_DIR: backend
  _FRONTEND_DIR: frontend
  _CHART_NAME: todo-chart
  _CHART_DIR: helm-chart

options:
  logging: CLOUD_LOGGING_ONLY
```

## 其它

- 按顺序执行，前面发生错误，后面直接跳过。

- 配置监控变化目录需在 Trigger 中进行。

  **Show included and ignored | Included files filter**：按需填入触发 Cloud Build 的监控目录

  - backend/**
  - frontend/**
  - helm-chart/**
