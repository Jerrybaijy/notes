---
title: terraform-kubernetes
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - iac
  - terraform
  - kubernetes
---

# Overview

[**Kubernetes Provider**](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs) 用于 Terraform 与 Kubernetes 支持的资源进行交互。

# Quick Start

## `terraform.tf`

```hcl
terraform {
  required_providers {
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = ">= 2.0.0"
    }
  }
}
```

## `provider.tf`

```hcl
data "google_client_config" "default" {}
provider "kubernetes" {
  host                   = "https://${google_container_cluster.primary.endpoint}"
  token                  = data.google_client_config.default.access_token
  cluster_ca_certificate = base64decode(google_container_cluster.primary.master_auth[0].cluster_ca_certificate)
}
```

## `api.tf`

```hcl
locals {
  services = [
    "compute.googleapis.com",        # Compute Engine API
    "container.googleapis.com",      # Kubernetes Engine API
  ]
}

resource "google_project_service" "project_services" {
  for_each           = toset(local.services)
  service            = each.key
  disable_on_destroy = false
}
```

## `main.tf`

```
resource "kubernetes_namespace" "example" {
  metadata {
    name = "my-first-namespace"
  }
}
```

# Core

## `kubernetes_service_account_v1`

[`kubernetes_service_account_v1`](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/service_account_v1) 用于为在 Pod 中运行的进程提供身份标识，即为 Pod 创建 KSA 并绑定 GSA。

完整功能详见 [Terraform GCP | GSA | Quick Start](<terraform-gcp.md#GSA Quick Start>)

```hcl
# 获取当前 Project ID
data "google_project" "project" {}

# 防止因 namespace 不存在而导致创建 IAM 失败
resource "kubernetes_namespace_v1" "app_ns" {
  metadata {
    name = var.app_namespace
  }
}

# 为 Pod 创建 KSA 并绑定 GSA
resource "kubernetes_service_account_v1" "my_app_ksa" {
  metadata {
    name      = var.app_ksa
    namespace = kubernetes_namespace_v1.app_ns.metadata[0].name
    annotations = {
      "iam.gke.io/gcp-service-account" = google_service_account.workload_identity.email
    }
  }
}
```

