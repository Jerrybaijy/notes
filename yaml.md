---
title: yaml
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - web
---

# YAML

YAML 是 `YAML Ain't a Markup Language`（YAML 不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是：`Yet Another Markup Language`（仍是一种标记语言）。

- 大小写敏感：所有的值最好全小写，避免严格检索字段时找不到。
- 缩进

  - 使用缩进表示层级关系；
  - 缩进的空格数不重要，只要相同层级的元素左对齐即可；
  - 缩进不允许使用 `Tab`，只允许 `Space`；
  - 上下级缩进 2 个空格；
  - 字符（如冒号）后缩进 1 个空格；

- `#` 表示注释
- `-` 表示列表项
- 数据以**键值对**的形式存储

  - 中间用冒号（`:`）分隔，冒号后面必须有一个**空格**。

## YAML Front Matter

**YAML Front Matter**，即 **YAML 前置元数据**， 是一种使用 **YAML** 语言在某些文档（主要是 Markdown）顶部**定义元数据**的方法。

```markdown
---
title: test
author: Jerry.Baijy
tags:
  - 标签1
  - 标签2
  - 标签n
---

<!-- 以下是 Markdown 正文 -->

这是正文内容
```

YAML Front Matter 必须是文件中的第一部分，并设置在三段虚线（`---`）之间。

元数据将在导出时使用。例如，将上述 Markdown 文件导出为 HTML 格式时，Typora 会将其输出 `<title>YAML Front Matter</title>` 为 HTML `<head>` 元素。

可以使用本地工具对元数据进行检索等操作。
