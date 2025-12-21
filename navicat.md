---
title: navicat
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - software
  - databese
---

# Navicat Premium Lite

**Navicat Premium Lite** 是 Navicat 的轻量版数据库管理工具，主要用于数据库管理和开发。

- **环境搭建**：[中文官网下载安装包](https://www.navicat.com.cn/download/navicat-premium-lite)
- 在连接容器化数据库时，记得将容器化数据库端口映射到本地。

**使用方法如下**：

- 数据库服务端已运行

- **连接数据库**
  - **连接名称**：随便填
  - **主机地址**
    - **本地**：localhost
    - **云端**：
      - localhost（需配置云服务商代理）
      - 公网 IP
  - **端口号**：一般为 3306
  - root 用户名和密码
  
- **创建 Databae**

  - 右键点击已连接的数据库 > `新建数据库`
  - **字符集**：`utf8mb4`
  - **排序规则**：`utf8mb4_general_ci`

- **创建 Table**

  - 在已创建的 Database 目录下，右键点击 `表` > `新建表`
