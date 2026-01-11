---
title: gitlab-container-registry
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
  - gitlab
  - registry
---

# Overview

**GitLab Container Registry** 是 GitLab 的镜像仓库，兼容 OCI 标准。每个项目有各自的项目级仓库。

- **公共 GitLab.com：** `registry.gitlab.com`
- **自建/私有 GitLab：** 您的实例地址，例如 `gitlab.example.com:4567`

**如何查看**：进入项目 > 左侧边栏 > `Deploy` > `Container registry`

[`<oci-registry>` 格式](<dev-ops.md#OCI 地址格式>)：

```
oci://<registry>/<namespace>/<project-name>
oci://registry.gitlab.com/jerrybai/todo-fullstack
```
