---
title: harbor
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - dev-ops
  - repo
---

# Harbor

[**Harbor**](https://goharbor.io/) 是一个开源镜像仓库。可以存储 Docker Image，Helm Chart ...

## 安装 Harbor

> [安装和配置 Harbor](https://goharbor.io/docs/2.14.0/install-config/)

- **先决条件**：已安装 Docker、Docker Compose 和 Helm

- 从[官方发布页面](https://github.com/goharbor/harbor/releases)下载 Harbor 安装程序：`harbor-online-installer-v2.14.1.tgz`

- 解压安装包，把解压目录移动至固定位置，如 `/D` （目录不要有空格）。

- 在 `harbor` 目录中，复制 `harbor.yml.tmpl` 文件到当前目录，并重命名为 `harbor.yml`。修改以下内容：

  ```yaml
  # 1. 填写你的 Windows 主机 IP（别用 localhost）
  hostname: 192.168.1.100  # 替换成你电脑的实际 IP（可通过 Git Bsh 输入 ipconfig 查看）
  
  # 2. 关闭 HTTPS（测试用）
  https:
    enabled: false  # 直接设为 false，把下面的 port/certificate/private_key 都注释掉
  
  # 3. 设置管理员密码
  harbor_admin_password: 123456  # 自定义密码
  
  # 4. 数据存储路径
  data_volume: /d/harbor/data
  
  # 5. 日志路径
  log:
    location: /d/harbor/logs
  ```

- Git Bash 进入 Harbor 目录

  ```bash
  cd /d/harbor
  # 给脚本加执行权限
  chmod +x install.sh prepare common.sh
  
  # 执行预配置！！！！到这一步没有安装成功
  ./prepare
  ```

  