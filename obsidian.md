---
title: obsidian
author: Jerry.Baijy
tags:
  - software
  - note-editor
  - markdown
  - obsidian
---

# Obsidian

[**Obsidian**](https://obsidian.md/) 是一个 Markdown 笔记工具。目前用它作为 Typora 的辅助。

> [Obsidian Docs](https://obsidian.md/zh/help/)

## 优点

- 图谱：没觉得有啥用
- 数据库：没研究
- 目前用它作为 Typora 的辅助，充当以下角色：
  - 搜索功能强大，能搜文件和内容。
  - 可以筛选文件元数据中的标签
  - 做链接到本地文件时更方便，有选择提示。（在设置中关闭 `Wiki 链接`）
  - ...

## 缺点

- 新建库以后，所有设置都要重新做。
- 没解决标题自动编号。
- 源码模式下复制表格，会打乱自己的格式
- Tab 键会缩进4个空格，改成2也无效
- 平时不要停留在编辑模式，尤其是和 Typora 双开时，容易产生不可预见性影响。

# 快捷键

<!-- prettier-ignore -->
| 操作 | obsidian 快捷键 |
| :---: | :---: |
| ==系统== |  |
| 开发者工具 | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd> |
| 查找替换（编辑模式） | <kbd>Ctrl</kbd> + <kbd>H</kbd> |
| 全局搜索 | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>H</kbd> |

# 核心插件

## 全局搜索

[**全局搜索**](https://obsidian.md/zh/help/plugins/search)是一个[核心插件](obsidian-community-plugins.md)，可以通过搜索词和运算符在 Obsidian 仓库中查找数据，从而缩小结果范围。

### 基本搜索

- 默认情况下，可以在左侧边栏中找到搜索按钮。
- 快捷键：<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>H</kbd>
- **搜索选中文本**：如果你在编辑器中选中了文本，然后通过快捷键打开搜索，搜索会显示所选文本的搜索结果。

### 搜索词

[**搜索词**](https://obsidian.md/zh/help/plugins/search#搜索词)中的每个单词默认在每个文件中独立匹配。可通过其它方式控制匹配规则：

- `hello world`：`hello` 和 `world` 不必相连，比如 **hello wanderful world**。
- `"hello world"`：`hello` 和 `world` 必须相连，必须是 **hello world**。
- `hello -world`：包含 `hello` 但不包含 `world`，可排除多个单词。
- 可以在引号前添加反斜杠（`\`）来*转义*引号，例如 `"they said \"hello\" to each other"`。

### 搜索运算符

[**搜索运算符**](https://obsidian.md/zh/help/plugins/search#搜索运算符)可以实现更精细的搜索词，进一步筛选你的结果。

- `file:`：查文件名，示例 `file:中国`，返回所有**名称**包含 `中国` 的文件。
- `content:`：查内容，示例 `content:中国`，返回所有**内容**包含 `中国` 的文件。
- `tag:`：查标签，示例 `content:中国`，返回所有**标签**包含（全等匹配） `中国` 的文件。

### 正则表达式

- 使用正斜杠（`/`）将[正则表达式](regex.md)包围，示例 `/$REGEX/`。
- 可以将正则表达式与搜索运算符结合使用

## 出链

[**出链**](https://obsidian.md/zh/help/plugins/outgoing-links)是一个[核心插件](obsidian-community-plugins.md)，可以显示当前笔记中指向仓库中其它文件的链接，以及潜在的可创建链接。

## 反向链接

[**反向链接**](https://obsidian.md/zh/help/plugins/backlinks)是一个[核心插件](obsidian-community-plugins.md)，可以显示仓库中其它文件指向当前笔记的链接。

## 大纲

[**大纲**](https://obsidian.md/zh/help/plugins/outline)是一个[核心插件](obsidian-community-plugins.md)，用于列出当前笔记中的标题。

要重新排列笔记中的各个部分，请在大纲中点击并拖动标题。

# 属性

[**属性**](https://obsidian.md/zh/help/properties)即 Markdown 文件的 [**YAML 前置元数据**](<yaml.md#YAML Front Matter>)，obsidian 支持多种[属性格式](https://obsidian.md/zh/help/properties#属性格式)。

[**YAML 前置元数据**](yaml.md#YAML%20Front%20Matter)

# 主题

## 自定义主题

- `设置` > `外观`

  - **基础颜色**：选择 `跟随系统`

  - **主题**：选择 `默认`

- `设置` > `外观` > `CSS 代码片段`，创建 CSS 文件，这里的样式会覆盖掉当前主题。

  **注意**：这个文件只作用于当前 Obsidian 仓库。

- 创建 `user.css`，相当于 Typora 中的 `base.user`。

  ```css
  /* 这里不要使用 :root，否则可能会被覆盖 */
  body {
    /* 作用于所有主题 */
  }
  
  .theme-dark {
    /* 作用于深色主题 */
  }
  
  .theme-light {
    /* 作用于浅色主题 */
    --table-border-color: gray;
  }
  
  /* -------------------其它部分----------------- */
  ```


## 主题变量

> [CSS 变量](https://docs.obsidian.md/Reference/CSS+variables/CSS+variables)

```css
/* 内容区 */
--background-primary: #2d333b;

/* 其它区 */
--background-secondary: #22272e;

/* HTML 属性值 */
--code-property: #a5d6ff;
--code-function: #a5d6ff;
```
