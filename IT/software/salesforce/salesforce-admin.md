# Admin 基础

## 核心职责

- 用户管理
- 数据管理
- 产品管理
- 安全
- 可作的分析

# 对象

在 Salesforce CRM 中，**对象**（Object）类似于数据库中的表，它们用于存储和管理数据。将列视为**字段（Fields）**，将行视为**记录（Records）**。

Salesforce 对象分为两大类：**标准对象（Standard Objects）**和 **自定义对象（Custom Objects）**。

## 标准对象（Standard Objects）

Salesforce 预定义了一些常见的业务对象，例如：

- **Account（账户）**：存储公司或个人的业务信息，如客户或合作伙伴。
- **Contact（联系人）**：存储与账户关联的个人信息，如客户联系人。
- **Opportunity（商机）**：存储销售机会及其状态。
- **Lead（潜在客户）**：存储未转化的销售机会，如营销活动获取的潜在客户。
- **Case（案例）**：存储客户的支持请求或问题报告。
- **User（用户）**：存储 Salesforce 系统中的用户信息。
- **Task & Event（任务 & 事件）**：管理待办事项和日程安排。

## 自定义对象（Custom Objects）

标准对象可能无法满足特定业务需求，Salesforce 允许用户创建**自定义对象**，这些对象可以存储特定的业务数据。例如：

- **Project（项目）**：如果你的公司管理多个项目，可以创建一个 Project 对象来存储项目信息。
- **Invoice（发票）**：如果需要管理财务数据，可以创建 Invoice 对象存储发票信息。

### 创建自定义对象

在 Salesforce 中，你可以通过以下步骤创建自定义对象：

1. 进入 **Setup（设置）** → **Object Manager（对象管理器）**。
2. 点击 **Create（新建）** → **Custom Object（自定义对象）**。
3. 填写对象名称（如 "Project"）。
4. 添加必要的**字段**（如 "Project Name", "Start Date", "Status"）。
5. 配置**页面布局**、权限等。
6. 保存并部署对象。

## 对象的主要组成部分

无论是标准对象还是自定义对象，都包含以下主要元素：

| 组成部分                           | 说明                                         |
| ---------------------------------- | -------------------------------------------- |
| **字段（Fields）**                 | 定义对象中的数据列，如姓名、邮箱、电话号码。 |
| **记录（Records）**                | 存储具体的数据行，如一个客户的详细信息。     |
| **页面布局（Page Layout）**        | 控制用户界面上字段的显示方式。               |
| **关系（Relationships）**          | 连接不同对象（如账户与联系人之间的关系）。   |
| **对象权限（Object Permissions）** | 控制用户是否可以查看、编辑、删除对象的数据。 |

## 对象之间的关系

Salesforce 支持不同对象之间建立关系，主要有两种：

1. Lookup Relationship（查找关系）
    - 类似外键，允许对象之间建立非严格依赖关系。例如，一个 Contact 可以关联到一个 Account，但 Contact 仍可独立存在。
2. Master-Detail Relationship（主从关系）
    - 主对象（Master）控制从对象（Detail），如果删除 Master 记录，相关 Detail 记录也会被删除。
    - 例如，Invoice Line Items（发票明细）必须关联到 Invoice（发票），如果发票被删除，所有明细也会被删除。

## **通过 SOQL 查询对象数据**

Salesforce 提供 SOQL（Salesforce Object Query Language）来查询对象数据，例如：

```sql
SELECT Name, Email FROM Contact WHERE Account.Name = 'Acme Corp'
```

此查询获取所有属于 **Acme Corp** 公司的联系人姓名和邮箱。