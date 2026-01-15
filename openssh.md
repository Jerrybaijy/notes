---
title: openssh
author: Jerry.Baijy
tags:
  - 应用科学
  - it
---

# Overview

**SSH (Secure Shell)** 是一种加密的网络传输协议，用于在不安全的网络中为网络服务提供安全的传输层。

[**OpenSSH**](https://www.openssh.org/) 是 SSH 协议的**免费开源版本**。它是目前 Linux、Unix（包括 macOS）以及现代 Windows 系统中默认使用的 SSH 工具集。

> [OpenSSH Docs](https://www.openssh.org/manual.html)

# Install

系统默认提供

# Quickstart

## 创建 SSH 密钥对

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/<secret_key_name> -C <comment>
ssh-keygen -t rsa -b 2048 -f ~/.ssh/my_secret_key -C my-comment
```

## 获取 SSH 公钥

```bash
cat ~/.ssh/my_secret_key.pub
```

## 配置 SSH 公钥

- 复制公钥内容，粘贴至其它平台公钥区域
- 例：创建 GCE 实例时，在 `Security` > `Manage access | Add manually generated SSH keys` > `Add item` 手动添加本地 `my_secret_key.public` 内容。

## 连接实例

- 复制私钥 `my_secret_key` 到任一电脑的 `~/.ssh` 目录（以 Windows 系统为例）

- 连接实例

  ```bash
  ssh -i ~/.ssh/<secret_key_name> <system_username>@<instance_external_ip>
  # eg
  ssh -i ~/.ssh/my_secret_key Ubuntu@34.96.174.31
  ```

- 如果收到警告无法连接，原因是远程主机的公钥已经发生了变化，而 `known_hosts` 文件中的条目与之前保存的公钥不匹配。应该删除 `known_hosts` 文件的冲突条目，重新连接。

# FAQ

## 防止自动断开连接

默认情况下，出于安全考虑，连接成功以后，几分钟无交互会断开连接。修改或创建本地 `~/.ssh/config` 文件：

```
Host 34.96.174.31
  ServerAliveInterval 30
  ServerAliveCountMax 6
```

# `ssh-keygen`

[`ssh-keygen`](https://man.openbsd.org/ssh-keygen) 是 OpenSSH 密钥生成工具。

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/<secret_key_name> -C <comment>
ssh-keygen -t rsa -b 2048 -f ~/.ssh/my_secret_key -C my-comment
```

**在以上代码中**：

- `ssh-keygen`：SSH 密钥生成的专用工具
- `-t rsa`：加密算法类型为 RSA
- `-b 2048`：指定 RSA 密钥的长度
- `-f ~/.ssh/my_secret_key`：
  - `--filename`，密钥路径和基础名称
  - `my_secret_key`：密钥基础名称
- `-C my-comment`：
  - 给生成的公钥添加注释信息，注意 `C` 是大写。


**命令结果**：

- 输入 passphrase （私钥密码），输入时终端不会显示任何字符。
- 新生成的密钥存储在 `C:\Users\jerry\.ssh\`
- 一个是私钥，`my_secret_key`，需妥善保管，不可泄露。
- 另一个是公钥，`my_secret_key.pub`，可公开，如配置到 GitHub/GitLab/ 服务器。