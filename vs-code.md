---
title: vs-code
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - software
---

# VS Code

[**VS Code**](https://code.visualstudio.com/)（Visual Studio Code），是一款由微软开发且跨平台的免费**源代码编辑器**。

> [VS Code 文档](https://vscode.github.net.cn/docs)

## 环境搭建

[官网下载 VS Code ](https://code.visualstudio.com/Download)

# 快捷键

## 快捷键列表

> [快捷键参考](https://code.visualstudio.com/docs/reference/default-keybindings)

<!-- prettier-ignore -->
| 操作 | [VS Code 快捷键](https://code.visualstudio.com/docs/reference/default-keybindings) |
| :---: | :---: |
| ==软件配置== |  |
| 设置<br />（注意与搜狗输入法冲突） | <kbd>Ctrl</kbd> + <kbd>,</kbd> |
| 打开命令面板 | <kbd>F1</kbd> |
| 操作 | <kbd>?</kbd> + <kbd>?</kbd> |
| ==光标== |  |
| 选择下一个匹配项，并添加多光标 | <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| 取消最近添加的匹配项和多光标 | <kbd>Ctrl</kbd> + <kbd>U</kbd> |
| 添加多光标 | <kbd>Alt</kbd> + <kbd>单击</kbd> |
| ==代码== |  |
| 代码格式化（自己修改） | <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Z</kbd> |
| 使用 Emmet 缩写包围 （自己修改） | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>A</kbd> |
| ==终端== |  |
| 打开内置终端 | <kbd>Ctrl</kbd> + <kbd>~</kbd> |

## 设置快捷键

> [快捷键文档](https://vscode.github.net.cn/docs/getstarted/keybindings)

### 快捷键编辑器

通过[快捷键编辑器](https://vscode.github.net.cn/docs/getstarted/keybindings#_keyboard-shortcuts-editor)在用户界面设置快捷键：`文件` > `首选项` > `键盘快捷方式`

### 快捷键配置文件

在 [`keybindings.json`](https://vscode.github.net.cn/docs/getstarted/keybindings#_advanced-customization) 文件中覆盖默认快捷键，以下任意方式打开：

- [打开 `keybindings.json`](C:\Users\jerry\AppData\Roaming\Code\User\keybindings.json)
- `文件` > `首选项` > `键盘快捷方式` > 右上角点击 `打开键盘快捷方式 (json)`

## 其它问题

- `Ctrl + ,` 快捷键失效
  - 与搜狗输入法冲突！
  - `搜狗输入法设置` > `管理输入法` > 将 `搜狗输入法快捷键` 设置为其它

# `settings.json`

## 基础

`settings.json` 是用户自定义配置文件，以下任意方式打开：

- [打开 `settings.json`](C:\Users\jerry\AppData\Roaming\Code\User\settings.json)
- `设置` > 右上角点击 `打开设置 (json)`

VS Code 的 `settings.json` 支持 `JSONC` 模式。

## 全局和局部

**全局配置**：

```json
"workbench.colorCustomizations": {
  // 修改全局滚动条颜色
  "scrollbarSlider.background": "#a0a0a0aa"
}
```

**局部配置**：

```json
"workbench.colorCustomizations": {
  // 仅修改名为 "GitHub Light" 的主题
  "[GitHub Light]": {
    // 修改滚动条颜色
    "scrollbarSlider.background": "#a0a0a0aa"
  }
}
```

```json
// 仅修改 Python 语言的设置
"[python]": {
  // 默认 1 个 Tab 的宽度为 4 个空格
  "editor.tabSize": 4
}
```

# 主题

> [VS Code 主题](https://vscode.github.net.cn/docs/getstarted/themes)
>
> [主题颜色参考](https://vscode.github.net.cn/api/references/theme-color)

## 自动主题

[**自动主题**](https://vscode.github.net.cn/docs/getstarted/themes#_auto-switch-based-on-os-color-scheme)：VS Code 侦听操作系统的配色方案自动切换到事先设定的颜色主题。

```json
"window.autoDetectColorScheme": true, // 启用自动主题
"workbench.preferredDarkColorTheme": "GitHub Dark Dimmed", // 启用自动主题时的深色主题
"workbench.preferredLightColorTheme": "GitHub Light", // 启用自动主题时的浅色主题
```

## 普通主题

**普通主题**：未启用自动主题时的颜色主题。

```json
"workbench.colorTheme": "GitHub Dark Dimmed"  // 未启用自动主题时的颜色主题
```

### 主题文件

- 以 `GitHub Light` 主题为例
- VS Code 扩展通常安装在用户目录下的 `.vscode/extensions` 文件夹中。
- 类似 `github.github-vscode-theme-6.3.5` 标识符的文件夹既是 GitHub 主题文件夹。
- 进入该文件夹，主题定义文件通常位于 `themes/` 目录下，文件名为 `light.json` 或类似名称。
- 打开这个 JSON 文件，您会看到两个主要的颜色部分：
  - `colors`: 定义了 VS Code UI 界面（如侧边栏、状态栏、输入框）的颜色。
  - `tokenColors` / `tokenColors.settings`: 定义了代码编辑器中各种语法元素（如关键字、字符串、变量）的高亮颜色。

## 自定义主题

[**自定义主题**](https://vscode.github.net.cn/docs/getstarted/themes#_customizing-a-color-theme)：可以对颜色主题进行部分覆盖。

### 工作台颜色

```json
"workbench.colorCustomizations": {
  // 覆盖规则
}
```

```json
"workbench.colorCustomizations": {
  "editor.background": "#3B4352",  // 编辑器背景色
  "sideBar.background": "#3B4352",  // 侧边栏背景色
  "statusBar.background": "#5c5d61", // 状态栏背景色
  "scrollbarSlider.background": "#575757aa", // 滚动条背景色
  "scrollbarSlider.hoverBackground": "#7a7a7aaa", // 悬停滚动条背景色
  "editorGutter.background": "#3B4352",  // 行号背景色
  "editor.selectionHighlightBackground": "#4c4948",  // 选中代码高亮背景色
  "editor.selectionBackground": "#000000",  // 选中区域背景色
  "editor.findMatchBackground": "#000000",  // 查找结果高亮背景色
  "editor.lineHighlightBackground": "#000000",  // 当前光标所在行的背景色
}
```

### 编辑器语法颜色

```json
"editor.tokenColorCustomizations": {
  // 覆盖规则
}
```

```json
"editor.tokenColorCustomizations": {
  "textMateRules",  // 作用域样式
  "comments": "#519657",  // 注释
  "strings": "#7e3648",  // 字符串
  "functions": "#1c7887",  // 函数
  "keywords": "#a207fc", // 关键字
  "variables": "#0720fc",  // 变量
  "numbers": "#e21d1d"   // 数字
}
```

#### `textMateRules`

**TextMate** 是一种用于语法高亮的语言定义格式。VS Code 沿用了这套系统来解析代码并确定代码中每个部分的**作用域（Scope）**。

**作用域样式** `textMateRules` 的工作原理就是：根据代码元素被赋予的特定**作用域名称**（即 `scope`），来应用您定义的颜色或样式（即 `settings`）。

```
textMateRules
  ├─ scope
  └─ settings
```

|      属性       |                 值类型                  |
| :-------------: | :-------------------------------------: |
| `textMateRules` | 一个值：`object`<br/>多个值：`object[]` |
|     `scope`     | 一个值：`string`<br>多个值：`string[]`  |
|   `settings`    |                `object`                 |

```json
"editor.tokenColorCustomizations": {
  "textMateRules": [
    {
      // 目标作用域：各种编程语言的关键字
      "scope": ["keyword", "storage.type"],
      // 设置要应用的样式
      "settings": {
        "foreground": "#ff0000",
        "fontStyle": "bold"
      }
    }
    // 其它 scope 和 settings
  ]
  // 其它 editor.tokenColorCustomizations 设置
}
```

### 编辑器语义颜色

```json
"editor.semanticTokenColorCustomizations": {
  // 覆盖规则
}
```

### 特定主题

```json
"workbench.colorCustomizations": {
  // 仅修改名为 "GitHub Light" 的主题
  "[GitHub Light]": {
    // 覆盖规则
  },

  // 修改 Abyss 和 Red 主题
  "[Abyss][Red]": {
    // 覆盖规则
  },

  // 修改以 Monokai 开头的主题
  "[Monokai*]": {
    // 覆盖规则
  }
}
```

## 图标主题

```json
"workbench.iconTheme": "vscode-icons", // 文件图标主题
```

# 工作台

```json
"workbench.startupEditor": "none", // 启动时默认打开项
```

工作台主题详见主题章节。

# 编辑器

## 格式化

格式化由两方面控制：

- VS Code 控制动态输入时的 Tab 宽度
- Prettier 控制格式化时的 Tab 宽度

### VS Code

VS Code 控制**动态输入时**的 Tab 宽度，即软件状态栏显示的空格数量 <img src="assets/image-20251020122212688.png" alt="image-20251020122212688" style="zoom:67%;" />，它控制以下两方面。

- 按下 `Tab` 键以后缩进的空格数量
- 按下 `Enter` 键以后缩进的空格数量

```json
"editor.detectIndentation": false, // 禁止 VSCode 自动检测文件的缩进方式
"editor.insertSpaces": true, // 输入 Tab 时，使用空格替代制表符
"editor.indentSize": "tabSize", // 引用 tabSize 的值来确定每次缩进使用多少个空格
"editor.tabSize": 2, // 默认 1 个 Tab 的宽度为 2 个空格
```

### Prettier

Prettier 等格式化工具控制**格式化时**的 Tab 宽度。

```json
"editor.defaultFormatter": "esbenp.prettier-vscode", // 启用 Prettier 格式化
"editor.formatOnSave": true, // 在手动保存后，会自动触发 Prettier 对代码格式化
```

### 特定语言

如果想让特定语言有特殊设置：

```json
"[json]": {
  "editor.tabSize": 4 // 动态输入时的 Tab 宽度
  "prettier.tabWidth": 4, // 格式化时的 Tab 宽度
}
```

**注意**：在实际项目中，应该在 Prettier 的 `.prettierrc` 文件中设置格式化，详见 `.prettierrc`。

## 编辑器其它

```json
"files.autoSave": "afterDelay", // 实时自动保存
"editor.codeActionsOnSave": {}, // 文件保存时自动执行代码操作
"editor.fontFamily": "Consolas, '微软雅黑'", // 编辑器字体
"editor.fontSize": 24, // 编辑器字体大小
"editor.wordWrap": "on", // 文本过长时自动换行显示
"editor.mouseWheelZoom": true, // Ctrl + 鼠标滚轮：对编辑器字体大小缩放
"editor.minimap.enabled": false, // 编辑器缩略图
"editor.renderWhitespace": "boundary", // 显示缩进空格标记为 boundary
"editor.unicodeHighlight.ambiguousCharacters": false, // 禁用 Unicode 模糊字符的高亮
"editor.unicodeHighlight.invisibleCharacters": false, // 禁用不可见字符的 Unicode 高亮
"editor.quickSuggestions": {}, // 自动补全建议
```

# `settings.json` 其它

## 窗口

```json
"window.autoDetectColorScheme": true, // 启用自动主题
```

## 终端

```json
"terminal.integrated.cursorStyle": "line", // 终端聚焦时光标的样式
"terminal.integrated.cursorStyleInactive": "line", // 终端未聚焦时光标的样式
// 默认终端
"terminal.integrated.defaultProfile.windows": "Git Bash",
"terminal.integrated.profiles.windows": {
  "Git Bash": {
    "path": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

## Git

```json
"git.autofetch": true, // 自动获取远程仓库信息，但不会自动合并到本地
"git.openRepositoryInParentFolders": "never", // 禁止在打开的文件夹的父级目录中搜索 Git 仓库
```

## 其它设置

```json
"markdown.styles": ["vscode-md-pre.css"], // Markdown 预览模式的样式
"diffEditor.ignoreTrimWhitespace": false, // 在 diff 比较时，不忽略尾部空白字符
"salesforcedx-vscode-apex.java.home": "C:\\\\Program Files\\\\Java\\\\jdk-21", // Salesforce 相关设置
"git.autofetch": true, // 自动获取远程仓库信息，但不会自动合并到本地
```

## 扩展设置

扩展设置详见各扩展章节

# 扩展

## 常驻扩展

- `Chinese (Simplified)`：汉化
- `IntelliCode`：智能代码补全
- `IntelliCode API Usage Examples`：比 `IntelliCode` 更厉害
- `Prettier`：代码格式化
- `Live Server`：实时预览前端网页
- `vscode-icons`：文件图标
- `Auto Rename Tag`：自动同步更改 HTML 或 XML 标签对的标签名
- `Python`：支持 Python
- `Black`：Python 格式化（首选）
- `HashiCorp Terraform`：Terraform 插件，含格式化

## Live Server

实时预览前端网页

```json
"liveServer.settings.CustomBrowser": "chrome", // Live Server 默认浏览器
"liveServer.settings.donotVerifyTags": true, // 禁用 Live Server 在启动时对 HTML 标签的验证
"liveServer.settings.donotShowInfoMsg": true, // 禁用 Live Server 在运行时弹出的各种信息通知
```

## open in browser

直接用浏览器打开本地文件

```json
"open-in-browser.default": "chrome", // Open in browser 扩展默认打开的浏览器
```

## vscode-icons

设置 VS Code 资源管理器**文件图标**。

```json
"vsicons.dontShowNewVersionMessage": true, // 禁用图标扩展更新弹窗提醒
```

## Red Hat 系列

对 Red Hat 系列的扩展进行如下设置：

```json
"redhat.telemetry.enabled": true, // 禁止 Red Hat 收集匿名使用数据
```

## 其它扩展

- `Auto Rename Tag`：自动同步更改 HTML 或 XML 标签对的标签名
- `Chinese (Simplified)`：汉化
- `IntelliCode`：智能代码补全
- `IntelliCode API Usage Examples`：比 `IntelliCode` 更厉害
- `Jinja`：为 Jinja2 模板语言提供语法高亮和自动完成支持
- `Python`：支持 Python
- `Black`：Python 格式化（首选）
- `autopep8`：Python 格式化（备用）
- `SQLite Viewer`：在 VSCode 中查看 SQLite 数据库
- `Prettier`：代码格式化
- `multi-command`：执行多命令，详见 `Markdown 硬换行` 章节。
- `cline`：AI 编程 + MCP 调用

# Markdown

## Markdown 预览

在 Markdown 页面右上角，有预览模式按钮。

可以对预览模式进行样式覆盖：

- 在项目根目录创建样式文件，如 `vscode-md-pre.css`。
- 此样式文件在 Git 有备份。

按如下方式进行自动编号：

```css
h1,
h2,
h3,
h4 {
  font-weight: 600;
}

body {
  counter-reset: h1;
}

h1 {
  text-align: center;
  counter-reset: h2;
}

h2 {
  counter-reset: h3;
}

h3 {
  counter-reset: h4;
}

h4 {
  counter-reset: h5;
}

h5 {
  counter-reset: h6;
}

h2::before {
  counter-increment: h2;
  content: counter(h2) ". ";
}

h3::before {
  counter-increment: h3;
  content: counter(h2) "." counter(h3) " ";
}

h4::before {
  counter-increment: h4;
  content: counter(h2) "." counter(h3) "." counter(h4) " ";
}

h5::before {
  counter-increment: h5;
  content: counter(h2) "." counter(h3) "." counter(h4) "." counter(h5) " ";
}

h6::before {
  counter-increment: h6;
  content: counter(h2) "." counter(h3) "." counter(h4) "." counter(h5) "."
    counter(h6) " ";
}
```

## Markdown 硬换行

**Markdown 硬换行**：即连续输入 `Space` `Space` `Enter`，可实现同一段落内换行。

在 VS Code 中可按以下方法实现一键硬换行。

- 安装 `multi-command` 扩展
- 在 `settings.json` 文件中添加命令

    ```json
    // ---------------## multi-command，为了实现 Markdown 一键硬换行---------------
    "multiCommand.commands": [
      {
        "command": "multiCommand.markdownHardBreak",
        "sequence": [
          {
            "command": "type",
            "args": { "text": "  " } // 插入两个空格
          },
          "editor.action.insertLineAfter" // 换行
        ]
      }
    ]
    ```

- 在 `keybindings.json` 文件中绑定快捷键

    ```json
    // -----### Markdown 硬换行-----
    {
      "key": "ctrl+enter",
      "command": "multiCommand.markdownHardBreak",
      "when": "editorLangId == markdown"
    }
    ```

- 重启 VS Code
- 编辑 Markdown 文件，按下 `Ctrl + Enter` 键，即可实现一键硬换行。

# 其它

## Emmet

**Emmet** 可通过**缩写语法**快速生成 HTML 和 CSS 代码片段，详见 [`software | Emmet`](software.md#emmet) 笔记。

## 选择解释器虚拟环境

- 如果项目根目录有虚拟环境，解释器会默认选择虚拟环境；
- 每次进入项目目录都应该检查；
- 如果没有默认选择虚拟环境，可手动选择，以 Python 为例；
- 点击 VSCode 右下角 `python` 右侧的 `3.12.1 64-bit`，会在上方弹出选项；
  - 或者按 `Ctrl + Shift + P` 打开命令面板；输入并选择 `Python: Select Interpreter`；
- 选择你创建的虚拟环境中的 Python 解释器，通常路径会是 `./venv/Scripts/python.exe`；
- 打开项目目录中的 Python 文件时，在 VSCode 右下角状态栏会看到，当前选择的 Python 解释器应该是你刚才选择的虚拟环境。
