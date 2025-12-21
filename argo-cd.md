---
title: argo-cd
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - k8s
  - argo-cd
---

# Overview

[**Argo CD**](https://argo-cd.readthedocs.io/en/stable/) 是一个声明式的、面向 Kubernetes 的 GitOps CD 工具。

![argo-cd](assets/argo-cd.png)

# Quick Start

## 安装 Argo CD

- Docker 和 kubectl 已安装，集群已启动。

- [安装 Argo CD](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

  ```bash
  # 创建 Argo CD 命名空间
  kubectl create namespace argocd
  
  # 安装 Argo CD
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  ```

- 查看 pod 状态，直到全部运行

  ```bash
  kubectl get pod -n argocd
  ```

- 获取密码

  ```bash
  kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
  
  # 用户名：admin
  # 本地上次密码：dAlsKbgZa4FvVT6V
  # GCP 上次密码：QaoZBvwjn7YQgEs9
  ```

- 配置网络之后即可查看 Argo CD UI 界面

  ```bash
  # 查看网络服务
  kubectl get svc -n argocd
  
  # 本地：转发端口到本地（临时），访问：127.0.0.1:8080
  kubectl port-forward svc/argocd-server 8080:443 -n argocd
  
  # 公网
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
  ```

- 本地访问

  - 端口转发以后，当前终端要保持打开，否则访问不到
  - 访问地址：https://127.0.0.1:8080

- 公网访问

  - 需要科学上网
  - 访问地址：http://$EXTERNAL-IP


## 部署应用

### 部署方式

有三种方式部署应用：

- Argo CD UI
- Argo CD CLI
- K8s 原生部署

### K8s 原生部署

- 前提条件

  - Argo CD 已安装并初始化
  - 源代码开发完成，已将引用的 Image 推送至镜像仓库。

- 说明：此部分的目录和文件源自 [Todo Fullstack](todo-fullstack.md) 项目

- 创建 K8s 和 Argo CD 目录

  ```
  cd d:/projects/todo-fullstack
  mkdir k8s argo-cd
  ```

- 在 `k8s` 目录创建以下 K8s 配置文件：

  **注意云上的集群有节点限制，试用时只能创建一个副本！**

  - `namespace.yaml`：应用的命名空间
  - `mysql.yaml`：数据库
  - `backend.yaml`：后端
  - `frontend.yaml`：前端

- 在 `argo-cd` 目录创建 Argo CD 的自定义应用配置文件 `application.yaml`

  ```yaml
  apiVersion: argoproj.io/v1alpha1
  kind: Application
  metadata:
    name: todo-app
    namespace: argocd
  spec:
    project: default
    source:
      repoURL: https://gitlab.com/jerrybai/todo-fullstack.git
      targetRevision: HEAD
      path: k8s
    destination:
      server: https://kubernetes.default.svc
      namespace: todo
    syncPolicy:
      automated:
        selfHeal: true
        prune: true
      syncOptions:
        - CreateNamespace=true
        - ApplyOutOfSyncOnly=true
      retry:
        limit: 5
        backoff:
          duration: 5s
          factor: 2
          maxDuration: 3m
  ```

- 推送至 Git 仓库

- 部署应用

  ```bash
  cd d:/projects/todo-fullstack/argo-cd
  kubectl apply -f application.yaml
  ```

- 在 Argo CD 页面查看应用已启动


## 访问应用

- 端口转发

  ```bash
  # 查看应用服务
  kubectl get svc -n todos
  
  # 将前端服务 80 端口到本地 8081 端口
  kubectl port-forward svc/frontend 8081:80 -n todos
  ```

  如有调试需要，也可将后端和数据库进行端口转发

  ```bash
  # 数据库
  kubectl port-forward svc/mysql 3306:3306 -n todos
  # 后端
  kubectl port-forward svc/backend 5000:5000 -n todos
  ```

- 访问应用：http://localhost:8081/

- 以后若想更改应用，只需需改 K8s 配置文件并推送至 Git 仓库，Argo CD 可自动识别并更改部署。


## 删除应用

```bash
cd d:/projects/todo-fullstack/argo-cd
kubectl delete -f application.yaml
kubectl delete ns todo
```


## 删除 Argo CD

- **删除 ArgoCD 自定义资源定义（CRD）**

  ```bash
  kubectl delete crd applications.argoproj.io appprojects.argoproj.io argocds.argoproj.io
  ```

- **删除 ArgoCD 的命名空间**

  ```bash
  kubectl delete ns argocd
  ```

# CR 清单

## 概述

[`application.yaml`](https://argo-cd.readthedocs.io/en/stable/user-guide/application-specification/) 是一个 Kubernetes CR 清单，它声明式地定义了 Argo CD 如何将 Git 仓库中指定的应用配置同步到目标 Kubernetes 集群。

- Argo CD 的安装过程已经在 Kubernetes 集群中配置并部署了 CRD，这个 CRD 就是 `Application` 对象的蓝图。
- 通过 `kubectl apply -f application.yaml` 命令所创建的 YAML 文件，正是该 [CRD](kubernetes.md#CRD) 定义的 [CR](kubernetes.md#CR) 的一个实例。

## 字段

> [官方字段规范](https://argo-cd.readthedocs.io/en/stable/user-guide/application-specification/)

[**Go 结构体**](https://pkg.go.dev/github.com/argoproj/argo-cd/v2/pkg/apis/application/v1alpha1)是 Argo CD Application CRD 字段的定义来源，Go 结构直接对应于 YAML 或 JSON 中的字段。

1. **查找字段：** 您可以在页面上找到名为 **`ApplicationSpec`** 的结构体（Struct）。这就是 `application.yaml` 文件中 **`.spec`** 字段对应的全部内容。
2. **字段名称：** 结构体中的每个字段名称（例如 `Source`、`Destination`、`SyncPolicy`）都对应于 YAML 中的键名（例如 `source`、`destination`、`syncPolicy`）。
3. **类型：** 字段旁边的类型（例如 `ApplicationSource`、`Destination`）表明该字段是一个**嵌套结构**。您需要点击这些类型名称，跳转到下一层结构体，才能看到子字段的完整列表。

## 常规写法

```yaml
apiVersion: argoproj.io/v1alpha1  # Argo CD API 版本
kind: Application                 # 自定义资源类型
metadata:                         # 应用程序元数据
  name: todos-app                 # 应用程序名称
  namespace: argocd               # Argo CD 所在命名空间
spec:                             # 规约
  project: default
  source:                         # 仓库源
    repoURL: https://github.com/Jerrybaijy/todo-fullstack.git # 仓库地址
    targetRevision: HEAD  # 版本指针，HEAD 为当前选定分支的最新提交
    path: k8s             # 配置文件在 Git 仓库中的路径
  destination:
    server: https://kubernetes.default.svc # 目标集群 API 地址
    namespace: todo                        # 资源所在命名空间
  syncPolicy:         # 同步策略
    automated:        # 自动同步配置
      selfHeal: true  # 自愈
      prune: true     # 修剪
    syncOptions:                   # 同步选项
      - CreateNamespace=true       # 自动创建命名空间
      - ApplyOutOfSyncOnly=true    # 仅同步未同步的资源，而不是所有资源
```

## `source`

`source` 用于指定 CR 的仓库源。

```yaml
# K8s 清单源
source:
  # Git 仓库地址
  repoURL: https://github.com/Jerrybaijy/todo-fullstack.git
  # 版本指针，HEAD 为当前选定分支的最新提交
  targetRevision: HEAD
  # K8s 配置文件在 Git 仓库中的路径
  path: k8s
```

```yaml
# Helm Chart 源
source:
  # <oci-registry>/<chart-name>
  repoURL: oci://registry.gitlab.com/jerrybai/todo-fullstack/todo-chart
  # Chart 版本号
  targetRevision: "99.99.99-latest"
  # Chart 名称
  chart: todo-chart
```

# 同步

Argo CD 允许用户自定义目标集群中所需状态的[**同步方式**](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/)。

# 相关项目

- Argo CD Git
- Argo CD Helm
- [Todo Fullstack](todo-fullstack.md)

# FAQ

## OutOfSync

- 当使用 ArgoCD 部署好应用以后，一切运行正常，但 UI 页面一直显示 OutOfSync，即使状态不同步，应用程序实际上也是同步的，但看到它不同步很烦人。若要消除此问题，有一种解决方案是使用资源排除。

  ![image-20240329143514361](assets/image-20240329143514361.png)

- [以下方法由博主提供](https://medium.com/@rojenshrestha100/argo-cd-out-of-sync-due-to-cilium-identity-f9d6188aa056)

- 访问 Argo CD 的 configmap

  ```bash
  kubectl get cm -n argocd
  ```

  ![image-20240329143851461](assets/image-20240329143851461.png)

- 使用 nano 编辑器编辑此配置图

  ```bash
  KUBE_EDITOR="nano" kubectl edit cm argocd-cm -n argocd
  ```

- 文末在第一层级添加以下数据并保存

  ```yaml
  data:
    resource.exclusions: |
      - apiGroups:
        - cilium.io
        kinds:
        - CiliumIdentity
        clusters:
        - "*"
  ```

