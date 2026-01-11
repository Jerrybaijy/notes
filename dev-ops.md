---
title: dev-ops
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - dev-ops
  - ci-cd
---

# DevOps

**DevOps**（**Dev**elopment **Op**eration**s**）是一种文化理念，旨在促进开发（Dev）和运维（Ops）团队之间的协作和沟通，以自动化软件交付过程，从而更快、更可靠地发布软件。

- DevOps 是 “指导思想”
- CI/CD 是 “具体做事的流程”
- GitOps 是 “用 Git 驱动这个流程的落地方式”

# CI/CD

**CI/CD** 是软件开发中的一组最佳实践，代表**持续集成（Continuous Integration）**和**持续交付/部署（Continuous Delivery/Deployment）**。它们的目标是提高软件开发效率，减少发布风险，并加速产品迭代。

## 持续集成（CI）

**持续集成**（CI）是一种开发实践，指的是开发人员频繁地（通常是每天多次）将代码集成到主分支，并自动化地执行构建和测试。

**核心流程**：

- **代码提交**：开发人员将代码推送到版本控制系统（如 Git）。
- **自动构建**：CI 工具（如 Jenkins、GitHub Actions、GitLab CI）自动拉取代码并执行构建脚本。
- **自动测试**：自动运行单元测试、集成测试，确保新代码不会破坏现有功能。
- **反馈**：构建或测试失败时，系统立即通知开发人员。

## 持续交付（CD - Continuous Delivery）

持续交付是在 CI 基础上，确保代码在任何时候都可以安全地发布到生产环境，但发布过程是**手动触发**的。

**核心流程**：

- **自动化部署到预生产环境**：在 CI 成功后，自动将代码部署到测试或预生产环境。
- **更多测试**：执行更高级别的测试，如用户验收测试（UAT）、安全扫描等。
- **人工批准发布**：在所有测试通过后，人工决定是否将代码发布到生产环境。

## 持续部署（CD - Continuous Deployment）

持续部署比持续交付更进一步，一旦通过测试，代码会**自动部署到生产环境**，无需人工干预。

**核心流程**：

- 自动化程度更高，任何通过测试的变更都会直接发布。
- 必须确保测试流程非常严谨，避免将不稳定的代码部署到生产。

## CI/CD 工具链示例

- **代码托管**：GitHub、GitLab、Bitbucket
- **CI/CD 平台**：Jenkins、GitLab CI/CD、GitHub Actions、CircleCI、Azure DevOps
- **构建工具**：Maven、Gradle、npm、Webpack
- **测试工具**：JUnit、PyTest、Selenium
- **部署工具**：Ansible、Docker、Kubernetes、Terraform

## CI/CD 示例流程

- 开发者提交代码
- CI 工具自动拉取代码
- 自动构建并运行单元测试
- 自动部署到测试环境
- 运行集成和验收测试
- **持续交付：人工审批后发布** 或 **持续部署：自动发布**
- **监控和回滚机制**（如有问题，快速回滚）

# GitOps

**GitOps** 是 DevOps 的一种具体落地实践，核心是将 **Git 仓库作为整个系统的 “单一真实来源”**—— 所有基础设施配置、应用部署规则、环境配置都存储在 Git 中，通过 Git 的版本控制、分支管理、PR/MR 流程来驱动部署和运维操作。

GitOps 以 Git 为中心：通过提交代码、合并分支来修改配置，工具（如 Argo CD、Flux）会自动监听 Git 仓库变化，将配置同步到目标环境（如 K8s 集群），无需手动执行部署命令，实现 “代码即配置、提交即部署”。

GitOps 是云原生场景下的 DevOps 最佳实践，专门适配 K8s 等云原生工具的配置管理与部署需求。

# 云原生

**云原生（Cloud Native）** 是一套让应用 “生于云、长于云” 的技术体系与设计理念，核心是让应用适配云环境（公有云、私有云、混合云），实现 **弹性伸缩、高可用、易部署、可观测** 的目标。

简单说，云原生不是单一技术，而是 “理念 + 工具栈” 的集合，核心支柱包括：

- **容器化**（如 Docker）：应用及依赖打包成容器，实现 “一次构建、到处运行”；
- **容器编排**（如 Kubernetes）：自动化管理海量容器的部署、伸缩、调度；
- **微服务**：将应用拆分成独立小服务，按需迭代、独立部署；
- **DevOps/CI/CD/GitOps**：通过自动化流程支撑快速迭代；
- **可观测性**（如 Prometheus、ELK）：实时监控应用状态。

# OCI

## Overview

**OCI**（Open Container Initiative，开放容器计划）旨在制定一套全球统一的容器**格式**和**运行时**标准。

## OCI Registry

**OCI Registry**（OCI 注册表）是一个用于存储、管理和分发符合 OCI 规范的云原生制品（如容器镜像和 Helm Chart）的服务器端点（域名或地址）。

### OCI Registry 种类

- 公有 OCI 仓库：Docker Hub、Amazon ECR、Azure Container Registry、Google Artifact Registry 等

- 私有 OCI 仓库：Harbor、Helm Chart 等

### OCI Registry 地址格式

```bash
oci://<oci-registry>
oci://registry-1.docker.io/jerrybaijy
```

- `oci://`：OCI 协议标识
- `<oci-registry>`：OCI Registry 服务地址

## OCI 占位符规范

- 使用 `<>`
- 使用小写字母
- 多个词使用连字符 `-` 连接

## OCI 制品

**OCI 制品**是遵循 OCI 分发规范（OCI Distribution Spec）的标准化可分发文件，核心是 “跨平台、跨工具兼容”，常见种类及典型用途如下：

- **容器镜像**：最基础的 OCI 制品，包含应用运行所需的代码、依赖、环境配置，是 Docker、K8s 等容器平台的核心运行单元。
- **Helm Chart**：K8s 应用的打包格式，Helm 3.8+ 支持以 OCI 制品形式存储 / 分发，可推送到 Docker Hub、GitLab、GHCR 等 OCI 仓库。
- **SBOM（软件物料清单）**：记录制品的依赖组件、版本、许可证等信息，用于供应链安全审计，支持以 OCI 格式附着在镜像 / Chart 上同步存储。
- **OCI 索引（Image Index）**：类似 “多架构镜像清单”，可关联不同系统架构（如 x86、ARM）的镜像，方便工具自动匹配对应架构的制品。
- **自定义二进制制品**：如编译后的应用二进制文件、配置包等，通过 ORAS 工具（OCI Registry as Storage）推送到 OCI 仓库，实现版本化管理。
- **其他标准化制品**：如 CNI 插件包、Kustomize 配置包等，只要遵循 OCI 格式规范，均可作为 OCI 制品存储和分发。

# Repo

**Repo**（Source Code Repository，源代码仓库）是基于**版本控制系统 (VCS)** 构建的逻辑单元。它不仅是软件源代码及其相关资产（如配置文件、测试脚本、文档）的存储中心，更是记录项目完整演进轨迹的**不可篡改的日志系统**。

常见的源代码托管平台：

- GitHub
- [GitLab](<gitlab.md#Code Repo>)
- Bitbucket
- Google
  -  [Repositories](gcp-cloud-build.md#Repositories) (链接到其它代码托管平台)
  - Cloud Source Repositories (新用户停用)
  - Secure Source Manager（$1000/月）
- AWS CodeCommit
- Azure Repos
- Gitee  (码云)
- Coding (腾讯云)
- Codeup (阿里云)