---
title: openclaw
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - ai
---

# Overview

[OpenClaw](https://docs.openclaw.ai/zh-CN)

```bash
# 打开浏览器 UI 面板
openclaw dashboard

# 使用 ollama 启动 openclaw
ollama launch openclaw
```

# Install

- Git 已安装

- Node.js (≥22.0) 已安装

- [安装 OpenClaw](https://docs.openclaw.ai/install)

  > [阿里云教程](https://developer.aliyun.com/article/1709772)
  
  ```bash
  # 安装
  curl -fsSL https://openclaw.ai/install.sh | bash
  
  # 浏览器面板
  openclaw dashboard
  ```
  

# Uninstall

```bash
# 卸载程序
openclaw uninstall --all --yes --non-interactive

# 卸载 CLI
npm rm -g openclaw

# 手动删除残留
# C:\Users\jerry\.ollama
```

# Channels

## Telegram

- Telegram 搜索 `@BotFather`

- 发送 `/newbot`，创建新机器人。

- 发送机器人名字

- 发送用户名

- 复制 Token 到 OpenClaw

- 点击链接进入机器人

- 复制 Pairing code，执行以下命令

  ```bash
  openclaw pairing approve telegram $YOUR_PAIRING_CODE
  ```

  返回以下内容则成功

  ```
  Approved telegram sender *******
  ```

  