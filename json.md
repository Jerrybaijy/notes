---
title: json
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - config
  - web
---

# JSON

[**JSON**](https://www.json.org/json-zh.html)（**J**ava**S**cript **O**bject **N**otation，JavaScript 对象简谱），是一种轻量级的数据交换格式。JSON 可以实现不同平台的数据交换，也可以使用它保存业务数据。

## 主要资源

> [JSON 官方中文文档](https://www.json.org/json-zh.html)

## 语法

**语法**：`{"KEY1": VALUE1, "KEY2": VALUE2, ....}`

```json
{
  "name": "Git Bash",
  "commandline": "D:\\Program Files\\Git\\bin\\bash.exe -l -i"
}
```

**说明**：

- 键必须是字符串，必须使用双引号；
- 多个键值对使用 `,` 分隔，最后一个键值对接尾不加 `,`；

## 代码风格

- **缩进**：不敏感，通常缩进 2 个空格。

## 注释

JSON 本身 **不支持注释**，标准的 JSON 解析器会将任何非数据部分（例如注释）视为无效内容。

如果你需要注释 JSON，可以尝试以下变通方法：

### 使用额外字段作为注释

**语法**：`"_comment": "这是一个注释！",`

```json
{
  "_comment": "这是一个注释！",
  "name": "Git Bash",
  "commandline": "D:\\Program Files\\Git\\bin\\bash.exe -l -i"
}
```

### 使用 JSON 解析支持的扩展格式

JSON5 是 JSON 的一个超集，允许使用 `//` 和 `/* */` 注释：

```json
{
  // 这是单行注释
  "name": "Git Bash" /* 这是一个内嵌注释 */,
  "commandline": "D:\\Program Files\\Git\\bin\\bash.exe -l -i"
}
```
