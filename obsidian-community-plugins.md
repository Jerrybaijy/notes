---
title: obsidian-community-plugins
author: Jerry.Baijy
tags:
  - obsidian
---

# Obsidian Community Plugins

Obsidian 中的插件可分为**核心插件**和**第三方插件**。

- **[核心插件](https://obsidian.md/zh/help/plugins)**：由 Obsidian 团队官方开发和维护，并内置于应用中。
- **[第三方插件](https://obsidian.md/zh/help/community-plugins)**：由社区构建，并需要安装才能使用。

以下是**第三方插件**的安装方法。

- 可以[在浏览器中浏览第三方插件](https://community.obsidian.md/)
- `设置` > `第三方插件`
- 关闭 `安全模式`
- 搜索插件，安装，启用。

# Tag Wrangler

**[Tag Wrangler](https://community.obsidian.md/search?q=Tag%20Wrangler)** 是一个元数据标签管理工具。

右键单击标签进行重命名。

# Show Whitespace

**[Show Whitespace](https://community.obsidian.md/search?q=Show%20Whitespace)** 可在**源码模式**和**实施阅览**模式中显示不可见字符的样式，比如行首的前导空格。

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

## Find-n-Replace

**[Find-n-Replace](https://community.obsidian.md/plugins/find-n-replace)** 可以像 VS Code 那样全局搜索和替换。

- 在侧边栏中可找到功能区
- 不如 VS Code 直观，没有修改前后文件对比。
- 操作不可撤销
