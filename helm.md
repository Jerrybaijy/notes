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

## 基本流程

1. 安装 Helm
2. 创建 Chart
3. 配置  Chart
4. 使用本地 Chart 目录部署 Release
5. 封装 Chart
6. 使用本地封装的 Chart 包部署 Release
7. 推送本地封装的 Chart 包至远程仓库
8. 使用远程 Chart 包部署 Release
9. 卸载 Release

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

这是项目 Argo CD Git 的步骤留存，最后两大步取一个操作

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
helm repo index <Chart_Dir> --url https://jerrybaijy.github.io/<repo_name>/

# 检查本地 Chart 语法
helm lint <Chart_Dir>
```

# Repository

[**Repository**](https://helm.sh/zh/docs/topics/chart_repository/) 存放和分享 Chart 的地方。

Helm Repo 实际只是一个 YAML 文件，存储于 `~/.config/helm/repositories.yaml`，里面声明了各个 Helm Repo 与 Remote Repo 的对应关系。

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

# Chart

## Chart

[**Chart**](https://helm.sh/zh/docs/topics/charts) 是 Helm 的包格式，包含一个应用所需的所有 Kubernetes 资源定义。有三种形式的 Chart：

- 未打包的 Chart 目录
- 已打包的 `.tgz` 格式的 Chart 包
- 远程仓库的 Chart 包

```bash
# 查看 chart 信息
helm show chart .
# 创建 chart
helm create <chart_name>
# 封装 chart
helm package <Chart_Dir>
# 发布 chart，没用过
helm push $CHART $CHART_REPO
# 测试 chart
helm lint $CHART
```

## 创建 Chart

这会创建一个名为 `<Chart_Dir>` 的 Chart 目录，其中包含了 Helm Chart 的默认结构和配置文件。

```bash
cd <Project_Root_Name>
helm create <Chart_Dir>
```

```
# 默认结构和配置文件

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
# 必要保留结构和配置文件
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

编写 Chart 目录的各文件，详见各章节。

## 封装 Chart

这会在 Chart 目录生成 `.tgz` 格式的 Chart 包（文件名格式：`<chart名称>-<版本号>.tgz`，版本号在 `Chart.yaml` 中定义）。

```bash
cd <Chart_Dir>
helm package .
```

## 推送 Chart

- 此部分记录推送 Chart 到 GitLab Container Registry

- 配置 GitLab Personal Access Token，详见 [GitLab 笔记](gitlab.md#gitlab-personal-access-tokens)。

- 登录 GitLab Registry

  ```bash
  # 登录
  helm registry login registry.gitlab.com -u jerrybai
  # 输入 Token（注意 Token 不会显示）
  Password:
  ```

- 推送

  ```bash
  # 有关 OCI 仓库地址的格式详见 GitLab 笔记
  
  helm push <Chart> oci://<Registry_Host>/<Namespace>/<Repository_Name>
  helm push todo-chart-0.1.0.tgz oci://registry.gitlab.com/jerrybai/todos-helm
  ```

# Release

## Release

Release 是 Chart 部署到 Kubernetes 集群后的实例。

```bash
# 查看 release
helm list

# 部署 release
helm install $RELEASE $HELM_REPO/$CHART_NAME
# 根据 oci 仓库部署
helm install todo oci://registry.gitlab.com/jerrybai/todos-helm/todo-chart --version 0.1.0

# 更新 Chart（当修改了应用代码或配置后，可以使用 Helm 更新部署）
helm upgrade <Release_Name> <Chart_Dir>
# 卸载 release
helm uninstall <Release_Name>
# 测试 release
helm test $RELEASE
```

## 部署 Release

有三种方式部署 Release：

- 使用本地 Chart 目录
- 使用本地 Chart 包
- 使用远程 Chart 包

### 部署 Release（本地 Chart 目录）

```bash
cd <Project_Root_Dir>
helm install <Release_Name> <Chart_Dir>
```

```bash
cd /d/projects/todos-helm
helm install todo-app ./todo-chart
```

### 部署 Release（本地 Chart 包）

```bash
cd <Chart_Dir>
helm install <Release_Name> <Chart_Name>

# 卸载
helm uninstall <Release_Name>
```

### 部署 Release（远程 Chart 包）

```bash
helm install <Release_Name> oci://<Registry_Host>/<Namespace>/<Repository_Name>/<Chart_Name> --version <Chart_Version>

helm install todo-app oci://registry.gitlab.com/jerrybai/todos-helm/todo-chart --version 0.1.0
```

## 卸载 Release

```bash
helm uninstall <Release_Name>
```

# Chart.yaml

这是 Chart 的元数据配置，主要用于标识 Chart 的基本信息。

# values.yaml

[**Values**](https://helm.sh/zh/docs/chart_best_practices/values/) 用于设置模板文件的配置参数，类似于环境变量。

- 配置变量值

  ```yaml
  # values.yaml
  
  global:
    namespace: todos-helm
  ```

- 使用变量

  ```yaml
  # templates/example.yaml
  
  namespace: {{ .Values.global.namespace }}
  ```

# namespace.yaml

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: {{ .Values.global.namespace }}
  labels:
    name: {{ .Values.global.namespace }}
```

# _helpers.tpl

模板函数，用于生成一致的资源名称和标签，类似与环境变量。

- 定义变量

  ```
  {{/* _helpers.tpl */}}
  
  {{/* 定义 Frontend 组件的完整名称 */}}
  {{- define "todo-chart.frontend.fullname" }}
  {{- printf "%s-frontend" (include "todo-chart.fullname" .) | trunc 63 | trimSuffix "-" }}
  {{- end }}
  ```

- 使用变量

  ```yaml
  # templates/example.yaml
  
  name: {{ include "todo-chart.frontend.fullname" . }}
  ```

# 模板文件

各种资源的配置模板，如 `mysql.yaml`，`backend.yaml`，`frontend.yaml`。
