---
title: gcp
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - cloud-computing
  - gcp
---

# Overview

[**GCP**](https://docs.cloud.google.com/docs/overview?hl=zh-cn) （Google Cloud Platform）是谷歌提供的一套云计算服务。

> [Google Cloud Docs](https://docs.cloud.google.com/docs)
>
> [Gcloud Reference](https://docs.cloud.google.com/sdk/gcloud/reference)
>
> [Google Cloud 使用入门](https://docs.cloud.google.com/docs/get-started)
>
> [Google Cloud 产品](https://cloud.google.com/products?hl=zh-cn&_gl=1*xq66jx*_ga*MTYwMDY0NjE4Ni4xNzYxNTY3Mjky*_ga_WH2QY8WWF5*czE3NjU4MDQ4MDkkbzgkZzEkdDE3NjU4MDc0NTQkajI5JGwwJGgw)

## 交互方式

Google Cloud 为您提供了三种与服务和资源[交互的基本方式](https://docs.cloud.google.com/docs/overview?hl=zh-cn#ways_to_interact_with_the_services)。

- [Google Cloud console](https://console.cloud.google.com/?hl=zh-cn) 提供基于 Web 的图形界面
- 命令行界面
  - [Google Cloud CLI](https://docs.cloud.google.com/sdk/gcloud)
  - [Cloud Shell](https://docs.cloud.google.com/shell/docs/features?hl=zh-cn)
- [客户端库](https://docs.cloud.google.com/sdk/cloud-client-libraries?hl=zh-cn)

# Quickstart

## 准备工作

- 注册 Google 账号并开通结算
- [安装并配置 Google Cloud CLI](gcp-gcloud-cli.md#Install)

## 创建 GCP Project

- [创建 GCP Project](<gcp-project.md#创建 GCP 项目>)

## 管理 GCP 服务资源

- 使用 Gcloud CLI 管理 GCP 服务资源
- [使用 Terraform 管理 GCP 服务资源](<terraform.md#Quickstart>)

## 删除 GCP Project

- 使用 Gcloud CLI 删除 GCP Project
- [使用 Terraform 删除 GCP Project](<gcp-project.md#Quickstart>)

# Resource Manager

Google Cloud 提供组织和项目等容器资源，可对其他 Google Cloud 资源进行分组和分层整理。

> [Resource Manager Docs](https://docs.cloud.google.com/resource-manager/docs?hl=zh-cn)

## 地理架构

[地理架构](https://docs.cloud.google.com/docs/geography-and-regions?hl=zh-cn)：指资源的可用地理范围。资源只能被同范围内的资源访问。

```
Location: 通用

Multi-region(多区域)
└── Region (区域)
    └── Zone (可用区)
```

- **Location (位置)**：一个通用的概念，指部署资源的地理范围。可以是 Multi-region、Region 和 Zone。
- **Multi-region (多区域)**：大洲级别，例如 `ASIA` （台湾），由多个 Region 组成，会跨 Region 备份。
- **Region (区域)**：城市级别，例如 `asia-east1` （台湾），由多个 Zone 组成，会跨 Zone 备份。
- **Zone (可用区)**：机房级别，例如 `asia-east1-a`（台湾 A 区），不备份。

## 资源层次结构

[**资源层次结构**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn)：Google Cloud 资源以分层方式进行整理。

```
Organization
└── Folder (可选)
    └── Project
```

- [**Organization**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#organizations) 资源是Google Cloud 资源层次结构中的**根节点**，通常对应一个公司或域名（如 `yourcompany.com`）。
- [**Folder**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#folders) 资源是 Organization 和 Project 之间的可选层级，可对项目进行分组。
- [**Project**](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy?hl=zh-cn#projects) 资源是 GCP 最基础的实体，是所有服务资源的“容器”。

# GCP Bare Metal

[**Bare Metal**](https://cloud.google.com/bare-metal/docs/bms-setup?hl=zh-cn)（裸金属）是指未经虚拟化的物理服务器，即裸机。在裸金属服务器上运行的操作系统直接安装在物理硬件上，而不是在虚拟化层上运行。

## 准备工作

- Google Cloud 控制台中的项目选择器页面上创建项目，并启用 API。

- [创建 VPC 网络](https://cloud.google.com/vpc/docs/create-modify-vpc-networks?hl=zh-cn#gcloud)

  ```bash
  # 创建
  gcloud compute networks create $VPC_NETWORK_NAME \
      --subnet-mode=auto \
      --bgp-routing-mode=$DYNAMIC_ROUTING_MODE \
      --mtu=$MTU
  
  # 删除
  gcloud compute networks delete $VPC_NETWORK_NAME
  ```

  ```bash
  # EG
  gcloud compute networks create my-vpc-network-1 \
      --subnet-mode=auto \
      --bgp-routing-mode=global \
      --mtu=1460
  ```

## 创建 VLAN 连接

- 按照以下步骤为 Cloud Interconnect 连接[创建 VLAN 连接](https://cloud.google.com/bare-metal/docs/bms-setup?hl=zh-cn#bms-vlan-attachments)

- 创建两个 Cloud Router 实例

  ```bash
  gcloud compute routers create $ROUTER_NAME \
      --network $VPC_NETWORK_NAME \
      --asn 16550 \
      --region $REGION
  ```

  ```bash
  # EG
  gcloud compute routers create my-router-1 \
      --network my-vpc-network-1 \
      --asn 16550 \
      --region us-central1
  
  gcloud compute routers create my-router-2 \
      --network my-vpc-network-1 \
      --asn 16550 \
      --region us-central1
  ```

- 创建两个 `InterconnectAttachment`

  ```bash
  # 创建
  gcloud compute interconnects attachments partner create $ATTACHMENT_NAME \
      --region $REGION \
      --router $ROUTER_NAME \
      --edge-availability-domain availability-domain-1 \
      --edge-availability-domain $AVAILABILITY_DOMAIN \
      --admin-enabled
  
  # 删除
  gcloud compute interconnects attachments delete $ATTACHMENT_NAME --region=us-central1
  ```

  ```bash
  # EG
  gcloud compute interconnects attachments partner create my-attachment-1 \
      --region us-central1 \
      --router my-router-1 \
      --edge-availability-domain availability-domain-1 \
      --admin-enabled
  
  gcloud compute interconnects attachments partner create my-attachment-2 \
      --region us-central1 \
      --router my-router-2 \
      --edge-availability-domain availability-domain-2 \
      --admin-enabled
  ```

- 描述连接，以检索其配对密钥。您在打开更改请求以创建与裸金属解决方案环境的连接后，将与 Google Cloud 共享密钥。

  ```bash
  gcloud compute interconnects attachments describe my-attachment-1 \
      --region us-central1
  
  gcloud compute interconnects attachments describe my-attachment-2 \
  	--region us-central1
  ```

- 激活 VLAN 连接

  ```bash
  gcloud compute interconnects attachments partner update $ATTACHMENT_NAME \
      --region $REGION \
      --admin-enabled
  ```

  ```bash
  # EG
  gcloud compute interconnects attachments partner update my-attachment-1 \
      --region us-central1 \
      --admin-enabled
  
  gcloud compute interconnects attachments partner update my-attachment-2 \
      --region us-central1 \
      --admin-enabled
  ```

- 至此仍为：`state: PENDING_PARTNER`，实际应为 `INACTIVE` 或 `ACTIVE`
