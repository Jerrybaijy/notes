---
title: jquery
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - javascript
  - code-language
  - frontend
  - library
  - framework
  - web
---

# jQuery

jQuery 是一个快速、轻量级、跨浏览器的 JavaScript 库，它简化了 DOM 操作、事件处理、动画效果等任务。

## 版本选择

- jQuery [官网](https://releases.jquery.com/)
- **Uncompressed（非压缩版）：**

  - 文件名通常不包含 `.min`，例如：`jquery-3.6.4.js`。
  - 这个版本是未经压缩的，包含所有的注释和可读性更好的代码。通常用于开发和调试目的，方便阅读和调试 jQuery 源码。

- **Minified（压缩版）\***
  - 文件名通常以 ".min.js" 结尾，例如：`jquery-3.6.4.min.js`。
  - 这个版本是经过压缩的，包括了所有 jQuery 功能，但是通过删除不必要的空格、注释等来减小文件大小。
  - 压缩版适合用于生产环境，因为它减小了文件大小，有助于提高页面加载性能。
- **Slim（精简版）：**
  - 文件名通常包含 `.slim`，例如：`jquery-3.6.4.slim.js`。
  - Slim 版本去除了一些不太常用的功能，例如处理 Ajax 请求的模块，以减小文件大小。适合在项目中需要更轻量级的 jQuery 版本的情况下使用。
- **Slim Minified（精简压缩版）：**

  - 文件名通常以 `.slim.min.js` 结尾，例如：`jquery-3.6.4.slim.min.js`。
  - 这是 Slim 版本的压缩版，经过了精简和压缩处理，适用于生产环境。

## 引入 jQuery

有两种引入方式：使用 CDN（内容分发网络）和本地引入 jQuery 文件

### 使用 CDN

- **使用 CDN 方式特性**

  - **速度快：** 使用 CDN 可以加速页面加载速度，因为用户可能已经在访问其他网站时加载了相同的 jQuery 版本，从而在访问你的网站时可以从浏览器缓存中获取该文件，而不需要再次下载。
  - **省去本地存储空间：** 不需要将 jQuery 文件存储在本地项目中，可以减少项目大小。
  - **实时更新：** CDN 通常会定期更新和维护文件，因此你的网页可以始终使用最新版本的 jQuery。
  - **简单方便：** 只需在项目中引入一个 `<script>` 标签，就可以使用 jQuery，无需下载和管理本地文件。

- 进入[jQuery 官网](https://releases.jquery.com/)，点击 `Minified` 版本，复制引入代码，粘贴到 html 文件 `<head>` 元素中。

  ```html
  <head>
    <!-- 其它 head 元素 -->

    <!-- 使用 CDN 引入 jQuery -->
    <link src="https://code.jquery.com/jquery-3.7.1.min.js" />
  </head>
  ```

### 本地引入

- **本地引入方式特性**

  - **离线使用：** 如果你的项目在没有互联网连接的环境中运行，或者你更喜欢掌握自己项目的所有依赖，可以选择下载 jQuery 文件并在本地项目中引入。
  - **更好的控制：** 将 jQuery 文件下载到本地意味着你可以更好地控制文件的版本和更新时间。你可以选择在项目需要时手动更新文件。
  - **不依赖外部网络：** 在使用本地文件的情况下，不需要依赖外部网络资源，这有助于确保你的网页在任何环境中都能正常工作。

- 官网[下载 jQuery ](https://code.jquery.com/jquery-3.7.1.js)

- HTML 文件同级目录创建名为 `js` 的文件夹，将下载的 `js` 文件复制进该文件夹

  ```html
  <head>
    <!-- 其它 head 元素 -->

    <!-- 本地引入 jQuery 文件 -->
    <script src="js/jquery-3.7.1.js"></script>
  </head>
  ```

## 选择器和筛选器

- 选择器和筛选器

  ```html
  <div class="c1">
    <div id="c2">北京</div>
    <h1>
      <span class="c1">北京</span>
      <a>北京</a>
    </h1>
    <input type="text" />
  </div>
  ```

  ```javascript
  // 选择器

  // class选择器
  $(".c1");
  // 标签选择器
  $("h1");
  // ID选择器
  $("c2");
  // 层级选择器
  $(".c1 h1");
  // 属性选择器
  $('input[type="text"]');
  ```

  ```javascript
  // 筛选器

  // 上一个兄弟
  $("h1").prev();
  // 下一个兄弟
  $("h1").next();
  // 所有兄弟
  $("h1").siblings();

  // 父亲
  $("h1").parent(); // 即<div class="c1"></div>,可叠加
  // 儿子
  $("h1").children("a"); // 即<a>北京</a>,可叠加
  $("h1").children(".c1"); // 即<span>北京</span>,可叠加
  // 子子孙孙
  $(".c1").find();
  ```

## 读写 HTML

- jQuery 读写 HTML

  ```javascript
  // 以下tag均为jQuery创建/获取的标签的变量

  // 创建标签
  let tag = $("<div>"); // div为标签形式

  // 获取标签,可通过各种选择器/筛选器获取标签
  let tag = $("#city"); // city为原HTML标签id

  // 添加标签
  tagFather.append(tag); // 添加至尾部
  tagFarher.prepend(tag); // 添加至顶部

  // 获取标签内容
  let data = tag.text();

  // 更改标签内容
  tag.text("666"); // tag 标签变量  666 更改内容

  // 获取输入框内容text/password
  let data = tag.val();
  // 清空输入框内容
  tag.val("");
  ```

## 标签转换

- DOM 标签和 jQuery 标签的转换

  ```javascript
  // DOM标签转换为jQuery标签
  let tag2 = $(tag1);
  // jQuery标签转换为DOM标签
  let tag4 = tag3[0];
  ```

## 框架加载

- 框架加载

  ```javascript
  $(function () {
    // 当页面框架加载完之后自动执行
    $("#x1").click(function () {
      console.log(123);
    });
  });
  ```
