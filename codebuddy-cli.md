---
title: codebuddy-cli
author: Jerry.Baijy
tags:
  - dev
  - cli
  - codebuddy
  - workbuddy
---

# Overview

[CodeBuddy CLI](https://www.workbuddy.cn/docs/cli/overview) 是 [CodeBuddy](https://www.codebuddy.cn/) 的 CLI 工具。

> [CodeBuddy CLI Docs](https://www.workbuddy.cn/docs/cli/overview)
>
> [CodeBuddy CLI Reference](https://www.workbuddy.cn/docs/cli/reference)

# Install

> [CodeBuddy CLI Installation](https://www.workbuddy.cn/docs/cli/installation)

# Quickstart

1. 进入交互模式

    ```bash
    codebuddy
    ```

2. 登录：第一次进入交互模式会直接要求登录：

    ```bash
    Select login method:
     ❯ Log in via Chinese Site
       Log in via International Site
       Log in via Enterprise Domain
       Log in via iOA (Tencent only)
    ```

3. 可以在非交互模式下与 Codebuddy 对话交互

    ```bash
    codebuddy -p "<text>"
    ```

# Command

```bash
# 进入交互模式（npm 版本支持别名 cbc）
codebuddy

# 查看版本
codebuddy -v

# 登录
/login
```

