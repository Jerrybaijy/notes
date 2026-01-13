---
title: windows-terminal
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - terminal
---

# Overview

[**Windows Terminal**](https://apps.microsoft.com/detail/9n0dx20hk701) 是 Windows 系统下的终端集合工具。

> [Windows Terminal Docs](https://learn.microsoft.com/zh-cn/windows/terminal/)

# Install

Microsoft Store 安装

# Config

- 下拉菜单中进入设置
- 左下角打开 JSON 文件，用 VS Code 编辑
- `notes` 笔记中有配置文件
- 主题：针对 Windows Terminal 全局
- 配色方案：针对各个窗口

# FAQ

## 添加终端

- 以 Git Bash 为例（Git Bash 可以在安装时勾选 `添加到 Windows Terminal`）

- 如果安装 Git Bash 时没有勾选 `添加到 Windows Terminal`，则执行以下步骤

- 电脑中安装好 Git

- 在 Microsoft Store 中安装 Windows Terminal 并运行

- 下拉菜单中进入设置

- 左下角打开 JSON 文件，用 VS Code 编辑

- 将以下内容加入到 `profiles` 的 `list` 中添加一项

  ```json
  {
    "guid": "{96E6AB7F-8963-20F8-5068-014DFAA8C12A}",
    "name": "Git Bash",
    "commandline": "D:\\Program Files\\Git\\bin\\bash.exe -l -i",
    "startingDirectory": "C:/Users/jerry",
    "icon": "D:\\Program Files\\Git\\mingw64\\share\\git\\git-for-windows.ico"
  }
  ```

  **在以上代码中**：

  - **`guid`**：唯一标识本命令行配置，可以使用[在线 guid 工具](http://tool.pfan.cn/guidgen)随机生成一个和 `list` 中其他配置不一样的 `guid` 即可。
  - **`name`**：本命令行配置的名字，会显示在菜单中。
  - **`commandline`**：表示如何启动一个命令行，前面是 Git Bash 的安装目录。
    - **`- l`**：表示以登录模式启动 Bash shell
    - **`- i`**：表示以交互模式启动 Bash shell

  - **`startingDirectory`**：启动时默认进入的目录
  - **`icon`**：显示在菜单中的图标

- 保存以后直接在下拉菜单打开 Git Bash。

## 无法读取历史命令

当再次进入 Git Bash，向上翻命令时，无法读取历史命令，可用如下方法解决：

- 进入用户目录。

- 记事本创建文件，在文件中添加以下内容。

  ```bash
  # 设置历史文件位置和大小
  export HISTFILE=~/.bash_history
  export HISTFILESIZE=1000
  export HISTSIZE=1000
  
  # 追加历史记录而不是覆盖
  shopt -s histappend
  
  # 实时更新历史记录
  PROMPT_COMMAND="history -a;$PROMPT_COMMAND"
  ```

- 保存以后，将文件名改为 `.bashrc`。

- 重启终端生效。