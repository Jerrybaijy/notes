---
title: helm
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - k8s
---

# Helm

Helm 是 Kubernetes 的包管理器，使用 "chart" 的打包格式来描述 Kubernetes 资源的集合，使得部署和管理应用程序变得更加简单和可重复。

> [Helm 文档](https://helm.sh/zh/docs/)

## 安装 Helm

- 集群已运行，Kubectl 已安装

- [Linux 安装（Debian / Ubuntu）](https://helm.sh/zh/docs/intro/install#from-snap)

  ```bash
  sudo snap install helm --classic
  # 添加环境变量
  export PATH="$PATH:/snap/bin"
  ```

- [Windows 安装](https://helm.sh/zh/docs/intro/install#from-chocolatey-windows)

  以管理员身份运行 Git Bash，使用 Chocolatey 包管理器安装
  
  ```bash
  choco install kubernetes-helm
  ```

## 创建 Chart

在项目根目录下执行以下命令：

```bash
helm create <chart_dir>
```

这条命令会创建一个名为 `<chart_dir>` 的 Chart 目录，其中包含了 Helm Chart 的基本结构和配置文件。

```
# 自动生成结构
todos-helm/                      # 项目根目录
│
├── todo-chart/                  # Chart 目录（存放 Chart 的文件夹）
│   ├── Chart.yaml               # Chart 元数据（名称、版本等）
│   ├── values.yaml              # 部署参数配置（镜像、端口、环境变量等）
│   ├── .helmignore              # 忽略不需要打包的文件
│   ├── charts/                  # 子 Chart 目录
│   └── templates/               # Kubernetes 资源模板目录
│       ├── NOTES.txt            # 部署成功后的提示信息
│       ├── _helpers.tpl         # 模板函数定义
│       ├── deployment.yaml      # 应用的 Deployment 配置清单文件（可替换）
│       ├── service.yaml         # 应用的 Service 配置清单文件（可替换）
│       ├── hpa.yaml             # 水平自动扩缩容配置（可选）
│       ├── httproute.yaml       # HTTP 路由配置（可选）
│       ├── ingress.yaml         # Ingress 配置（可选）
│       ├── serviceaccount.yaml  # 服务账号配置（可选）
│       └── tests/               # 测试文件目录
│           └── test-connection.yaml  # 连接测试
└── 项目其它文件
```

```
# 必要保留结构
todos-helm/                      # 项目根目录
│
├── todo-chart/                  # Chart 目录（存放 Chart 的文件夹）
│   ├── Chart.yaml               # Chart 元数据（名称、版本等）
│   ├── values.yaml              # 模板文件参数配置（镜像、端口、环境变量等）
│   ├── .helmignore              # 忽略不需要打包的文件
│   └── templates/               # Kubernetes 资源模板目录
│       ├── namespace.yaml       # 命名空间
│       ├── _helpers.tpl         # 模板函数
│       └── 其它模板文件
│
└── 项目其它文件
```

## 配置 Chart

### Chart.yaml

这是 Chart 的元数据配置，主要用于标识 Chart 的基本信息。

### values.yaml

模板文件的参数设置

### namespace.yaml

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: {{ .Values.global.namespace }}
  labels:
    name: {{ .Values.global.namespace }}
```

### _helpers.tpl

模板函数，用于生成一致的资源名称和标签

### 配置模板

各种资源的配置模板，如 `mysql.yaml`，`backend.yaml`，`frontend.yaml`。

## 部署 Release

```bash
cd <project_root_dir>
helm install <release_name> <chart_dir>
```

```bash
cd /d/projects/todos-helm
helm install todo-app ./todo-chart
```

## 卸载 Release

```bash
helm uninstall <release_name>
```

## 封装 Chart

这会在 Chart 目录生成 `.tgz` 格式的 Chart 包（文件名格式：`<chart名称>-<版本号>.tgz`，版本号在 `Chart.yaml` 中定义）。

```bash
cd <chart_dir>
helm package .
```

## 基本流程

1. 安装 Helm
2. 创建 Chart
3. 配置  Chart
4. 部署 Release（本地测试）
5. 卸载 Release
6. 封装 Chart

## 基本流程（旧）

### 建立远程仓库

- UI 界面创建 Git 仓库，clone 至本地

- Repo 根目录创建创建 Chart

  ```bash
  helm create $CHART_NAME
  ```

- 配置 Chart

  - 编辑模板 `mychart/templates`
  - 编辑 values `mychart/values.yaml`

- 封装 Chart

  ```bash
  helm package $CHART_PATH
  ```

- 重置 index

  ```bash
  helm repo index $CHART_PATH
  ```

- Git 推送，GitHub 设置 Pages - Branch（一定不要提前设置）

- 重置 index

  ```bash
  helm repo index $CHART_PATH --url https://jerrybaijy.github.io/$REPO/
  ```

- Git 推送

- 至此，远程 Helm Chart 仓库已建好，可供其它调用：https://jerrybaijy.github.io/$REPO/

### 使用远程仓库

- 添加本地 Helm 仓库，与远程仓库关联

  ```bash
  helm repo add $HELM_REPO https://jerrybaijy.github.io/$REPO
  ```

- 使用 Helm Charts

  ```bash
  helm install $RELEASE $HELM_REPO/$CHART_NAME
  ```

### 流程实例

- 这是项目 Argo CD Git 的步骤留存，最后两大步取一个操作

  ```bash
  # UI 界面创建 Git 仓库，clone 至本地，进入 repo 目录
  
  helm create argocd-helm-chart
  helm package argocd-helm-chart
  helm repo index .
  
  # Git 推送，GitHub 设置 Pages - Branch（一定不要提前设置）
  
  helm repo index . --url https://jerrybaijy.github.io/argocd-helm/
  
  # Git 推送
  
  # 1.以下是本地使用远程 Helm Charts
  helm repo add argocd-helm https://jerrybaijy.github.io/argocd-helm/
  kubectl create namespace argocd-helm
  helm install argocd-helm-app argocd-helm/argocd-helm-chart -n argocd-helm
  kubectl get pod -n argocd-helm
  kubectl get svc -n argocd-helm
  kubectl delete namespace argocd-helm
  
  # 2.以下是 Argo CD 使用远程 Helm Charts
  kubectl apply -f application.yaml
  kubectl get namespace
  kubectl get pod -n argocd-helm
  kubectl get svc -n argocd-helm
  kubectl delete namespace argocd-helm
  ```

# Helm 命令

> [Helm 命令](https://helm.sh/docs/helm/)

```bash
# 查看 helm 版本
helm version

# 查看 chart 配置值（values.yaml 文件中的值）
helm show values .

# 重置 index
helm repo index <chart_dir> --url https://jerrybaijy.github.io/<repo_name>/

# 检查本地 Chart 语法
helm lint <chart_dir>
```

# Repository

[**Repository**](https://helm.sh/zh/docs/topics/chart_repository/) 存放和分享 Chart 的地方。

```bash
# 查看 Helm Repo
helm repo list
# 添加 Helm Repo
helm repo add $HELM_REPO https://jerrybaijy.github.io/$REPO
helm repo add arldka https://arldka.github.io/helm-charts
helm repo update
# 删除 Helm Repo
helm repo remove $HELM_REPO
# 删除所有 Helm Repo
rm ~/.config/helm/repositories.yaml
```

- Helm Repo 实际只是一个 YAML 文件，存储于 `~/.config/helm/repositories.yaml`，里面声明了各个 Helm Repo 与 Remote Repo 的对应关系。

# Chart

[**Chart**](https://helm.sh/zh/docs/topics/charts) 是 Helm 的包格式，包含一个应用所需的所有 Kubernetes 资源定义。

```bash
# 查看 chart 信息
helm show chart .
# 创建 chart
helm create <chart_name>
# 封装 chart
helm package <chart_dir>
# 发布 chart，没用过
helm push $CHART $CHART_REPO
# 测试 chart
helm lint $CHART
```

# Release

Release 是 Chart 部署到 Kubernetes 集群后的实例。

```bash
# 查看 release
helm list
# 部署 release
helm install $RELEASE $HELM_REPO/$CHART_NAME
# 更新 Chart（当修改了应用代码或配置后，可以使用 Helm 更新部署）
helm upgrade <release_name> <chart_dir>
# 卸载 release
helm uninstall <release_name>
# 测试 release
helm test $RELEASE
```

# Values

[**Values**](https://helm.sh/zh/docs/chart_best_practices/values/) 用于自定义 Chart 时，模板文件的配置参数，类似于环境变量。

`values.yaml` 示例：

```yaml
# 全局配置
global:
  namespace: todos-helm

# MySQL配置
mysql:
  image: mysql
  tag: 8.0
  imagePullPolicy: IfNotPresent
  rootPassword: "123456"
  database: todos_db
  user: jerry
  password: "000000"
  replicaCount: 1
  persistence:
    enabled: true
    size: 1Gi
  service:
    type: ClusterIP
    port: 3306

# Backend配置
backend:
  replicaCount: 1
  image:
    repository: jerrybaijy/todos-helm-backend
    tag: latest
    pullPolicy: IfNotPresent
  service:
    type: ClusterIP
    port: 5000
  env:
    SECRET_KEY: your_secret_key_here

# Frontend配置
frontend:
  replicaCount: 1
  image:
    repository: jerrybaijy/todos-helm-frontend
    tag: latest
    pullPolicy: IfNotPresent
  service:
    type: NodePort
    port: 80
    nodePort: 30080

```

# 问 AI

本项目前后端已开发完成并通过测试，不要再动我的源代码。

你把接下来的步骤写成一个 `新教程.md` 放在项目根目录：

- 创建一个 Chart 目录，目录名为 todo-chart
- 完善 chart 内的各个文件，把前端、后端和数据库的各个配置都放在各自的同一个文件里
  - frontend.yaml
  - backend.yaml
  - mysql.yaml
  - chart 目录内的所有文件，哪个有用，哪个没有，需要删除或修改哪个，你都给我说清楚。
- 数据库
  - Root 密码：123456
  - 用户名：jerry
  - 密码：000000
- 编写完文件，要本地部署测试一下，测试通过以后删除清理
- 本地 Helm Chart 打包
- 推送 Chart 到私有 Harbor 仓库
- 使用 helm 命令安装一下这个 Chart，测试一下，测试通过以后删除清理
- 编写 argo cd 的应用定义文件 argocd-application.yaml，引用的就是这个 Harbor 仓库的 chart
- 根据这个 argocd-application.yaml 去在 minikube 中部署应用
- 在 GitLab CI 时，能自动构建 chart 并推送至私有 Harbor 仓库，所以要创建 `.gitlab-ci.yml` 文件
- 最后实现，推送代码到 Git 仓库时：
  - 能自动构建 chart 并推送至私有 Harbor 仓库
  - argo cd 能监测这个 chart 的变化并调整部署

我是一个初学者，所以你的步骤务必要详细。

我的表述未必准确，你帮我组织语言。

我的步骤可能有错误或缺失，你帮我完善。

你不需要有任何操作，只帮我生成教程即可！！！！！

教程文档要求：

- 所有标题不需要数字编号
