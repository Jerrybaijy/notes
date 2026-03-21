---
title: openclaw
author: Jerry.Baijy
tags:
  - it
  - ai
  - openclaw
---

# Overview

> [OpenClaw](https://docs.openclaw.ai/zh-CN)
>
> [CLI](https://docs.openclaw.ai/zh-CN/cli)

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

| 来源       | 优先级   | 用途                       | 升级时        |
| ---------- | -------- | -------------------------- | ------------- |
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

# 工作空间

工作空间 `~/.openclaw/workplace/` 是 OpenClaw 的"家"，主要有这些作用：

```
C:\Users\jerry\.openclaw\workspace\
├── .openclaw/                    # OpenClaw 运行时状态
├── memory/                       # 记忆目录
│   └── 2026-03-20.md             # 每日记忆日志
├── outputs/                      # 输出目录（个人创建）
├── skills/                       # 自定义技能（个人创建）
├── AGENTS.md                     # 工作空间指南（行为准则）
├── BOOTSTRAP.md                  # 启动指南（首次运行）
├── HEARTBEAT.md                  # 心跳任务配置
├── IDENTITY.md                   # Agent 身份定义
├── SOUL.md                       # Agent 人格定义
├── TOOLS.md                      # 工具本地笔记
└── USER.md                       # User 信息
```

# 浏览器插件

```bash
# 安装插件
openclaw browser extension install

# OPENCLAW_GATEWAY_TOKEN
openclaw configure --section gateway
```

# 浏览器管理

> https://docs.openclaw.ai/zh-CN/tools/browser
>
> https://docs.openclaw.ai/zh-CN/cli/browser

以下是 OpenClaw 提供的浏览器管理命令，专门用于通过命令行（CLI）直接操控和观察一个“受控”的浏览器实例。

```bash
# 启动浏览器：连接到浏览器（需提前开启 Remote debugging）
openclaw browser --browser-profile user start
# 查看状态：
openclaw browser --browser-profile user status
# 列出标签页
openclaw browser --browser-profile user tabs
# AI 网页快照
openclaw browser --browser-profile user snapshot --format ai
```

临时存储

```
当我打开Boss直聘“推荐牛人”页面时，浏览器URL是“https://www.zhipin.com/web/chat/recommend”，但是当我点开某个简历的详情时，有简历弹窗弹出，浏览器URL还是“https://www.zhipin.com/web/chat/recommend”，所以，它可能存在于 iframe 中。

那么现在问题来了，当我使用“openclaw browser --browser-profile user snapshot --format ai”命令去抓取时，抓到的是“推荐牛人”页面的简历列表，而不是简历弹窗里的详情内容。此时我要的是弹窗里面的内容，而不是“推荐牛人”页面的简历列表。
```

```
- 你通过 Remote debugging 的方式打开 `https://www.zhipin.com/web/chat/recommend` 这个网页
- 这个网页有一系列简历列表，有多个候选人的基本信息
- 你点击第二个候选人的姓名，就会打开他的简历弹窗
- 如果你检测到了这个弹窗，请告诉我一声，然后继续工作。
- 把简历弹窗的完整简历信息拿回来，以 json 格式存入 `./outputs/resumes/` 目录
```

```
- 前端渲染是“懒加载”的（元素不在视口就不绘制 Canvas），在你点开简历弹窗以后，需要将简历页面从上到下缓慢滚动到底部，强迫页面将所有简历信息都绘制一遍，从而确保沙箱脚本能收窄抓取到所有的文字数据。滚动的核心方法在 `./resumes/content-script.ts`（在第 24 行左右开始）。
- Convas 劫持的方法在 `./resumes/sandbox.ts 文件。
- 这两个文件是我以前开发的浏览器插件中的文件，现在拿出来给你参考。
```

```
通过 user profile 浏览器打开 https://www.zhipin.com/web/chat/recommend
```

