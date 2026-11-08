---
title: browser-skill
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - ai
  - agent
  - browser
---

# Overview

[BrowserSkill](https://github.com/Tencent/BrowserSkill) 是一个腾讯开源的、允许 Agent 使用**真实浏览器**的 CLI 工具。

# Install

> [Install](https://github.com/Tencent/BrowserSkill/blob/main/AGENT_INSTALL.md)

## Windows

1. 安装 BrowserSkill CLI

    ```powershell
    irm https://raw.githubusercontent.com/Tencent/BrowserSkill/main/install.ps1 | iex
    ```

2. 查看版本

    ```bash
    bsk --version
    ```

3. 列出当前环境能装 skill 的 Agent 目标

    ```bash
    bsk install-skill --list --json
    ```

4. 为 Claude Code 安装名为 `browser-skill` 的 skill

    ```bash
    bsk install-skill --harness claude-code --json
    ```

5. 为浏览器安装 [BrowserSkill](https://chromewebstore.google.com/detail/hhcmgoofomhgciiibhipgmgkgnoenaoi) 扩展
6. 保持 Claude Code 和浏览器开启
7. Claude Code 可以使用**真实浏览器**

# 窗口局限性

浏览器有两个窗口：

- User 窗口：用户自己用的窗口
- Agent 窗口：Agent 打开的窗口（同一个浏览器的分离窗口）

bsk 的局限性：

- 在每次 `session start` 时，必须开启 Agent 窗口，无法更改。
- User 窗口只能读，不能操作。

在需要操作网页时，bsk 的默认操作是：

- 新开 Agent 窗口
- 在 Agent 窗口中再打开一个网页（即使 User 窗口中已经有相应 tab 页）

在 [Claude Code 用户级记忆](claude-code.md#用户级记忆)中添加以下约束，可以解决**在 Agent 窗口中再打开一个网页**的问题。

```markdown
## 操作浏览器优先借用用户标签页

用 bsk 操作网页时：

- 先 `bsk tab list --scope user` 查用户窗口有没有现成标签页；有就 `tab borrow` 借用，干完 `tab return` 归还，别在 Agent Window 里重开同一个网页。
- 没有就在 Agent Window 新开（`navigate` / `tab create`）。
- 动手前先只读确认：`get-html` / `snapshot` / `screenshot` 对用户标签页直接可用，不用借。
- 一次对话只开一个 session，中途不停，最后统一 `bsk session stop`。
```

