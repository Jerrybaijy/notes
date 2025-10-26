---
title: anaconda
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - ai
  - ai-agent
---

# Anaconda

**Anaconda** 是一个专为**数据科学**、**机器学习**和**大规模数据处理**设计的开源 Python 和 R **语言发行版本**。

它是一个**集成平台**，旨在简化数据科学领域的软件包管理和部署。包含内容：

- **Conda：** 环境和包管理器（**核心**）。
- **Python/R 语言解释器：** 预装。
- **大量预装的数据科学库：** 包含超过 1400 个流行的包，如 NumPy、Pandas、SciPy 等，用户无需单独安装。
- **Anaconda Navigator：** 一个图形用户界面 (GUI) 工具，方便管理环境、启动应用程序和访问文档等。

# Conda

## Conda

**Conda** 是一个**开源**的**包管理系统**（Package Manager）和**环境管理系统**（Environment Manager）。它是 Anaconda 发行版的核心组成部分，但也可以独立使用（例如通过 **Miniconda** 安装）。

- **包管理：** 类似于 Python 的 `pip`，可以安装、更新、删除软件包及其依赖项。但 Conda 的强大之处在于它**语言无关**，可以管理 Python、R、Ruby、Scala、Java 甚至是 C/C++ 库的包。
- **环境管理：** 这是 Conda 的**关键功能**。它允许用户创建多个**相互隔离**的虚拟环境，每个环境可以拥有自己独立的 Python 版本和一套包集合。

## 常用命令

```bash
# 创建虚拟环境
# conda create -n 环境名称 python=版本 -y
conda create -n medibot python=3.10 -y

# 激活虚拟环境
# conda activate 环境名称
conda activate medibot
```

## 在 Git Bash 中启用 `conda` 命令

在 Windows 系统上，即使安装了 Anaconda，Conda 命令默认也只在 Anaconda 自己的命令行环境（如 Anaconda Prompt）中能直接识别，而在其他第三方终端（如 Git Bash、PowerShell、或普通的 Command Prompt）中通常无法直接运行，除非您手动进行了配置。

- 打开 Anaconda Prompt 执行初始化命令：

  ```bash
  conda init bash
  ```
- 重启 Git Bash 生效
- 默认所有命令的输出会以 `(base)` 结尾，除非有虚拟环境。

## 创建虚拟环境

```bash
# 创建虚拟环境
# conda create -n 环境名称 python=版本 -y
conda create -n medibot python=3.10 -y

# 激活虚拟环境
# conda activate 环境名称
conda activate medibot

# 退出环境
conda deactivate
```

- 虚拟环境相关文件存储在目录：`C:\Users\jerry\.conda\envs\medibot`
- 如果没有指定版本的 Python 解释器，conda 会自动下载到虚拟环境的存储目录。
- 激活虚拟环境以后：
  - 所有命令的输出会以环境名称结尾，如 `(medibot)`。
  - VS Code 需手动选择虚拟环境
  - 所有通过 `conda` 和 `pip` 安装的包，都会安装到虚拟环境的存储目录。
