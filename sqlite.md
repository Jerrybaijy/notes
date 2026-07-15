---
title: software
author: Jerry.Baijy
tags:
  - dev
  - db
  - sql
---

# Overview

[**SQLite**](https://sqlite.org/) 是一个轻量级的[关系型数据库](database.md)管理系统（RDBMS），它的主要特点是：

- **嵌入式**：直接内嵌在应用里，无需安装。
- **无需安装**：因为 SQLite 是一个库而非服务器，它直接访问数据库文件，所以无需额外的安装配置。
- **服务器独立**：数据存储在一个 `.db` 文件中，如果数据库文件不存在，SQLite 会自动创建它。

# Install

## 容器化 SQLite

- Docker 已成功搭建，详见 [Docker > 环境搭建](../devops/docker/docker.md#环境搭建)。

- 运行容器

    ```bash
    docker run -d -v $(pwd):/tmp --name sqlite-container -it jitesoft/sqlite:latest /tmp/test.db
    ```

    **在以上代码中**：

    - **`--name sqlite-container`**：指定容器的名字
    - **`-v $(pwd):/tmp`**：挂载到本地当前文件夹下的 `tmp`，但是本次实验没有挂载成功。
    - **`/tmp/test.db`**：容器中 `test.db` 的位置
    - **`-d`**：让容器在后台运行
    - **`-it`**：以交互模式运行命令，并且分配一个伪终端。
    - **`jitesoft/sqlite:latest`**：镜像

- 如果想在命令行中操作 SQLite，可进入容器内 SQLite 交互界面。

    ```bash
    docker exec -it sqlite-container sqlite3
    ```

    **在以上代码中**：

    - **`-it`**：以交互模式运行命令，并且分配一个伪终端。

    - **`sqlite-container`**：容器名

    - **`sqlite3`**：SQLite 命令行客户端

        ```bash
        sqlite>
        ```

- 退出 SQLite 交互界面

    ```bash
    sqlite> .exit
    ```

# SQLite 基础

- 无需安装。

- 在连接 SQLite 时，如果数据库不存在，会立即创建一个空数据库。

- **常用命令**

    ```sql
    -- 退出 SQLite 交互界面
    .exit
    
    -- 查看所有数据库
    .database
    
    -- 查看数据库中的所有表
    .tables
    
    -- 查看某个表的结构
    .schema tbl1
    ```

# 交互方式

- **命令行客户端**：`sqlite3`
- **编程语言客户端**：如 Python 的 `pymysql`
- **ORM**：如 Python 的 `sqlalchemy`
- **GUI 工具**：如 `Navicat`

# SQLite 命令样板

- **直接创建 Database**

    ```sql
    sqlite3 db_users.db
    ```

- **在程序中创建 Database（如果数据库文件不存在，会直接创建）**

    ```sql
    conn = sqlite3.connect('db_users.db')
    ```

- **创建 Table**

    ```sql
    CREATE TABLE IF NOT EXISTS tb_users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        username VARCHAR(16) NOT NULL UNIQUE,
        password VARCHAR(255) NOT NULL
    );
    ```

# SQLite 可视化

- VSCode 插件查看
    - VSCode 安装 `SQLite Viewer` 插件；
    - 双击 `SQLite` 的 `.db` 文件；
    - 此插件只支持查看，不支持修改。
- 使用 [Navicat Premium Lite](navicat.md)