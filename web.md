---
title: web
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - web
  - dev-ops
  - ci-cd
---

# Web 开发

## Web 开发资源

> [Web](https://developer.mozilla.org/zh-CN/docs/Web)：MDN 关于 Web 的主页面

## 互联网底层协议与基础

### 网络基础

| 概念                    | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| **Client-Server Model** | 客户端（浏览器）请求资源，服务器响应并提供资源。             |
| **HTTP / HTTPS**        | 超文本传输协议（HyperText Transfer Protocol），Web 数据传输标准，HTTPS 是加密安全的版本。 |
| **URL / URI**           | 统一资源定位符（地址），用于识别资源位置。                   |
| **DNS**                 | 域名系统（Domain Name System），将域名翻译成 IP 地址。       |

### HTTP 工作机制

- **请求方法**：`GET` (获取), `POST` (提交), `PUT` (更新), `DELETE` (删除)。
- **状态码**：1xx (信息), 2xx (成功), 3xx (重定向), 4xx (客户端错误), 5xx (服务器错误)。
- **Headers**：请求头和响应头，包含元数据（如内容类型、缓存控制、Cookie）。

## 前端

前端负责用户界面的结构、样式和交互逻辑，运行在用户的浏览器中。

### 核心三要素

- **HTML**：结构和语义化（Semantic HTML）。
- **CSS**：样式和布局（Flexbox, Grid, 响应式设计）。
- **JavaScript**：交互逻辑和浏览器 API 操作（DOM 操作、事件处理）。

### 框架与库

| 框架        | 核心特点                                     | 主要用途                           |
| ----------- | -------------------------------------------- | ---------------------------------- |
| **React**   | 组件化、声明式编程、虚拟 DOM (Virtual DOM)。 | 构建高性能、复杂的单页应用 (SPA)。 |
| **Vue.js**  | 渐进式框架，易于集成和学习。                 | 中小型项目或逐步引入复杂交互。     |
| **Angular** | 完整框架体系，依赖 TypeScript。              | 企业级大型应用。                   |

### 前端工程化

- **Node Package Manager (npm/yarn/pnpm)**：依赖管理和脚本运行。
- **模块打包器 (Bundlers)**：**Webpack**, **Vite**，用于将代码、资源打包、压缩和优化。
- **Transpilers**：**Babel**，将 ES6+ 代码转换为浏览器兼容的 JS。
- **TypeScript (TS)**：为 JavaScript 添加静态类型检查。

## 后端

后端负责服务器逻辑、数据库交互、身份验证和 API 接口。

### 语言与框架

| 语言            | 框架                                            | 适用场景                                |
| --------------- | ----------------------------------------------- | --------------------------------------- |
| **Python**      | **Flask** (微服务/API), **Django** (全功能框架) | 快速原型开发、数据科学、复杂 Web 应用。 |
| **Node.js**     | **Express.js**, **NestJS**                      | 实时应用、高并发 I/O 密集型任务。       |
| **Java**        | Spring Boot                                     | 企业级应用、高稳定性。                  |
| **Go (Golang)** | Gin, Echo                                       | 高性能、微服务。                        |

### 数据库

- **关系型数据库 (SQL)**：**PostgreSQL**, **MySQL**。适用于结构化、强一致性数据。
- **非关系型数据库 (NoSQL)**：**MongoDB** (文档型), **Redis** (键值缓存), **Cassandra** (列式)。适用于灵活、高扩展性数据。

### API 设计

- **REST (Representational State Transfer)**：最常见的架构风格，基于 HTTP 动词和资源 URI。
- **GraphQL**：客户端可以精确请求所需数据，减少过度获取 (over-fetching)。

## 架构、部署与安全

### 架构模式

- **Monolithic (单体架构)**：所有功能集中在一个应用中。
- **Microservices (微服务)**：应用拆分成独立的服务，通过 API 通信。
- **SPA (单页应用)**：前端框架加载一次，通过 JS 动态更新内容（如 React）。
- **SSR (服务器端渲染)**：服务器预渲染 HTML，有助于 SEO 和性能。

### 部署与运维

即 **DevOps**

- **环境**：开发、测试、生产。
- **容器化**：**Docker**，用于打包应用及其依赖，确保环境一致性。
- **编排**：Kubernetes (K8s)，用于管理大规模容器化应用。
- **持续集成/持续部署 (CI/CD)**：自动化测试和部署流程。

### 安全

- **HTTPS/SSL/TLS**：加密数据传输。
- **用户认证 (Authentication)**：验证用户身份（如 JWT, Session）。
- **授权 (Authorization)**：控制用户对资源的访问权限。
- **常见漏洞防护**：
  - **XSS** (跨站脚本攻击)
  - **CSRF** (跨站请求伪造)
  - **SQL 注入**

### 性能优化

- **缓存策略**：浏览器缓存、CDN 缓存、服务器端缓存（Redis）。
- **资源优化**：代码压缩 (Minification)、图片优化、懒加载 (Lazy Loading)。
- **CDN (内容分发网络)**：将资源分发到全球边缘节点，加速访问。
- **Core Web Vitals**：评估用户体验的关键指标。

# Web 术语

> [MDN Web 文档术语表](https://developer.mozilla.org/zh-CN/docs/Glossary)：Web 相关术语的定义

此部分作为不方便归档的集中收纳。

# Web 机制

本部分涵盖与 Web 生态系统的一般知识及其工作原理相关的问题。

> [Web 机制](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Howto/Web_mechanics)

## URL

[**URL**](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL)（Uniform Resource Locator，统一资源定位符）是因特网中的唯一资源的地址。

## Web 服务器

[**Web 服务器**](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_web_server)可以代指硬件或软件，或者是它们协同工作的整体。

- **硬件部分**，web 服务器是一台存储了 web 服务器软件以及网站的组成文件（比如，HTML 文档、图片、CSS 样式表和 JavaScript 文件）的计算机。它接入到互联网并且支持与其他连接到互联网的设备进行物理数据的交互。
- **软件部分**，web 服务器包括控制网络用户如何访问托管文件的几个部分，至少是一台 _HTTP 服务器_。一台 HTTP 服务器是一种能够理解 [URL](https://developer.mozilla.org/zh-CN/docs/Glossary/URL)（网络地址）和 [HTTP](https://developer.mozilla.org/zh-CN/docs/Glossary/HTTP)（浏览器用来查看网页的协议）的软件。一个 HTTP 服务器可以通过它所存储的网站域名进行访问，并将这些托管网站的内容传递给最终用户的设备。

静态或动态服务器：

- **静态 web 服务器**（static web server）由一个计算机（硬件）和一个 HTTP 服务器（软件）组成。我们称它为“静态”是因为这个服务器把它托管文件的“保持原样”地传送到你的浏览器。
- **动态 web 服务器**（dynamic web server）由一个静态的网络服务器加上额外的软件组成，最普遍的是一个*应用服务器*和一个*数据库*。我们称它为“动态”是因为这个应用服务器会在通过 HTTP 服务器把托管文件传送到你的浏览器之前会对这些托管文件进行更新。

# 前后端分离

**前后端分离**是现代 Web 开发中一种**架构模式**，它将传统的集中式开发模式分解为两个相对独立的项目：**前端项目**和**后端项目**。

在传统（非分离）的开发模式中，后端服务器不仅处理数据逻辑，还负责页面的渲染（比如使用 JSP, PHP 或模板引擎）。

而**前后端分离**意味着：

1. **前端（Frontend）**：专注于用户界面（UI）和用户体验（UX），通常使用 HTML、CSS 和 JavaScript（如 React, Vue, Angular 等框架）来构建页面和处理交互逻辑。前端拥有自己的开发、构建和部署流程。
2. **后端（Backend）**：专注于业务逻辑、数据处理和数据存储，通常使用 Java、Python（如 Flask, Django）、Node.js 等语言构建，并通过 **API（应用程序接口）** 来向前端提供数据服务。后端也拥有独立的开发、测试和部署流程。

前后端通过标准的 **API 接口** 进行通信，这是分离架构的核心机制：

- **数据交换格式**：通常使用 **JSON** 或 **XML**。
- **通信协议**：通常是 **HTTP/HTTPS** 协议。
- **工作流程**：前端需要数据时，会向后端服务器发起一个 HTTP 请求（例如 GET/POST 请求），后端执行完业务逻辑后，将数据封装成 JSON 格式返回给前端。前端接收到 JSON 数据后，再使用 JavaScript 将数据渲染到页面上。

# 浏览器开发者工具

> [浏览器开发者工具](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Howto/Tools_and_setup/What_are_browser_developer_tools)

# Web 表单

> [Web 表单构建块](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Extensions/Forms)

```html
<form action="/my-handling-form-page" method="post">
  <h1>付款表单</h1>
  <p>
    必需的字段已使用
    <strong><span aria-label="required">*</span></strong> 标示。
  </p>
  <section>
    <h2>联系人信息</h2>
    <fieldset>
      <legend>称号</legend>
      <ul>
        <li>
          <label for="title_1">
            <input type="radio" id="title_1" name="title" value="A" />
            Ace
          </label>
        </li>
        <li>
          <label for="title_2">
            <input type="radio" id="title_2" name="title" value="K" />
            King
          </label>
        </li>
        <li>
          <label for="title_3">
            <input type="radio" id="title_3" name="title" value="Q" />
            Queen
          </label>
        </li>
      </ul>
    </fieldset>
    <p>
      <label for="name">
        <span>名字：</span>
        <strong><span aria-label="必须">*</span></strong>
      </label>
      <input type="text" id="name" name="username" required />
    </p>
    <p>
      <label for="mail">
        <span>邮箱：</span>
        <strong><span aria-label="必须">*</span></strong>
      </label>
      <input type="email" id="mail" name="usermail" required />
    </p>
    <p>
      <label for="pwd">
        <span>密码：</span>
        <strong><span aria-label="必须">*</span></strong>
      </label>
      <input type="password" id="pwd" name="password" required />
    </p>
  </section>
  <section>
    <h2>付款信息</h2>
    <p>
      <label for="card">
        <span>信用卡类型</span>
      </label>
      <select id="card" name="usercard">
        <option value="visa">Visa</option>
        <option value="mc">Mastercard</option>
        <option value="amex">American Express</option>
      </select>
    </p>
    <p>
      <label for="number">
        <span>卡号：</span>
        <strong><span aria-label="required">*</span></strong>
      </label>
      <input type="tel" id="number" name="cardnumber" required />
    </p>
    <p>
      <label for="expiration">
        <span>到期日：</span>
        <strong><span aria-label="required">*</span></strong>
      </label>
      <input
        type="text"
        id="expiration"
        name="expiration"
        required
        placeholder="MM/YY"
        pattern="^(0[1-9]|1[0-2])\/([0-9]{2})$"
      />
    </p>
  </section>
  <section>
    <p>
      <button type="submit">验证付款请求</button>
    </p>
  </section>
</form>
```

**在以上代码中**：

- `<section>`：将表单分为几部分
- `<fieldset>` 和 `<legend>`：表单分组

```css
h1 {
  margin-top: 0;
}

ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

form {
  /* 居中表单 */
  margin: 0 auto;
  width: 400px;
  padding: 1em;
  border: 1px solid #cccccc;
  border-radius: 1em;
}

label span {
  display: inline-block;
  text-align: right;
}

input,
fieldset {
  font: 1em sans-serif;
  width: 250px;
  box-sizing: border-box;
  border: 1px solid #999999;
}

input[type="checkbox"],
input[type="radio"] {
  width: auto;
  border: none;
}

input:focus {
  background-color: yellow;
}

button {
  margin-top: 20px;
}

label {
  /* 确保所有 label 大小相同并正确对齐 */
  display: inline-block;
}

p label {
  width: 100%;
}
```

# 无障碍

[**无障碍**](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Accessibility)是一种让尽可能多的用户可以使用你的网站的做法。所有用户包括但不限于：残疾人士、使用移动设备的人、使用低速网络连接的人。

- 使用严格的语义化 HTML 元素
- 使用 [WAI-ARIA](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Accessibility/WAI-ARIA_basics#进入_wai-aria) 规范，如 `<nav role="navigation">`  中的 `role`  属性。
- 更多...

# 跨浏览器测试

[跨浏览器测试](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Extensions/Testing)是确保网站能在不同浏览器和设备上运行的一种做法。

- 不同浏览器
- 不同硬件设备
- 无障碍

# 服务器端网站编程

[服务器端网站编程](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Extensions/Server-side)

# 数据库

数据库是一个用来组织、存储和管理数据的系统。

## 数据库类型

**关系型数据库（RDBMS）**： 关系型数据库是基于关系模型来存储数据的，数据存储在表中，并且这些表之间有关系。常见的关系型数据库管理系统有：

- **SQLite**：轻量级的数据库（只是一个文件），通常用于嵌入式应用中，适用于小型应用和开发阶段。
- **MySQL**：开源的关系型数据库系统，广泛应用于 Web 开发。
- **Oracle**：使用表、行和列的结构存储数据，常用于企业级应用中需要处理大量复杂数据关系的场景。

**非关系型数据库（NoSQL）**： 非关系型数据库通常不使用表格结构，而是使用键值对、文档、列族等不同的数据模型。适用于大规模的数据存储，尤其是在需要灵活扩展时。常见的 NoSQL 数据库有：

- **MongoDB**：以文档的形式存储数据，存储 JSON 格式的数据，适用于灵活和快速变化的数据模型。
- **Redis**：以键值对的形式存储数据，数据存储在内存中，读写速度极快，通常用于缓存数据和快速检索。

## 数据库基础

- **数据表（Table）**： 数据表是数据库中存储数据的基本结构。它由行（记录）和列（字段）组成。每个字段存储一个特定类型的数据（如文本、数字、日期等），而每一行代表一个记录。
- **行（Row）**： 行（又称记录）是表中的一条数据。每个记录包含表中所有列的数据。
- **列（Column）**： 列（又称字段）是表中的一个数据属性。例如，用户表可能有“用户名”、“密码”、“邮箱”等列。
- **主键（Primary Key）**： 主键是表中唯一标识每一行数据的字段。它确保每条记录是唯一的。通常情况下，主键是一个数字字段（如 ID），并且不会为空。
- **外键（Foreign Key）**： 外键是指向另一张表的主键的字段。外键用来表示两个表之间的关联。通过外键，数据库能够保持数据的完整性。
- **索引（Index）**： 索引是加速查询速度的一种数据结构，类似于书本的目录。它帮助快速查找表中的数据。
- **视图（View）**： 视图是一个虚拟的表，它不是物理存储的，而是通过查询其他表来动态生成的。它帮助简化复杂的查询操作，提供只读数据视图。
- **查询语言（SQL）**： SQL（Structured Query Language，结构化查询语言）是与数据库交互的标准语言。使用 SQL 可以查询数据、插入数据、更新数据、删除数据，以及创建和管理数据库结构。

## 数据库交互方式

### 命令行客户端

各个数据库都提供了一个命令行工具，如 MySQL 数据库的 `mysql`，可以通过该工具在命令行直接与 MySQL 数据库交互。

- 登录进入 MySQL 交互界面

  ```bash
  mysql -u root -p
  ```

- 登录到 MySQL 后，可以使用 SQL 命令进行数据库管理。

  ```bash
  mysql> $SQL_SYNTAX
  ```

- 退出 MySQL 交互界面

  ```bash
  EXIT;
  ```

### 编程语言客户端

各个编程语言都有自己的交互 MySQL 客户端，如 Python 的 `pymysql`。

### ORM

**ORM（对象关系映射，Object-Relational Mapping）** 是一种用于将面向对象编程中的对象与关系型数据库中的数据表进行映射的技术。

在交互**关系型数据库**方面，它提供了一个统一的操作接口，屏蔽了不同数据库之间的差异。无论交互哪种关系型数据库，都可以用相似的代码逻辑去操作，大大提高了代码的复用性和可移植性。

如 Python 的 `sqlalchemy`。

### GUI 工具

**GUI 工具**（Graphical User Interface Tools）指的是图形用户界面工具，如 `Navicat`。

# IaC

**IaC** (Infrastructure as Code)，即**基础设施即代码**，是一种通过**代码**（而非手动流程或图形界面）来管理和配置基础设施（如服务器、网络、数据库、存储等）的 IT 实践。

典型的 IaC 工作流通常包含以下步骤：

1. **编写 (Write)**：使用特定语言（如 HCL, YAML, Python）定义资源。
2. **计划 (Plan)**：预览代码将对现有环境做出的更改（Dry Run）。
3. **应用 (Apply)**：执行代码，云服务商或本地服务器按指令变更。
4. **销毁 (Destroy)**：不再需要时，一键删除所有相关资源，避免产生额外费用。

主流工具对比：

| **工具名称**           | **开发者** | **核心语言**      | **适用平台** | **特点**                                               |
| ---------------------- | ---------- | ----------------- | ------------ | ------------------------------------------------------ |
| **Terraform**          | HashiCorp  | HCL               | 全平台       | 开源、多云支持、使用 HCL 语言。                        |
| **CloudFormation**     | AWS        | YAML / JSON       | 仅限 AWS     | AWS 原生，深度集成。                                   |
| **Deployment Manager** | Google     | YAML / Python     | 仅限 GCP     | 支持 Python 和 Jinja2 模板，能编排几乎所有谷歌云资源。 |
| **Azure Bicep**        | Microsoft  | Bicep (DSL)       | 仅限 Azure   | ARM 模板的简洁进化版，专注于 Azure 资源的声明式管理。  |
| **Ansible**            | Red Hat    | YAML              | 跨平台       | 侧重于**配置管理**（在系统内装软件）。                 |
| **Pulumi**             | Pulumi     | Python, Go, TS 等 | 多云         | 使用通用语言（Python, JS, Go）。                       |
| **Kubernetes**         | CNCF       | YAML / JSON       | 跨平台       | 容器编排领域的“事实上的 IaC”。                         |

# OCI

## OCI 仓库

**OCI Registry**（OCI 仓库）是一个用于存储、管理和分发符合 OCI 规范的云原生制品（如容器镜像和 Helm Chart）的服务器端点（域名或地址）。

### OCI 仓库种类

- 公有 OCI 仓库：Docker Hub、Amazon ECR、Azure Container Registry、Google Artifact Registry 等

- 私有 OCI 仓库：Harbor、Helm Chart 等

### OCI 仓库地址

```bash
oci://<registry>/<namespace>
oci://registry-1.docker.io/jerrybaijy
```

- `oci://`：OCI 协议标识
- `<registry>`：仓库服务地址
- `<namespace>`：用户名或组织名

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

# DevOps

**DevOps**（**Dev**elopment **Op**eration**s**）是一种文化理念，旨在促进开发（Dev）和运维（Ops）团队之间的协作和沟通，以自动化软件交付过程，从而更快、更可靠地发布软件。

- DevOps 是 “指导思想”
- CI/CD 是 “具体做事的流程”
- GitOps 是 “用 Git 驱动这个流程的落地方式”

## CI/CD

**CI/CD** 是软件开发中的一组最佳实践，代表**持续集成（Continuous Integration）**和**持续交付/部署（Continuous Delivery/Deployment）**。它们的目标是提高软件开发效率，减少发布风险，并加速产品迭代。

### 持续集成（CI）

**持续集成**（CI）是一种开发实践，指的是开发人员频繁地（通常是每天多次）将代码集成到主分支，并自动化地执行构建和测试。

**核心流程**：

- **代码提交**：开发人员将代码推送到版本控制系统（如 Git）。
- **自动构建**：CI 工具（如 Jenkins、GitHub Actions、GitLab CI）自动拉取代码并执行构建脚本。
- **自动测试**：自动运行单元测试、集成测试，确保新代码不会破坏现有功能。
- **反馈**：构建或测试失败时，系统立即通知开发人员。

### 持续交付（CD - Continuous Delivery）

持续交付是在 CI 基础上，确保代码在任何时候都可以安全地发布到生产环境，但发布过程是**手动触发**的。

**核心流程**：

- **自动化部署到预生产环境**：在 CI 成功后，自动将代码部署到测试或预生产环境。
- **更多测试**：执行更高级别的测试，如用户验收测试（UAT）、安全扫描等。
- **人工批准发布**：在所有测试通过后，人工决定是否将代码发布到生产环境。

### 持续部署（CD - Continuous Deployment）

持续部署比持续交付更进一步，一旦通过测试，代码会**自动部署到生产环境**，无需人工干预。

**核心流程**：

- 自动化程度更高，任何通过测试的变更都会直接发布。
- 必须确保测试流程非常严谨，避免将不稳定的代码部署到生产。

### CI/CD 工具链示例

- **代码托管**：GitHub、GitLab、Bitbucket
- **CI/CD 平台**：Jenkins、GitLab CI/CD、GitHub Actions、CircleCI、Azure DevOps
- **构建工具**：Maven、Gradle、npm、Webpack
- **测试工具**：JUnit、PyTest、Selenium
- **部署工具**：Ansible、Docker、Kubernetes、Terraform

### CI/CD 示例流程

- 开发者提交代码
- CI 工具自动拉取代码
- 自动构建并运行单元测试
- 自动部署到测试环境
- 运行集成和验收测试
- **持续交付：人工审批后发布** 或 **持续部署：自动发布**
- **监控和回滚机制**（如有问题，快速回滚）

## GitOps

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

# FAQ

## 复制网页

- 当复制某些网页内容时，不允许复制，或者需要登录才能复制
- 在浏览器地址栏前面添加 `read:`，即可打开 `阅读器模式`
- 随后即可自由复制
