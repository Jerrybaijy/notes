---
title: gcp-gke
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud-computing
  - gcp
  - gke
---

# Overview

[**GKE**](https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview?hl=zh-cn) (Google Kubernetes Engine)，是由 Google 开发的代管式 Kubernetes 服务，可以使用 Google 的基础架构大规模部署和运营容器化应用。

# Quick Start

## 前提条件

- Google Cloud CLI 已安装并完成初始化
- 本地 kubectl 已安装
- Google Cloud 项目已创建

## 创建 GKE

```bash
# 创建标准集群
gcloud container clusters create $CLUSTER_NAME --region=$REGION
# e.g.
gcloud container clusters create todo-cluster \
    --region=asia-east2 \
    --node-locations=asia-east2-a \
    --num-nodes=2 \
    --machine-type=e2-medium \
    --disk-size=40 \
    --disk-type=pd-standard \
    --enable-autoscaling \
    --min-nodes=1 \
    --max-nodes=5 \
    --scopes=cloud-platform
# 查看集群
gcloud container clusters list
```

## 安装 `gke-gcloud-auth-plugin` 插件

否则无法使用 `kubectl` 命令管理集群

```bash
# 安装
gcloud components install gke-gcloud-auth-plugin
# 验证
gke-gcloud-auth-plugin --version
```

## 更新 `kubectl` 配置

以使用 `gke-gcloud-auth-plugin` 插件

```bash
gcloud container clusters get-credentials $CLUSTER_NAME \
    --location=$CONTROL_PLANE_LOCATION

# 更新配置
gcloud container clusters get-credentials todo-cluster \
    --location asia-east2 \
    --project project-60addf72-be9c-4c26-8db

# 验证配置
kubectl get ns
```

## 交互 GKE

将 kubectl 上下文切换至 GKE，使用 kubectl 交互 GKE

## 删除 GKE

```bash
gcloud container clusters delete $CLUSTER_NAME --region=$REGION
gcloud container clusters delete todo-cluster --region=asia-east2
```

# GKE Reference

