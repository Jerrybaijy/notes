---
title: html-elements
author: Jerry.Baijy
tags:
  - code-language
  - frontend
  - html
  - it
  - web
---

> [WHATWG 元素参考](https://html.spec.whatwg.org/multipage/indices.html#Elements-3 "WHATWG 元素参考")
>
> [MDN 元素参考](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements "MDN HTML 元素参考")

HTML 元素基础详见 `html | 元素` 笔记。

本笔记的元素分类参照 WHATWG 文档的 [HTML 元素目录](https://html.spec.whatwg.org/multipage/#toc-semantics)。

# 元素归类

## 文档

- [`<html>`](#`<html>`) 主根元素
- [`<body>`](#`<body>`) 分区根元素
- [`<head>`](#`<head>`) 文档头部
- [`<meta>`](#`<meta>`) 元数据
- [`<title>`](#`<title>`) 文档标题
- [`<link>`](#`<link>`) 外部资源链接
- [`<style>`](#`<style>`) 内部样式表
- [`<base>`](#`<base>`) 文档根 URL

## 章节

- [`<header>`](#`<header>`) 页眉
- [`<nav>`](#`<nav>`) 导航栏
- [`<main>`](#`<main>`) 主内容
- [`<aside>`](#`<aside>`) 侧边栏
- [`<article>`](#`<article>`) 独立结构
- [`<section>`](#`<section>`) 独立章节
- [`<h>`](#`<h>`) 标题
- [`<hgroup>`](#`<hgroup>`) 标题组
- [`<address>`](#`<address>`) 地址
- [`<footer>`](#`<footer>`) 页脚

## 强调

- [`<strong>`](#`<strong>`) 重要性强调
- [`<em>`](#`<em>`) 语气强调
- [`<b>`](#`<b>`) 注意文本
- [`<mark>`](#`<mark>`) 标记高亮，高亮渲染

## 引用

- [`<q>`](#`<q>`) 行内引用
- [`<blockquote>`](#`<blockquote>`) 块级引用
- [`<cite>`](#`<cite>`) 引用作品

## 特殊文本

- [`<del>`](#`<del>`) 删除内容（编辑标识）
- [`<ins>`](#`<ins>`) 插入内容（编辑标识）
- [`<s>`](#`<s>`) 不准确文本
- [`<u>`](#`<u>`) 非文本注释
- [`<small>`](#`<small>`) 附注，小字体渲染
- [`<abbr>`](#`<abbr>`) 缩略语

## 定义和术语

- [`<dl>`](#`<dl>`) 定义列表
- [`<dt>`](#`<dl>`) 定义术语
- [`<dd>`](#`<dd>`) 定义描述
- [`<dfn>`](#`<dfn>`) 定义中的术语
- [`<i>`](#`<i>`) 术语文本

## 计算机和数学

- [`<var>`](#`<var>`) 变量
- [`<sup>`](#`<sup>`) 上标
- [`<sub>`](#`<sub>`) 下标
- [`<code>`](#`<code>`) 行内代码
- [`<pre>`](#`<pre>`) 与格式化（代码块）
- [`<kbd>`](#`<kbd>`) 键盘输入
- [`<samp>`](#`<samp>`) 程序输出

## 列表

- [`<li>`](#`<li>`) 列表项
- [`<ol>`](#`<ol>`) 有序列表
- [`<ul>`](#`<ul>`) 无序列表

## 表格

## 表单

## 交互

- [`<details>`](#`<details>`) 折叠组件
- [`<dialog>` ](#`<dialog>`) 对话框

## 脚本

- [`<script>`](#`<script>`) 脚本
- [`<noscript>`](#`<noscript>`) 无脚本
- [`<template>`](#`<template>`) 模板
- [`<slot>`](#`<slot>`) 插槽
- [`<canvas>`](#`<canvas>`) 画布

# 文档

## `<base>`

**文档根 URL** [`<base>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/base) 指定用于一个文档中包含的所有相对 URL 的根 URL。一份中只能有一个该元素，是空元素。

### 其它属性

- `href` 属性详见 `<a>` 元素。

## `<body>`

**分区根元素** [`<body>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/body) 包含文档的结构信息（如页眉、页脚等）和文档其它内容。

## `<head>`

**文档头部** [`<head>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/head) 包含文档相关的元数据信息，包括文档的标题、脚本和样式表等。

## `<html>`

[`<html>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/html) 元素称为**主根元素**。该元素包含整个页面的所有内容，其他所有元素必须是此元素的后代。

## `<link>`

### 语法

**外部资源链接** [`<link>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/link) 元素用于引入外部资源。

```html
<head>
  <link href="styles.css" rel="stylesheet" />
</head>
```

```css
/* styles.css */
p {color: red;}
```

**说明**

- **`rel="stylesheet"`** 表示当前文档与`main.css`文件的关系是样式表，浏览器会将其视为页面的外部CSS样式文件，并应用其中的样式规则。
- `<link>` 元素可以出现在 [`<head>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/head) 元素或 [`<body>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/body) 元素中，具体取决于它是否有一个 **body-ok** 的[链接类型](https://html.spec.whatwg.org/multipage/links.html#body-ok)，但最好将其放在 `<head>` 中。
- 该元素最常用于链接 CSS，此外也可以被用来创建站点图标 。

### 其它属性

- `href` 属性详见 `<a>` 元素。

## `<meta>`

 **元数据** [`<meta>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/meta) 用于表示文档的元数据信息。

### `charset`

**字符集** `charset` 告诉文档使用哪种字符编码：`<meta charset="UTF-8">`

### `name` 和 `content`

- `name` 和 `content` 属性一起使用，以名 - 值对的方式给文档提供元数据，其中 name 作为元数据的名称，content 作为元数据的值。
- [标准元数据名称](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/meta/name)
- **作者信息**：`<meta name="author" content="NAME" />`
- **描述信息**：`<meta name="description" content="content..." />`
- [**视口**](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Viewport_concepts)：`<meta name="viewport" content="width=device-width">`  
    视口可以确保页面以视口宽度进行渲染，避免移动端浏览器上因页面过宽导致缩放。

## `<style>`

**内部样式** [`<style>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/style) 用于创建文档内部样式表。最好的方式是使用 `<link>` 元素引入 CSS 外部样式表。

```html
<head>
  <style>
    p {
      color: #26b72b;
  </style>
</head>

<body>
  <p>
    This text will be green. Inline styles take precedence over CSS included
    externally.
  </p>
</body>
```

## `<title>`

**文档标题** [`<title>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/title) 元素用于定义文档的标题。

- 显示在浏览器的标题栏或标签页上
- 作为收藏网页的描述文字
- 用在搜索的结果中

# 章节

## `<address>`

[`address`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/address) 元素表示联系地址。

```html
<p>Contact the author of this page:</p>

<address>
  <a href="mailto:jim@example.com">jim@example.com</a><br />
  <a href="tel:+14155550132">+1 (415) 555‑0132</a>
</address>
```

```css
a[href^='mailto']::before {
  content: '📧 ';
}

a[href^='tel']::before {
  content: '📞 ';
}
```

> ![image-20241128135927232](assets/image-20241128135927232.png)

## `<article>`

**独立结构 ** [`<article>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/article) 元素表示文档、页面、应用或网站中的独立结构，其意在成为可独立分配的或可复用的结构，是块级元素。

例如，阅读器在博客上滚动时一个接一个地显示每篇文章的文本，每个帖子将包含在 `<article>` 元素中，可能包含一个或多个 `<section>`。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link href="../css/css-test.css" rel="stylesheet" />
  </head>

  <body>
    <article class="forecast">
      <h1>Weather forecast for Seattle</h1>
      <article class="day-forecast">
        <h2>03 March 2018</h2>
        <p>Rain.</p>
      </article>
      <article class="day-forecast">
        <h2>04 March 2018</h2>
        <p>Periods of rain.</p>
      </article>
      <article class="day-forecast">
        <h2>05 March 2018</h2>
        <p>Heavy rain.</p>
      </article>
    </article>
  </body>
</html>
```

```css
.forecast {
  margin: 0;
  padding: 0.3rem;
  background-color: #eee;
}

.forecast > h1,
.day-forecast {
  margin: 0.5rem;
  padding: 0.3rem;
  font-size: 1.2rem;
}

.day-forecast {
  background: right/contain content-box border-box no-repeat
    url('../images/rain.svg') white;
}

.day-forecast > h2,
.day-forecast > p {
  margin: 0.2rem;
  font-size: 1rem;
}
```

> ![image-20241128130311310](assets/image-20241128130311310.png)

## `<aside>`

**侧边栏 ** [`<aside>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/aside) 表示一个和其余页面内容几乎无关的部分，被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。其通常表现为侧边栏或者标注框（call-out boxes）。

```html
<head>
  <link href="../css/css-test.css" rel="stylesheet" />
</head>

<body>
  <p>
    Salamanders are a group of amphibians with a lizard-like appearance, including short legs and a tail in both larval
    and adult forms.
  </p>

  <aside>
    <p>The Rough-skinned Newt defends itself with a deadly neurotoxin.</p>
  </aside>

  <p>
    Several species of salamander inhabit the temperate rainforest of the Pacific Northwest, including the Ensatina, the
    Northwestern Salamander and the Rough-skinned Newt. Most salamanders are nocturnal, and hunt for insects, worms and
    other small creatures.
  </p>  
</body>
```

```css
aside {
  width: 40%;
  padding-left: 0.5rem;
  margin-left: 0.5rem;
  float: right;
  box-shadow: inset 5px 0 5px -5px #29627e;
  font-style: italic;
  color: #29627e;
}

aside > p {
  margin: 0.5rem;
}
```

> ![image-20241128132126937](assets/image-20241128132126937.png)

## `<footer>`

**页脚** [`<footer>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/footer) 通常包含该章节作者、版权数据或者与文档相关的链接等信息。

```html
<head>
  <link href="../css/css-test.css" rel="stylesheet" />
</head>
<body>
  <h3>FIFA 世界杯最佳射手</h3>
  <ol>
    <li>米罗斯拉夫 · 克洛泽，16</li>
    <li>罗纳尔多 · 纳扎里奥，15</li>
    <li>格尔德 · 穆勒，14</li>
  </ol>

  <footer>
    <small> 版权所有 © 2023 足球历史档案馆。保留所有权利。 </small>
  </footer>
</body>
```

```css
footer {
  text-align: center;
  padding: 5px;
  background-color: #abbaba;
  color: #000;
}
```

> ![image-20241128131541136](assets/image-20241128131541136.png)

## `<h>`

**标题** [`<h>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/Heading_Elements) 用于定义标题级别，从 `<h1>` 到 `<h6>`，是块级元素。

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

> ![image-20241128135532190](assets/image-20241128135532190.png)

**注意**：

- 避免跳过某级标题：始终要从 `<h1>` 开始，接下来依次使用 `<h2>` 等等
- 不要为了减小标题的字体而使用低级别的标题
- 同一篇幅尽量不要超过三级标题

## `<header>`

**页眉** [`<header>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/header) 用于展示介绍性内容，通常包含一组介绍性的或是辅助导航的实用元素。它可能包含一些标题元素，但也可能包含其他元素，比如 Logo、搜索框、作者名称，等等。

```html
<head>
  <link href="../css/css-test.css" rel="stylesheet" />
</head>

<body>
  <header>
    <a class="logo" href="#">Cute Puppies Express!</a>
  </header>
  
  <article>
    <header>
      <h1>Beagles</h1>
      <time>08.12.2014</time>
    </header>
    <p>I love beagles <em>so</em> much! Like, really, a lot. They’re adorable and their ears are so, so snugly soft!</p>
  </article>
</body>
```

```css
.logo {
  background: left / cover url('../images/dog.jpg');
  display: flex;
  height: 120px;
  align-items: center;
  justify-content: center;
  font:
    bold calc(1em + 2 * (100vw - 120px) / 100) 'Dancing Script',
    fantasy;
  color: #ff0083;
  text-shadow: #000 2px 2px 0.2rem;
}

header > h1 {
  margin-bottom: 0;
}

header > time {
  font: italic 0.7rem sans-serif;
}
```

> ![image-20241128130156849](assets/image-20241128130156849.png)

## `<hgroup>`

**标题组**  [`<hgroup>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/hgroup) 元素

##  `<main>`

**主内容** [`<main>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/header) 元素用于做页面分组，呈现文档的主要内容，可以有各种子内容区段，如 `<article>`、`<section>` 和 `<aside>` 等。

```html
<head>
  <link href="../css/css-test.css" rel="stylesheet" />
</head>

<body>
  <header>Gecko facts</header>

  <main>
    <p>
      Geckos are a group of usually small, usually nocturnal lizards. They are
      found on every continent except Antarctica.
    </p>

    <p>
      Many species of gecko have adhesive toe pads which enable them to climb
      walls and even windows.
    </p>
  </main>
</body>
```

```css
header {
  font: bold 7vw Arial, sans-serif;
}
```

> ![image-20241128132615446](assets/image-20241128132615446.png)

**扩展**：

- 主内容中还可以有各种子内容区段，可用 `<article>`、`<section>` 和 `<div>` 等元素表示。
- 侧边栏 `<aside>`、 独立结构 `<article>`、独立章节 `<section>` 和 `<div>` 经常嵌套在 `<main>` 中。

## `<nav>`

**导航栏 ** [`<nav>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/nav) 用于在当前文档或其他文档中提供导航链接。导航部分的常见示例是菜单，目录和索引。

```html
<head>
  <link href="../css/css-test.css" rel="stylesheet" />
</head>

<body>
  <nav class="crumbs">
    <ol>
      <li class="crumb"><a href="#">Bikes</a></li>
      <li class="crumb"><a href="#">BMX</a></li>
      <li class="crumb">Jump Bike 3000</li>
    </ol>
  </nav>

  <h1>Jump Bike 3000</h1>
  <p>
    This BMX bike is a solid step into the pro world. It looks as legit as it
    rides and is built to polish your skills.
  </p>
</body>
```

> ![image-20241128130034228](assets/image-20241128130034228.png)

## `<section>`

**独立章节** [`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/section) 是一个通用的分节元素，只有在没有更具体的元素来代表它的时候才可以使用。

```html
<head>
  <link href="../css/css-test.css" rel="stylesheet" />
</head>

<body>
  <h1>Choosing an Apple</h1>
  <section>
    <h2>Introduction</h2>
    <p>This document provides a guide to help with the important task of choosing the correct Apple.</p>
  </section>

  <section>
    <h2>Criteria</h2>
    <p>
      There are many different criteria to be considered when choosing an Apple — size, color, firmness, sweetness,
      tartness...
    </p>
  </section>  
</body>
```

```css
h1,
h2 {
  margin: 0;
}
```

> ![image-20241128132929225](assets/image-20241128132929225.png)

# 内容分组

## `<blockquote>`

**块级引用** [`<blockquote>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/blockquote) 表示其中的文字是引用内容，是块级元素，渲染时有缩进，且加引号。

```html
<div>
  <blockquote cite="https://www.huxley.net/bnw/four.html">
    <p>
      Words can be like X-rays, if you use them properly—they’ll go through
      anything. You read and you’re pierced.
    </p>
  </blockquote>
  <p>—Aldous Huxley, <cite>Brave New World</cite></p>
</div>
```

```css
div:has(> blockquote) {
  background-color: #ededed;
  margin: 10px auto;
  padding: 15px;
  border-radius: 5px;
}

blockquote p::before {
  content: "\201C";
}

blockquote p::after {
  content: "\201D";
}

blockquote + p {
  text-align: right;
}    
```

> ![image-20241128163006929](assets/image-20241128163006929.png)

**说明**：

- 若引文来源于网络，则可以将原内容的出处 URL 地址设置到 cite 特性上。
- 若要以文本的形式告知读者引文的出处时，可以通过 `<cite>` 元素。

## `<dd>`

**定义描述** [`<dd>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/dd) 是块级元素，详见 `<dl>` 元素。

## `<div>`

**内容划分** [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/div) 元素无语义，用于将零散的行内元素组成区块，是块级元素。

```html
<div class="shadowbox">
  <p>这是一张非常有趣的说明，陈列在一个可爱的影盒里。</p>
</div>
```

```css
.shadowbox {
  width: 15em;
  border: 1px solid #333;
  box-shadow: 8px 8px 5px #444;
  padding: 8px 12px;
  background-image: linear-gradient(180deg, #fff, #ddd 40%, #ccc);
}
```

> ![image-20241128144407274](assets/image-20241128144407274.png)

## `<dl>`

**定义列表** [`<dl>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/dl) 是一个包含*术语定义 `<dt>`* 和*术语描述 `<dd>`* 的列表，通常用于展示词汇表或者元数据（键 - 值对列表），是块级元素，渲染时术语描述部分有缩进。

```html
<p>Cryptids of Cornwall:</p>

<dl>
  <dt>Beast of Bodmin</dt>
  <dd>A large feline inhabiting Bodmin Moor.</dd>

  <dt>Morgawr</dt>
  <dd>A sea serpent.</dd>

  <dt>Owlman</dt>
  <dd>A giant owl-like creature.</dd>
</dl>
```

```css
p,
dt {
  font-weight: bold;
}

dl,
dd {
  font-size: 0.9rem;
}

dd {
  margin-bottom: 1em;
}
```

> ![image-20241128154157844](assets/image-20241128154157844.png)

- **扩展**：`<dt>` 元素的文本可以使用 `<dfn>` 包围。

## `<dt>`

**定义描述** [`<dt>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/dt) 是块级元素，详见 `<dl>` 元素。

## `<figcaption>`

## `<figure>`

**可附标题内容** [`<figure>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/figure) 表示“独立的媒体单元”，是块级元素。可能包含 `<figcaption>` 元素定义的说明内容。

- **语法**

    ```html
    <!-- 一个图注 -->
    <figure>
      <img src="assets/图片.png" alt="替代" style="width: 40%" />
      <figcaption style="font-size: 16px; color: gray">图注</figcaption>
    </figure>
    
    <!-- 多个图注 -->
    <figure>
      <img src="assets/图片.png" alt="替代" style="width: 40%" />
      <figcaption style="font-size: 16px; color: gray">
        <div>图注</div>
        <div>图注</div>
      </figcaption>
    </figure>
    ```

- **扩展示例**

    ```html
    <figure>
      <img src="../images/elephant-660-480.jpg" alt="Elephant at sunset" />
      <figcaption>An elephant at sunset</figcaption>
    </figure>
    ```

    ```css
    figure {
      border: thin #c0c0c0 solid;
      display: flex;
      flex-flow: column;
      padding: 5px;
      max-width: 220px;
      margin: auto;
    }
    
    img {
      max-width: 220px;
      max-height: 150px;
    }
    
    figcaption {
      background-color: #222;
      color: #fff;
      font: italic smaller sans-serif;
      padding: 3px;
      text-align: center;
    }
    ```

- **渲染效果**

    > ![image-20241128160504158](assets/image-20241128160504158.png)

## `<hr>`

**主题分割** [`<hr>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/hr) 即水平线，语义上表示段落级元素之间的主题转换，是块级元素。

```html
<p>§1: The first rule of Fight Club is: You do not talk about Fight Club.</p>
<hr />
<p>§2: The second rule of Fight Club is: Always bring cupcakes.</p>
```

```css
hr {
  border: none;
  border-top: 3px double #333;
  color: #333;
  overflow: visible;
  text-align: center;
  height: 5px;
}

hr::after {
  background: #fff;
  content: '§';
  padding: 0 4px;
  position: relative;
  top: -13px;
}
```

> ![image-20241128161540618](assets/image-20241128161540618.png)

## `<li>`

### 语法

**列表项** [`<li>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/li) 用于表示列表中的项目，详见 `<ol>` 元素。

### `value`

[`value`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/li#value) 属性在有序列表中，指定列表项 `<li>` 的序号。

```html
<ol>
  <li value="100">第一百列表项</li>
  <li value="200">第二百列表项</li>
  <li value="300">第三百列表项</li>
</ol>
```

> <ol>
> <li value="100">第一百列表项</li>
> <li value="200">第二百列表项</li>
> <li value="300">第三百列表项</li>
> </ol>

## `<menu>`

**菜单** [`<menu>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/menu) 在 HTML 规范中被描述为 `<ul>` 的语义替代，但浏览器将其视为与 `<ul>` 没有区别。

```html
<menu>
  <li>第一列表项</li>
  <li>第二列表项</li>
  <li>第三列表项</li>
</menu>
```

> <menu>
> <li>第一列表项</li>
> <li>第二列表项</li>
> <li>第三列表项</li>
> </menu>

## `<ol>`

### 语法

**有序列表** [`<ol>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ol) 显示按顺序排列的列表项 `<li>`，默认以数字等符号进行标记。

```html
<ol>
  <li>第一列表项</li>
  <li>第二列表项</li>
  <li>第三列表项</li>
</ol>
```

> <ol>
> <li>第一列表项</li>
> <li>第二列表项</li>
> <li>第三列表项</li>
> </ol>

### 列表嵌套

**列表嵌套**是指在一个列表项 `<li>` 中包含另一个列表

```html
<!-- 规范写法 -->
<ul>
  <li>
    项目一
    <ol>
      <li>子项目一</li>
      <li>子项目二</li>
    </ol>
  </li>
  <li>项目二</li>
</ul>

<!-- 不规范写法 -->
<ul>
  <li>项目一</li>
  <ol>
    <li>子项目一</li>
    <li>子项目二</li>
  </ol>
  <li>项目三</li>
</ul>
```

> <ul>
> <li>
>  项目一
>  <ol>
>    <li>子项目一</li>
>    <li>子项目二</li>
>  </ol>
> </li>
> <li>项目二</li>
> </ul>

**注意**：不要将一个列表当成列表项 `<li>` 进行嵌套，而是要把列表放在 `<li>` 的内容中。

### `start`

[`start`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ol#start) 属性用于指定有序列表的起始值。

```html
<ol start="5">
  <li>第五列表项</li>
  <li>第六列表项</li>
  <li>第七列表项</li>
</ol>
```

> <ol start="5">
> <li>第五列表项</li>
> <li>第六列表项</li>
> <li>第七列表项</li>
> </ol>

### `type` 属性

[`type`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ol#type) 属性在有序列表中，用于指定有序列表的计数器类型，即序列号的类型。

```html
<ol type="A">
  <li>第一列表项</li>
  <li>第二列表项</li>
  <li>第三列表项</li>
</ol>
```

> <ol type="A">
> <li>第一列表项</li>
> <li>第二列表项</li>
> <li>第三列表项</li>
> </ol>

## `<p>`

[`<p>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/p) 元素用于定义 HTML 文档中的段落，是块级元素。

```html
<p>这是第一个段落</p>
<p>这是第一个段落</p>
```

**渲染效果**：浏览器默认会在段落的前后添加空行。

> <p>这是第一个段落</p>
>
> <p>这是第二个段落</p>

## `<pre>`

**预格式化** [`<pre>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/pre) 用于保证文本的编排顺序不变，文本中的空白符（比如空格和换行符）都会显示出来，是行内元素。类似于 Markdown 的代码块。

```html
<pre>
function greet() {
  console.log("Hello, world!");
}
</pre>
```

> <pre>
> function greet() {
> console.log("Hello, world!");
> }
> </pre>

## `<search>`

[`<search>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/search) 元素

## `<ul>`

**无序列表** [`<ul>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ul) 用于显示无顺序排列的列表项 `<li>`。渲染时默认以圆点等符号进行标记，如果想修改，应该在 CSS 中修改。

```html
<ul>
  <li>第一列表项</li>
  <li>第二列表项</li>
  <li>第三列表项</li>
</ul>
```

> <ul>
> <li>第一列表项</li>
> <li>第二列表项</li>
> <li>第三列表项</li>
> </ul>

# 文本级语义

>  [WHATWG 文本级语义元素汇总](https://html.spec.whatwg.org/multipage/text-level-semantics.html#usage-summary)

## `<a>`

### 语法

**锚元素** [`<a>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/a) 可以通过它的 `href` 属性创建通向其他网页、文件、电子邮件地址、同一页面内的位置或任何其他 URL 的超链接，供用户点击，属于行内元素。

```html
<a href="https://www.example.com">点击这里</a>
```

> <p>You can reach Michael at:</p>
>
> <ul>
> <li><a href="https://example.com">Website</a></li>
> <li><a href="mailto:m.bluth@example.com">Email</a></li>
> <li><a href="tel:+123456789">Phone</a></li>
> </ul>

### `href`

#### 语法

[`href`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/a#href)（***h**ypertext **ref**erence*，超文本引用）用于超链接所指向的 URL。跳转目标可以是绝对路径、相对路径、锚点、电话号、E-mail、JS 代码和文件等。

```html
<p>You can reach Michael at:</p>
<ul>
  <li><a href="https://example.com">Website</a></li>
  <li><a href="mailto:m.bluth@example.com">Email</a></li>
  <li><a href="tel:+123456789">Phone</a></li>
</ul>
```

> <p>You can reach Michael at:</p>
> <ul>
> <li><a href="https://example.com">Website</a></li>
> <li><a href="mailto:m.bluth@example.com">Email</a></li>
> <li><a href="tel:+123456789">Phone</a></li>
> </ul>

#### 锚点

**锚点**是分隔 URL 中*地址*和*片段*的**标识符**，可以在点击链接后跳转到该网页的锚点位置。

锚点元素添加 `id="锚点"` 属性，跳转元素在 URL/SRC 地址后添加 `#锚点`。

```html
<!-- 跳转到本地锚点 -->
<div id="锚点">百度</div>
<a href="#锚点">点击跳转至百度</a>

<!-- 跳转到 URL 锚点 -->
<a href="https://example.com#Home">Website</a>
```

**锚点的规范**：

- 同一地址可省略 URL/SRC
- **全转换成小写**：即 `Full-page` → `full-page`
- **空格替换为连字符 `-`**：
    - 标题中的空格需用半角连字符（`-`）替代，避免 URL 中的空格引发解析错误。
    - `full-page databases` → `full-page-databases`
- **保留特殊符号（如连字符）**：标题原有的半角连字符（如 `Full-page` 中的 `-`）无需处理，直接保留。

### 跳转方式 `target`

[`target`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/a#target) 属性用于指定链接的*打开方式* 或者指定提交表单时的*目标窗口*。通常用于 `<a>` 和 `<form>`。

```html
<a href="https://www.example.com" target="_blank">Visit Example.com</a>
```

**属性值**：

- **`_self`**：默认值，在当前窗口中打开。
- **`_blank`**：在新窗口或新标签页中打开。
- **`_parent`**：在父级框架中打开。
- **`_top`**：在顶级窗口中打开。

## `<abbr>`

**缩略语** [`<abbr>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/abbr) 用于代表缩写。

```html
<p>你可以用 <abbr>EMS</abbr> 把这个包裹寄给我。</p>
<p>你可以用 <abbr title="邮政特快专递服务">EMS</abbr> 把这个包裹寄给我。</p>
```

> <p>你可以用 <abbr>EMS</abbr> 把这个包裹寄给我。</p>
>
> <p>你可以用 <abbr title="邮政特快专递服务">EMS</abbr> 把这个包裹寄给我。</p>

**说明**：`title` 属性用于当鼠标悬停时，对缩略词提供一个扩展解释。

## `<b>`

**注意文本** [`<b>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/b) 元素用于引起人们的注意，但不传达任何额外的重要性，也不暗示其他语气或情绪，例如文档摘要中的关键词、评论中的产品名称、交互式文本驱动软件中的可操作词或文章导语。是行内元素，渲染为粗体。

```html
<p>
  本文档描述了几个<b class="keywords">文本级</b>元素，并解释了它们在
  <b class="keywords">HTML</b> 文档中的用法。
</p>
```

> <p>
> 本文档描述了几个<b class="keywords">文本级</b>元素，并解释了它们在
> <b class="keywords">HTML</b> 文档中的用法。
> </p>

## `<bdi>`

**双向文本隔离** [`<bdi>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/bdi) 元素用于隔离文本默认的渲染方向，防止未知方向的文本影响周围文本的布局，是行内元素。

## `<bdo>`

**双向文本覆盖** [`<bdo>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/bdo) 元素用于覆盖文本默认的渲染方向，默认从左向右，是行内元素。

```html
<p>该文本应从左到右绘制。</p>
<p><bdo dir="rtl">该文本应从右到左绘制。</bdo></p>
```

> <p>该文本应从左到右绘制。</p>
>
> <p><bdo dir="rtl">该文本应从右到左绘制。</bdo></p>

## `<br>`

**换行** [`<br>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/br) 用于在文本中生成一个换行符（回车），将 `<br>` 之后的文本从下一行开始渲染，是空元素。

```html
<p>这是第一行<br>这是第二行</p>
```

> <p>这是第一行<br>这是第二行</p>

**注意**

- 不要使用 <kbd>Enter</kbd> 进行换行
- 不要用 `<br>` 来增加文本之间的行间隔

## `<cite>`

[`<cite>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/cite) 元素用于引用作品，是行内元素，渲染时为斜体。

```html
<p>
  更多内容详见<cite>《计算机基础》</cite>。
</p>
```

> <p>
> 更多内容详见<cite>《计算机基础》</cite>。
> </p>

## `<code>`

**行内代码** [`<code>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/code) 表示在段落内的一段文本是一段代码，是行内元素。

```html
<p>请将以下代码添加到项目中：<code>console.log("Hello, world!");</code></p>
```

> <p>请将以下代码添加到项目中：<code>console.log("Hello, world!");</code></p>

## `<data>`

[`<data>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/data) 元素

## `<dfn>`

[`<dfn>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/dfn) 元素表示定义中的术语，是行内元素，渲染为斜体。

```html
<p>
  <!-- Define "The Internet" -->
  <dfn id="def-internet">The Internet</dfn> is a global system of interconnected
  networks that use the Internet Protocol Suite (TCP/IP) to serve billions of
  users worldwide.
</p>

<dl>
  <dt>
    <!-- Define "World-Wide Web" and reference definition for "the Internet" -->
    <dfn>
      <abbr title="World-Wide Web">WWW</abbr>
    </dfn>
  </dt>
  <dd>
    The World-Wide Web (WWW) is a system of interlinked hypertext documents
    accessed on <a href="#def-internet">the Internet</a>.
  </dd>
</dl>
```

> <p>
>   <!-- Define "The Internet" -->
>   <dfn id="def-internet">The Internet</dfn> is a global system of
>   interconnected networks that use the Internet Protocol Suite (TCP/IP) to
>   serve billions of users worldwide.
> </p>
> <dl>
>   <dt>
>     <!-- Define "World-Wide Web" and reference definition for "the Internet" -->
>     <dfn>
>       <abbr title="World-Wide Web">WWW</abbr>
>     </dfn>
>   </dt>
>   <dd>
>     The World-Wide Web (WWW) is a system of interlinked hypertext documents
>     accessed on <a href="#def-internet">the Internet</a>.
>   </dd>
> </dl>

- **扩展**：可以作为 `<dl>` 中的 `<dt>` 的元素内容。

## `<em>`

[`<em>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/em) 元素表示语气上的强调，是行内元素，斜体渲染。

```html
<p>Get out of bed <em>now</em>!</p>
<p>We <em>had</em> to do something about it.</p>
<p>This is <em>not</em> a drill!</p>
```

> <p>Get out of bed <em>now</em>!</p>
> <p>We <em>had</em> to do something about it.</p>
> <p>This is <em>not</em> a drill!<p>

## `<i>`

**术语文本** [`<i>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/i) 用于标记因某些原因需要区分普通文本的一系列文本。例如技术术语、音译、思想或船名等。是行内元素，渲染为斜体。

```html
<p>The Latin phrase <i>Veni, vidi, vici</i> is often mentioned in music, art, and literature.</p>
```

> <p>The Latin phrase <i>Veni, vidi, vici</i> is often mentioned in music, art, and literature.</p>

## `<kbd>`

**键盘输入** [`<kbd>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/kbd) 表示用户输入，是行内元素。

```html
<kbd>Enter</kbd>
```

> <kbd>Enter</kbd>

## `<mark>`

**标记高亮** [`<mark>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/mark) 表示上下文相关或突出显示以供参考，是行内元素，渲染为高亮。

```html
<p>&lt;mark&gt; 元素用于 <mark>高亮</mark> 文本</p>
```

> <p>&lt;mark&gt; 元素用于 <mark>高亮</mark> 文本</p>

浏览器通常以黄色背景高亮显示 `<mark>` 元素的内容，但不要纯粹为了高亮显示而用 `<mark>` 元素，而是应该使用 CSS 来实现。

```css
mark {
  background-color: yellow;
  color: black;
}
```

## `<q>`

**行内引用** [`<q>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/q) 用于引用短文本，是行内元素，渲染时加引号。

```html
<p>他说：<q>今天的天气真好！</q></p>
```

> <p>他说：<q>今天的天气真好！</q></p>

## `<rp>`

[`<rp>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/rp) 元素

## `<rt>`

[`<rt>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/rt) 元素

## `<ruby>`

**注音** [`<ruby>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ruby) 用来展示东亚文字注音或字符注释。

```html
<ruby>汉字<rp>(</rp><rt>hàn zì</rt><rp>)</rp></ruby>
```

> <ruby>汉字<rp>(</rp><rt>hàn zì</rt><rp>)</rp></ruby>

## `<s>`

[`<s>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/s) 元素表示不再准确或不再相关的内容，不适用于指示文档编辑，是行内元素，渲染时加删除线。

```html
<s>Today's Special: Salmon</s> SOLD OUT
```

> <s>Today's Special: Salmon</s> SOLD OUT

## `<samp>`

**程序输出** [`<samp>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/samp) 表示程序输出，是行内元素。

```html
<p>程序运行后输出：<samp>Hello, world!</samp></p>
```

> <p>程序运行后输出：<samp>Hello, world!</samp></p>

## `<small>`

**附注** [`<small>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/small) 元素

## `<span>`

**内容跨越** [`<span>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/span) 元素无语义，用于给段落内的文本加样式，是行内元素。该元素仅应在无其他合适语义元素时使用。

```html
<p>
  Add the <span class="ingredient">basil</span>,
  <span class="ingredient">pine nuts</span> and
  <span class="ingredient">garlic</span> to a blender and blend into a paste.
</p>

<p>
  Gradually add the <span class="ingredient">olive oil</span> while running the
  blender slowly.
</p>
```

```css
span.ingredient {
  color: #f00;
}
```

> ![image-20241128170152520](assets/image-20241128170152520.png)

## `<strong>`

**重要性强调 ** [`<strong>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/strong) 用来对一个句子的部分**文本**增加重要性，是行内元素，渲染时为粗体。

```html
<p>这个句子里的<strong>这个词语</strong>比较重要。</p>
```

> <p>这个句子里的<strong>这个词语</strong>比较重要。</p>

## `<sub>`

**下标** [`<sub>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/sub) 元素

## `<sup>`

**上标** [`<sup>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/sup) 元素

## `<time>`

[`<time>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/time) 元素表示一个特定的时间段。

```html
<p>演出于 <time datetime="2018-07-07T20:00:00">20:00</time> 开始。</p>
```

> <p>演出于 <time datetime="2018-07-07T20:00:00">20:00</time> 开始。</p>

**注意**：

- 在使用公历之前的日期时不应使用该元素（因为这些日期的计算比较复杂）。
- 此部分关于 [**有效的日期时间值**](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/time#有效的日期时间值) 没弄懂。

## `<u>`

**非文本注释** [`<u>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/u) 表示行内文本拥有一个非文本形式的注释，该注释需要以某种方式渲染出来。例如拼写错误和中文专有名词。是行内元素，渲染时加下划线。

```html
<p>This paragraph includes a <u>wrnogly</u> spelled word.</p>
```

> <p>This paragraph includes a <u>wrnogly</u> spelled word.</p>

## `<var>`

**变量** [`<var>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/var) 表示数学表达式或编程上下文中的变量名称，是行内元素，渲染为斜体。

```html
<p>
  长方体的体积公式为：<var>v</var> = <var>l</var> × <var>w</var> × <var>h</var>
</p>
```

> <p>
> 长方体的体积公式为：<var>v</var> = <var>l</var> × <var>w</var> × <var>h</var>
> </p>

## `<wbr>`

**换行机会** [`<wbr>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/wbr) 元素

# 编辑

## `<ins>`

**插入文本** [`<ins>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/ins) 表示被插入文档中的内容，属于编辑标识，与 `<del>` 对应，是行内元素，渲染时加下划线。

```html
<body>
  <p><ins>这是一段新增的文本</ins></p>
</body>
```

> <p><ins>这是一段新增的文本</ins></p>

## `<del>`

**删除文本** [`<del>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/del) 表示被从文档中删除的内容，属于编辑标识，与 `<ins>` 对应，是行内元素，渲染时加删除线。

```html
<p><del>This text has been deleted</del>, here is the rest of the paragraph.</p>
```

> <p><del>This text has been deleted</del>, here is the rest of the paragraph.</p>

# 嵌入内容

## `<img>`

**图像** [`<img>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/img) 用于在页面中嵌入图像，是行内元素，空元素。

### 语法

```html
<img src="assets/dog.jpg" alt="dog" />
```

> <img src="assets/dog.jpg" alt="dog" style="width: 50%; float: left" />

### `src`

**外部资源** [`src`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/img#src) 属性用于指定脚本文件引用的外部资源的路径。可以是本地路径，也可以是网络上的 URL。

```html
<img src="path/to/image.jpg" alt="Description">
```

### `alt`

**替代文本** [`alt`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/img#alt) 属性作用：

- 如果图像无法加载，`alt` 属性的文本将被显示。
- 屏幕阅读器等辅助技术可以读取 `alt` 文本，以提供对图像的描述，帮助视觉障碍用户理解图像内容。

```html
<img src="example.jpg" alt="一个展示示例的图像">
```

`alt` 属性适用元素：[`<img>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/img)、[`<input>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input)、[`<area>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/img)

### `width`

**语法**：[`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性是 HTML 中用于指定元素宽度和高度的属性。

- **属性值单位**：可以是像素 `px`、百分比 `%`、视口 `vw/vh`、`em`、`rem` 和绝对长度单位（如mm）等，详见 `CSS` - `值和单位`。
- **自适应**：通常情况下，如果只设置 `width: 200px;`，而没有设置 `height`，浏览器将根据图像的纵横比自动计算 `height`。

### 响应式图片

[**响应式图片**](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Reference/Multimedia_and_embedding/Responsive_images)可以解决不同尺寸屏幕对图片的要求

## `<audio>`

**音频** [`<audio>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/audio) 元素用于在页面中嵌入音频，是行内元素。

```html
<audio src="music/实验音频.mp3" controls>降级文本</audio>
```

> <audio src="music/实验音频.mp3" controls>降级文本</audio>

- `降级文本` 是当浏览器不支持 `<audio>` 元素时的回退

## `<picture>`

[`<picture>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/picture) 包含零或多个 `<source>` 元素和一个 `<img>` 元素来为不同的显示 / 设备场景提供图像版本。

## `<map>`

**图像映射** [`<map>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/map) 与*图像映射区域* `<area>` 元素一起使用来定义一个图像映射（一个可点击的链接区域）。

## `<area>`

**图像映射区域** [`<area>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/area) 元素...，是空元素。

### 其它属性

- `href` 属性详见 `<a>` 元素。

## `<source>`

**播放源** [`<source>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/source) 元素为 `<picture>`、`<audio>` 或 `<video>` 元素指定多个媒体资源。

在 `<video>` 里嵌套 `<source>` 使视频有备用播放源，浏览器将会使用它所支持的第一个源。

```html
<video controls>
  <source src="video/终局第01集.mp4" type="video/MP4" />
  <source src="video/终局第01集.mkv" type="video/mkv" />
</video>
```

## `<video>`

**视频** [`<video>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/video) 元素用于支持文档内的视频播放，属性 `controls` 用于添加播放按钮。

```html
<video src="video/终局第01集.mp4" controls></video>
```

### 视频属性

- `src`、`height`、`width`
- `autoplay` 自动播放
- `loop` 布尔属性；指定后，会在视频播放结束的时候，自动返回视频开始的地方，继续播放。
- `muted` 默认静音
- `poster` 播放前显示海报

### 视频事件

## `<track>`

**嵌入文本轨** [`<track>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/track) 作为媒体元素 `<audio>` 和 `<video>` 的子元素使用。每个文本轨元素允许你指定一个定时文本轨（或基于时间的数据），可以与媒体元素并行显示，例如在视频上叠加字幕或隐藏式字幕，或与音频轨一起显示。

## `<iframe>`

**内联框架** [`<iframe>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/iframe) 能够将另一个 HTML 页面嵌入到当前页面中。

## `<embed>`

**外部内容嵌入** [`<embed>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/embed) 能够将外部内容嵌入文档中的指定位置。

## `<object>`

**嵌入对象** [`<object>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/object) 表示引入一个外部资源，这个资源可能是一张图片，一个嵌入的浏览上下文，亦或是一个插件所使用的资源。

## `<svg>`

[`<svg>`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Reference/Elements/svg) 元素

## `<math>`

**数学公式** [`<math>`](https://developer.mozilla.org/zh-CN/docs/Web/MathML/Reference/Elements/math) 元素

# 表格

## `<table>`

[`<table>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/table) 元素

### 完整表格

- **语法**

    ```html
    <table>
      <caption>表格标题</caption>
      <thead>
        <tr>
          <th>表头1</th>
          <th>表头2</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>数据1</td>
          <td>数据2</td>
        </tr>
        <tr>
          <td>数据3</td>
          <td>数据4</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td>总计</td>
          <td>100</td>
        </tr>
      </tfoot>
    </table>
    ```

- **渲染效果**

    > ![image-20241128151117058](assets/image-20241128151117058.png)

- **元素说明**

    - `<table>`：定义整个表格。
    - `<caption>` 标题  `<thead>` 表头  `<tbody>` 主体   `<tfoot>` 页脚，可省略。
    - `<tr>`：定义表格中的行。
    - `<th>`：定义表格中的表头单元格（表头单元格会加粗且默认居中显示）。
    - `<td>`：定义表格中的数据单元格。

### 基本表格

- **语法**

    ```html
    <table>
      <tr>
        <th>表头1</th>
        <th>表头2</th>
      </tr>
      <tr>
        <td>数据1</td>
        <td>数据2</td>
      </tr>
      <tr>
        <td>数据3</td>
        <td>数据4</td>
      </tr>
    </table>
    ```

- **渲染效果**

    > ![image-20241128151252635](assets/image-20241128151252635.png)

- **`border` 属性**：属性 `<table border="1">` 控制边框已经弃用，在实际开发中，建议使用 CSS 样式来进行更灵活和精细的样式控制，或者引入 BootStrap。

- **嵌套**：`<table>` 可以嵌套在 `<th>` 或 `<td>` 中

### 合并单元格

- **语法**：合并行  `rowspan`，合并列 `colspan`，单元格占几行（列），值就等于几。

    ```html
    <table border="1">
      <tr>
        <th>表头1</th>
        <th colspan="2">表头2</th>
      </tr>
      <tr>
        <td rowspan="2">数据1</td>
        <td>数据2</td>
        <td>数据3</td>
      </tr>
      <tr>
        <td>数据4</td>
        <td>数据5</td>
      </tr>
    </table>
    ```

- **渲染效果**

    > ![image-20241128151538056](assets/image-20241128151538056.png)

### 自由表头

- 属性 `scope` 可以添加在 `<th>` 元素中，以告诉屏幕阅读器该表头的类型——它是所在行的表头，还是所在列的表头。

- `scope` 的值

    - 单列表头 `col`
    - 多列表头 `colgroup`
    - 单行表头 `row`
    - 多行表头 `rowgroup`

- **示例**

    ```html
    <table border="1">
      <tr>
        <th>&nbsp;</th>
        <th scope="col">单列表头</th>
        <th colspan="2" scope="colgroup">多列表头</th>
        <th scope="col">单列表头</th>
      </tr>
      <tr>
        <th scope="row">单行表头</th>
        <td>数据1</td>
        <td>数据1</td>
        <td>数据1</td>
        <td>数据1</td>
      </tr>
      <tr>
        <th rowspan="2" scope="rowgroup">多行表头</th>
        <td>数据2</td>
        <td>数据2</td>
        <td>数据2</td>
        <td>数据2</td>
      </tr>
      <tr>
        <td>数据3</td>
        <td>数据3</td>
        <td>数据3</td>
        <td>数据3</td>
      </tr>
      <tr>
        <th scope="row">单行表头</th>
        <td>数据4</td>
        <td>数据4</td>
        <td>数据4</td>
        <td>数据4</td>
      </tr>
    </table>
    ```

- **渲染效果**

    > ![image-20241128151655606](assets/image-20241128151655606.png)



## `<caption>`

**表格标题**  [`<caption>`](https://html.spec.whatwg.org/multipage/tables.html#the-caption-Elements) 用于

## `<tbody>`

**表格主体** [`<tbody>`](https://html.spec.whatwg.org/multipage/tables.html#the-tbody-Elements) 用于

## `<col>`

**表格列** [`<col>`](https://html.spec.whatwg.org/multipage/tables.html#the-col-Elements) 用于

## `<colgroup>`

**表格列组** [`<colgroup>`](https://html.spec.whatwg.org/multipage/tables.html#the-colgroup-Elements) 用于

## `<thead>`

**表格表头行** [`<thead>`](https://html.spec.whatwg.org/multipage/tables.html#the-thead-Elements) 用于

## `<tr>`

**表格数据行** [`<tr>`](https://html.spec.whatwg.org/multipage/tables.html#the-tr-Elements) 用于

## `<tfoot>`

**表格汇总行** [`<tfoot>`](https://html.spec.whatwg.org/multipage/tables.html#the-tfoot-Elements) 用于

## `<th>`

**表格表头单元格** [`<th>`](https://html.spec.whatwg.org/multipage/tables.html#the-th-Elements) 用于

## `<td>`

**表格数据单元格** [`<td>`](https://html.spec.whatwg.org/multipage/tables.html#the-td-Elements) 用于

# 表单

## `<form>`

**表单** [`<form>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/form) 元素表示文档中的一个区域，此区域包含交互控件，用于向 Web 服务器提交信息。

### 表单语法

- **语法**

    ```html
    <form action="/submit" method="post">
      <!-- 这里是表单内容，包括输入框、按钮等 -->
      <input type="submit" value="提交">
    </form>
    ```

- **扩展**：在 Django 框架下，必须校验，否则无法提交。

    ```html
    <form action="/login/" method="post">
      <!-- 校验，否则无法提交 -->
      {% csrf_token %}
      <!-- 这里是表单内容，包括输入框、按钮等 -->
      <input type="submit" value="提交">
    </form>
    ```

### 表单属性

- 允许的值在 [`<form>` 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/form#%E5%B1%9E%E6%80%A7)中

    - `action`：提交的目标 URL
    - `method`：数据传输方式
    - `target`：跳转方式

### `action`

[`action`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/form#action) 属性用于指定表单数据提交的目标 URL。当用户填写表单并点击提交按钮时，浏览器会将表单数据发送到指定的 `action` URL。

**语法**：`<form action="/submit">`

### `method`

[`method`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/form#method) 属性用于指定表单数据提交时使用的 HTTP 方法。HTTP 方法定义了浏览器将如何发送表单数据以及服务器应该如何处理这些数据。`method` 属性有两个常用的取值： `get` 和 `post`。

**语法**：`<form method="post">`

**[GET方法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)**

- 当使用 `GET` 方法提交表单时，表单数据会附加在 URL 的末尾（query string），并以键值对的形式出现。这种方式适合用于获取数据，但不适合包含敏感信息，因为数据会明文显示在 URL 中。GET 方法通常用于数据检索，而不涉及对服务器上数据的修改。

**[POST方法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST)**

- 使用 `POST` 方法提交表单时，表单数据会包含在表单体内，而不会显示在 URL 中。这种方式更适合用于提交敏感信息和对服务器上数据进行修改。POST 方法通常用于表单提交，文件上传等需要传输大量数据或包含敏感信息的场景。传递文件必须使用 `POST` 形式传递。

## `<label>`

- **标签** [`<label>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/label) 用于为表单元素提供标签，并且在用户界面上通常表现为可点击的文本。

    -  点击关联的标签来聚焦或者激活输入框，就像直接点击输入框一样，这扩大了输入框的可点击区域。
    -  当用户聚焦到输入框时，屏幕阅读器可以读出标签，让使用辅助技术的用户更容易理解应输入什么数据。

- **语法**：

    ```html
    <form>
      <label for="username">用户名:</label>
      <input type="text" id="username" name="username" placeholder="请输入用户名">
    </form>
    ```

    ![image-20241204211508665](assets/image-20241204211508665.png)

    **在上述示例中**：

    1. 使用 `<label>` 元素来标识 `用户名：` 字段。
    2. 使用 `for` 属性用于关联 `<input>` 元素的 `id`。
    3. 使用 `<input>` 元素来创建文本输入框。
    4. 当用户点击 `用户名：` 时，也可以激活输入框，而不是必须点击输入框。

- **`for` 属性**：用于关联表单元素的 `id`。

- **扩展**：如果将 `<input>` 元素嵌套在 `<label>` 元素内部，就不需要使用 `for` 和 `id` 属性，因为它们将自动关联。但这种方式不利于 CSS 样式控制。

    ```html
    <form>
      <label>
        用户名:
        <input type="text" name="username" placeholder="请输入用户名">
      </label>
    </form>
    ```

## `<input>`

**输入框** [`<input>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input) 用于创建各种表单控件，允许用户输入数据或进行选择。

### 输入框语法

```html
<form action="/submit" method="post">
  <label for="username">用户名：</label>
  <input type="text" id="username" name="username" placeholder="请输入用户名">
  <input type="submit" value="提交">
</form>
```

![image-20241204213459154](assets/image-20241204213459154.png)

**在上述示例中**：

1. 使用 `<label>` 元素的 `for` 属性来标识 `用户名：` 字段。
2. 使用 `id` 属性关联 `label` 元素的 `for` 属性。
3. 使用 `name` 属性标识输入框的内容。
4. 使用 `placeholder` 属性进行输入提示。

### 输入框属性

- 允许的值在 [`<input>` 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#%E5%B1%9E%E6%80%A7)中
- [`type`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#type)：控件类型
- [`name`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#name)：输入框名称，用于在提交表单时标识输入框的内容
- [`value`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#value)：输入框默认值
- [`placeholder`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Attributes/placeholder)：占位符，用于输入框提示
- [`accept`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#accept)：限制文件类型。`accept="image/*"`，仅允许选择图片文件。
- [`required`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#required)：当存在时，要求用户在提交表单之前必须填写该字段
- [`readonly`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#readonly)：当存在时，使输入框变为只读，用户无法编辑输入框的内容
- [`disabled`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#disabled)：当存在时，禁用输入框或按钮，使其不可编辑或不可点击
- [`size`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#size)：控件尺寸

### `type`

[`type`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#type) 属性指定要渲染的控件的类型。`<input>` 的工作方式相当程度上取决于 `type` 属性的值。

- 允许的值在 [Input 类型](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input#input_类型)中
- 如果未指定此属性，则采用的默认类型为 `text`。

#### `text`

- [`text`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input/text) 类型的 `<input>` 元素用于创建单行文本输入框。

- **语法**：`<input type="text">`

    ```html
    <form action="/submit" method="post">
      <label for="name">用户名：</label>
      <input type="text" id="name" name="username" placeholder="请输入用户名">
      <input type="submit" value="提交">
    </form>
    ```

    ![image-20241204213529813](assets/image-20241204213529813.png)

    **在以上示例中**：

    1. 使用 `placeholder` 属性进行输入提示。

#### `password`

- [`password`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input/password) 类型的 `<input>` 元素用于创建密码输入框，允许用户输入密码或其他敏感信息。与普通的文本输入框不同，密码输入框中的输入通常以点或星号的形式显示，以隐藏实际输入的字符。

- **语法**：`<input type="password">`

    ```html
    <form>
      <input type="password" name="password" placeholder="请输入密码">
    </form>
    ```

    ![image-20241204175001002](assets/image-20241204175001002.png)

#### `file`

- [`file`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input/file) 类型的 `<input>` 元素用于创建文件上传表单控件，允许用户从本地文件系统中选择一个或多个文件，并将其上传到服务器。

- **语法**：`<input type="file">`

    ```html
    <form action="/upload" method="post" enctype="multipart/form-data">
      <label for="avatar">请上传图片：</label>
      <input type="file" id="avatar" name="avatar" accept="image/*">
      <input type="submit" value="上传">
    </form>
    ```

    ![image-20241204185108699](assets/image-20241204185108699.png)

    **在上述示例中**：

    1. `method="post"`：传递文件必须使用 `POST` 形式传递。
    2. `enctype="multipart/form-data"`：指定了表单数据的编码类型，通常在上传文件时使用。
    3. `type="file"`：表示创建一个文件上传控件。
    4. `accept="image/*"` 限制文件类型，仅允许选择图片文件。

#### `radio`

- [`radio`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input/radio) 类型的 `<input>` 元素用于创建**单选框**，允许用户从一组选项中选择一个选项。

- **语法**：`<input type="radio">`

    ```html
    <form>
      <input type="radio" name="gender" value="male"> 男性
      <input type="radio" name="gender" value="female"> 女性
    </form>
    ```

    ![image-20241204185234245](assets/image-20241204185234245.png)

    **在上述示例中**：

    1. 使用 `name` 属性将单选框分组在一起，确保用户只能从同一组中选择一个选项。
    2. 使用 `value` 属性为每个选项指定一个值，这个值将在表单提交时被发送到服务器。

#### `checkbox`

- [`checkbox`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input/checkbox) 类型的 `<input>` 元素用于创建**复选框**，允许用户选择或取消选择一个或多个选项。

- **语法**：`<input type="checkbox">`

    ```html
    <form>
      <input type="checkbox" name="vehicle" value="Bike">我喜欢自行车<br>
      <input type="checkbox" name="vehicle" value="Car">我喜欢小汽车
    </form>
    ```

    ![image-20241204185713038](assets/image-20241204185713038.png)

    **在上述示例中**：

    1. 使用 `name` 属性将复选框分组在一起，确保用户可以从同一组中选择多个选项。
    2. 使用 `value` 属性为每个选项指定一个值，这个值将在表单提交时被发送到服务器。

- **说明**：用户可以点击复选框以选择或取消选择相应的选项。如果 `value` 属性未指定，提交表单时将默认使用 `on` 作为复选框的值。

#### `submit`

- [`submit`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/input/submit) 类型的 `<input>` 元素用于创建表单中的**提交按钮**。当用户点击该按钮时，将触发表单的提交行为，将表单中的数据发送到服务器。

- **语法**：`<input type="submit">`

    ```html
    <form action="/submit" method="post">
      <!-- 这里是其他表单元素 -->
    
      <input type="submit" value="提交">
    </form>
    ```

    ![image-20241204191228212](assets/image-20241204191228212.png)

    **在上述示例中**：

    1. `value` 属性定义了按钮上显示的文本，这里是 `提交`。
    2. 当用户点击 `提交` 按钮时，表单将按照指定的 `action` 和 `method` 属性提交到服务器。

- **扩展**：除了 `<input>` 元素之外，也可以使用 `<button>` 元素创建提交按钮。

    ```html
    <form action="/submit" method="post">
      <!-- 这里是其他表单元素 -->
    
      <button type="submit">提交</button>
    </form>
    ```

## `<textarea>`

- **多行文本** [`<textarea>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/textarea) 元素用于在 HTML 表单中创建**多行文本输入框**，允许用户输入大段自由格式的文本。

- **语法**：

    ```html
    <form action="/submit" method="post">
      <label for="story">Tell us your story:</label>
    
      <textarea id="story" name="story" rows="5" cols="33">
        It was a dark and stormy night...
      </textarea>
    </form>
    ```

    ![image-20241204202909809](assets/image-20241204202909809.png)

    **在上述示例中**：

    1. 使用 `<textarea>` 元素创建多行文本输入框。
    2. `rows` 和 `cols` 属性定义了文本框的行数和列数，这是可选的。

## `<select>`

- **下拉框** [`<select>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/select) 元素表示一个提供下拉菜单的控件。通常与 `<option>` 元素结合使用，每个 `<option>` 表示一个可选项。

- **语法**

    ```html
    <form  action="/submit" method="post">
      <label for="cars">请选择一辆汽车：</label>
      <select name="car" id="cars">
        <option value="">请点击选择</option>
        <option value="volvo">沃尔沃</option>
        <option value="saab">萨博</option>
        <option value="mercedes">奔驰</option>
        <option value="audi">奥迪</option>
      </select>
      <input type="submit" value="提交">
    </form>
    ```

    ![image-20241204223958572](assets/image-20241204223958572.png)

    **在上述示例中**：

    1. 使用 `<select>` 元素创建下拉列表框。
    2. 使用 [`<option>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/option) 元素定义了下拉列表中的每个选项。
    3. 使用 `name` 属性定义了在提交表单时将选择的值关联到的名称。
    4. 用户可以通过点击下拉列表框并选择其中的一个选项。当表单被提交时，所选选项的值将被作为表单数据的一部分发送到服务器。

- **扩展**：`<select>` 元素还支持 `multiple` 属性，允许用户通过 `Ctrl` 键选择多个选项。

    ```html
    <form>
      选择一辆汽车:
      <select name="cars" multiple>
        <option value="volvo">沃尔沃</option>
        <option value="saab">萨博</option>
        <option value="mercedes">奔驰</option>
        <option value="audi">奥迪</option>
      </select>
      <input type="submit" value="提交" />
    </form>
    ```

    ![image-20241204224352505](assets/image-20241204224352505.png)

## `<button>`

- [`<button>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/button) 元素用于在 HTML 中创建**按钮**，可以包含文本、图像或其他 HTML 元素。它是一个多功能的元素，通常用于与 JavaScript 配合执行自定义操作。

- **语法**

    ```html
    <button type="reset">重置</button>
    ```

- [`type`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/button#type)

    - **`submit`**：默认值，提交按钮，在表单内点击时会提交表单。
    - **`button`**：普通按钮，没有默认行为。
    - **`reset`**：重置按钮，在表单内点击时会重置表单中的输入字段为默认值。

- **扩展**

    - 与 `<input>` 元素的按钮相比，`<button>` 元素具有更多的自定义选项和样式，可以包含其他 HTML 元素，并且更容易通过 CSS 进行样式化。

        ```html
        <!-- 这是一个包含按钮的示例 -->
        <button>
          <img src="icon.png" alt="图标"> 点击我
        </button>
        ```

    - 在使用 `<button>` 元素时，通常会结合 JavaScript 使用，例如：

        ```html
        <button onclick="myFunction()">点击我</button>
        
        <script>
          function myFunction() {
            alert("按钮被点击了！");
            // 执行其他自定义操作
          }
        </script>
        ```

### `disabled`

[`disabled`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/button#disabled) 属性用于禁止用户与某个元素进行交互。

```html
<input type="text" disabled>
```

## `<datalist>`

[`<datalist>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-datalist-Elements)

## `<option>`

[`<option>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-option-Elements)

## `<optgroup>`

[`<optgroup>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-optgroup-Elements)

## `<output>`

[`<output>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-output-Elements)

## `<progress>`

[`<progress>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-progress-Elements)

## `<meter>`

[`<meter>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-meter-Elements)

## `<fieldset>`

[`<fieldset>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-fieldset-Elements)

## `<legend>`

[`<legend>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-legend-Elements)

## `<selectedcontent>`

[`<selectedcontent>`](https://html.spec.whatwg.org/multipage/form-Elements.html#the-selectedcontent-Elements)

# 交互

## `<details>`

**折叠组件** [`<details>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/details) 可创建一个折叠组件，仅在被切换成展开状态时，它才会显示内含的信息。`<summary>` 元素可为该部件提供概要或者标签。

```html
<details>
  <summary>古埃及</summary>
  <p>
    <a href="https://zh.wikipedia.org/wiki/早王朝時期_(埃及)">早王朝时期</a> 前3150年–前2686年
  </p>
  <p>
    <a href="https://zh.wikipedia.org/wiki/古王国时期">古王国时期</a> 前2686年–前2181年
  </p>
  <p>
    <a href="https://zh.wikipedia.org/wiki/第一中间时期">第一中间时期</a> 前2181年–前2055年
  </p>
  <p>更多...</p>
</details>
```

> <details>
> <summary>古埃及</summary>
> <p>
> <a href="https://zh.wikipedia.org/wiki/早王朝時期_(埃及)">早王朝时期</a> 前3150年–前2686年
> </p>
> <p>
> <a href="https://zh.wikipedia.org/wiki/古王国时期">古王国时期</a> 前2686年–前2181年
> </p>
> <p>
> <a href="https://zh.wikipedia.org/wiki/第一中间时期">第一中间时期</a> 前2181年–前2055年
> </p>
> <p>更多...</p>
> </details>

## `<summary>`

**折叠摘要** [`<summary>`](https://html.spec.whatwg.org/multipage/interactive-Elements.html#the-summary-Elements) 元素用于

## `<dialog>`

**对话框** [`<dialog>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/dialog) 元素用于

# 脚本

## `<script>`

**脚本** [`<script>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/script) 用于嵌入可执行代码或数据，通常用作嵌入或者引用 JavaScript 代码。

## `<noscript>`

**无脚本** [`<noscript>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/noscript) 定义了在页面上的脚本类型不支持或浏览器当前关闭脚本时插入的 HTML 部分。

## `<template>`

**内容模板** [`<template>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/template) 是一种用于保存客户端内容机制，该内容在加载页面时不会呈现，但随后可以 (原文为 may be) 在运行时使用 JavaScript 实例化。

## `<slot>`

**插槽** [`<slot>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/slot) 是一个在 web 组件内部的占位符，你可以使用自己的标记来填充该占位符，从而创建单独的 DOM 树并将其一起呈现。

## `<canvas>`

**画布** [`<canvas>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements/canvas) 元素可被用来通过 JavaScript（[Canvas](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API) API 或 [WebGL](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API) API）绘制图形及图形动画。