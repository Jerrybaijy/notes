---
title: chrome
author: Jerry.Baijy
tags:
  - dev
  - software
  - google
  - browser
---

# Overview

[Chrome](https://www.google.com/chrome/) 是由 Google 开发的一款免费、跨平台的网页浏览器，自 2008 年发布以来，已成为全球市场占有率最高的浏览器。

# 快捷键

<!-- prettier-ignore -->
|       操作        |                      快捷键                       |
| :---------------: | :-----------------------------------------------: |
| 显示 / 隐藏书签栏 | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> |
|     添加书签      |          <kbd>Ctrl</kbd> + <kbd>D</kbd>           |
|       操作        |            <kbd>?</kbd> + <kbd>?</kbd>            |

# 扩展

- **Adblock Plus**：广告拦截器
- **Infinity 新标签页 (Pro)**：新标签页定制
- **Dark Reader**：为每个网站启用暗色模式
- **Google 翻译**
- **划词翻译**
- **沉浸式翻译**
- **Markdown Viewer**
- **Material Simple Dark Grey**：黑色主题
- **OneTab**：把不活动的网页暂时冻结在一起
- **Screenshot YouTube**：YouTube 截屏
- **YouTube Summary with ChatGPT & Claude**：总结 YouTube 视频内容
- **复制受保护的文本**：自由复制
- **篡改猴**
- **迅雷下载支持**
- **Export Tabs URLs**：批量复制标签页网址
- **Anti Anti Debug**：绕过网页的"反调试"保护

# Experiments

**Experiments** 指的是 Chrome 内置的一整套**实验性功能机制**，主要通过访问 chrome://flags 向用户暴露**尚未完全稳定、但已经可试用**的新特性或新实现方式。

## `Auto Dark Mode for Web Contents`

`Auto Dark Mode for Web Contents` 选项用于设置强制将浏览器背景色设置为深色，目前使用 `Enabled with selective image inversion` 效果，抵抗 Google Cloud Docs 无法调整背景色的问题。

# Remote Debugging

**Remote Debugging** 是 Chrome 浏览器中**远程调试**的入口页面。

```
chrome://inspect/#remote-debugging
```

# FAQ

## 管理搜索引擎

- `设置` > `搜索引擎` > `管理搜索引擎和网站搜索`
- 可以在浏览器地址栏输入关键词配合快捷键，实现在特定网站搜索，如 `g chrome使用技巧`

## Google Search Engine

- Google 搜索引擎是全球最大的搜索引擎。
- 搜索特定网站的特定内容，如 `intitle:"google使用教程" site:youtube.com`