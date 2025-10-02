# [HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML)

**超文本标记语言**（**H**yper **T**ext **M**arkup **L**anguage，简称 HTML），是一种用来定义 Web 网页**结构**和**语义**的**标记语言**；HTML 文件的扩展名为 `.html`。

## HTML 主要资源

**HTML 参考**：

> <details>
>   <summary>
>     <a
>       href="https://html.spec.whatwg.org/multipage/indices.html#index"
>       alt="WHATWG 参考"
>       >WHATWG 参考</a
>     >：官方参考
>   </summary>
>   <ul>
>     <li>
>       <a
>         href="https://html.spec.whatwg.org/multipage/indices.html#elements-3"
>         alt="HTML 元素参考"
>         >HTML 元素参考</a
>       >：所有 HTML 元素的表格
>     </li>
>     <li>
>       <a
>         href="https://html.spec.whatwg.org/multipage/indices.html#attributes-3"
>         alt="HTML 属性参考"
>         >HTML 属性参考</a
>       >：所有 HTML 属性的表格（不包括事件处理程序内容属性）
>     </li>
>   </ul>
> </details>
> <details>
>   <summary>
>     <a
>       href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference"
>       alt="MDN 参考"
>       title="MDN 参考"
>       >MDN 参考</a
>     >：MDN 对 WHATWG 参考的解释
>   </summary>
>   <ul>
>     <li>
>       <a
>         href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements"
>         alt="HTML 元素参考"
>         >HTML 元素参考</a
>       >：所有 HTML 元素详解
>     </li>
>     <li>
>       <a
>         href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Attributes"
>         alt="HTML 属性参考"
>         >HTML 属性参考</a
>       >：所有 HTML 属性详解
>     </li>
>   </ul>
> </details>

**其它资源**：

> <details>
>   <summary>
>     <a
>       href="https://developer.mozilla.org/zh-CN/docs/Web/HTML"
>       alt="MDN HTML"
>       title="MDN HTML"
>       >MDN HTML</a
>     >：MDN 关于 HTML 的主页面
>   </summary>
>   <ul>
>     <li>
>       <a
>         href="https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/HTML_basics"
>         alt="HTML 基础"
>         >HTML 基础</a
>       >：了解 HTML 的含义和最基本用法
>     </li>
>     <li>
>       <a
>         href="https://developer.mozilla.org/zh-CN/docs/Learn/HTML"
>         alt="HTML 学习区"
>         >HTML 学习区</a
>       >：学习 HTML 基础知识
>     </li>
>     <li>
>       <details>
>         <summary>
>           <a href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference"
>             >HTML 参考</a
>           >：MDN 对 WHATWG 官方文档的解释
>         </summary>
>         <ul>
>           <li>
>             <a
>               href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Elements"
>               alt="HTML 元素参考"
>               >HTML 元素参考</a
>             >：所有 HTML 元素详解
>           </li>
>           <li>
>             <a
>               href="https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Attributes"
>               alt="HTML 属性参考"
>               >HTML 属性参考</a
>             >：所有 HTML 属性详解
>           </li>
>         </ul>
>       </details>
>     </li>
>   </ul>
> </details>

