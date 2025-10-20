---
title: prettier
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - software
  - plugins
  - formater
---

# Prettier

[**Prettier**](https://prettier.io/docs/) 是一个非常流行的**代码格式化工具**。

## 全局安装

```bash
# 本地安装，保存在项目目录，项目内生效
npm install --save-dev prettier

# 全局安装，系统全局内生效
npm install --global prettier

# 使用：先在命令行导航至 index.js 目录，再执行命令。
# npx 优先使用本地安装版本，其次使用全局版本。
npx prettier --write index.js
```

## VS Code 扩展

使用方法详见 [`vs-code`](#vs-code)  笔记。

# 配置

## `.prettierrc`

[`.prettierrc`](https://prettier.io/docs/configuration) 文件用于对 Prettier 进行精细化配置，存放于项目根目录下。

官方文档提及：Prettier 有意**不支持**任何类型的**全局配置**。

学习环境使用 VS Code 的 `settings.json`  文件进行精细化配置，详见 [`vs-code`](#vs-code) 笔记。

## 忽略代码

> [忽略代码](https://prettier.io/docs/ignore)

### `.prettierignore`

要从格式化中排除文件，在项目根目录中创建一个 `.prettierignore` 文件。`.prettierignore` 使用 [gitignore 语法](https://git-scm.com/docs/gitignore#_pattern_format)。

```
# Ignore artifacts:
build
coverage

# Ignore all HTML files:
**/*.html
```

### `prettier-ignore`

`prettier-ignore` 用于忽略代码片段。

**语法**：将 `prettier-ignore` 加入到语言的注释中。

```markdown
<!-- prettier-ignore -->
| 操作 | Typora 快捷键 |
| :---: | :---: |
| ==系统== |  |
| 偏好设置 | <kbd>Ctrl</kbd> + <kbd>,</kbd> |
```
