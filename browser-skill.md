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

> [CLI Reference](https://browserskill.weixin.qq.com/#commands)

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

# CLI

```bash
# 健康检查
bsk doctor

# 查看状态
bsk status
```

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

在 Agent **用户级记忆**文件或 Skill 文件中添加以下约束，可以解决**在 Agent 窗口中再打开一个网页**的问题。

```markdown
## 浏览器自动化（browser-skill / bsk CLI）

执行任何浏览器任务时，遵循以下两条规则：

1. **优先借用 user scope 标签页**：开工前先 `bsk tab list --scope user --json`，如果用户窗口里已经有目标网页，就 `bsk tab borrow <tab-id>` 借用它来操作，不要另开新页；相关步骤结束后立即 `bsk tab return <tab-id>` 还回用户窗口（还回后页面仍保持打开）。
2. **收尾关闭 agent scope**：任务结束时，把我自己创建的 agent 标签页显式 `bsk tab close <tab-id>` 全部关掉，不依赖 `session stop` 的隐式清理。

注意：若在关窗后仍需给用户保留某个页面，先把该页移到/交给 user 窗口，或在收尾前向用户确认。
```

# 问题排查

```
jerry@PC-Jerry-2 MINGW64 ~
$ bsk doctor
waiting for browser extension to connect… (if it is installed: check that a window with the extension enabled is open in the expected profile and that it targets this daemon; reinstall from the store if missing)
ok    bsk home writable                C:\Users\jerry\.bsk
ok    agent skill matches bundled CLI  bundled bsk v0.4.2; already matches bundled CLI: claude-code, workbuddy
ok    daemon running                   pid 35180 at ws://127.0.0.1:52800 (sock \\.\pipe\bsk-daemon-7fdb4c3b4c05e0d4)
ok    daemon local process identity    IPC peer PID matches daemon identity
ok    protocol compatible              daemon protocol 1.8 (app 0.4.2)
ok    auto-update                      no update attempt recorded
FAIL  extension connected              0 browsers connected — hint: if the extension is not installed, install it from https://chromewebstore.google.com/detail/hhcmgoofomhgciiibhipgmgkgnoenaoi (Chrome) or https://microsoftedge.microsoft.com/addons/detail/browserskill/emacgiaaaiojkkpkddmmdfhmokgmnikg (Edge); if it is already installed, it is not connected to this daemon — keep a window of that browser open with the extension enabled in the profile you are using (the extension is per-profile), point the extension at this daemon's address/port, and reload the extension if it was just updated
N/A   browser protocol compatible      no browsers online, nothing to compare
```

