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

# Quick Start

- 启用 [Cloud Build API](https://console.cloud.google.com/marketplace/product/google/cloudbuild.googleapis.com?referrer=search&project=project-60addf72-be9c-4c26-8db&returnUrl=%2Fcloud-build%2Fbuilds%3Freferrer%3Dsearch%26project%3Dproject-60addf72-be9c-4c26-8db%26inv%3D%26invt%3DAcFoRQ)

- [将 Repositories 关联到 GitLab](gcp-repositories.md#GitLab)

- 创建 Docker Repository

  ```bash
  # 启用 Artifact Registry API
  gcloud services enable artifactregistry.googleapis.com
  
  # 创建 Docker Repository
  gcloud artifacts repositories create todo-docker-repo \
      --repository-format=docker \
      --location=asia-east2 \
  
  # 为 Docker 配置身份验证
  gcloud auth configure-docker asia-east2-docker.pkg.dev
  ```

- 为触发器添加条件

  ```bash
  Included files filter
  backend/**
  frontend/**
  helm-chart/**
  
  gcloud builds triggers list --region=asia-east2
  
  gcloud builds triggers update [TRIGGER_NAME] \
      --included-files="test/**"
  
  gcloud builds triggers update e951e607-ec8b-4720-8157-58ad8710a732 \
      --region=asia-east2 \
      --included-files="test/**"
  
  gcloud builds triggers update gitlab todo-trigger \
      --region=asia-east2 \
      --included-files=["test/**"]
  
  gcloud builds triggers update \
      --region=asia-east2 \
      --name="todo-trigger" \
      --included-files="test/**"
  ```

- 给服务账号添加角色

  ```bash
  378042797368-compute@developer.gserviceaccount.com
  Artifact Registry Writer
  Logs Writer
  ```

- 定数等分



[使用 Cloud Build 构建镜像](https://cloud.google.com/build/docs/build-push-docker-image?hl=zh-cn)

[连接到 GitLab 代码库](https://cloud.google.com/build/docs/automating-builds/gitlab/connect-repo-gitlab?hl=zh-cn)

[创建 Cloud Build 配置文件 (`cloudbuild.yaml`)](https://www.google.com/search?q=[https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration%3Fhl%3Dzh-cn](https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration%3Fhl%3Dzh-cn))

[使用 Cloud Build 部署到 Kubernetes](https://www.google.com/search?q=https://cloud.google.com/build/docs/deploying-builds/deploy-gke%3Fhl%3Dzh-cn)