**[WHATWG](https://html.spec.whatwg.org/)  中 HTML 官方文档不同版本的含义**：

- **[单页版](https://html.spec.whatwg.org/)**：单页显示。

- **[多页版](https://html.spec.whatwg.org/multipage/)**：分多个页面显示，自己默认使用该版。

- **[开发者版](https://html.spec.whatwg.org/dev/)**：与多页版相比，此版删除了只有浏览器供应商才需要知道的信息。
- **[官方中文版1](https://whatwg-cn.github.io/html/)**：单页显示。
- **[官方中文版2](https://htmlspecs.com/)**：单页显示。

## [HTML 注释](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Guides/Comments)

- 单行注释：`Ctrl + / `，多行注释：`Ctrl + Shift + /`

    ```html
    <div>
      <!-- 这是一个单行注释 -->
      <h1>Hello, World!</h1>
        
      <!--
      多行注释第一行
      多行注释第二行
      多行注释第三行
      -->
      <h1>Hello, World!</h1>
    </div>
    ```

## [实体](https://developer.mozilla.org/zh-CN/docs/Glossary/Entity)

- **HTML 实体**（也叫 `字符引用`）：是一段以符号 `&` 开始，以 `;` 结束的文本（字符串）。
- 在 HTML 中，某些特殊字符是 HTML 语法自身的一部分，如果想将这些字符包含进文本中，必须使用 `HTML 实体`。
- 每个 HTML 实体以符号 `&` 开始，以 `;` 结束。

    |   原义字符   | HTML 实体         |
    | :----------: | ----------------- |
    |      <       | `&lt;`            |
    |      >       | `&gt;`            |
    |      "       | `&quot;`          |
    |      '       | `&apos;`          |
    |      &       | `&amp;`           |
    |     空格     | `&nbsp;`          |
    | ............ | ................. |

- **示例**

    ```html
    <!-- 错误写法 -->
    <p>HTML 中用 <p> 来定义段落元素。</p>
    
    <!-- 正确写法 -->
    <p>HTML 中用 &lt;p&gt; 来定义段落元素</p>
    ```

# [HTML 元素](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Getting_started/Your_first_website/Creating_the_content#html_元素详解)

HTML 由一系列的元素组成，这些元素可以用来包围不同部分的内容，使其以某种方式呈现或者工作。目前符合要求的[元素](https://html.spec.whatwg.org/multipage/indices.html#elements-3)共计115个。

本章节讲解 HTML 元素的基础，关于各元素的具体情况，详见 `html-elements 笔记`。

## [元素结构](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax#%E5%89%96%E6%9E%90%E4%B8%80%E4%B8%AA_html_%E5%85%83%E7%B4%A0)

![image-20231205005652176](assets/image-20231205005652176.png)

**元素的主要部分有**：

- **开始标签**（Opening tag）：`<元素名称>` （本例为 `<p>`），表示元素从这里开始起作用。
- **结束标签**（Closing tag）：`</元素名称>` （本例为 `</p>`），表示元素的结尾。
- **元素内容**（Content）：元素的内容，本例为 `My cat is veru grumpy`。
- **元素**（Element）：开始标签、结束标签与内容相结合，便是一个完整的元素。

## [元素属性](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax#%E5%B1%9E%E6%80%A7)

![image-20231205010242559](assets/image-20231205010242559.png)

- **有值的属性（Attribute）应包含**：

    -  **空格符**：在属性与元素名称（或上一个属性，如果有超过一个属性的话）之间的空格。
    -  **属性名称**，并接等号，本例为 `class`。
    -  **属性值**：由双（单）引号所包围，本例为 `editor-note`。

- **说明**
    - 属性一般存在于开始标签。
    - 一个元素可以有多个属性，每个属性之间用 `空格` 分隔。
    - 一个属性可以有多个属性值，每个属性值之间用 `空格` 分隔。
    - 属性和属性值对大小写不敏感，但新版本的 (X)HTML 要求使用小写属性。
    - 不包含 [ASCII](https://developer.mozilla.org/zh-CN/docs/Glossary/ASCII) 空格（以及 `"`、`'`、`=`、`<`、`>`）的简单属性值可以不使用引号，但是建议将所有属性值用引号括起来，这样的代码一致性更佳，更易于阅读。

## 嵌套元素

元素可以嵌套符合条件的另一个元素。

```html
<p>My cat is <strong>very</strong> grumpy.</p>
```

## [空元素](https://developer.mozilla.org/zh-CN/docs/Glossary/Void_element)

**空元素**，也称**自闭合标签**，只有开始标签，没有结束标。

```html
<img src="images/firefox-icon.png" alt="My test image" />
```

关于空元素**自闭合**的说明，以 `<img>` 为例：

- 在 HTML5 中，`<img>` 是空元素，**不需要**自闭合标签。这是现代 HTML 的标准写法，简洁且符合规范。
- 在 XHTML 中要求所有标签必须闭合，但 XHTML 已逐渐被 HTML5 取代。
- 因为代码格式化工具 `Prettier` 会将 `<img>` 自动格式化为 `<img />` ，所以暂时保持为 `<img />` 写法。
- 所有空元素同理。

# 文档结构

## [文档类型](https://developer.mozilla.org/zh-CN/docs/Glossary/Doctype)

在 [HTML](https://developer.mozilla.org/zh-CN/docs/Glossary/HTML) 中，**文档类型声明**是必要的。在所有文档的头部，你都将会看到“`<!DOCTYPE html>`”序言。这个声明的目的是防止浏览器在渲染文档时，切换到我们称为[“怪异模式”](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Guides/Quirks_mode_and_standards_mode)的渲染模式。“`<!DOCTYPE html>`”确保浏览器按照最佳的相关规范进行渲染，而不是使用一个不符合规范的渲染模式。

## [文档结构](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/HTML_basics#html_文档详解)

- **文档结构**

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Document</title>
      </head>
      <body>
    
      </body>
    </html>
    ```

- **基本结构包含：**

    1. [**文档类型**](#[文档类型](https://developer.mozilla.org/zh-CN/docs/Glossary/Doctype))：`<!DOCTYPE html>`
    2. [**根元素**](#[根元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/html))：`<html>`

    3. [**元数据分区**](#[元数据分区](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element#文档元数据))：`<head>`
    4. [**内容分区**](#[内容分区 `<body>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/body))：`<body>`

- VS Code 快速创建文档结构：`!`

# 标记

## 标记消歧义

标记类的元素一般在渲染时，呈现特殊格式，以突出显示，不能为了某种视觉效果而滥用该类元素。

- **粗体**

    - `<strong>` 用来对一个句子的部分**文本**增加重要性
    - `<b>` 用来引起人们的注意，如关键词、评论中的产品名称、交互式文本驱动软件中的可操作词或文章导语。

- **斜体**

    - `<em>` 表示语气上的强调
    - `<i>` 用于技术术语、音译、思想或船名等
    - `<dfn>` 表示定义中的术语
    - `<cite>` 用于引用作品

- **删除线**

    - `<del>` 属于编辑标识，表示被从文档中删除的内容。
    - `<s>` 表示不再准确或不再相关的内容，不适用于指示文档编辑。

- **下划线**

    -  `<del>` 属于编辑标识，表示已经被插入文档中的文本。
    -  `<u>` 表示非文本注释，例如拼写错误和中文专有名词。

- **高亮**：`<mark>` 表示上下文相关或突出显示以供参考



