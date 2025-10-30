---
title: web
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - web
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
