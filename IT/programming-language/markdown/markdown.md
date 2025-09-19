# 基础

## 简介

Markdown 是一种轻量级的标记语言，可用于在纯文本文档中添加格式化元素。Markdown 由 John Gruber 于 2004 年创建，如今已成为世界上最受欢迎的标记语言之一。

一些有用的技术文档：

- [John Gruber 的 Markdown 文档](https://daringfireball.net/projects/markdown/)。Markdown的创建者编写的原始指南。
- [Markdown 中文网](https://markdown.p2hp.com/index.html)
- [Markdown 中文教程](https://markdown.com.cn/basic-syntax/)
- [一个很好的 Markdown 项目](https://github.com/mundimark/awesome-markdown/tree/master)

## 速查表

<table style="text-align: left;">
  <tr>
    <th>元素</th>
    <th>Markdown语法</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>标题（Heading）</td>
    <td>
      # H1<br>
      ## H2<br>
      ### H3<br>
    </td>
    <td>
      <h1>
      一级标题
      </h1>
    </td>
  </tr>
  <tr>
    <td>段落（paragraph）</td>
    <td>
      <p>这是第一段，下面有一个空行。</p>
      <p>这是第二段，上面有一个空行。</p>
    </td>
    <td>
      <p>这是第一段，下面有一个空行。</p>
      <p>这是第二段，上面有一个空行。</p>
    </td>
  </tr>
  <tr>
    <td>换行</td>
    <td>这是第一行&lt;br&gt;这是第二行</td>
    <td>这是第一行<br>这是第二行</td>
  </tr>
  <tr>
    <td>粗体（Bold）</td>
    <td>**粗体**</td>
    <td><strong>粗体</strong></td>
  </tr>
  <tr>
    <td>斜体（Italic）</td>
    <td>*斜体*</td>
    <td><em>斜体</em></td>
  </tr>
  <tr>
    <td>删除线</td>
    <td>~~删除~~</td>
    <td><del>删除</del></td>
  </tr>
  <tr>
    <td>有序列表（Ordered List）</td>
    <td>
      1. 第一列表项<br>
      2. 第二列表项<br>
      3. 第三列表项
    </td>
    <td>
      <ol>
        <li>第一列表项</li>
        <li>第二列表项</li>
        <li>第三列表项</li>
      </ol>
    </td>
  </tr>
  <tr>
    <td>无序列表（Unordered List）</td>
    <td style="text-align:left">
      - 第一列表项<br>
      - 第二列表项<br>
      - 第三列表项
    </td>
    <td style="text-align:left">
      <ul>
        <li>第一列表项</li>
        <li>第二列表项</li>
        <li>第三列表项</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>行内代码</td>
    <td>`code`</td>
    <td><code>code</code></td>
  </tr>
  <tr>
    <td>围栏代码块</td>
    <td>
      ```json<br>
      {<br>
      &nbsp;&nbsp;"firstName": "John",<br>
      &nbsp;&nbsp;"lastName": "Smith",<br>
      &nbsp;&nbsp;"age": 25<br>
      }<br>
      ```
    </td>
    <td>此处不展示</td>
  </tr>
  <tr>
    <td>图片（Image）</td>
    <td>![Linux](/assets/Linux.png)</td>
    <td>此处不展示</td>
  </tr>
  <tr>
    <td>链接（Link）</td>
    <td>[title](https://www.example.com)</td>
    <td><a href="https://www.example.com">title</a></td>
  </tr>
  <tr>
    <td>引用块（Blockquote）</td>
    <td>&gt; blockquote</td>
    <td>此处不展示</td>
  </tr>
</table>

## 内嵌 HTML 标签

- 在 Markdown 中可以直接使用 HTML 标签。
- 并非所有 Markdown 应用程序都支持在 Markdown 文档中添加 HTML。
- 无法在 HTML 块级标签内使用 Markdown 语法。
- 块级 HTML 元素（例如`<div>`、、、 等）必须用空行与周围内容分隔，并且块的开始和结束标记不应使用制表符或空格缩进。

## 转义字符

- **普通字符**：使用反斜杠 \ 进行转义。

    ```
    \   backslash
    `   backtick
    *   asterisk
    _   underscore
    {}  curly braces
    []  square brackets
    ()  parentheses
    #   hash mark
    +   plus sign
    -   minus sign (hyphen)
    .   dot
    !   exclamation mark
    ```

- **特殊字符**：`<` 和 `&` 等字符，**无需**转换成 **HTML 实体**，Markdown 会自动转换。

## 扩展语法

John Gruber 的原始设计文档中概述的基本语法主要是为了应付大多数情况下的日常所需元素，但对于某些人来说还不够，开始通过添加其他元素（例如表，代码块，语法突出显示，URL 自动链接和脚注）来扩展基本语法。可以通过使用基于基本 Markdown 语法的轻量级标记语言，或通过向兼容的 Markdown 处理器添加扩展来启用这些元素。

**注意**：并非所有 Markdown 应用程序都支持扩展语法元素。如果不支持，那么可以在 Markdown 处理器中启用扩展。

## 注释

Markdown 原生语法没有官方标准的注释功能，但可以使用 HTML 实现注释效果。

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

# 标题

**语法**：不同数量的 `#`可以完成不同级别的标题，`#` 和标题内容之间留一个空格。 

<table style="text-align: center;">
  <tr>
    <th>Markdown语法</th>
    <th>HTML</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>#&nbsp;一级标题</td>
    <td>&lt;h1&gt;一级标题&lt;/h1&gt;</td>
    <td>
      <h1>
      一级标题
      </h1>
    </td>
  </tr>
  <tr>
    <td>##&nbsp;二级标题</td>
    <td>&lt;h2&gt;二级标题&lt;/h2&gt;</td>
    <td>
      <h2>
      二级标题
      </h2>
    </td>
  </tr>
  <tr>
    <td>###&nbsp;三级标题</td>
    <td>&lt;h3&gt;三级标题&lt;/h3&gt;</td>
    <td>
      <h3>
      三级标题
      </h3>
    </td>
  </tr>
</table>

# 段落

**段落**只是一行或多行连续的文本，由一个或多个空行分隔。（空行是任何看起来像空行的行 — 只包含空格或制表符的行被视为空白。）普通段落不应使用空格或制表符缩进。

- **语法**：使用 `空白行` 将一行或多行文本进行分隔。

    <table style="text-align: center;">
      <tr>
        <th>Markdown语法</th>
        <th>HTML</th>
        <th>预览效果</th>
      </tr>
      <tr>
        <td>
          <p>这是第一段，下面有一个空行。</p>
          <p>这是第二段，上面有一个空行。</p>
        </td>
        <td>
          <p>&lt;p&gt;这是第一段，下面有一个空行。&lt;/p&gt;</p>
          <p>&lt;p&gt;这是第二段，上面有一个空行。&lt;/p&gt;</p>
        </td>
        <td>
          <p>这是第一段，下面有一个空行。</p>
          <p>这是第二段，上面有一个空行。</p>
        </td>
      </tr>
    </table>

- **注意**

    - 不要用空格 (Spaces)或制表符 (Tab) 缩进段落。
    - 要始终保持文本左对齐。

# 换行

## 换行

- **语法**：使用 <kbd>Space</kbd><kbd>Space</kbd><kbd>Enter</kbd> 在一个段落内创建换行。

    <table style="text-align: center;">
      <tr>
        <th>Markdown语法</th>
        <th>HTML</th>
        <th>预览效果</th>
      </tr>
      <tr>
        <td style="text-align: left">这是第一行<kbd>Space</kbd><kbd>Space</kbd><kbd>Enter</kbd><br>
          这是第二行
        </td>
        <td>
          <p>&lt;p&gt;这是第一行&lt;br&gt;这是第二行&lt;/p&gt;</p>
        </td>
        <td>这是第一行<br>这是第二行</td>
      </tr>
    </table>

- **说明**：**同一个段落内**，不要使用 <kbd>Enter</kbd> 换行，这仅仅会添加**单换行符**。

## 单换行符

- **单换行符**：文本中每一行结束时按一次 <kbd>Enter</kbd>，在代码或文本编辑中用来分隔内容的一种方式。
- 不要使用单换行符进行换行。
- **语法**：同一个段落内使用单换行符，渲染时不会真的分成两行，而是在换行符处表现为一个空格。
- **源码模式**

    ```markdown
    这是第一行
    这是第二行
    ```

- **渲染效果**

    > 这是第一行
    > 这是第二行

# 强调

## 粗体

**创建粗体**：在文本前后各加两个星号 `**` 。

<table style="text-align: center;">
  <tr>
    <th>Markdown语法</th>
    <th>HTML</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>**这是一段粗体文本**</td>
    <td>&lt;strong&gt;这是一段粗体文本&lt;/strong&gt;</td>
    <td><strong>这是一段粗体文本</strong></td>
  </tr>
</table>

## 斜体

**创建斜体**：在文本前后各加一个星号 `*` 。

<table style="text-align: center;">
  <tr>
    <th>Markdown语法</th>
    <th>HTML</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>*这是一段斜体文本*</td>
    <td>&lt;em&gt;这是一段斜体文本&lt;/em&gt;</td>
    <td><em>这是一段斜体文本</em></td>
  </tr>
</table>

## 删除线

- 删除线是 Markdown 的扩展语法。
- **创建删除线**：在文本前后各加两个波浪号 `~~` 。

    <table style="text-align: center;">
      <tr>
        <th>Markdown语法</th>
        <th>HTML</th>
        <th>预览效果</th>
      </tr>
      <tr>
        <td>~~这是一段删除文本~~</td>
        <td>&lt;del&gt;这是一段删除文本&lt;/del&gt;</td>
        <td><del>这是一段删除文本</del></td>
      </tr>
    </table>

## 嵌套

粗体和斜体可以相互嵌套

# 列表

## 有序列表

- **语法**：在每个列表项前添加**数字**并紧跟一个**英文句点**，然后空格。

    <table style="text-align: center;">
      <tr>
        <th>Markdown语法</th>
        <th>HTML</th>
        <th>预览效果</th>
      </tr>
      <tr>
        <td>
          1. 第一个有序列表<br>
          2. 第二个有序列表<br>
          3. 第三个有序列表
        </td>
        <td style="text-align:left">
          &lt;ol&gt;<br>
          &nbsp;&nbsp;&lt;li&gt;第一个有序列表&lt;/li&gt;<br>
          &nbsp;&nbsp;&lt;li&gt;第二个有序列表&lt;/li&gt;<br>
          &nbsp;&nbsp;&lt;li&gt;第三个有序列表&lt;/li&gt;<br>
          &lt;/ol&gt;
        </td>
        <td style="text-align:left">
          <ol>
            <li>第一个有序列表</li>
            <li>第二个有序列表</li>
            <li>第三个有序列表</li>
          </ol>
        </td>
      </tr>
    </table>

## 无序列表

**创建无序列表**：在每个列表项前添加**减号**并紧跟一个**英文句点**，然后空格。

<table style="text-align: center;">
  <tr>
    <th>Markdown语法</th>
    <th>HTML</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>
      - 第一个无序列表<br>
      - 第二个无序列表<br>
      - 第三个无序列表
    </td>
    <td style="text-align:left">
      &lt;ul&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;第一个无序列表&lt;/li&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;第二个无序列表&lt;/li&gt;<br>
      &nbsp;&nbsp;&lt;li&gt;第三个无序列表&lt;/li&gt;<br>
      &lt;/ul&gt;
    </td>
    <td style="text-align:left">
      <ul>
        <li>第一个无序列表</li>
        <li>第二个无序列表</li>
        <li>第三个无序列表</li>
      </ul>
    </td>
  </tr>
</table>

## 列表说明

- 可以随意写列表编号，但不会影响 Markdown 生成的 HTML 输出。
- **缩进**：列表项内的文字，有无缩进都可以

    ```markdown
    - Lorem ipsum dolor sit amet, consectetuer adipiscing elit.  
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,  
    viverra nec, fringilla in, laoreet vitae, risus.

    - Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
        Suspendisse id sem consectetuer libero luctus adipiscing.
    ```

- **项间空行**：项间有空行时，渲染的行间距增加

    - **无空行**

        ```markdown
        - 第一列表项
        - 第二列表项
        - 第三列表项
        ```

        ```html
        <ul>
          <li>第一列表项</li>
          <li>第二列表项</li>
          <li>第三列表项</li>
        </ul>
        ```

    - **有空行**

        ```markdown
        - 第一列表项
        
        - 第二列表项
        
        - 第三列表项
        ```

        ```html
        <ul>
          <li><p>第一列表项</p></li>
          <li><p>第二列表项</p></li>
          <li><p>第三列表项</p></li>
        </ul>
        ```

## 列表嵌套

- 在嵌套一种元素时，为了**保证列表连续性**，应保证以下两点：

    - 嵌套元素独占一个段落，即**上下各空一行**。
    - 嵌套元素缩进 `四个空格`（或一个制表符）。

- 嵌套元素独占一个段落的影响

    - 如果独占一个段落，其它列表项行间距会增加。
    - 如果不独占一个段落，渲染可能异常。

### 嵌套列表

- **语法**

    ```markdown
    - 第一个列表项
    - 第二个列表项

        - 第一个嵌套列表项
        - 第二个嵌套列表项

    - 第三个列表项
    - 第四个列表项
    ```

- **渲染效果**

    > - 第一个列表项
    > - 第二个列表项
    >
    >     - 第一个嵌套列表项
    >     - 第二个嵌套列表项
    >
    > - 第三个列表项
    > - 第四个列表项

### 嵌套段落

- **语法**

    ```markdown
    - 第一个列表项
    - 第二个列表项

        第一个嵌套段落

        第二个嵌套段落

    - 第三个列表项
    - 第四个列表项
    ```

- **渲染效果**

    > - 第一个列表项
    > - 第二个列表项
    >
    > 	  第一个嵌套段落
    >
    > 	  第二个嵌套段落
    >
    > - 第三个列表项
    > - 第四个列表项

### 嵌套引用块

- **语法**

    ```markdown
    - 第一个列表项
    - 第二个列表项

        > 嵌套引用块

    - 第三个列表项
    - 第四个列表项
    ```

- **渲染效果**

    > - 第一个列表项
    > - 第二个列表项
    > 
    > 	  > 嵌套引用块
    > 	
    > - 第三个列表项
    > - 第四个列表项

### 嵌套图片

- **语法**

    ```markdown
    - 第一个列表项
    - 第二个列表项

        ![Linux](/assets/Linux.png)

    - 第三个列表项
    - 第四个列表项
    ```

- **渲染效果**

    > - 第一个列表项
    > - 第二个列表项
    >
    >     ![Linux](/assets/Linux.png)
    >
    > - 第三个列表项
    > - 第四个列表项

### 嵌套围栏代码块

- **语法**

    ````markdown
    - 第一列表项
    - 第二列表项
    
        ```markdown
        这是一个**围栏代码块**
        ```
    
    - 第三列表项
    - 第四列表项
    ````

# 代码

## 行内代码

要想让行内代码不被渲染，可以将其包裹在一个或多个反引号 (<code>`</code>) 中。

<table style="text-align: center;">
  <tr>
    <th>Markdown语法</th>
    <th>HTML</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>请输入行内代码 `none`</td>
    <td>&lt;code&gt;none&lt;/code&gt;</td>
    <td>请输入行内代码 <code>none</code></td>
  </tr>
</table>

## 转义反引号

如果行内代码中包含**一个或多个反引号**，则将行内代码包裹在双反引号（<code>``</code>）中。

<table style="text-align: center;">
  <tr>
    <th>Markdown语法</th>
    <th>HTML</th>
    <th>预览效果</th>
  </tr>
  <tr>
    <td>``请将 `none` 输入到文本框``</td>
    <td>请将 &lt;code&gt;`none`&lt;/code&gt; 输入到文本框</td>
    <td>请将 <code>`none`</code> 输入到文本框</td>
  </tr>
</table>

## 围栏代码块

- **语法**：在代码块之前和之后的行上使用**三个反引号** (<code>```</code>）。  
如果在前面的反引号后加上**语言名称**，即可实现**语法高亮**。

    ````markdown
    ```json
    {
    "firstName": "John",
    "lastName": "Smith",
    "age": 25
    }
    ```
    ````

- **渲染效果**

    ```json
    {
    "firstName": "John",
    "lastName": "Smith",
    "age": 25
    }
    ```

# 链接

Markdown 支持两种样式的链接：*内联*和*引用*。都支持创建超链接和图片。

- **内联链接**：替代文本和链接地址在一起，`[alt](SRC/URL)`
- **引用链接**：链接地址放在别处。

## 超链接

### 内联超链接

- **语法**：**链接文本**放在方括号内，**链接地址**放在后面的圆括号中。

    - **Markdown 格式**：`[超链接显示名](超链接地址)`

        ```markdown
        <!-- 标准链接 -->
        这是一个标准链接 [Markdown语法](https://markdown.com.cn)。
        
        <!-- 悬停带解释的链接 -->
        这是一个悬停带注释的链接 [Markdown语法](https://markdown.com.cn "关于链接的解释")。
        ```

    - **HTML 格式**：`<a href="超链接地址">超链接显示名</a>`

        ```html
        <!-- 标准链接 -->
        这是一个链接 <a href="https://markdown.com.cn">Markdown语法</a>。
        
        <!-- 悬停带解释的链接 -->
        这是一个悬停带注释的链接 <a href="https://markdown.com.cn" title="关于链接的解释">Markdown语法</a>。
        ```

- **渲染效果**

    > 这是一个链接 [Markdown语法](https://markdown.com.cn)。
    >
    > 这是一个悬停带注释的链接 [Markdown语法](https://markdown.com.cn "关于链接的解释")。

### 自动超链接

- **语法**：使用**尖括号**把 URL 或者 Email 地址变成可点击的链接。

    ```markdown
    <https://markdown.com.cn>

    <fake@example.com>
    ```

- **渲染效果**

    > <https://markdown.com.cn>
    > 
    > <fake@example.com>

## 图片

### 内联图片

- 由于 Markdown 文件是纯文本文件，因此不能直接在 Markdown 文件中插入图像数据，而是插入对图像文件的**引用**。
- **语法**：使用感叹号 (!) **开头**，然后在方括号 ([]) 增加**替代文本** (alt)，在圆括号里放**图片路径**。另有 `title` 可选。

    - **Markdown 格式**：`![alt](SRC/URL)`

        ```markdown
        ![Linux](/assets/Linux.png)
        ```

    - **HTML 格式**：`<img src="SRC/URL" alt="alt">`

        ```markdown
        <img src="/assets/Linux.png" alt="Linux">
        ```

- **渲染效果**

    ![Linux](assets/Linux.png)

### 内联图片超链接

- **语法**：请将**图像的 Markdown 语法整体**括在方括号中，然后将**链接**添加在圆括号中。

    ```markdown
    [![Linux](/assets/Linux.png)](https://markdown.com.cn)
    ```

- **渲染效果**

    [![Linux](assets/Linux.png)](https://markdown.com.cn)

## 引用链接

引用链接可以增加文章连续性和可读性。以超链接为例，图片同理。

- **语法**：`[alt][id]`

    ```markdown
    请访问 [John Gruber 的 Markdown 文档][John Gruber] 了解更多内容

    [John Gruber]: https://daringfireball.net/
    ```

- **渲染效果**

    > 请访问 [John Gruber 的 Markdown 文档][John Gruber] 了解更多内容
    >
    > [John Gruber]: https://daringfireball.net/

## 锚点

- 锚点属于 Markdown 的扩展语法。
- **使用标题自动生成锚点**

    - Markdown 中标题自带 `id`，`id` 值为 `标题名`
    - **语法**：`[跳转文本](#标题名)`

        ```markdown
        # 第一部分
        
        回到[顶部](#第一部分)
        ```

- **非标题锚点**：内嵌 HTML ，详见 [`HTML` > `锚点`](../frontend/html/html.md#anchor)

    ```markdown
    <span id="example">第一部分</span>

    [点击跳转至百度](#example)
    ```

- **跨文件锚点示例**

    ```markdown
    <span id="anchor">锚点</span>
    ```

    ```markdown
    详见 [`HTML` > `锚点`](../frontend/html/html.md#anchor)
    ```

    **在以上示例中**：

    1. 如果 `html.md` 文件事先处于关闭状态，要点击两次才能直达锚点。

# 分隔线

- **语法**：在**单独一个段落**（即前后都有空白行）使用三个或多个星号 (`***`)、破折号 (`---`) 或下划线 (`___`) ，并且不能包含其他内容。

    ```markdown
    ***

    ---

    _________________
    ```

- **以上三个分隔线的渲染效果如下：**

    ---

# 表格

- 表格属于 Markdown 的扩展语法。
- Markdown 格式无法完成**合并单元格**等其它复杂操作，所以尽量使用 **HTML** 的 `<table>`。

## 创建表格

- **语法**：使用三个或多个连字符（`---`）创建每列的标题，并使用管道（`|`）分隔每列。

    ```markdown
    | 表头  | 表头 |
    | ---- | ---- |
    | 内容  | 内容 |
    | 内容  | 内容 |
    ```

- **渲染效果**

    > | 表头 | 表头 |
    > | ---- | ---- |
    > | 内容 | 内容 |
    > | 内容 | 内容 |

## 对齐表格

- **语法**：通过在标题行中的连字符的左侧，右侧或两侧添加冒号（`:`），将列中的文本对齐到左侧，右侧或中心。

    ```markdown
    | 表头  | 表头  | 表头  |
    | :--- | :---: | ---: |
    | 内容  | 内容  | 内容  |
    | 内容  | 内容  | 内容  |
    ```

- **渲染效果**

    > | 表头 | 表头 | 表头 |
    > | :--- | :---: | ---: |
    > | 内容 | 内容 | 内容 |
    > | 内容 | 内容 | 内容 |

## 格式化表格

- **可以添加**：链接，行内代码和强调。
- **不可添加**：标题，块引用，列表，水平规则，图像或 HTML 标签。

## 管道字符

可以使用表格的 HTML 字符代码（`|`）在表中显示竖线（`|`）字符。

## 换行

如果想在表格中换行，应该使用 HTML 的换行元素 `<br>`。

## 提示词

这是让 AI 根据所给图片，自动生成 markdown 格式的表格的提示词：

- 改成 markdown 格式
- 所有单元格内容和管道符之间保留一个空格，不需要对齐管道符
- 第二行的格式为 `| :---: |`（注意只有三个-），以确保所有内容居中显示
- 最后以代码块形式给我 markdown 源码

    | 标题 | 标题 | 标题 |
    | :---: | :---: | :---: |
    | 内容 | 内容 | 内容 |

# 引用块

## 单个块引用

- **语法**：在段落前添加一个 `>` 符号，然后空格。

    ```markdown
    > 这是一个块引用。
    ```

- **渲染效果**

    > 这是一个块引用。

## 多个段落块引用

- **语法**：在**段落之间的空白行**添加一个 `>` 符号，然后空格。

    ```markdown
    > 这是块引用的第一个段落。
    > 
    > 这是块引用的第一个段落。
    ```

- **渲染效果**

    > 这是块引用的第一个段落。
    >
    > 这是块引用的第二个段落。

## 嵌套

### 嵌套块引用

- **语法**：在**要嵌套的段落前**添加一个 `>>` 符号，然后空格。

    ```markdown
    > 这是块引用的第一个段落。
    > 
    >> 这是嵌套的块引用。
    ```

- **渲染效果**

    > 这是块引用的第一个段落。
    >
    > > 这是嵌套的块引用。

### 嵌套其它元素

- **语法**：块引用可以包含其他 Markdown 格式的元素，并非所有元素都可以使用。

    ```markdown
    > #### 嵌套四级标题
    >
    > - 嵌套无序列表
    > - 嵌套无序列表
    >
    >  嵌套**粗体文本**和*斜体文本*
    ```

- **渲染效果**

    > #### 嵌套四级标题
    >
    > - 嵌套无序列表
    > - 嵌套无序列表
    >
    >  嵌套**粗体文本**和*斜体文本*

# 脚注

- 脚注属于 Markdown 的扩展语法。
- **语法**：在方括号（`[^1]`）内添加插入符号和标识符。

    ```markdown
    Here's a simple footnote,[^1] and here's a longer one.[^bignote]

    [^1]: This is the first footnote.

    [^bignote]: Here's one with multiple paragraphs and code.
    ```

- **渲染效果**

    > Here's a simple footnote,[^1] and here's a longer one.[^bignote]
    >
    > [^1]: This is the first footnote.
    >
    > [^bignote]: Here's one with multiple paragraphs and code.

# 任务列表

- 任务列表属于 Markdown 的扩展语法。
- **语法**：在任务列表项之前添加**减号**和**方括号**，并在方括号前面加上**空格**。  
要选择一个复选框，请在方括号`[x]`之间添加 x 。

    ```markdown
    - [x] 工作列表1
    - [ ] 工作列表2
    - [ ] 工作列表3
    ```

- **渲染效果**

    > - [x] 工作列表1
    > - [ ] 工作列表2
    > - [ ] 工作列表3

# 定义列表

- 定义列表属于 Markdown 的扩展语法。
- 该列表的 Markdown 语法没有试验成功。
- **语法**：在第一行上键入术语。在下一行，键入一个冒号，后跟一个空格和定义。

    ```markdown
    First Term
    : This is the definition of the first term.

    Second Term
    : This is one definition of the second term.
    : This is another definition of the second term.
    ```

    ```html
    <dl>
    <dt>First Term</dt>
    <dd>This is the definition of the first term.</dd>
    <dt>Second Term</dt>
    <dd>This is one definition of the second term. </dd>
    <dd>This is another definition of the second term.</dd>
    </dl>
    ```

- **渲染效果**

    > <dl>
    >     <dt>First Term</dt>
    >     <dd>This is the definition of the first term.</dd>
    >     <dt>Second Term</dt>
    >     <dd>This is one definition of the second term. </dd>
    >     <dd>This is another definition of the second term.</dd>
    > </dl>

# Emoji 表情

- Emoji 表情属于 Markdown 的扩展语法。
- [表情符号简码列表](https://gist.github.com/rxaviers/7360908)
- **语法**：在**表情符号短代码**前后各加1个**冒号**。

    ```markdown
    真好笑！:joy:
    ```

- **渲染效果**

    > 真好笑！:joy:

# 其它

## 个人代码风格

- 缩进：

    - 每个缩进为，4个空格
    - 围栏代码块之内的换行，源码不需要空格，这是 Typora 系统缺陷，应手动删除

        ````markdown
        ```css
        .example {
          color: red;
        }
        <!-- 此行是为了提高代码可读性的空行。在源码模式下，行首不应该有空格 -->
        .example1 {
          color: blue;
        }
        ```
        ````
        
    - 每个不同项目之间的空行，不需要加空格，这是 Typora 系统缺陷，应手动删除

        ````markdown
        ```html
        <p class="example">example</p>
        ```
        <!-- 此行是为了提高代码可读性的空行。在源码模式下，行首不应该有空格 -->
        ```css
        .example {
          color: red;
        }
        ```
        ````
    
- 不同项目之间必须有整行空格

    - 比如图片和围栏代码块
    - 比如不同级别的列表

## 已整理完

- 历史、CSS、Markdown、HTML
