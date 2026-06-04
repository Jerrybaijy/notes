---
title: pyenv
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - version-managers
  - python
---

# Overview

[**Pyenv**](https://github.com/pyenv/pyenv) 是一个 Python 版本管理工具， 可以让您在多个 Python 版本之间切换。

[**Pyenv-win**](https://github.com/pyenv-win/pyenv-win) 是 Pyenv 的 Windows 版本。

# Install

- 在当前 PowerShell 会话中临时允许运行脚本（关闭窗口后自动恢复默认安全模式）。

  ```powershell
  Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
  ```

- 在 PowerShell 中安装 pyenv-win。

  ```powershell
  Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
  ```

- 重启终端，在 GitBash 中运行一下命令检查安装是否成功。

    ```bash
    pyenv --version
    ```


# Quickstart

- 安装指定版本 python

  ```bash
  pyenv install <version>
  pyenv install 3.13.7
  ```

  安装路径：`C:\Users\jerry\.pyenv\pyenv-win\versions`

- 设置全局 python 版本

  ```bash
  # 设置
  pyenv global 3.13.7
  # 查看
  pyenv global
  ```

- 如果只希望在一个**特定项目文件夹**中使用 **Python 3.13.7**，请进入该文件夹并执行以下命令：

  > [!Warning]
  > 此处只记录这种用法，在项目中现已使用 [pdm](pdm.md) 指定 Python 版本。
  
  ```bash
  pyenv local 3.13.7
  ```
  
  执行后，`pyenv-win` 会在该文件夹下创建一个 `.python-version` 文件，仅对该文件夹及其子目录生效。

# 命令

```bash
# 查看 pyenv 版本
pyenv --version
# 升级 pyenv
pip install --upgrade pyenv-win

# 查看所有通过 Python 安装的 python 版本
pyenv versions

# 查看当前正在使用的 Python 版本及其路径
pyenv version

# pyenv-win 支持的 Python 版本列表
pyenv install -l

# 安装 <version> 版本的 python
pyenv install <version>

# 卸载 <version> 版本的 python
pyenv uninstall <version>
```

# FAQ

## 执行别名

在执行 `where python` 时，会多出一行 `C:\Users\jerry\AppData\Local\Microsoft\WindowsApps\python.exe`，这个是 Windows 自带的“Python 应用执行别名”，经常干扰 pyenv。

关闭 Windows 的 Python App 执行别名：

- `设置` > `应用` > `高级应用设置` > `应用执行别名`
- 把下面两个关掉：
  - `python.exe`
  - `python3.exe`
- 重启所有终端