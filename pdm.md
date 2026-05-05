---
title: pdm
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - project-managers
  - package-managers
  - python
---

# Overview

[**PDM**](https://pdm-project.org/zh-cn/latest/) (Python Development Master) 是一个现代 Python 项目管理工具，它支持最新 PEP 标准。

> [Docs](https://pdm-project.org/zh-cn/latest/)
>
> [Reference](https://pdm-project.org/zh-cn/latest/reference/pep621/)
>
> [GitHub](https://github.com/pdm-project/pdm)

PDM 具有如下功能：

- 项目管理
- 依赖管理
- 虚拟环境管理
- 安装 Python
- Python 解释器管理
- 更多...

# Install

> [安装](https://pdm-project.org/zh-cn/latest/#_3)

使用 [pipx](pipx.md) 安装 pdm，以供全部 Python 版本使用。

```bash
pipx install pdm
pdm --version
```

# Quickstart

## 初始化项目

```bash
mkdir my-project && cd my-project
pdm init
```

# `add`

[`add`](https://pdm-project.org/zh-cn/latest/reference/cli/#add) 命令用于将依赖添加至 `pyproject.toml`，并安装依赖。

# `init`

[`init`](https://pdm-project.org/zh-cn/latest/reference/cli/#init) 命令用于初始化 `pyproject.toml` 以使用 PDM。

```bash
pdm init
```

**有如下选项**：

- **选择 Python 解释器**
  - 生成虚拟环境目录 `.venv`
  - 

# `run`

[`run`](https://pdm-project.org/zh-cn/latest/reference/cli/#run) 命令用于运行命令或脚本。

可以使用脚本别名简化 pdm 的启动命令

- `pyproject.toml`

  ```toml
  [tool.pdm.scripts]
  dev = "uvicorn ga.main:app --reload"
  ```

- 执行以下命令启动 Python 应用

  ```bash
  pdm run dev
  
  # 代替以下完整命令
  pdm run uvicorn ga.main:app --reload
  ```

# `install`

[`install`](https://pdm-project.org/zh-cn/latest/reference/cli/#install) 命令用于从依赖锁定文件安装依赖项。