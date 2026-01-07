---
title: hcl
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - iac
  - terraform
---

# Overview

[**HCL**](https://github.com/hashicorp/hcl)（HashiCorp Configuration Language，HashiCorp 配置语言）是一个用于定义应用程序配置语言的系统。HCL 信息模型旨在支持多种具体的配置语法（如 **Terraform**），但这种原生语法被认为是主要格式。

官方文档分散在几个主要位置，具体取决于你是想了解其**语法规范**，还是想在特定的工具（如 **Terraform**）中使用它。

> [HCL GitHub 主页](https://github.com/hashicorp/hcl)
>
> [HCL 原生语法规范](https://github.com/hashicorp/hcl/blob/main/hclsyntax/spec.md)
>
> [Terraform Configuration Language Docs](https://developer.hashicorp.com/terraform/language)

该语言由三个相互关联的子语言组成：

- 结构*化*语言定义了整体层次配置结构，是 HCL 主体、块和属性的序列化。
- 表达式语言用于表达属性值，可以是字面值，也可以是其他值的派生值*。*
- 模板语言用于将值组合成字符串，它是表达式语言中的几种表达式类型之一*。*

HCL 的核心是两个主要概念：*attributes (属性)* 和 *blocks (块)*。在原生语法中，一个假想应用程序的配置文件可能如下所示：

```hcl
# Attribute
io_mode = "async"

# Block
service "http" "web_proxy" {
  listen_addr = "127.0.0.1:8080"
  
  process "main" {
    command = ["/usr/local/bin/awesome-app", "server"]
  }

  process "mgmt" {
    command = ["/usr/local/bin/awesome-app", "mgmt"]
  }
}
```

