> HTML 属性基础：`HTML 语法 | HTML 元素 | 元素属性`
>
> [WHATWG 属性参考](https://html.spec.whatwg.org/multipage/indices.html#attributes-3 "WHATWG 属性参考")
>
> [MDN 属性参考](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Reference/Attributes "MDN HTML 属性参考")

# HTML 属性未分类

## [标识 `id` ](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/id)

- **语法**

    - `id` 属性用于为元素指定唯一的标识符。
    - 每个 HTML 文档中的 `id` 属性值必须是唯一的，不同元素之间不能有相同的 `id` 值。

- **命名规则**

    - 必须以字母（a-z，A-Z）开头。
    - 可以包含字母、数字（0-9）、连字符（-）、下划线（_）和句点（.）。
    - 区分大小写。
    - 不应包含空格和其他特殊字符。

- **应用**

    - 在 CSS 中通过 `#id` 方法，访问和操作元素。
    - 在 JS中 通过 `document.getElementById` 方法，访问和操作元素。

## [类名 `class`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/class)

- **定义**：`class` 属性用于为多个具有相似特征的一组元素定义类名。
- **语法**：`class="类名1 类名2 ..."`

    ```html
    <p class="example">example</p>
    <p class="example1 example2">example</p>
    ```

    ```css
    .example {
      color: red;
    }
    
    .example1 {
      color: blue;
    }
    
    .example2 {
      background-color: green;
    }
    ```

    ![image-20241205184715619](assets/image-20241205184715619.png)

- **说明**

    - 一个元素拥有多个类名，即可接受多个类选择器的样式

- **应用**

    - 在 CSS 中通过类选择器 `.类名`，访问和操作元素。
    - 在 JS 中通过 DOM 方法 `getElementsByClassName`，访问和操作元素。

## [样式 `style`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/style)

- `style` 属性用于为 HTML 元素添加样式，详见 **[`CSS` - `css 来源`](../css/css.md#CSS 来源)**。
- 关于 `style` 属性最后一个声明结尾 `;` 的说明

    - 保留最后一个分号更规范，而且不易出错
    - 因为代码格式化工具 `Prettier` 会将结尾 `;` 自动格式化删掉，所以暂时保持结尾没有 `;` 的写法。

        ```html
        <!-- 结尾有分号更规范 -->
        <img src="assets/测试.png" alt="测试" style="width: auto; height: 400px;" />
        
        <!-- Prettier 会格式化删掉结尾分号 -->
        <img src="assets/测试.png" alt="测试" style="width: auto; height: 400px" />
        ```

## 路径 `src`

- **语法**：用于指定脚本文件引用的外部资源的路径。可以是本地路径，也可以是网络上的 URL。
- 通常用于元素，如 `<img>`、`<script>`、`<audio>`、`<video>` 等。

    ```html
    <img src="path/to/image.jpg" alt="Description">
    ```

## 链接 `href`

- **语法**：`href`（超文本引用）是用于指定超链接。
- 通常用于 `<a>`、`<link>` 和 `<area>` 元素，一般用于链接资源文件，比如样式表。

    ```html
    <a href="https://www.example.com">点击这里</a>
    ```

- 跳转目标可以是绝对路径、相对路径、锚点、电话号、E-mail、JS 代码和文件等。

- **<span id="anchor">锚点</span>**：锚点元素添加属性 `id="锚点"`，跳转元素在 URL/SRC 后添加 `#锚点`（同一地址可省略 URL/SRC）

    ```html
    <div id="example">百度</div>
    
    <a href="#example">点击跳转至百度</a>
    ```

## [跳转方式 `target`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#target)

- 属性 `target` 用于指定链接的 *打开方式* 或者指定提交表单时的 *目标窗口*。通常用于 `<a>` 和 `<form>`。

- **语法**：`<a target="_blank"></a>`

    ```html
    <a href="https://www.example.com" target="_blank">Visit Example.com</a>
    ```

- **属性值**

    - **`_self`**：默认值，在当前窗口中打开。
    - **`_blank`**：在新窗口或新标签页中打开。
    - **`_parent`**：在父级框架中打开。
    - **`_top`**：在顶级窗口中打开。

## 替代文本 `alt`

- **语法**：用于描述图像的内容或作用。

    - 如果图像无法加载，`alt` 属性的文本将被显示。

    - 屏幕阅读器等辅助技术可以读取 `alt` 文本，以提供对图像的描述，帮助视觉障碍用户理解图像内容。

        ```html
        <img src="example.jpg" alt="一个展示示例的图像">
        ```

## [宽度 `width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width)

- **语法**：`width` 和 `height` 属性是 HTML 中用于指定元素宽度和高度的属性。
- **属性值单位**：可以是像素 `px`、百分比 `%`、视口 `vw/vh`、`em`、`rem` 和绝对长度单位（如mm）等，详见 `CSS` - `值和单位`。
- **自适应**：通常情况下，如果只设置 `width: 200px;`，而没有设置 `height`，浏览器将根据图像的纵横比自动计算 `height`。

## 悬停提示 `title`

- **语法**：当用户将鼠标悬停在带有 `title` 属性的元素上时，浏览器会显示该属性的值。

    ```html
    <!-- 用于锚元素 -->
    <a href="https://www.baidu.com/" title="点击跳转至百度">百度</a>
    
    <!-- 用于其它元素 -->
    <span title="公元前">AD</span>
    ```

- **渲染效果**

    > <a href="https://www.baidu.com/" title="点击跳转至百度">百度</a>
    >
    > <span title="公元前">AD</span>

## 禁用 `disabled`

- **语法**：禁用用户与某个元素进行交互。

    ```html
    <input type="text" disabled>
    ```
