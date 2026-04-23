---
title: pipx
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - python
---

# Overview

[**Pipx**](https://pipx.pypa.io/stable/) 是一个专门用于安装和运行 **Python 命令行应用程序**（CLI 工具）的工具。它的核心目标是将 Python 工具安装在隔离的环境中，同时让你能像使用普通系统命令一样直接在终端调用它们。

> [Docs](https://pipx.pypa.io/stable/#documentation)
>
> [Reference](https://pipx.pypa.io/stable/reference/)

# Install

> [Installing pipx](https://pipx.pypa.io/stable/how-to/install-pipx/)

## Windows

- 使用 [**Scoop**](scoop.md) 安装

  ```bash
  scoop install pipx
  ```

- 添加环境变量

  ```bash
  pipx ensurepath
  ```

- 查看版本

  ```bash
  pipx --version
  ```

  