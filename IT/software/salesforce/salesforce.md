# Salesforce 基础

## 组织

在 Salesforce 中，**组织**（Organization，简称 **Org**）一套完整的 Salesforce 环境，可以是生产环境，也可以是非生产环境。Salesforce 提供多种组织，以下是 Salesforce 的主要组织分类：

- **生产环境**：Production
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
- 之后可以点击 `Launch` 进入。
- 如果您使用英语以外的语言的 Trailhead，请确保您的 Playground 设置为与动手挑战相同的语言。否则，您可能会遇到通过挑战的问题。
- 如果从 Trailhead 外部访问组织，例如从 Salesforce CLI 和 VS Code 等开发人员工具访问组织，需要密码。
    - 单击启动 `App Launcher`，然后搜索并单击 `Playground Starter`。
    - 单击 `Get Your Login Credentials` 选项卡。在这里，您可以看到 `当前 TP 用户名`。
    - 点击 `Reset My Password`，然后点击 `Ok`，这会将一封电子邮件发送到与您的用户名关联的地址。
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

### 安装 Salesforce CLI

- **Windows**

    - [官网下载 Salesforce CLI 并安装](https://developer.salesforce.com/tools/salesforcecli)
    - 确认 CLI 已正确安装并处于最新版本

        ```bash
        sf update
        ```

    - 查看版本

        ```bash
        sf -v
        ```

- **Linux**

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

- 更新 CLI

    ```bash
    sf update
    ```

- VS Code 扩展

    - 在 `VS Code` 中安装 `Salesforce Extension Pack (Expanded)` 扩展。
    - 在 VS Code 中按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX`，即可选择 Salesforce 扩展提供的命令。
    - 如果扩展在命令面板中找不到命令，先禁用再启用扩展。

- JDK

    - 扩展的某些功能需要 JDK 支持，所以要安装 JDK，详见 `Java笔记`。

    -  [设置 Apex 服务器的 Java 运行时的完整路径名：](https://developer.salesforce.com/docs/platform/sfvscode-extensions/guide/java-setup.html)

    - 设置 > 搜索 `apex` > `Salesforcedx-vscode-apex › Java: Home`

        ```
        C:\\Program Files\\Java\\jdk-21
        ```

## [创建项目](https://trailhead.salesforce.com/content/learn/projects/get-started-with-salesforce-development/get-ready-to-develop)

- **前置**

    - 创建一个全新的 TP

    - Salesforce CLI 已安装

    - Node.js 已安装

- VS Code 中按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX`。

- 选择 `SFDX: Create Project` 。

- 选择 `Standard`。

- 键入项目名称 `Dreamhouse` 并按 **Enter** 键。

- 确认项目位置。

- 授权

    - 按 **Ctrl+Shift+P** 打开命令面板，输入 `SFDX: Authorize an Org`。
    - 选择 `Production`，输入组织别名 `myDevOrg`。
    - 弹出浏览器登录授权。这里要输入之前创建 TP 时候的用户名和密码。

- 打开组织的方式

    - 命令行：在项目根目录终端运行命令

        ```bash
        sf org open
        ```

    - VS Code

        <img src="assets/image-20250302212052512.png" alt="image-20250302212052512" style="zoom:50%;" />

- 终端进入项目根目录，执行下面命令完成工具设置

    ```bash
    npm install
    ```

## 搜索文件

- 按 **Ctrl+P** 搜索文件 `project-scratch-def.json` 并打开。
- 将 `orgName` 项的值更改为 `Learning VS Code` 并保存。

# Objects 对象

在 Salesforce CRM 中，将数据表称为**对象（Object）**，它们用于存储和管理数据。将列称为**字段（Fields）**，将行称为**记录（Records）**。

Salesforce 支持多种不同类型的对象。有：

- 标准对象（Standard Objects）
- 自定义对象（Custom Objects）
- 外部对象
- 平台事件
- BigObjects

## 对象的主要组成部分

无论是标准对象还是自定义对象，都包含以下主要元素：

| 组成部分                           | 说明                                         |
| ---------------------------------- | -------------------------------------------- |
| **字段（Fields）**                 | 定义对象中的数据列，如姓名、邮箱、电话号码。 |
| **记录（Records）**                | 存储具体的数据行，如一个客户的详细信息。     |
| **页面布局（Page Layout）**        | 控制用户界面上字段的显示方式。               |
| **关系（Relationships）**          | 连接不同对象（如账户与联系人之间的关系）。   |
| **对象权限（Object Permissions）** | 控制用户是否可以查看、编辑、删除对象的数据。 |

## Standard Objects

**标准对象**是 Salesforce 附带的对象，例如：

- **Account（账户）**：存储公司或个人的业务信息，如客户或合作伙伴。
- **Contact（联系人）**：存储与账户关联的个人信息，如客户联系人。
- **Opportunity（商机）**：存储销售机会及其状态。
- **Lead（潜在客户）**：存储未转化的销售机会，如营销活动获取的潜在客户。
- **Case（案例）**：存储客户的支持请求或问题报告。
- **User（用户）**：存储 Salesforce 系统中的用户信息。
- **Task & Event（任务 & 事件）**：管理待办事项和日程安排。

## Custom Objects

**自定义对象**是您创建的用于存储特定于您的公司或行业的信息的对象。例如：

- **Project（项目）**：如果你的公司管理多个项目，可以创建一个 Project 对象来存储项目信息。
- **Invoice（发票）**：如果需要管理财务数据，可以创建 Invoice 对象存储发票信息。

### Create Custom Objects

- Select an Org.
- **Setup** > **Object Manager**
- **Create** > **Custom Object**
    - For **Label**, enter `<label_name>`. Notice that the **Object Name** and **Record Name** fields auto-fill.
    - For **Plural Label**, enter `<label_names>`.
    - Select the checkbox **Launch New Custom Tab Wizard after saving this custom object**.
    - Leave the rest of the values as default and click **Save**.

- **New Custom Object Tab**
    - Click the **Tab Style** field and select a style you like.
    - Click **Next**, **Next**, and **Save**.


## [Object Relationships](https://trailhead.salesforce.com/content/learn/modules/data_modeling/object_relationships?trail_id=force_com_dev_beginner)

There are two main types of object relationships: **lookup** and **master-detail**.

Salesforce 支持不同对象之间建立关系，主要有两种：

1. Lookup Relationship（查找关系）
    - 类似外键，允许对象之间建立非严格依赖关系。例如，一个 Contact 可以关联到一个 Account，但 Contact 仍可独立存在。
2. Master-Detail Relationship（主从关系）
    - 主对象（Master）控制从对象（Detail），如果删除 Master 记录，相关 Detail 记录也会被删除。

### Lookup Relationship

#### Create a Lookup Relationship

- Select an org and create a custom object.
- From **Setup**, go to **Object Manager** | **<object_name>**.
- In the sidebar, click **Fields & Relationships**. 
- Click **New** in the top right.
    - For **data type**, Choose **Lookup Relationship** and click **Next**.
    - For **Related To**, choose a right one, and click **Next**.
    - For **Field Name**, enter Contact, then click **Next**.
    - Click **Next**, **Next**, **Next**, and **Save**.

### Master-Detail Relationship

#### Create a Master-Detail Relationship

- Select an org.
- Create the 1st custom object **<1st_object_name>**.
    - Create a field.
    - Create a record.
- Create the 2nd custom object **<2nd_object_name>**.
- Create a **lookup relationship**.
- Create a **Master-Detail Relationship**.
    - From **Setup**, go to **Object Manager** | **<object_name>**.
    - In the sidebar, click **Fields & Relationships**. 
    - Click **New** in the top right.
    - For **data type**, Choose **Master-Detail Relationship** and click **Next**.
    - For **Related To**, choose **<1st_object_name>**, and click **Next**.
    - For Field Name, enter `Property` and click **Next**.
    - Click **Next**, **Next**, and **Save**.
- Contact **<2nd_object_name>** with **<1st_object_name>**.
    - From the **App Launcher** find and select **Sales**.
    - Click the **<1st_object_name>** tab in the navigation bar. 
    - Click **Related**. You’ll see **<2nd_object_name>** (0) in the Related tab.
    - Click **New**. Enter a name for **Favorite Name**, then click **Save**.

# Fields 字段

每个标准和自定义对象都有附加的字段，即**自定义字段**。

在 Field Name （字段名称） 列中，例如 `Price__c`，`__c` 是判断自定义字段的一种简单方法。

## Create Fields

- Select an org and create a custom object.
- From **Setup**, go to **Object Manager** | **<object_name>**.
- In the sidebar, click **Fields & Relationships**. 
- Click **New** in the top right.
    - For **data type**, select the right one, Then click **Next**.
    - Fill out **Field Label** field, and **Field Name** field auto-fill.
    - Check the **Required** box.
    - Click **Next**, **Next** again, and then **Save**.
- Create Records
    - From the **App Launcher** find and select **Sales**.
    - Click the **<object_name>** tab in the navigation bar. 
    - Click **New** in the top corner.
    - Enter a name and price for the Object and click **Save**.

## **通过 SOQL 查询对象数据**

Salesforce 提供 SOQL（Salesforce Object Query Language）来查询对象数据，例如：

```sql
SELECT Name, Email FROM Contact WHERE Account.Name = 'Acme Corp'
```

此查询获取所有属于 **Acme Corp** 公司的联系人姓名和邮箱。