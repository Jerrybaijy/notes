---
title: github
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - git
  - ci-cd
---

# GitHub

## 登录

- GitHub 不再支持密码登录，以下是使用令牌登录方法；

  - 后来，在使用验证器二次验证登录以后， GitHub 又支持网页登录了。

- 网页登录到你的 GitHub 帐户；
- 点击你的头像，在下拉菜单中选择 `Settings`；
- 在左侧导航栏中，选择 `Developer settings`；
- 在左侧导航栏中，选择 `Generate new token`；
- 点击 `Tokens (classic)`；
- 在下拉菜单中选择 `Generate new token (classic)`；

  - `Note` 随便填，只是用于标记这个令牌想在哪用；
  - `Expiration` 使用期限；
  - 如果自己用，所有选项都打勾（实际经验只勾选 `repo` 大类也没影响目前使用）；
  - 创建令牌，会得到令牌，注意令牌内容只能看见这一次；

- 当在 Bash 中要求输入用户名密码时；

  - 用户名依然是原来的用户名；
  - 密码用令牌代替；

## 创建远程 GitHub 仓库

GitHub 网页创建 Code Repo：

- 仓库名填写本地文件夹名称 `FOLDER_NAME`，保证本地文件夹和远程仓库同名，便于管理；
- `Repository name` 填写小写连字符文件名；
- `Visibility Level` 选 `Public`；
- 不要在这里创建 `README.md`，否则本地无法直接 `push`；

## 存储库限制

- [GitHub 官方关于存储库大小的限制](https://docs.github.com/zh/repositories/working-with-files/managing-large-files/about-large-files-on-github)

### 单个文件

- 推荐小于 50MB，阻止超过 100MB 的单个文件。
- 超过 100MB 的单个文件应使用 LFS。
- 通过浏览器将文件添加到存储库，该文件不得大于 25 MiB。

### 存储库

- 理想情况下小于 1 GB，强烈建议小于 5 GB。

### 历史经验

- 单次推送总大小达到 1.17GB

# GitHub Actions

**GitHub Actions** 是 GitHub 内置的 **CI/CD** 工具。

## GitHub Actions 基础示例

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  # 构建阶段
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "18"

      - name: Install Dependencies
        run: npm install

      - name: Build Application
        run: npm run build

      - name: Upload Build Artifacts
        uses: actions/upload-artifact@v4
        with:
          name: build-dist
          path: dist/

  # 测试阶段
  test:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "18"

      - name: Download Build Artifacts
        uses: actions/download-artifact@v4
        with:
          name: build-dist

      - name: Install Dependencies
        run: npm install

      - name: Run Tests
        run: npm test

  # 部署阶段
  deploy:
    runs-on: ubuntu-latest
    needs: test
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Download Build Artifacts
        uses: actions/download-artifact@v4
        with:
          name: build-dist

      - name: Deploy to Server
        run: scp -r dist/ user@server:/var/www/html
        env:
          SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}

      - name: Clean Up Artifacts
        run: rm -rf dist/
```

## 推送至云服务器并部署

>  此部分参考自 [medi-chatbot-full-stack](https://www.youtube.com/watch?v=KnoVFU0yCUc&list=PLkz_y24mlSJa5JQCRA519psvRqTMqxvMv&index=13) 项目

### 源代码

- `Dockerfile`
- `.github/workflows/cicd.yaml`

### 云服务器

- 创建实例
  - 升级 `apt`
  - 安装 Docker
- 创建镜像仓库：用来存储 Docker Image

### GitHub

#### 创建 Self-hosted Runner

- 远程仓库 > `Settings` > `Actins` > `Runners`
- 新建自托管：`New self-hosted runner`
- 在云服务虚拟机实例中执行 GitHub 推荐的命令，详见具体页面，以连接到 GitHub。

#### 第三方

- 远程仓库 > `Settings` > `Secrets and variables` > `Actions`
- 创建各种密钥变量
  - 云服务器
  - 云服务器镜像仓库
  - 源代码的环境变量

# 解决办法

## 下载文件

在 Linux 中从 GitHub 上下载特定文件

```bash
curl -O https://raw.githubusercontent.com/$USER/$REPO/$BRANCH/$PATH_TO_FILE
# eg：同时下载两个，可同时使用两个 -O 下载两个文件
curl -O https://raw.githubusercontent.com/Jerrybaijy/it-notes/main/devops/docker/docker.md
```

## 使用 Web VSCode 查看代码

在 GitHub 中查看代码时，可通过将 URL 中的 `.com` 修改为 `.dev`，使用 Web VSCode 查看代码：

```
# 原地址
https://github.com/Jerrybaijy/blog-flak-sqlite-html

# 原地址
https://github.dev/Jerrybaijy/blog-flak-sqlite-html
```

## 远程仓库改名

- **改名**：导航栏 > `Settings` > `Repository name`
- **改地址**：GitHub 改完项目名称后，仓库地址自动更改。
- **本地仓库**：移除旧仓库，重新添加远程地址，重新关联 `main` 分支。