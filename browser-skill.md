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
