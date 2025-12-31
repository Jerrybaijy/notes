---
title: gitlab-ci-cd-yaml
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
  - gitlab
  - gitlab-ci-cd
  - code-language
---

# Overview

[**CI/CD YAML 语法**](CI/CD YAML 语法)是 GitLab CI/CD 的适用语法。

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
