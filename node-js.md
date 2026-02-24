---
title: node-js
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - node-js
  - javascript
  - web
---

# Overview

[**Node.js**](https://nodejs.org/zh-cn) 是一个开源、跨平台的 JavaScript 运行时环境，能够在服务器端运行 JavaScript。它最初由 Ryan Dahl 于 2009 年创建，并且使用了 Google 的 **V8 JavaScript 引擎**，该引擎最初是用于 Chrome 浏览器的，用于将 JavaScript 代码编译成高效的机器代码。Node.js 的核心优势在于它的非阻塞、事件驱动架构，使得它在构建高性能的网络应用时非常高效。

## npm

**npm** 是 node.js 的默认包管理工具。

**命令**：

```bash
# 查看 npm 版本
npm -v
# 更新 npm 到最新版
npm install -g npm
# 查看安装过的包
npm list -g --depth=0

# 创建静态文件夹
npm run build
```

**选项**

```bash
-g # 全局
```

## pnpm

`pnpm` 是一个快速、节省磁盘空间的 Node.js 包管理器，它是 `npm` 和 `yarn` 的替代品。

### 安装

```bash
pnpm install -g pnpm
```

### 命令

```bash
# 查看 pnpm 版本
pnpm -v
# 更新 pnpm 包管理工具到最新版
pnpm install -g pnpm
# 查看安装过的包
pnpm list -g --depth=0
```

## nvm

nvm (Node Version Manager) 是 Node.js 的版本管理器。简单来说，它就像一个“Node.js 版本的遥控器”，允许你在同一台电脑上安装、管理并快速切换多个不同版本的 Node.js。

### Quickstart

```bash
# 安装 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# 重新加载环境变量（或重启终端）
source ~/.bashrc

# 验证 nvm 安装
nvm --version

# 使用 nvm 安装特殊版本的 node.js
nvm install 22
node -v
```

### 常用命令

| **任务**               | **命令**               |
| ---------------------- | ---------------------- |
| **安装指定版本**       | `nvm install 22`       |
| **查看已安装版本**     | `nvm ls`               |
| **切换当前使用版本**   | `nvm use 22`           |
| **查看远程可安装版本** | `nvm ls-remote`        |
| **设置默认版本**       | `nvm alias default 22` |
| **卸载某个版本**       | `nvm uninstall 18`     |

## http-server

**http-server** 是一个基于 Node.js 的简单的静态文件服务器，可以用来快速地在本地启动一个 HTTP 服务器，用于提供静态文件服务。

```bash
# 安装
npm install -g http-server
# 启动
http-server -p 8080
```

# Install

## 通用安装

- 官网下载 [Node.js](https://nodejs.org/zh-cn) 并安装

- 查看 Node.js 版本

  ```bash
  node -v
  ```

## 特殊版本安装

详见 [nvm](#nvm) 工具

