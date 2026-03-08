---
title: win-chocolatey
author: Jerry.Baijy
tags:
  - it
  - 包管理工具
  - windows
---

## Overview

Chocolatey 是一个功能强大的 Windows 包管理工具。

# Install

**安装**：以管理员身份运行 PowerShell 安装，但可以在 Bash 中使用。

```powershell
# 安装
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# 查看版本
choco -v
```

# 其它

```bash
choco install <app>
```
