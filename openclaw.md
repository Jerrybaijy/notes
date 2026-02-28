---
title: openclaw
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - ai
  - openclaw
---

# Overview

[OpenClaw](https://docs.openclaw.ai/zh-CN)

```bash
# 打开浏览器 UI 面板
openclaw dashboard

# 使用 ollama 启动 openclaw
ollama launch openclaw

# 重启网关
openclaw gateway restart

# 配置 sections
openclaw configure --section default_model
```

# Install

[安装 OpenClaw](https://docs.openclaw.ai/install)

> [阿里云教程](https://developer.aliyun.com/article/1709772)

```bash
# Linux/MacOS
curl -fsSL https://openclaw.ai/install.sh | bash

# Windows PowerShell (管理员)
iwr -useb https://openclaw.ai/install.ps1 | iex
```

# Uninstall

```bash
# 卸载程序 (C:\Users\jerry\)
openclaw uninstall --all --yes --non-interactive

# 卸载 CLI (C:\Users\jerry\AppData\Roaming\npm\node_modules\openclaw)
npm rm -g openclaw

# 手动删除残留
# C:\Users\jerry\.openclaw
```

# Skills

## Skill 目录

- 系统自带：`C:\Users\jerry\AppData\Roaming\npm\node_modules\openclaw\skills\`
- 全局目录：`C:\Users\jerry\.openclaw\skills\`
- 工作区目录：`C:\Users\jerry\.openclaw\workspace\skills\`

| 来源       | 优先级   | 用途                       | 升级时       |
| ---------- | -------- | -------------------------- | ------------ |
| 系统自带   | **最低** | OpenClaw 内置技能          | ⚠️ 可能被覆盖 |
| 全局技能   | **中**   | 用户全局安装的技能         | ✅ 保留       |
| 工作区技能 | **最高** | 项目专属技能、开发中的技能 | ✅ 保留       |

## 安装 Skill

### 手动安装

- 从 [ClawHub](https://clawhub.ai/)下载 skill 压缩包
- 解压并按需复制到以下任一目录
  - 全局目录：`C:\Users\jerry\.openclaw\skills\`
  - 工作区目录：`C:\Users\jerry\.openclaw\workspace\skills\`
- 安装后需要**重启 OpenClaw 会话**才能加载新技能。

### 通过 CLI 安装

详见 [ClawHub](<clawhub.md#安装 Skill>)

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

  

# 浏览器插件

```bash
# 安装插件
openclaw browser extension install

# OPENCLAW_GATEWAY_TOKEN
openclaw configure --section gateway
```