> [GKE Reference](https://docs.cloud.google.com/sdk/gcloud/reference/container/clusters)

```bash
# 创建标准集群
gcloud container clusters create $CLUSTER_NAME [Flags]
# e.g.
gcloud container clusters create todo-cluster \
    --region=asia-east2 \
    --node-locations=asia-east2-a \
    --num-nodes=2 \
    --machine-type=e2-medium \
    --disk-size=40 \
    --disk-type=pd-standard \
    --enable-autoscaling \
    --min-nodes=1 \
    --max-nodes=5 \
    --scopes=cloud-platform
# 列出所有集群
gcloud container clusters list
# 删除集群
gcloud container clusters delete $CLUSTER_NAME [Flags]
# 停止集群
gcloud container clusters resize $CLUSTER_NAME [Flags]
```

# 手动部署

- 来源：[部署容器化应用](https://cloud.google.com/kubernetes-engine/docs/deploy-app-cluster)

- 这是一个 GKE 练习，将一个简单的容器化 Web Server 部署到 GKE 集群，并可以在互联网访问。

- 此练习没有使用 Yaml 文件部署

- **准备**

  - Google Cloud CLI 环境搭建完成，详见 《Google Cloud》

  - 在 Google Cloud 中启用 API

  - 设置默认项目

    ```bash
    gcloud config set project opportune-study-413101
    ```

- **创建集群**

  - 创建集群

    ```bash
    gcloud container clusters create-auto jerry-cluster --region=asia-east2
    ```

  - 获取用于集群的身份验证凭据

    ```bash
    gcloud container clusters get-credentials jerry-cluster --region asia-east2
    ```

- **部署应用**

  - 手动部署应用

    ```bash
    kubectl create deployment hello-server --image=us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
    ```

  - 可替换为自己创建的镜像

- **公开端口**

  ```bash
  kubectl expose deployment hello-server --type LoadBalancer --port 80 --target-port 8080
  ```

- **获取外部 IP**

  ```bash
  kubectl get service hello-server
  ```

- **访问应用**

  ```bash
  curl http://EXTERNAL-IP
  ```

- **清理**

  - 删除 Service

    ```bash
    kubectl delete service hello-server
    ```

  - 删除集群

    ```bash
    gcloud container clusters delete hello-cluster --region us-central1
    ```

# Yaml 部署

- 来源：[部署特定语言应用](https://cloud.google.com/kubernetes-engine/docs/quickstarts/deploy-app-container-image?hl=zh-cn#go)
- 这是一个 GKE 练习，将一个简单的容器化 Web Server 部署到 GKE 集群，并可以在互联网访问
- 此练习使用 Yaml 文件部署

### 准备

- Google Cloud CLI 已安装

- 在 Google Cloud 中启用 API

- 设置默认项目

  ```bash
  gcloud config set project opportune-study-413101
  ```

- 安装 Go 语言环境

  ```bash
  sudo apt-get install golang
  go version
  ```

### 编写应用

- 如果使用自己的镜像，可以跳过此步。

- 创建工作目录 `helloworld-gke` 并进入

- 创建名为 `example.com/helloworld` 的新模块

  ```bash
  go mod init example.com/helloworld
  ```

- 创建名为 `helloworld.go` 的新文件

  ```go
  package main
  
  import (
          "fmt"
          "log"
          "net/http"
          "os"
  )
  
  func main() {
          http.HandleFunc("/", handler)
  
          port := os.Getenv("PORT")
          if port == "" {
                  port = "8080"
          }
  
          log.Printf("Listening on localhost:%s", port)
          log.Fatal(http.ListenAndServe(fmt.Sprintf(":%s", port), nil))
  }
  
  func handler(w http.ResponseWriter, r *http.Request) {
          log.Print("Hello world received a request.")
          target := os.Getenv("TARGET")
          if target == "" {
                  target = "World"
          }
          fmt.Fprintf(w, "Hello %s!\n", target)
  }
  ```

### 创建镜像

- 如果使用自己的镜像，可以跳过此步

- 创建 Dockerfile

  ```dockerfile
  FROM golang:1.21.0 as builder
  WORKDIR /app
  RUN go mod init quickstart-go
  COPY *.go ./
  RUN CGO_ENABLED=0 GOOS=linux go build -o /quickstart-go
  
  # 使用 Docker 多阶段构建来创建精简的生产镜像
  # https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
  # 原文件不是这个image，导致容器无法启动
  FROM debian
  WORKDIR /
  COPY --from=builder /quickstart-go /quickstart-go
  
  # 原文件没有这句，导致找不到nonroot用户，容器无法启动
  RUN groupadd -r nonroot && useradd -r -g nonroot nonroot
  
  USER nonroot:nonroot
  ENTRYPOINT ["/quickstart-go"]
  ```

- 获取 Google Cloud 项目 ID

  ```bash
  gcloud config get-value project
  ```

- 在集群所在的位置创建名为 `hello-repo` 的仓库

  ```bash
  gcloud artifacts repositories create hello-repo --project=opportune-study-413101 --repository-format=docker --region=us-central1 --description="Docker repository"
  ```

- 创建镜像

  ```bash
  gcloud builds submit --tag us-central1-docker.pkg.dev/opportune-study-413101/hello-repo/helloworld-gke .
  ```

### 创建集群

- 创建集群

  ```sh
  gcloud container clusters create-auto helloworld-gke --region us-central1
  ```

- 验证有权访问该集群

  ```
  kubectl get nodes
  ```

### 创建 Deployment

- 创建 `deployment.yaml` 文件

  `$GCLOUD_PROJECT` 是您的 Google Cloud 项目 ID，$LOCATION 是代码库位置，例如 us-central1

  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: helloworld-gke
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: hello
    template:
      metadata:
        labels:
          app: hello
      spec:
        containers:
          - name: hello-app
            # Replace $LOCATION with your Artifact Registry location (e.g., us-west1).
            # Replace $GCLOUD_PROJECT with your project ID.
            image: $LOCATION-docker.pkg.dev/$GCLOUD_PROJECT/hello-repo/helloworld-gke:latest
            # This app listens on port 8080 for web traffic by default.
            ports:
              - containerPort: 8080
            env:
              - name: PORT
                value: "8080"
            resources:
              requests:
                memory: "1Gi"
                cpu: "500m"
                ephemeral-storage: "1Gi"
              limits:
                memory: "1Gi"
                cpu: "500m"
                ephemeral-storage: "1Gi"
  ```

- 部署应用

  ```bash
  kubectl apply -f deployment.yaml
  ```

- 查看应用

  如果所有 `AVAILABLE` 部署都为 `READY`，则表示 Deployment 已完成。否则再次运行 `kubectl apply -f deployment.yaml`，更新 Deployment 以纳入任何更改

  ```bash
  kubectl get deployments
  ```

- 查看 Pod

  ```bash
  kubectl get pods
  ```

### 创建 Service

- 创建 `service.yaml` 文件

  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: hello
  spec:
    type: LoadBalancer
    selector:
      app: hello
    ports:
      - port: 80
        targetPort: 8080
  ```

- 部署 Service

  ```sh
  kubectl apply -f service.yaml
  ```

### 访问应用

- 获取外部 IP

  输出结果的 `EXTERNAL-IP` 列中，复制 Service 的外部 IP 地址

  ```bash
  kubectl get service
  ```

- 访问应用

  ```bash
  http://EXTERNAL-IP
  ```

### 清理

- Delete service

  ```bash
  kubectl delete service hello
  ```

- Delete cluster

  ```bash
  gcloud container clusters delete helloworld-gke --region us-central1
  ```

- Delete repo

  ```bash
  gcloud artifacts repositories delete hello-repo --region=us-central1 --project=opportune-study-413101
  ```
