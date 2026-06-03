---
title: win-wsl
author: Jerry.Baijy
tags:
  - dev
  - software
  - windows
  - vm
---

# Overview

[**WSL**](https://learn.microsoft.com/zh-cn/windows/wsl/about)（Windows Subsystem for Linux，适用于 Linux 的 Windows 子系统） 是 Windows 的一项功能， 基于 Hyper-V，可用于在 Windows 计算机上运行 Linux 环境，而无需单独的虚拟机或双重启动。

> [WSL Doc](https://learn.microsoft.com/zh-cn/windows/wsl/)

# Install

> [安装 WSL 和 Linux 分发版](https://learn.microsoft.com/zh-cn/windows/wsl/install)

## 前提条件

- Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11
    - 较旧的 Windows 版本或 Windows Server Core 参照[旧版 WSL 的手动安装步骤](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)
- [开启 CPU 虚拟化](<windows.md#开启 CPU 虚拟化>)

## Install

- 以**管理员**身份打开终端

- 如遇网络问题可多试几次

    > [!TIP]
    > 开启科学上网，可大大加快下载速度。

### 安装 WSL

- 安装 WSL

    ```bash
    wsl --install
    ```

- 重启系统生效

- 查看 WSL 版本

    ```bash
    wsl -v
    ```

- 安装 WSL 后，软件列表会出现两个图标：
    - WSL
    - WSL Settings

### 安装 Linux 分发版

- 查看可用的 Linux 分发版

    ```bash
    wsl --list --online
    ```

- 安装指定的 Linux 分发版

    ```bash
    wsl --install [Distro]
    wsl --install Ubuntu-24.04
    ```

- 安装成功以后会先设置 Linux 用户名和密码

- 然后自动进入 Linux 系统，执行 `exit` 命令退出 Linux 系统。

- 查看已安装的 Linux 分发版

    ```bash
    wsl -l -v
    ```

- 重启终端，Windows Terminal 下拉菜单会自动出现 `Ubuntu-24.04` 选项。

## WSL 网络配置

- 安装 Linux 分发版以后，[查看主机网卡](<windows.md#查看网卡>)，会自动创建一个 `vEthernet (WSL (Hyper-V firewall))` 虚拟网卡。

- 当停止 Linux 后，主机网络会出现 DNS 异常，此时需要配置 WSL 的网络模式为 `Mirrored` 模式。

    - 运行 WSL Settings：`网络` > `网络模式`：切换为 `Mirrored`

    - 或者在 `~` 目录下创建 `.wslconfig` 文件

        ```
        [wsl2]
        networkingMode=mirrored
        ```

    - 重启 WSL 和 Linux 生效。

    - 此模式会镜像主机网络的 DNS 和网络代理。

# 基本命令

> [WSL 的基本命令](https://learn.microsoft.com/zh-cn/windows/wsl/basic-commands)

```bash
# 安装 wsl
wsl --install
# 更新 WSL
wsl --update
# 检查 WSL 版本
wsl --version
wsl -v

# 列出可用的 Linux 分发版
wsl --list --online
wsl -l -o
# 列出已安装的 Linux 分发版
wsl --list --verbose
wsl -l -v

# 检查 WSL 状态
wsl --status
# 关机
wsl --shutdown
```

