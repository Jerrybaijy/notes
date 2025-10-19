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

> [VS Code 快捷键](https://code.visualstudio.com/docs/reference/default-keybindings)

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

## 快捷键相关问题

- **设置快捷键**：左下角 `管理` - `键盘快捷方式`
- `Ctrl + ,` 快捷键失效

    - 与搜狗输入法冲突！
    - `搜狗输入法设置` - `管理输入法` - 将 `搜狗输入法快捷键` 设置为其它

# 配置文件

`settings.json` 是 用户自定义配置文件，以下任意方式打开：

- [打开配置文件](C:\Users\jerry\AppData\Roaming\Code\User\settings.json)

- `设置` > 右上角点击 `打开设置 (ui)`

VS Code 的 `settings.json` 是一种 `JSONC` 模式。

## `settings.json`

```json
{
    // ------------------|| 功能--------------------------------
    "workbench.startupEditor": "none", // 启动时默认打开项
    "files.autoSave": "afterDelay", // 实时自动保存
    "editor.codeActionsOnSave": {}, // 文件保存时自动执行代码操作
    "editor.fontFamily": "Consolas, '微软雅黑'", // 编辑区字体
    "editor.fontSize": 24, // 编辑区字体大小
    "editor.mouseWheelZoom": true, // Ctrl + 鼠标滚轮：对编辑器字体大小缩放
    "open-in-browser.default": "chrome", // 默认浏览器

    // ------------------|| 主题---------------------------
    "workbench.colorTheme": "GitHub Dark Dimmed", // 主题
    "workbench.iconTheme": "vscode-icons", // 侧边栏和文件树图标样式
    "vsicons.dontShowNewVersionMessage": true, // 禁用图标扩展更新弹窗提醒

    // ------------------|| 代码---------------------------
    "editor.guides.bracketPairs": true, // 启用花括号的引导线
    "editor.linkedEditing": true, // 同时修改 HTML/XML 等标记语言中配对的标签

    // ------------------|| 格式化---------------------------
    "editor.defaultFormatter": "esbenp.prettier-vscode", // 使用 Prettier 对代码格式化
    "editor.detectIndentation": false, // 禁止 VSCode 自动检测文件的缩进方式
    "editor.insertSpaces": true, // 输入 Tab 时，使用空格替代制表符
    "editor.indentSize": "tabSize", // 引用 tabSize 的值来确定每次缩进使用多少个空格
    "editor.tabSize": 4, // 默认 1 个 Tab 的宽度为 4 个空格
    // ------特定语言------
    "[css]": {
        "editor.tabSize": 2 // Tab 宽度设置为 2 个空格
    },
    "[html]": {
        "editor.tabSize": 2 // Tab 宽度设置为 2 个空格
    },
    "[javascript]": {
        "editor.tabSize": 2 // Tab 宽度设置为 2 个空格
    },
    "[json]": {
        "prettier.tabWidth": 4 // Prettier 对 JSONC 文件使用 4 个空格缩进
    },
    "[jsonc]": {
        "prettier.tabWidth": 4 // Prettier 对 JSONC 文件使用 4 个空格缩进
    },
    "[markdown]": {
        "editor.renderWhitespace": "boundary", // 显示缩进空格标记为 boundary
        "editor.unicodeHighlight.ambiguousCharacters": false, // 禁用 Unicode 模糊字符的高亮
        "editor.unicodeHighlight.invisibleCharacters": false, // 禁用不可见字符的 Unicode 高亮
        "diffEditor.ignoreTrimWhitespace": false, // 在 diff 比较时，不忽略尾部空白字符
        "editor.wordWrap": "on", // 自动换行，文本过长时自动换行
        // 自动补全建议
        "editor.quickSuggestions": {
            "comments": "off",
            "strings": "off",
            "other": "off"
        }
    },
    "[python]": {
        "editor.defaultFormatter": "mikoz.black-py" // Python 默认格式化工具
    },

    // ------------------|| 终端---------------------------
    "terminal.integrated.cursorStyle": "line", // 终端聚焦时光标的样式
    "terminal.integrated.cursorStyleInactive": "line", // 终端未聚焦时光标的样式
    // 默认终端
    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "terminal.integrated.profiles.windows": {
        "Git Bash": {
            "path": "C:\\Program Files\\Git\\bin\\bash.exe"
        }
    },

    // ------------------|| Git---------------------------
    "git.autofetch": true, // 自动获取远程仓库信息，但不会自动合并到本地
    "git.openRepositoryInParentFolders": "never", // 禁止在打开的文件夹的父级目录中搜索 Git 仓库

    // ------------------|| Live Server---------------------------
    "liveServer.settings.CustomBrowser": "chrome", // Live Server 默认浏览器
    "liveServer.settings.donotVerifyTags": true, // 禁用 Live Server 在启动时对 HTML 标签的验证
    "liveServer.settings.donotShowInfoMsg": true, // 禁用 Live Server 在运行时弹出的各种信息通知

    // ------------------|| 其它设置---------------------------
    "redhat.telemetry.enabled": true, // 禁止 Red Hat 收集匿名使用数据

    // ------------------|| 文件嵌套和关联，稳定以后再删除---------------------------
    // "explorer.fileNesting.patterns": {
    //     "*.ts": "${capture}.js",
    //     "*.js": "${capture}.js.map, ${capture}.min.js, ${capture}.d.ts",
    //     "*.jsx": "${capture}.js",
    //     "*.tsx": "${capture}.ts",
    //     "tsconfig.json": "tsconfig.*.json",
    //     "package.json": "package-lock.json, yarn.lock, pnpm-lock.yaml, bun.lockb",
    //     "*.sqlite": "${capture}.${extname}-*",
    //     "*.db": "${capture}.${extname}-*",
    //     "*.sqlite3": "${capture}.${extname}-*",
    //     "*.db3": "${capture}.${extname}-*",
    //     "*.sdb": "${capture}.${extname}-*",
    //     "*.s3db": "${capture}.${extname}-*"
    // },
    // ------------------|| 文件类型和编辑器关联，稳定以后再删除---------------------------
    // "workbench.editorAssociations": {
    //     "{git,gitlens,git-graph}:/**/*.{md,csv,svg}": "default"
    // },
    // --------------|| 以下为系统自动创建----------------------------------------------
    "[dockercompose]": {
        "editor.insertSpaces": true,
        "editor.tabSize": 2,
        "editor.autoIndent": "advanced",
        "editor.quickSuggestions": {
            "other": true,
            "comments": false,
            "strings": true
        },
        "editor.defaultFormatter": "redhat.vscode-yaml"
    },
    "[github-actions-workflow]": {
        "editor.defaultFormatter": "redhat.vscode-yaml"
    }
}

```

## 功能

```json
"workbench.startupEditor": "none", // 启动时默认打开项
"files.autoSave": "afterDelay", // 实时自动保存
"editor.codeActionsOnSave": {}, // 文件保存时自动执行代码操作
"editor.fontFamily": "Consolas, '微软雅黑'", // 编辑区字体
"editor.fontSize": 24, // 编辑区字体大小
"editor.mouseWheelZoom": true, // Ctrl + 鼠标滚轮：对编辑器字体大小缩放
"open-in-browser.default": "chrome", // 默认浏览器
```

## 主题

```json
"workbench.colorTheme": "GitHub Dark Dimmed", // 主题
"workbench.iconTheme": "vscode-icons", // 侧边栏和文件树图标样式
"vsicons.dontShowNewVersionMessage": true, // 禁用图标扩展更新弹窗提醒
```

## UI 颜色

```json
"workbench.colorCustomizations": {
    "editor.background": "#3B4352",  // 编辑区背景色
    "sideBar.background": "#3B4352",  // 侧边栏背景色
    "statusBar.background": "#5c5d61", // 状态栏背景色
    "editorGutter.background": "#3B4352",  // 行号背景色
    "editor.selectionHighlightBackground": "#4c4948",  // 选中代码高亮背景色
    "editor.selectionBackground": "#000000",  // 选中区域背景色
    "editor.findMatchBackground": "#000000",  // 查找结果高亮背景色
    "editor.lineHighlightBackground": "#000000",  // 当前光标所在行的背景色
}
```

## 格式化

### Prettier

```json
"editor.defaultFormatter": "esbenp.prettier-vscode", // 使用 Prettier 对代码格式化
```

```json
// Prettier 对 JSONC 文件使用 4 个空格进行缩进
"[jsonc]": {
    "prettier.tabWidth": 4
}
```

### VS Code

```json
"editor.detectIndentation": false, // 禁止 VSCode 自动检测文件的缩进方式
"editor.insertSpaces": true, // 输入 Tab 时，使用空格替代制表符
"editor.indentSize": "tabSize", // 引用 tabSize 的值来确定每次缩进使用多少个空格
"editor.tabSize": 4, // 默认 1 个 Tab 的宽度为 4 个空格
```

### 特定语言

如果想让特定语言有特殊设置，如想让 CSS 的 Tab 宽度设置为 2 个空格：

```json
"[css]": {
    "editor.tabSize": 2 // Tab 宽度设置为 2 个空格
},
```

## 代码高亮

### 方式一

代码语法高亮

```json
"editor.tokenColorCustomizations": {}
```

#### 语法

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

| 属性 | 值类型 |
| :---: | :---: |
| `textMateRules` | 一个值：`object`<br/>多个值：`object[]` |
| `scope` | 一个值：`string`<br>多个值：`string[]` |
| `settings` | `object` |

```json
"editor.tokenColorCustomizations": {
    "textMateRules": [
        {
            // 目标作用域：各种编程语言的关键字
            "scope": [
                "keyword",
                "storage.type"
            ],
            // 设置要应用的样式
            "settings": {
                "foreground": "#ff0000",
                "fontStyle": "bold"
            }
        },
        // 其它 scope 和 settings
    ],
    // 其它 editor.tokenColorCustomizations 设置
}
```

### 方式二

代码语义高亮

```json
"editor.semanticTokenColorCustomizations": {}
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

## Live Server

```json
"liveServer.settings.CustomBrowser": "chrome", // Live Server 默认浏览器
"liveServer.settings.donotVerifyTags": true, // 禁用 Live Server 在启动时对 HTML 标签的验证
"liveServer.settings.donotShowInfoMsg": true, // 禁用 Live Server 在运行时弹出的各种信息通知
```

## Git

```json
"git.autofetch": true, // 自动获取远程仓库信息，但不会自动合并到本地
"git.openRepositoryInParentFolders": "never", // 禁止在打开的文件夹的父级目录中搜索 Git 仓库
```

## 其它设置

```json
"editor.renderWhitespace": "boundary", // 显示缩进空格标记为 boundary
"editor.unicodeHighlight.ambiguousCharacters": false, // 禁用 Unicode 模糊字符的高亮
"editor.unicodeHighlight.invisibleCharacters": false, // 禁用不可见字符的 Unicode 高亮
"diffEditor.ignoreTrimWhitespace": false, // 在 diff 比较时，不忽略尾部空白字符
"editor.wordWrap": "on", // 自动换行，文本过长时自动换行
"salesforcedx-vscode-apex.java.home": "C:\\\\Program Files\\\\Java\\\\jdk-21", // Salesforce 相关设置
"redhat.telemetry.enabled": true, // 禁止 Red Hat 收集匿名使用数据
"git.autofetch": true, // 自动获取远程仓库信息，但不会自动合并到本地
"editor.quickSuggestions": {}, // 自动补全建议
```

# 扩展

- **`Auto Rename Tag`**：自动同步更改 HTML 或 XML 标签对的标签名
- **`Chinese (Simplified)`**：汉化
- **`IntelliCode`**：智能代码补全
- **`IntelliCode API Usage Examples`**：比 `IntelliCode` 更厉害
- **`Jinja`**：为 Jinja2 模板语言提供语法高亮和自动完成支持
- **`Live Server`**：实时预览前端网页
- **`Python`**：支持 Python
- **`Black`**：Python 格式化（首选）
- **`autopep8`**：Python 格式化（备用）
- **`SQLite Viewer`**：在 VSCode 中查看 SQLite 数据库

# 其它

## Emmet

**Emmet** 可通过**缩写语法**快速生成 HTML 和 CSS 代码片段，详见 [`software | Emmet`](software.md#emmet) 笔记。

## 选择解释器虚拟环境

1. 如果项目根目录有虚拟环境，解释器会默认选择虚拟环境；
2. 每次进入项目目录都应该检查；
3. 如果没有默认选择虚拟环境，可手动选择，以 Python 为例；
4. 点击 VSCode 右下角 `python` 右侧的 `3.12.1 64-bit`，会在上方弹出选项；

    - 或者按 `Ctrl + Shift + P` 打开命令面板；输入并选择 `Python: Select Interpreter`；

5. 选择你创建的虚拟环境中的 Python 解释器，通常路径会是 `./venv/Scripts/python.exe`；
6. 打开项目目录中的 Python 文件时，在 VSCode 右下角状态栏会看到，当前选择的 Python 解释器应该是你刚才选择的虚拟环境。