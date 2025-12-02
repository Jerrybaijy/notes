---
title: argo-cd
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - k8s
---

# Argo CD

## Argo CD

[**Argo CD**](https://argo-cd.readthedocs.io/en/stable/) 是一个面向 Kubernetes 的声明式 GitOps 持续交付工具。

![argo-cd](assets/argo-cd.png)

## 安装

- Docker 和 kubectl 已安装，集群已启动。

- 安装 Argo CD

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

- 将端口转发至本地或公网即可查看 Argo CD UI 界面

  ```bash
  # 查看网络服务
  kubectl get svc -n argocd
  
  # 本地：转发端口到本地（临时），访问：127.0.0.1:8080
  kubectl port-forward svc/argocd-server 8080:443 -n argocd
  
  # 公网
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
  ```

- 获取密码

  ```bash
  kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
  
  # 上次密码：dAlsKbgZa4FvVT6V
  ```

- 在本地或公网通过 IP 访问 Argo CD 页面登录，用户名为 admin，公网访问需要科学上网。
- 端口转发以后，当前终端要保持打开，否则访问不到 https://127.0.0.1:8080

## 基本流程

- Argo CD 已安装并初始化

- 此流程以推送至 Git 仓库为例

- 项目根目录创建 `k8s` 目录，并创建以下配置清单文件：
  
  **注意云上的集群有节点限制，试用时只能创建一个副本！**
  
  - `namespace.yaml`：应用的命名空间
  - `mysql.yaml`：数据库
  - `backend.yaml`：后端
  - `frontend.yaml`：前端
  - `application.yaml`：Argo CD
  
- `application.yaml`，该文件源自 `todos-fullstack` 项目。

  ```yaml
  apiVersion: argoproj.io/v1alpha1
  kind: Application
  metadata:
    name: todos-app
    namespace: argocd
  spec:
    project: default
    source:
      repoURL: https://github.com/Jerrybaijy/todos-fullstack.git
      targetRevision: HEAD
      path: k8s
    destination:
      server: https://kubernetes.default.svc
      namespace: todos
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
  cd k8s
  kubectl apply -f application.yaml
  ```

- 在 Argo CD 页面查看应用已启动

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

- 以后若想更改应用，只需需改配置清单文件并推送至 Git 仓库，Argo CD 可自动识别并更改自动部署。

- 删除应用

  ```bash
  cd k8s
  kubectl delete -f application.yaml
  kubectl delete ns todos
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

## 创建应用

目前已知有三种方法创建应用：

- Argo CD UI
- Argo CD CLI
- `kubectl apply -f application.yaml`

### 通过 Argo CD UI 创建应用

- 登录 Argo CD UI
- 点击 "NEW APP" 按钮
- 填写应用信息：
  - Application Name: `todos-fullstack`
  - Project: `default`
  - Repository URL: `https://gitlab.com/<your-namespace>/todos-fullstack.git`
  - Path: `dev`
  - Cluster URL: `https://kubernetes.default.svc`
  - Namespace: `default`
- 点击 "CREATE" 按钮创建应用
- 点击 "SYNC" 按钮同步应用

### 通过 Argo CD CLI 创建应用

```bash
# 登录 Argo CD CLI
argocd login <argocd-server-address> --username admin --password <initial-password>

# 创建应用
argocd app create todos-fullstack \
  --repo https://gitlab.com/<your-namespace>/todos-fullstack.git \
  --path dev \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default

# 同步应用
argocd app sync todos-fullstack
```

# application.yaml

[`application.yaml`](https://argo-cd.readthedocs.io/en/stable/user-guide/application-specification/) 是 Argo CD 的自定义应用配置清单文件，属于 K8s 的 CRD 。

## 常规写法

```yaml
apiVersion: argoproj.io/v1alpha1  # Argo CD API 版本
kind: Application                 # 自定义资源类型
metadata:                         # 应用程序元数据
  name: todos-app                 # 应用程序名称
  namespace: argocd               # Argo CD 所在命名空间
spec:                             # 规约
  project: default
  source:
    repoURL: https://github.com/Jerrybaijy/todos-fullstack.git
    targetRevision: HEAD
    path: k8s
  destination:
    server: https://kubernetes.default.svc
    namespace: todos
  syncPolicy:         # 同步策略
    automated:        # 自动同步配置
      selfHeal: true  # 自愈
      prune: true     # 修剪
    syncOptions:                 # 同步选项
      - CreateNamespace=true       # 自动创建命名空间
      - ApplyOutOfSyncOnly=true    # 仅同步未同步的资源，而不是所有资源
```

## 官方说明

关于 `application.yaml` 的[官方说明](https://argo-cd.readthedocs.io/en/stable/user-guide/application-specification/)

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: guestbook
  # 通常你会希望将资源添加到 argocd 命名空间。
  namespace: argocd
  # 仅当你希望这些资源级联删除时才添加此 finalizer。
  finalizers:
    # 默认行为是前台级联删除
    - resources-finalizer.argocd.argoproj.io
    # 或者，你可以使用后台级联删除
    # - resources-finalizer.argocd.argoproj.io/background
  # 为你的应用对象添加标签。
  labels:
    name: guestbook
spec:
  # 应用所属的项目。
  project: default

  # 应用清单的来源
  source:
    repoURL: https://github.com/argoproj/argocd-example-apps.git # 可以指向一个 Helm chart 仓库或一个 git 仓库。
    targetRevision: HEAD # 对于 Helm，这指的是 chart 的版本。
    path: guestbook # 对于直接从 Helm 仓库而不是 Git 拉取的 Helm chart，这个路径没有意义。

    # helm 特定配置
    chart: chart-name # 直接从 Helm 仓库拉取时设置此项。对于 Git 托管的 Helm chart，请勿设置。
    helm:
      passCredentials: false # 如果为 true，则会向 Helm 命令添加 --pass-credentials 以将凭据传递给所有域。
      # 要设置的额外参数（与通过 values.yaml 设置相同，但这些参数优先）
      parameters:
        - name: "nginx-ingress.controller.service.annotations.external-dns\\.alpha\\.kubernetes\\.io/hostname"
          value: mydomain.example.com
        - name: "ingress.annotations.kubernetes\\.io/tls-acme"
          value: "true"
          forceString: true # 确保该值被视为字符串

      # 使用文件内容作为参数（使用 Helm 的 --set-file）
      fileParameters:
        - name: config
          path: files/config.json

      # Release 名称覆盖（默认为应用程序名称）
      releaseName: guestbook

      # 用于覆盖 Helm Chart 中值的 Helm values 文件
      # 路径是相对于上面定义的 spec.source.path 目录的
      valueFiles:
        - values-prod.yaml

      # 在安装 Helm chart 时忽略本地缺失的 valueFiles。默认为 false
      ignoreMissingValueFiles: false

      # 块文件形式的 Values 文件。如果可能，请优先使用 valuesObject（见下文）
      values: |
        ingress:
          enabled: true
          path: /
          hosts:
            - mydomain.example.com
          annotations:
            kubernetes.io/ingress.class: nginx
            kubernetes.io/tls-acme: "true"
          labels: {}
          tls:
            - secretName: mydomain-tls
              hosts:
                - mydomain.example.com

      # 块文件形式的 Values 文件。这优先于 values
      valuesObject:
        ingress:
          enabled: true
          path: /
          hosts:
            - mydomain.example.com
          annotations:
            kubernetes.io/ingress.class: nginx
            kubernetes.io/tls-acme: "true"
          labels: {}
          tls:
            - secretName: mydomain-tls
              hosts:
                - mydomain.example.com

      # 如果 chart 包含自定义资源定义，则跳过自定义资源定义的安装。默认为 false
      skipCrds: false

      # 如果 chart 包含 JSON schema 验证，则跳过 schema 验证。默认为 false
      skipSchemaValidation: false

      # 用于模板化的可选 Helm 版本。如果省略，它将回退到查看 Chart.yaml 中的 'apiVersion'
      # 并自动决定使用哪个 Helm 二进制文件。此字段可以是 'v2' 或 'v3'。
      version: v2

      # 你可以指定要传递给 Helm 以进行清单模板化的 Kubernetes API 版本。默认情况下，Argo CD 使用
      # 目标集群的 Kubernetes 版本。该值必须是 semver 格式。不要以 `v` 作为前缀。
      kubeVersion: 1.30.0

      # 你可以指定要传递给 Helm 以进行清单模板化的 Kubernetes 资源 API 版本。默认情况下，Argo
      # CD 使用目标集群的 API 版本。格式为 [group/]version/kind。
      apiVersions:
        - traefik.io/v1alpha1/TLSOption
        - v1/Service

      # 用于模板化的可选命名空间。如果留空，则默认为应用程序的目标命名空间。
      namespace: custom-namespace

    # kustomize 特定配置
    kustomize:
      # 可选的 kustomize 版本。注意：版本必须在 argocd-cm ConfigMap 中配置
      version: v3.5.4
      # 支持的 kustomize 转换器。https://kubectl.docs.kubernetes.io/references/kustomize/kustomization/
      namePrefix: prod-
      nameSuffix: -some-suffix
      commonLabels:
        foo: bar
      commonAnnotations:
        beep: boop-${ARGOCD_APP_REVISION}
      # 切换以启用/禁用 commonAnnotations 中的环境变量替换
      commonAnnotationsEnvsubst: true
      # 定义是否应将通用标签应用于资源选择器。它还将通用标签从
      # 模板中排除，除非 `labelIncludeTemplates` 设置为 true。
      labelWithoutSelector: false
      # 定义是否应将通用标签应用于资源模板。
      labelIncludeTemplates: false
      forceCommonLabels: false
      forceCommonAnnotations: false
      images:
        - quay.io/argoprojlabs/argocd-e2e-container:0.2
        - my-app=gcr.io/my-repo/my-app:0.1
      namespace: custom-namespace
      replicas:
        - name: kustomize-guestbook-ui
          count: 4
      components:
        - ../component # 相对于 kustomization.yaml (`source.path`)。
      # 使用 Kustomize 组件时，忽略本地缺失的组件目录。默认为 false
      ignoreMissingComponents: true
      patches:
        - target:
            kind: Deployment
            name: guestbook-ui
          patch: |-
            - op: add # Add new element to manifest
              path: /spec/template/spec/nodeSelector/
              value:
                env: "pro"

      # 你可以指定要传递给 Helm 以进行清单模板化的 Kubernetes API 版本。默认情况下，Argo CD 使用
      # 目标集群的 Kubernetes 版本。该值必须是 semver 格式。不要以 `v` 作为前缀。
      kubeVersion: 1.30.0

      # 你可以指定要传递给 Helm 以进行清单模板化的 Kubernetes 资源 API 版本。默认情况下，Argo
      # CD 使用目标集群的 API 版本。格式为 [group/]version/kind。
      apiVersions:
        - traefik.io/v1alpha1/TLSOption
        - v1/Service

    # 目录
    directory:
      recurse: true
      jsonnet:
        # Jsonnet 外部变量列表
        extVars:
          - name: foo
            value: bar
            # 你可以使用 "code" 来确定值是字符串（false，默认值）还是 Jsonnet 代码（如果 code 为 true）。
          - code: true
            name: baz
            value: "true"
        # Jsonnet 顶层参数列表
        tlas:
          - code: false
            name: foo
            value: bar
      # Exclude 包含一个 glob 模式，用于匹配应从清单生成过程中明确排除的路径。
      # 这优先于 `include` 字段。
      # 要匹配多个模式，请将模式用 {} 包裹并用逗号分隔。例如：'{config.yaml,env-use2/*}'
      exclude: "config.yaml"
      # Include 包含一个 glob 模式，用于匹配应在清单生成过程中明确包含的路径。
      # 如果设置了此字段，则仅包含匹配的清单。
      # 要匹配多个模式，请将模式用 {} 包裹并用逗号分隔。例如：'{*.yml,*.yaml}'
      include: "*.yaml"

    # 插件特定配置
    plugin:
      # 如果插件被定义为 sidecar 并且没有传递 name，插件将根据插件的发现规则自动匹配
      # Application。
      name: mypluginname
      # 传递给插件的环境变量
      env:
        - name: FOO
          value: bar
      # 插件参数在 v2.5 中是新增的。
      parameters:
        - name: string-param
          string: example-string
        - name: array-param
          array: [item1, item2]
        - name: map-param
          map:
            param-name: param-value

  # Sources 字段指定了应用程序的来源列表
  sources:
    - repoURL: https://github.com/argoproj/argocd-example-apps.git # 可以指向一个 Helm chart 仓库或一个 git 仓库。
      targetRevision: HEAD # 对于 Helm，这指的是 chart 的版本。
      path: guestbook # 对于直接从 Helm 仓库而不是 Git 拉取的 Helm chart，这个路径没有意义。
      ref: my-repo # 对于 Helm，它作为此源的引用，用于从此源获取 values 文件。在 `source` 字段下没有意义。

  # 部署应用程序的目标集群和命名空间
  destination:
    # 集群 API URL
    server: https://kubernetes.default.svc
    # 或集群名称
    # name: in-cluster
    # 命名空间只会为那些未设置 .metadata.namespace 值的命名空间范围资源设置
    namespace: guestbook

  # 在 Argo CD Application 详情标签页中显示的额外信息
  info:
    - name: "Example:"
      value: "https://example.com"

  # 同步策略
  syncPolicy:
    automated: # 自动同步默认会重试失败的尝试 5 次，每次尝试之间的延迟如下 ( 5s, 10s, 20s, 40s, 80s )；重试由 `retry` 字段控制。
      enabled: true # 启用应用程序的自动同步（默认为 true）。
      prune: true # 修剪，删除 Git 仓库中不再存在的集群资源。（默认为 false）。
      selfHeal: true # 自愈，当从 Git 仓库以外的方式修改资源状态时，将根据 Git 仓库中定义的配置自动执行同步操作。（默认为 false）。
      allowEmpty: false # 允许在自动同步期间删除所有应用程序资源（默认为 false）。
    syncOptions: # 修改同步行为的同步选项
      - Validate=false # 禁用资源验证（相当于 'kubectl apply --validate=false'）（默认为 true）。
      - CreateNamespace=true # 自动创建命名空间。
      - PrunePropagationPolicy=foreground # 支持的策略有 background（后台）、foreground（前台）和 orphan（孤立）。
      - PruneLast=true # 允许资源修剪作为同步操作的最终、隐式波次发生
      - RespectIgnoreDifferences=true # 在同步更改时，遵守 ignoreDifferences 配置忽略的字段
      - ApplyOutOfSyncOnly=true # 仅同步不同步的资源，而不是应用应用程序中的每个对象
      - SkipDryRunOnMissingResource=true # 允许跳过对缺失资源的空运行（dry run）
      - Replace=true # Argo CD 将使用 kubectl replace 或 kubectl create 命令来应用更改。
    managedNamespaceMetadata: # 设置应用程序命名空间的元数据。仅当 CreateNamespace=true（见上文）时有效，否则是空操作（no-op）。
      labels: # 要在应用程序命名空间上设置的标签
        any: label
        you: like
      annotations: # 要在应用程序命名空间上设置的注解
        the: same
        applies: for
        annotations: on-the-namespace

    # 重试功能自 v1.7 版本可用
    retry:
      limit: 5 # 失败同步尝试的重试次数；如果小于 0，则为无限次尝试
      backoff:
        duration: 5s # 退避的时长。默认单位是秒，但也可以是持续时间（例如 "2m"、"1h"）
        factor: 2 # 每次重试失败后用于乘以基础时长的因子
        maxDuration: 3m # 允许退避策略的最大时间量

  # 在差异对比期间，将忽略实时状态和期望状态之间的差异。请注意，除非启用了 `RespectIgnoreDifferences=true` 同步选项，否则这些配置不会
  # 在同步过程中使用。
  ignoreDifferences:
    # 对于指定的 json pointers
    - group: apps
      kind: Deployment
      jsonPointers:
        - /spec/replicas
    - kind: ConfigMap
      jqPathExpressions:
        # 示例：忽略 ConfigMap 中特定键的更改
        - '.data["config.yaml"]'
    # 对于指定的 managedFields managers
    - group: "*"
      kind: "*"
      managedFieldsManagers:
        - kube-controller-manager
      # name 和 namespace 是可选的。如果指定，它们必须完全匹配，这些不是 glob 模式。
      name: my-deployment
      namespace: my-namespace

  # RevisionHistoryLimit 限制了应用程序修订历史中保留的条目数量，这用于
  # 信息目的以及回滚到以前的版本。这应该只在特殊情况下更改。
  # 将其设置为零将不存储任何历史记录。这将减少存储使用。增加会增加用于存储历史记录的空间，
  # 因此我们不建议增加它。
  revisionHistoryLimit: 10
```

# 同步

Argo CD 允许用户自定义目标集群中所需状态的[**同步方式**](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-options/)。

# 相关项目

- Argo CD Git
- Argo CD Helm
- Todos Fullstack

# 解决方案

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

