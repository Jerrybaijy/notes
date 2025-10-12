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

# Node.js

## Node.js

[**Node.js**](https://nodejs.org/zh-cn) 是一个开源、跨平台的 JavaScript 运行时环境，能够在服务器端运行 JavaScript。它最初由 Ryan Dahl 于 2009 年创建，并且使用了 Google 的 **V8 JavaScript 引擎**，该引擎最初是用于 Chrome 浏览器的，用于将 JavaScript 代码编译成高效的机器代码。Node.js 的核心优势在于它的非阻塞、事件驱动架构，使得它在构建高性能的网络应用时非常高效。

### 环境搭建

- 官网下载 [Node.js](https://nodejs.org/zh-cn) 并安装

- 查看 Node.js 版本

    ```bash
    node -v
    ```

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

## http-server

**http-server** 是一个基于 Node.js 的简单的静态文件服务器，可以用来快速地在本地启动一个 HTTP 服务器，用于提供静态文件服务。

```bash
# 安装
npm install -g http-server
# 启动
http-server -p 8080
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