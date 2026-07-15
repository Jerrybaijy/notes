---
title: emmet
author: Jerry.Baijy
tags:
  - dev
  - software
  - code
  - ide-tools
---

# Overview

[**Emmet**](https://emmet.io/) 是一款用于提高 Web 开发效率的工具，它可以通过简短的缩写语法快速生成 HTML 和 CSS 代码片段。它最初由 Sergey Chikuyonok 开发，前身是 **Zen Coding**，后更名为 **Emmet**。如今，它已经成为许多主流编辑器（如 VS Code）的内置工具。

# Install

VS Code 内置

# 使用方法

- **使用**：`缩写 | Tap` 或 `缩写 | Enter`
- **基础语法规则**

  <!-- prettier-ignore -->
  | 符号 | 描述 | 示例 | 结果 |
  | :---: | :---: | :---: | :---: |
  | `>` | 子元素 | `div>p` | `<div><p></p></div>` |
  | `+` | 兄弟元素 | `div+p` | `<div></div><p></p>` |
  | `*` | 多个相同元素 | `div*2` | `<div></div><div></div>` |
  | `{}` | 文本内容 | `p{Hello}` | `<p>Hello</p>` |
  | `[]` | 添加属性 | `input[type="text"]` | `<input type="text">` |
  | `()` | 分组 | `div>(header+footer)` | `<div><header></header><footer></footer></div>` |


# 常用缩写

<!-- prettier-ignore -->
| 示例 | 描述 | 结果 |
| :---: | :---: | :---: |
| `!` | HTML5 文档结构 | 自动生成 HTML5 标准结构 |
| `HTML:5` | HTML5 文档结构 | 自动生成 HTML5 标准结构 |
| `div` | 元素 | `<div></div>` |
| `div*2` | 多个同级元素 | `<div></div><div></div>` |
| `ul>li*2` | 列表 | `<ul><li></li><li></li></ul>` |
| `input[type="text"]` | 带属性的元素 | `<input type="text">` |
| `div.class` | 带 `class` 属性的元素 | `<div class="class"></div>` |
| `div#id` | 带 `id` 属性的元素 | `<div id="id"></div>` |
| `div>p` | 子元素 | `<div><p></p></div>` |
| `div+p` | 兄弟元素 | `<div></div><p></p>` |
| `div>(p+p)` | 分组 | `<div><p></p><p></p></div>` |

# 缩写包围

```html
<div class="one">block</div>
<div class="two">block</div>
<div class="three">inline-block</div>
<div class="four">inline-block</div>
<div class="five">none</div>
```

```html
<div>
  <div class="one">block</div>
  <div class="two">block</div>
  <div class="three">inline-block</div>
  <div class="four">inline-block</div>
  <div class="five">none</div>
</div>
```

- 修改 Emmet 缩写包围快捷键
  - 按下 `Ctrl + Shift + P`（macOS：`Cmd + Shift + P`）打开命令面板。
  - 搜索并选择 `Emmet: Wrap with Abbreviation`。
  - 修改快捷键为 `Ctrl + Shift + A`，注意删除热键冲突。
- 选中包围内容，按 `Ctrl + Shift + A`
- 在弹出的输入框中，输入想要使用的 Emmet 缩写，按 `Enter` 确认。