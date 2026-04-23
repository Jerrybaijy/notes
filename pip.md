---
title: pip
author: Jerry.Baijy
tags:
  - dev
  - dev-tools
  - package-managers
  - python
---

# Overview

[**Pip**](https://pip.pypa.io/en/stable/)（package installer for python）是 Python 包管理工具，默认情况下 `pip` 将从 [Python Package Index](https://pypi.org/) 安装软件包。

# Windows 系统

**Windows 常用命令：**

```bash
# 查看 pip 版本
pip --version
# 升级 pip
python -m pip install --upgrade pip

# 查看 pip 下载源
pip config get global.index-url
# 设置 pip 下载源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/

# 查看已经安装的第三方模块
pip list
# 查看需要升级的模块
pip list -o
# 升级模块
pip install --upgrade $MODULE_NAME

# 安装模块（选项为指定下载源）
pip install $MODULE_NAME
# 卸载第三方模块
pip uninstall $MODULE_NAME
# 一键卸载除 pip 以外的所有第三方模块
pip freeze | grep -v "pip==" | cut -d "=" -f 1 | xargs pip uninstall -y
# 显示模块信息
pip show $MODULE_NAME

# 将库列表保存到指定文件中（注意路径）
pip freeze > requirements.txt
# 从指定文件中安装库（注意路径）
pip install -r requirements.txt
```

**安装目录**：使用 pip 安装模块时，会被安装到 Python 环境中，而不是当前目录。

- 全局环境
- 虚拟环境

# Ubuntu 系统

**Ubuntu 常用命令：**

```bash
# Ubuntu 中安装 pip
sudo apt install python3-pip

# 查看 pip 版本
pip3 --version

# 升级 pip
sudo apt upgrade python3-pip

# 安装模块
pip3 install $MODULE_NAME
```

## Ubuntu 中配置 pip 下载源

- 创建 pip 配置目文件

  ```bash
  mkdir -p ~/.config/pip
  nano ~/.config/pip/pip.conf
  ```

- 编辑配置文件，添加清华镜像源

  ```
  [global]
  index-url = https://pypi.tuna.tsinghua.edu.cn/simple/
  ```

- 查看已配置的下载源

  ```bash
  pip config get global.index-url
  ```
