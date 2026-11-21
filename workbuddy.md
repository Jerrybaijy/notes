---
title: workbuddy
author: Jerry.Baijy
tags:
  - dev
  - ai
  - agent
---

# Overview

[**WorkBuddy**](https://www.workbuddy.cn/) 是一个以办公自动化为主的 [AI Agent](ai-agent.md)。

> [WorkBuddy Docs](https://www.workbuddy.cn/docs/workbuddy/Overview)
>
> [WorkBuddy 网页版](https://www.workbuddy.cn/app)
>
> [WorkBuddy 开放平台](https://open.workbuddy.cn/)
>
> [WorkBuddy 开放平台 Docs](https://open.workbuddy.cn/docs)

# CLI

- WorkBuddy 内置 [CodeBuddy CLI](codebuddy-cli.md)，将 `C:\Program Files\WorkBuddy\resources\app.asar.unpacked\cli\bin` 加入[用户环境变量](windows.md#用户变量)，即可在全局使用。
- 也可安装完整的 [CodeBuddy CLI](codebuddy-cli.md)。

# 内置环境

WorkBuddy 内置多个运行环境：`设置` > `安全中心` > `内置运行时`

- Node.js
- Python
- Git Bash

# 记忆

长期记忆：`C:\Users\jerry\.workbuddy\$user-***\MEMORY.md`

# Skill

[WorkBuddy 的 skill 规范](https://open.workbuddy.cn/docs/skill#技能基础结构)并没有被纳入 [Anthropic 开放规范客户端展示](https://agentskills.io/clients)中。
