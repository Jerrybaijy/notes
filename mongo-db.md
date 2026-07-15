---
title: software
author: Jerry.Baijy
tags:
  - dev
  - db
  - nosql
---

# Overview

[**MongoDB**](https://www.mongodb.com/) 是一种[非关系型数据库](database.md)管理系统（NoSQL），使用的是**文档导向模型**，以 BSON（Binary JSON，二进制 JSON）格式展示数据。

# Install

- 此步骤为在 Ubuntu 中安装

- 导入 MongoDB 公钥

    ```bash
    wget -qO - https://www.mongodb.org/static/pgp/server-7.0.asc | sudo apt-key add -
    ```

- 创建 MongoDB 的列表文件

    ```bash
    echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu $(lsb_release -cs)/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
    ```

- 更新包数据库

    ```bash
    sudo apt-get update
    ```

- 安装 MongoDB

    ```bash
    sudo apt-get install -y mongodb-org
    ```

- 安装 MongoDB Shell

    ```bash
    sudo apt-get install mongodb-mongosh
    ```

- 启动 MongoDB 服务

    ```bash
    sudo systemctl start mongod
    ```

- 设置 MongoDB 服务开机自启动

    ```bash
    sudo systemctl enable mongod、
    ```

- 查看状态

    ```bash
    sudo systemctl status mongod
    ```

# MongoDB 基础

- **MongoDB 管理**

    ```bash
    # 查看 mongod 版本
    mongod --version
    # 查看 MongoDB Shell 版本
    mongo --version
    # 查看 status
    sudo systemctl status mongod
    
    # 启动
    sudo systemctl start mongod
    # 停止
    sudo systemctl stop mongod
    # 重启
    sudo systemctl restart mongod
    # 启动 MongoDB Shell
    mongosh
    # 退出 MongoDB Shell
    exit
    ```

- **其它命令**

    ```bash
    # 清屏
    cls
    ```

# Database

- **基础命令**

    ```sh
    # 查看所有
    show dbs
    # 进入（如果没有，会自动创建）
    use $DATABASE;
    # 删除
    drop database $DATABASE;
    ```

# Collection

MongoDB 中的 `collection` 类似于 MySQL 中的 `table`。

- **基础命令**

    ```sh
    # 查看 collection
    show collections
    # 创建 Collection / document
    db.$COLLECTION_NAME.insertOne({$KEY1:"$VALUE1"}[,{$KEY2:"$VALUE2"},...])
    # 删除 Collection
    db.$COLLECTION_NAME.drop()
    ```

# Document

MongoDB 中的 `document` 类似于 MySQL 中的 `row`，所有数据以 `document` 形式，按照 BSON 格式存储。不同 `document` **不需要**有相同的结构和字段。

- **基础命令**

    ```bash
    # 查看 document
    db.$COLLECTION_NAME.find()
    
    # 操作第一个 document 用'~One'
    # 操作所有 document 用'~Many'
    
    # 创建 Collection / document
    db.$COLLECTION_NAME.insertOne({$KEY1:"$VALUE1"},{$KEY2:"$VALUE2"},...)
    # 修改 document
    db.$COLLECTION_NAME.updateOne({KEY:"VALUE"},{$set:{KEY1:"VALUE1",KEY2:"VALUE2"}})
    db.$COLLECTION_NAME.updateMany({KEY:"VALUE"},{$set:{KEY1:"VALUE1",KEY2:"VALUE2"}})
    # 删除 document
    db.$COLLECTION_NAME.updateOne({KEY:"VALUE"})
    db.$COLLECTION_NAME.updateMany({KEY:"VALUE"})
    ```
