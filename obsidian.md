---
title: obsidian
author: Jerry.Baijy
tags:
  - software
  - note-editor
  - markdown
---

# Obsidian

[**Obsidian**](https://obsidian.md/) 是一个 Markdown 笔记工具。目前用它作为 Typora 的辅助。

## 特点

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
| 查找替换 | <kbd>Ctrl</kbd> + <kbd>H</kbd> |

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

# Plugins

## Plugins Quick Start

- 插件分为官方插件和第三方插件，以下是第三方插件的安装方法。
- `设置` > `第三方插件`
- 关闭 `安全模式`
- 搜索插件，安装，启用。
- 优秀插接件：
  - Tag Wrangler：元数据标签管理

## Tag Wrangler

Tag Wrangler 是一个元数据标签管理工具。

右键单击标签进行重命名。

## Show Whitespace

可显示不可见字符的样式，比如行首的前导空格。

- 打开 `Show all whitespace` 选项

- 在自己的 CSS 片段中添加以下规则，以覆盖插件的默认样式。

  ```css
  body {
    /* 针对 Show Whitespace 插件 */
    /* 覆盖行尾软换行样式为 ↲ */
    --line-end: "↲" !important;
    /* 覆盖行尾硬换行样式为 ↓ */
    --line-break: "↓" !important;
  }
  ```

  
