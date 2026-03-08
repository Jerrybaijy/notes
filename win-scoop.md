---
title: win-scoop
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - 包管理工具
---

# Overview

[**Scoop**](https://github.com/ScoopInstaller/Scoop/wiki) 是一个开源的 Windows 包管理工具。

Scoop 的设计哲学是**“轻量、绿色、非侵入式”**。

- **无弹窗，无全家桶**：安装软件时，没有安装程序界面，没有“下一步”，更没有捆绑软件。
- **非管理员权限**：默认安装在 `C:\Users\<用户名>\scoop` 下，不需要 UAC 管理员授权，不会污染系统的 C:\Program Files。
- **不污染注册表**：尽可能将程序安装为“绿色版”，保持系统注册表干净。
- **自动处理环境变量**：安装完编译器（如 Python, Go, Node.js）后，它会自动把路径挂载到 `shims` 文件夹并加入 PATH，你开箱即用。
- **版本切换极其简单**：通过 `scoop reset` 命令，你可以秒级在不同版本的 Java 或 Node.js 之间切换。

# Install

```bash
# PowerShell 临时授权
powershell -Command "Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass"

# 安装
powershell -Command "iwr -useb get.scoop.sh | iex"

# 查看版本（重启终端）
scoop --version
```



```bash
# 查看已安装软件
scoop list
```

# Quickstart

- Install

- 添加 Bucket

  ```bash
  scoop bucket add exstras
  scoop bucket add scoopcn https://github.com/scoopcn/scoopcn.git
  scoop bucket add dorado https://github.com/chawyehsu/dorado.git
  ```

- 安装软件

  ```bash
  scoop install qqmusic
  ```

# Bucket

建议你的 Scoop 桶组合保持在 3-4 个即可，太多会影响 `scoop search` 的速度：

1. **`main`**: 核心开发工具（默认已装）。
2. **`extras`**: 国外桌面软件（你已装）。
3. **`scoopcn`**: **核心推荐**，搞定所有国产软件。`scoop bucket add scoopcn https://github.com/scoopcn/scoopcn.git`
4. **`dorado`**: 可选，如果你在 `scoopcn` 里找不到某个软件，这里通常有惊喜。

```bash
# 添加
scoop bucket add <bucket> [bucket-dir]
scoop bucket add scoopcn https://github.com/scoopcn/scoopcn.git

scoop bucket list
```

