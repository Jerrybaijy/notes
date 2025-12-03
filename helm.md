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

  提前安装包管理器 Chocolatey，详见 Windows
  
  以管理员身份运行 Git Bash
  
  ```bash
  choco install kubernetes-helm
  ```

## Helm 命令

> [Helm 命令](https://helm.sh/docs/helm/)

```bash
# 查看 helm 版本
helm version

# 查看 chart 配置值（values.yaml 文件中的值）
helm show values .

# 重置 index
helm repo index $CHART_PATH --url https://jerrybaijy.github.io/$REPO/
```

## 基本流程

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

## Repository

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

## Chart

[**Chart**](https://helm.sh/zh/docs/topics/charts) 是 Helm 的包格式，包含一个应用所需的所有 Kubernetes 资源定义。

- **基础命令**

  ```bash
  # 查看 chart 信息
  helm show chart .
  # 创建 chart
  helm create $CHART_NAME
  # 封装 chart
  helm package $CHART_PATH
  # 发布 chart，没用过
  helm push $CHART $CHART_REPO
  # 测试 chart
  helm lint $CHART
  ```

## Release

Release 是 Chart 部署到 Kubernetes 集群后的实例。

```bash
# 查看 release
helm list
# 部署 release
helm install $RELEASE $HELM_REPO/$CHART_NAME
# 删除 release
helm delete $RELEASE
# 测试 release
helm test $RELEASE
```

## Values

[**Values**](https://helm.sh/zh/docs/chart_best_practices/values/) 用于自定义 Chart 部署时的配置参数。

- values.yaml

  ```yaml
  # 副本数量
  replicaCount: 2
  
  image:
    repository: jerrybaijy/jerry-image
    tag: "v1.0"
    pullPolicy: IfNotPresent
  
  imagePullSecrets: []
  nameOverride: ""
  fullnameOverride: ""
  
  serviceAccount:
    # Specifies whether a service account should be created
    create: true
    # Automatically mount a ServiceAccount's API credentials?
    automount: true
    # Annotations to add to the service account
    annotations: {}
    # The name of the service account to use.
    # If not set and create is true, a name is generated using the fullname template
    name: ""
  
  podAnnotations: {}
  podLabels: {}
  
  podSecurityContext:
    {}
    # fsGroup: 2000
  
  securityContext:
    {}
    # capabilities:
    #   drop:
    #   - ALL
    # readOnlyRootFilesystem: true
    # runAsNonRoot: true
    # runAsUser: 1000
  
  service:
    type: ClusterIP
    port: 80
  
  ingress:
    enabled: false
    className: ""
    annotations:
      {}
      # kubernetes.io/ingress.class: nginx
      # kubernetes.io/tls-acme: "true"
    hosts:
      - host: chart-example.local
        paths:
          - path: /
            pathType: ImplementationSpecific
    tls: []
    #  - secretName: chart-example-tls
    #    hosts:
    #      - chart-example.local
  
  resources:
    {}
    # We usually recommend not to specify default resources and to leave this as a conscious
    # choice for the user. This also increases chances charts run on environments with little
    # resources, such as Minikube. If you do want to specify resources, uncomment the following
    # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
    # limits:
    #   cpu: 100m
    #   memory: 128Mi
    # requests:
    #   cpu: 100m
    #   memory: 128Mi
  
  livenessProbe:
    httpGet:
      path: /
      port: http
  readinessProbe:
    httpGet:
      path: /
      port: http
  
  autoscaling:
    enabled: false
    minReplicas: 1
    maxReplicas: 100
    targetCPUUtilizationPercentage: 80
    # targetMemoryUtilizationPercentage: 80
  
  # Additional volumes on the output Deployment definition.
  volumes: []
  # - name: foo
  #   secret:
  #     secretName: mysecret
  #     optional: false
  
  # Additional volumeMounts on the output Deployment definition.
  volumeMounts: []
  # - name: foo
  #   mountPath: "/etc/foo"
  #   readOnly: true
  
  nodeSelector: {}
  
  tolerations: []
  
  affinity: {}
  ```
