# Salesforce 基础

## 运行环境

Salesforce 提供多种环境，适用于不同的开发、测试、培训和生产需求。以下是 Salesforce 的主要环境分类：

- **正式业务运行**：使用 **Production**
- **开发和测试**：
    - **轻量开发**：Developer Edition
    - **生产数据测试**：Sandbox（Partial/Full Copy）
    - **DevOps 开发**：Scratch Org
- **学习和实验**：Trailhead Playground
- **提前测试新版本**：Preview Sandbox

### [TP](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management)

**TP**（Trailhead Playground ）是 Salesforce 提供的一个沙盒环境，专门用于 Trailhead 练习和实验 Salesforce 功能。它类似于 Developer Edition（DE），但主要用于学习，不会过期，而且可以创建多个。

#### TP 的特点

| 特点         | 说明                                     |
| ------------ | ---------------------------------------- |
| **用途**     | 主要用于 Trailhead 课程、挑战和实验      |
| **免费**     | 可以免费创建多个 TP，没有时间限制        |
| **不会过期** | 只要 Trailhead 账户存在，TP 就不会被删除 |
| **限制**     | 部分高级功能（如 API 访问）可能受限      |
| **自动配置** | 默认安装了一些 Trailhead 课程需要的组件  |

#### [创建 TP](https://trailhead.salesforce.com/content/learn/modules/trailhead_playground_management/create-a-trailhead-playground)

- **有两种方法创建**
    - 在模块的实践挑战中创建
    - 在 Trailhead 的个人简档中创建
- **以下是在 Trailhead 的个人简档中创建**
- Trailhead > 右上角图标 > `Hands-On Orgs` > `Create Playground`
- 等待几分钟，系统自动创建 TP。
- 之后可以点击 **"Launch"** 进入。
- 如果您使用英语以外的语言的 Trailhead，请确保您的 Playground 设置为与动手挑战相同的语言。否则，您可能会遇到通过挑战的问题。
- 需要密码才能从 Trailhead 外部访问组织，例如从 Salesforce CLI 和 VS Code 等开发人员工具访问组织。
    - 单击启动 App Launcher，然后搜索并单击 **Playground Starter**。
    - 单击 **Get Your Login Credentials** 选项卡。在这里，您可以看到您的 Trailhead Playground 用户名。
    - 点击 **Reset My Password**，然后点击 **Ok**，这会将一封电子邮件发送到与您的用户名关联的地址。
    - 单击电子邮件中的链接。输入新密码，确认，然后单击 **更改密码**。

#### TP 和 DE 的区别

| 对比项         | Trailhead Playground（TP）            | Developer Edition（DE）        |
| -------------- | ------------------------------------- | ------------------------------ |
| **适用场景**   | Trailhead 练习和挑战                  | 开发、测试、自定义 Salesforce  |
| **创建方式**   | 由 Trailhead 自动创建                 | 需要手动注册                   |
| **过期时间**   | 永久有效（不删除）                    | 可能因长时间未登录被删除       |
| **API 访问**   | 可能受限                              | 完整支持 API 访问              |
| **自定义权限** | 预配置了一些 Trailhead 课程需要的功能 | 完全自主配置                   |
| **组织管理**   | 可在 Trailhead 管理多个 TP            | 需要在 Salesforce Setup 里管理 |

### DE

**DE**（Developer Edition）是一种免费的 Salesforce 组织（Org），专门为开发者和学习者设计，用于学习、测试和构建 Salesforce 应用，而不会影响生产环境。

#### DE 的特点

1. **永久免费**：
    - 任何人都可以免费注册一个DE账户，并且不会过期，非常适合个人学习和开发。
2. **功能齐全**：
    - DE组织包含Salesforce的核心功能，如标准对象（Accounts、Contacts、Opportunities等）、自定义对象、Apex、Visualforce、Lightning Components、REST/SOAP API等。
    - 它与生产环境相似，因此可以用来测试和开发新功能。
3. **用户限制**：
    - DE组织默认只有**2个激活用户**（管理员和额外用户）。
    - 适合个人开发和小型测试，而不适用于企业级部署。
4. **数据存储限制**：
    - 默认提供**5MB** 数据存储和**20MB** 文件存储，因此不能用于大规模数据测试。
5. **API 访问**：
    - 支持 REST/SOAP API 调用，可以与外部系统集成并进行开发测试。
6. **适用于 Trailhead 学习**：
    - 在 **Trailhead（Salesforce 官方学习平台）** 上，许多练习需要使用DE组织。
7. **可用于开发和测试 AppExchange 应用**：
    - 如果你想在 Salesforce AppExchange 上发布应用，可以使用 DE 进行开发和测试。

## [Salesforce CLI](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop)

**Salesforce CLI**（命令行界面）是 Salesforce 提供的命令行工具，用于简化 Salesforce 组织的开发、CI/CD、测试和管理。它使开发人员能够高效地执行各种任务，如创建和管理 Salesforce 组织、部署代码、运行测试、导入/导出数据等。

Salesforce CLI 是 Salesforce 开发者工具链（DevOps Center、VS Code 插件等）的核心组件，并且支持 **Salesforce DX（Developer Experience）** 模型。

### Windows

- [官网下载 Salesforce CLI 并安装](https://developer.salesforce.com/tools/salesforcecli)

- 确认 CLI 已正确安装并处于最新版本

    ```bash
    sf update
    ```

- 查看版本

    ```bash
    sf -v
    ```

- 在 `VS Code` 中安装 `Salesforce Extension Pack (Expanded)` 扩展。

- 扩展的某些功能需要 JDK 支持，所以要安装 JDK，详见 `Java笔记`。

### Linux

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

- 在 `VS Code` 中安装 `Salesforce Extension Pack (Expanded)` 扩展。

- 扩展的某些功能需要 JDK 支持，所以要安装 JDK，详见 `Java笔记`。


## [创建项目](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop)

- 创建一个全新的 TP。

- VS Code 中按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX`。

- 选择 `SFDX: Create Project` （SFDX：创建项目）。

- 选择 **Standard（标准）**。

- 键入项目名称 `Dreamhouse` 并按 **Enter** 键。

- 选择桌面作为创建项目的位置，方便以后查找。

- 授权

    - 按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX: Authorize an Org`。
    - 选择 `Production`，输入组织别名 `myDevOrg`。
    - 弹出浏览器登录授权。

- 安装 `Node.js(LTS)`，详见 `JavaScript`。

- 打开组织

    - 命令行：在项目根目录终端运行命令

        ```bash
        sf org open
        ```

    - VS Code

        <img src="assets/image-20250302212052512.png" alt="image-20250302212052512" style="zoom:50%;" />


## 搜索文件

- 按 **Ctrl+P** 搜索文件 `project-scratch-def.json` 并打开。
- 将 `orgName` 项的值更改为 `Learning VS Code` 并保存。

# Playground

## Playground 验证

- 按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX:Authorize an Org`（SFDX：授权一个组织）。
- 选择 **SFDX: Authorize an Org（SFDX：授权一个组织）**。
- 要接受默认登录 URL，输入别名 `VSCodePlayground`，按 **Enter** 键。
- 浏览器将打开新的 Salesforce 登录窗口。使用上一步中检索到的 Playground 用户名和密码登录 Playground。
- 当要求您向连接的应用授予访问权限时，单击 **Allow（允许）**。
- 关闭浏览器窗口。
    事务完成时，命令行终端窗口会返回一条成功消息。

# 编程语言