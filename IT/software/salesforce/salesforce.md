# Salesforce CLI

**Salesforce CLI**（命令行界面）是 Salesforce 提供的命令行工具，用于简化 Salesforce 组织的开发、CI/CD、测试和管理。它使开发人员能够高效地执行各种任务，如创建和管理 Salesforce 组织、部署代码、运行测试、导入/导出数据等。

Salesforce CLI 是 Salesforce 开发者工具链（DevOps Center、VS Code 插件等）的核心组件，并且支持 **Salesforce DX（Developer Experience）** 模型。

## 环境搭建

- 安装 `npm` 包管理器。

    ```bash
    sudo apt update
    sudo apt install npm -y
    ```

- 从 `npm` 安装 `Salesforce CLI`

    ```bash
    sudo npm install -g @salesforce/cli
    ```

- 验证安装

    ```bash
    sf -v
    ```

- 在 `VS Code` 中安装 `Salesforce Extension Pack` 扩展。

- 安装 `JDK21` 以配合 `Salesforce Extension Pack` 更好工作。

    ```bash
    sudo apt update
    sudo apt install openjdk-21-jdk
    java -version
    ```

## 创建项目

- 按 **Ctrl+Shift+P** (Windows) 或 **Cmd+Shift+P** (macOS) 打开命令面板。
- 确保新提示开头为 `>`。
- 输入 `SFDX:Create Project`（SFDX：创建项目）。
- 选择 **SFDX: Create Project（SFDX：创建项目）**。
- 选择 **Standard（标准）**。
- 键入项目名称 `VSCodeQuickstart` 并按 **Enter** 键。
- 选择桌面作为创建项目的位置，方便以后查找。
- 等待新的 Visual Studio Code 窗口打开。

## 搜索文件

- 按 **Ctrl+P** 搜索文件 `project-scratch-def.json` 并打开。
- 将 `orgName` 项的值更改为 `Learning VS Code` 并保存。

## Playground 验证

- 按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX:Authorize an Org`（SFDX：授权一个组织）。
- 选择 **SFDX: Authorize an Org（SFDX：授权一个组织）**。
- 要接受默认登录 URL，输入别名 `VSCodePlayground`，按 **Enter** 键。
- 浏览器将打开新的 Salesforce 登录窗口。使用上一步中检索到的 Playground 用户名和密码登录 Playground。
- 当要求您向连接的应用授予访问权限时，单击 **Allow（允许）**。
- 关闭浏览器窗口。
    事务完成时，命令行终端窗口会返回一条成功消息。