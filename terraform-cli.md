---
title: terraform-cli
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - cloud
  - iac
  - terraform
---

# Overview

[Terraform CLI](https://developer.hashicorp.com/terraform/cli) 是 Terraform 的命令行界面工具。

> [Terraform CLI Docs](https://developer.hashicorp.com/terraform/cli)

# Install

## 安装 Terraform

以管理员身份启动终端，使用 Chocolatey [安装 Terraform](https://developer.hashicorp.com/terraform/tutorials/gcp-get-started/install-cli)，重启终端生效。

```bash
# 安装（安装完成后需重启所有终端）
choco install terraform
# 查看版本
terraform version
```

## Tab 键自动补全

[Tab 键自动补全](https://developer.hashicorp.com/terraform/cli/commands#shell-tab-completion)

在 `/c/Users/jerry/.bashrc` 文件中添加如下内容，重启终端生效。
- 例：输入 `terrform pl`，然后按 `Tab` 会补全至 `terrform plan`。
- 注：如果有多个子命令符合条件，连按两次 `Tab` 会返回全部可用子命令。

```bash
# Terraform 别名和自动补全
alias terraform='terraform.exe'
complete -C /c/ProgramData/chocolatey/lib/terraform/tools/terraform.exe terraform
```

## VS Code Plugin

在 VS Code 中安装 `HashiCorp Terraform` 插件。

- 语法高亮
- 代码格式化（需在 VS Code 的 `settings.json` 文件中设置）

## 代码格式化

有两种方法进行格式化：

- VS Code 插件 `HashiCorp Terraform`（需在 VS Code 的 `settings.json` 文件中设置）

- 使用 Terraform 命令

  ```bash
  cd /d/projects/0000-tests/learn-terraform-gcp
  # 格式化
  terraform fmt
  # 验证格式化时有效的
  terraform validate
  ```

# Reference

> [Terraform CLI Docs](https://developer.hashicorp.com/terraform/cli)

```bash
# 查看版本
terraform version
# 帮助
terraform -help
# 特定命令帮助
terraform plan -help
terraform $COMMAND -help
```

# `init`

[`init`](https://developer.hashicorp.com/terraform/cli/commands/init) 命令用于初始化一个包含 Terraform 配置文件的工作目录。

```bash
terraform init [options]
```

修改 provider 配置以后，需要执行：

```bash
terraform init -upgrade
```

# `apply`

[`apply`](https://developer.hashicorp.com/terraform/cli/commands/apply)

# `destroy`

[`destroy`](https://developer.hashicorp.com/terraform/cli/commands/destroy) 用于销毁 Terraform 配置管理的大多数对象。

```bash
terraform destroy
```

销毁特定对象：

```bash
terraform destroy -target=$RESOURCE_TYPE.$RESOURCE_LABEL
terraform destroy -target=google_container_cluster.primary
```

# `plan`

[`plan`](https://developer.hashicorp.com/terraform/cli/commands/plan)
