---
title: obsidian
author: Jerry.Baijy
tags:
  - software
  - note-editor
  - markdown
---

# [Obsidian](https://obsidian.md/)

**Obsidian** 是一个 Markdown 笔记工具。目前用它作为 Typora 的辅助。

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
- 平时不要停留在编辑模式，尤其是和 Typora 双开时，容易产生不可预见性影响。

# 快捷键

|   操作   |                   obsidian 快捷键                    |
| :----: | :-----------------------------------------------: |
| ==系统== |                                                   |
| 开发者工具  | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>I</kbd> |

# 主题

## 主题

- 下载主题：`设置 / 外观 / 主题`
- 自定义部分：`设置 / 外观 / CSS 代码片段`，相当于 `base.user`。
- 当前文件夹下的 `claude-底板.css` 文件是 Claude Code 生成的代码片段，没解决重置问题。

## 主题变量

> [CSS 变量](https://docs.obsidian.md/Reference/CSS+variables/CSS+variables)

- 颜色

    ```css
    .theme-dark {
      --background-primary: #22272e;
      --background-secondary: #2d333b;
    }
    ```

# 插件

- 插件分为*官方插件*和*第三方插件*，以下是第三方插件的安装方法。
- `设置` > `第三方插件`
- 关闭 `安全模式`
- 搜索插件，安装，启用。
- 优秀插接件：
    - Tag Wrangler：插件管理