---
title: openssh
author: Jerry.Baijy
tags:
  - dev
  - it-basics
---

# Overview

**SSH (Secure Shell)** 是一种加密的网络传输协议，用于在不安全的网络中为网络服务提供安全的传输层。

[**OpenSSH**](https://www.openssh.org/) 是 SSH 协议的**免费开源版本**。它是目前 Linux、Unix（包括 macOS）以及现代 Windows 系统中默认使用的 SSH 工具集。

> [OpenSSH Docs](https://www.openssh.org/manual.html)

# Install

系统默认提供

# `ssh-keygen`

[`ssh-keygen`](https://man.openbsd.org/ssh-keygen) 是 OpenSSH 密钥生成工具。

## 基本命令

```bash
ssh-keygen
```

**命令结果**：

- 输入 passphrase （私钥密码）
  - 默认为空即可，否则以后每次 git pull /git push / 连服务器都要输密码。
  - 输入密码时终端不会显示任何字符。

- 这会在 `~/.ssh/` 目录生成一对 Ed25519 类型密钥对
- **私钥**，`id_ed25519`，需妥善保管，不可泄露。
- **公钥**，`id_ed25519.pub`，可公开，如配置到 GitHub 或者服务器。

## 完整命令

```bash
ssh-keygen -t <secret_type> -b 2048 -f ~/.ssh/<secret_key_name> -C <comment>
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

# Quickstart

## 创建 SSH 密钥对

```bash
ssh-keygen
```

## 获取 SSH 公钥

```bash
cat ~/.ssh/id_ed25519.pub
```

## 使用公钥

### 登录平台

- 复制公钥内容，粘贴至平台公钥区域，如 Gitee。

- 登录 Gitee

  ```bash
  ssh -T git@gitee.com
  ```

### 登录服务器

- 将公钥内容发送至服务器

  ```bash
  ssh-copy-id <user>@<server>
  ssh-copy-id jerry@114.55.65.143
  ```

- 输入登录密码

- 这会公钥内容添加至服务器的 `~/.ssh/authorized_keys` 文件（如果没有此文件会自动创建）。

  ```
  # 免密连接服务器
  ssh <user>@<server>
  
  # 查看自己的公钥是否添加到服务器
  cat ~/.ssh/authorized_keys
  ```

- 将指定的其他人的公钥添加到服务器

  ```bash
  ssh-copy-id -f -i <public_secret_file> <user>@<server>
  ssh-copy-id -f -i ./id_rsa.pub jerry@114.55.65.143
  ```

  

# FAQ

## 防止自动断开连接

默认情况下，出于安全考虑，连接成功以后，几分钟无交互会断开连接。修改或创建本地 `~/.ssh/config` 文件：

```
Host 34.96.174.31
  ServerAliveInterval 30
  ServerAliveCountMax 6
```

## 远程主机标识已更改

当远程主机标识已更改（比如重装系统），使用密钥连接远程主机时，会出现如下错误：

```
jerry@PC-Jerry-2 MINGW64 ~
$ ssh root@47.115.210.245
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:tdHQdzhKytoWTrCVy13NAf3H7yC8M6T7vg/akR1tcqc.
Please contact your system administrator.
Add correct host key in /c/Users/jerry/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /c/Users/jerry/.ssh/known_hosts:16
Host key for 47.115.210.245 has changed and you have requested strict checking.
Host key verification failed.
```

这可能是由于服务器系统重装、SSH服务重新配置或服务器迁移导致的正常情况。您需要更新您本地计算机上存储的旧的主机密钥。根据错误信息，具体的操作步骤如下：

- 定位并删除旧的密钥记录

  错误信息指出有问题的ECDSA密钥位于您本地文件 `/c/Users/jerry/.ssh/known_hosts` 中的第 16 行。

  这个命令会自动从 `known_hosts`文件中移除IP地址 `47.115.210.245` 对应的所有密钥。

  ```bash
  ssh-keygen -R 47.115.210.245
  ```

- 删除以后，[重新连接](#登录服务器)即可。
