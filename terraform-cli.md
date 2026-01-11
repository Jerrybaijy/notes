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

```bash
# 查看版本
terraform version
# 帮助
terraform -help
# 特定命令帮助
terraform plan -help
terraform $COMMAND -help
```

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

- VS Code 插件 [`HashiCorp Terraform`](<vs-code.md#HashiCorp Terraform>)（需在 VS Code 的 `settings.json` 文件中设置）

- 使用 Terraform 命令

  ```bash
  cd /d/projects/0000-tests/learn-terraform-gcp
  # 格式化
  terraform fmt
  # 验证格式化时有效的
  terraform validate
  ```

# `init`

[`init`](https://developer.hashicorp.com/terraform/cli/commands/init) 命令用于初始化一个包含 Terraform 配置文件的工作目录。

```bash
terraform init [options]
```

当执行 `terraform init` 后，Terraform 会根据 `.tf` 文件进行初始化工作，会在配置根目录出现：

- `.terraform`：本地缓存目录，详见 [`.terraform`](<terraform-configuration-language.md#`.terraform`>)。
- `.terraform.lock.hcl`：依赖锁定文件，详见 [`.terraform.lock.hcl`](<terraform-configuration-language.md#`.terraform.lock.hcl`>)。

修改 provider 配置以后，需要执行：

```bash
terraform init -upgrade
```

# `apply`

[`apply`](https://developer.hashicorp.com/terraform/cli/commands/apply) 用于部署资源。

```hcl
# 使用 gcloud CLI 授权
gcloud auth application-default login

# 部署
cd /d/projects/my-project/terraform
terraform apply
```

执行 `terraform apply` 命令以后，看到的是 Terraform 的 **Plan**，输入 `yes`（必须完整输入这三个字母）并按回车。

当执行 `terraform apply` 后，会在配置根目录出现：

- `terraform.tfstate`：状态文件，详见 [`terraform.tfstate`](<terraform-configuration-language.md#`terraform.tfstate`>)。
- `terraform.tfstate.backup`：状态备份文件，详见 [`terraform.tfstate.backup`](<terraform-configuration-language.md#`terraform.tfstate.backup`>)。

部署特定对象：

```bash
terraform apply -target=module.my-module
terraform apply -target=google_container_cluster.primary
```

# `plan`

# `destroy`

[`destroy`](https://developer.hashicorp.com/terraform/cli/commands/destroy) 用于销毁 Terraform 配置管理的大多数对象。

```bash
terraform destroy
```

销毁特定对象：

```bash
terraform destroy -target=module.my-module
terraform destroy -target=google_container_cluster.primary
```

# `plan`

[`plan`](https://developer.hashicorp.com/terraform/cli/commands/plan)

# FAQ

## 通过 `kubectl` 安装 Argo CD 并部署应用的特殊说明

- 在删除命名空间后，如果想再次部署应用，需要重新执行 `terraform apply` 以恢复 KSA，否则后端会部署失败。

- 清理资源步骤

  - 卸载应用

    ```bash
    kubectl delete -f application.yaml
    ```

  - 删除命名空间

    ```
    kubectl delete ns argocd
    kubectl delete ns my-ns
    ```

  - 重复执行 `terraform apply`，直到 terraform 提示 no changes。

    ```bash
    terraform apply
    ```

- 如在执行 `terraform destroy` 时，发生如下错误：

  > Error: context deadline exceeded
  >
  > 此时 app-ns 命名空间的状态会变为 Terminating

  - 执行 `kubectl delete ns argocd` 和 `kubectl delete ns my-ns`
  - 重复执行 `terraform appy`，直到 terraform 提示 no changes。
  - 执行 `terraform destroy`，第一次执行可能还会出错。
  - 重复执行上述步骤，直到销毁成功。
