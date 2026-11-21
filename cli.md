---
title: cli
author: Jerry.Baijy
tags:
  - dev
  - computer
  - 交互工具
  - cli
---

# Overview

**CLI**（**C**ommand **L**ine **I**nterface，命令行界面），是一种通过输入文本命令与计算机或软件交互的方式。与 [**GUI**](computer.md#GUI)（图形用户界面）不同，CLI 主要依赖键盘输入命令行指令，而不是鼠标点击操作。

## **CLI 的特点**

- **高效性**：比 GUI 快速，适用于自动化任务。
- **可编写脚本**：CLI 命令可以编写成脚本，自动化执行任务。
- **资源占用低**：比 GUI 需要的计算资源更少。
- **远程操作**：可以通过 SSH 远程管理服务器。
- **精准控制**：提供更细粒度的操作能力。

## CLI 实例

- **Windows** ：CMD、[PowerShell](powershell.md)、[Windows Terminal](windows-terminal.md) 和 Git Bash
- **Linux / macOS**：Terminal

# 常识和快捷键

在命令行界面有以下常识和快捷键：

- **大小写**：命令中的大小写不敏感（Windows 中的文件名敏感）
- **`$`**：行首的 `$` 表示终端正在等待输入命令
- **跨行输入**：行尾使用 `\`
- **多条命令**：以 `;` 隔开

<!-- prettier-ignore -->
| 操作 | 快捷键 |
| :---: | :---: |
| ==光标== |  |
| 将光标移动到行首 | <kbd>Home</kbd> \| <kbd>Ctrl</kbd> + <kbd>A</kbd> |
| 将光标移动到行尾 | <kbd>End</kbd> \| <kbd>Ctrl</kbd> + <kbd>E</kbd> |
| ==退出== |  |
| 强制从输出中退出 | <kbd>Ctrl</kbd> + <kbd>C</kbd> |
| 退出系统 | `exit` \| <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| ==复制粘贴== |  |
| 复制 | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> |
| 粘贴 | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>V</kbd> |
| ==删除== |  |
| 删除光标到行首的内容 | <kbd>Ctrl</kbd> + <kbd>U</kbd> |
| 删除光标到行尾的内容 | <kbd>Ctrl</kbd> + <kbd>K</kbd> |
| ==其它== |  |
| 向上/下翻一条命令 | <kbd>↑</kbd> \| <kbd>↓</kbd> |

# Curl

`curl` 是一个用于与网络服务器进行数据交换的命令行工具。

## Install

```bash
sudo apt install curl
curl --version
```

## 下载文件

- 下载并显示文件内容

    ```bash
    curl http://example.com/file.txt
    ```

- 下载的文件，并按原文件名保存

    ```bash
    curl -O http://example.com/file.txt
    ```

- 下载的文件，并按指定路径和文件名保存

    ```bash
    curl -o myfile.txt http://example.com/file.txt
    ```

## 上传文件

- 上传文件

    ```bash
    curl -X POST -F "file=@myfile.txt" http://example.com/upload
    ```

# tldr

**tldr** 是一个简化的命令行工具，名字来源于 "Too Long; Didn't Read"，旨在提供比传统 `man` 页面更简洁、更实用的命令帮助信息。

- 安装

    ```bash
    sudo apt update && sudo apt full-upgrade
    sudo apt install tldr
    ```

- 升级

    ```bash
    tldr --update
    ```

- 使用（以 `apt` 为例）

    ```bash
    tldr apt
    ```

