---
title: react
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - javascript
  - code-language
  - frontend
  - library
  - framework
  - web
  - react
  - vite
---

# Overview

[**React**](https://zh-hans.react.dev/) 是一个用于构建用户界面的 JavaScript 库，由 Facebook 开发。

> [React 教程](https://zh-hans.react.dev/learn)
>
> [React 参考](https://zh-hans.react.dev/reference/react)

# Quick Start

React 推荐多种创建项目的方法：

> [全栈框架](https://zh-hans.react.dev/learn/creating-a-react-app)
>
> [从零开始构建 React 应用](https://zh-hans.react.dev/learn/build-a-react-app-from-scratch)

- **Next.js**：全栈 React 框架
  - 提供了完整的全栈解决方案，包括路由、数据获取、服务端渲染等
  - 适用于前后端统一使用 JavaScript/TypeScript 构建的应用
  - 前后端不分离
- **Vite**：前端 React 框架
  - 前端只需要与后端 API 通信，不需要 Next.js 的全栈功能
  - 适用于前后端分离项目

本 Quick Start 记录 Vite 方法的基本实现。

## 环境依赖

Node.js 已安装，npm 更新至最新版，详见 [node.js](node-js.md) 笔记。

## 创建项目

```bash
cd $PROJECT_dir
npm create vite@latest $FRONTEND_DIR -- --template react
npm create vite@latest frontend -- --template react
```

这会初始化 React 项目结构

```
$FRONTEND_DIR
│
├── node_modules/          # NPM 依赖包安装目录
├── public/                # 静态资源目录，包含无需打包的文件
├── src/                   # 源代码目录
│   ├── App.css            # App 主组件的样式文件
│   ├── App.jsx            # App 主组件文件
│   ├── assets/            # 资源文件目录
│   │   └── react.svg      # React 图标文件
│   ├── index.css          # 全局样式文件
│   └── main.jsx           # 应用入口 JavaScript 文件，渲染 React 组件
│
├── .gitignore             # Git 版本控制忽略文件配置
├── eslint.config.js       # ESLint 代码质量检查配置
├── index.html             # 应用入口 HTML 文件
├── package-lock.json      # NPM 依赖版本锁定文件，确保依赖一致性
├── package.json           # 项目配置文件，包含依赖、脚本等信息
├── README.md              # 项目说明文档
└── vite.config.js         # Vite 构建工具配置文件
```

## 安装依赖

```bash
cd $FRONTEND_DIR
npm install
```

## 编写代码文件

### `App.jsx`

应用主组件 `src/App.jsx`，编写逻辑方法等。

```jsx
import { useState } from 'react'
import './App.css'

function App() {
  // 主组件内容
}

export default App
```

### `main.jsx`

应用入口文件 `src/main.jsx`，引入主组件 `App.jsx`

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

### `index.html`

应用入口 HTML 文件 `src/index.html`，引入应用入口文件 `src/main.jsx`。

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>frontend</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

## 启动开发服务器

```bash
cd $FRONTEND_DIR
npm run dev
```

访问地址：http://localhost:5173

## 构建静态资源包（可选）

**静态资源包**可以预览在生产环境是否能运行。

```bash
cd $FRONTEND_DIR
npm run build
```

实际是调用了 `package.json` 里定义的脚本 `"build": "vite build"`。

这会在前端项目根目录生成 `dist` 目录，将项目源码构建为生产环境就绪的静态资源包。

```
dist/
├── assets/          # 编译后的 JS/CSS/图片等
│   ├── index.xxx.js # 业务代码
│   ├── vendor.xxx.js # React 等第三方依赖
│   └── style.xxx.css # 样式文件
└── index.html       # 入口 HTML（引用了上面的资源）
```

生成 `dist` 后，可以用 Vite 自带的 `preview` 命令启动静态服务器，验证静态资源包。

```bash
npm run preview
```

## 构建镜像

```dockerfile
# 阶段1：构建 React 应用
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
COPY src ./src
COPY vite.config.js ./
RUN npm install
# 构建 dist
RUN npm run build

# 阶段2：生产运行
FROM nginx:alpine
# 仅复制 Docker 内生成的 dist
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

# Create React App

自 2025 年 2 月 14 日起，React 官方将正式弃用 [Create React App](https://create-react-app.dev/) 作为新应用的推荐工具。此部分内容仅作为学习留存，以备旧项目再次再次使用。

## 基本流程

### 创建项目

- Node.js 已安装，npm 更新至最新版

- 创建 React 项目

  ```bash
  npx create-react-app $PROJECT_NAME
  ```

- 安装组件库

- 编写主程序文件和组件文件

### 本地测试

- 后端与数据库已启动

- 调试源文件

  ```bash
  npm start
  ```

### 生成静态文件

- 在项目的根目录中运行 npm 命令，这将项目根目录中生成一个名为 `build` 的静态文件夹。

  ```bash
  npm run build
  ```

- 将 `.gitignore` 中的 build 注释掉

### 生成 Image

- 使用 GitLab Pipeline 生成 Image

- `.gitlab-ci.yml` 按通用格式写

- Dockerfile

  ```dockerfile
  FROM node:latest
  WORKDIR /app
  COPY ./build .
  RUN npm install -g http-server
  CMD ["http-server", "-p", "8080"]
  ```

## React 管理

```bash
# 查看 React 版本
npm list react
# 安装 React
npm install react[@VERSION]
# 删除 React
npm uninstall react
```

## 组件

### Material UI

Material-UI 是一个流行的 React UI 组件库，它基于 Google 的 Material Design 规范，提供了丰富的 React 组件，用于构建美观、易用的用户界面。

- **Material UI 管理**

  ```bash
  # 查看版本
  npm list @mui/material

  # 安装 Material UI
  npm install @mui/material @emotion/react @emotion/styled
  # 安装 Material Icons
  npm install @mui/icons-material

  # 删除 Material UI
  npm uninstall @mui/material
  ```

- **使用方法**

  - 注意：组件依赖于 React 不同版本，要根据时下官网进行安装

  - 此方法以 Material Icons 中的 App Bar 组件为例

  - [安装组件库 Material UI](https://mui.com/material-ui/getting-started/installation/)

    ```bash
    cd PATH/TO/PROJECT_FILE
    npm install @mui/material @emotion/react @emotion/styled
    ```

  - [安装图标类 Material Icons](https://mui.com/material-ui/material-icons/)

    ```bash
    cd PATH/TO/PROJECT_FILE
    npm install @mui/icons-material
    ```

  - [官网搜索 App Bar，复制代码](https://mui.com/material-ui/react-app-bar/)

  - `src` 文件夹下创建 `components` 文件夹，在里面创建组件文件 `Appbar.js`，粘贴代码

  - 在主程序文件内引入组件文件 `Appbar.js`，并以标签形式调用 Appbar.js 中的函数

## 主程序文件

- 主程序文件 App.js 有一个主函数，以标签形式调用组件的函数，自项目 student-springboot-react-frontend

  ```js
  import "./App.css";
  // 引入 Appbar.js 文件
  import Appbar from "./components/Appbar";
  // 引入 Student.js 文件
  import Student from "./components/Student";
  
  // APP 主函数
  function App() {
    return (
      <div className="App">
        {/* 调用 Appbar.js 中的 Appbar 函数 */}
        <Appbar />
  
        {/* 调用 Student.js 中的 Student 函数 */}
        <Student />
      </div>
    );
  }
  export default App;
  ```

## Router

- From project `Login-flask-react`

- Jump to another page

  ```javascript
  import React, { useState } from "react";
  import axios from "axios";
  import {
    BrowserRouter as Router,
    Routes,
    Route,
    Navigate,
  } from "react-router-dom";
  import Login from "./components/Login";
  import Home from "./components/Home";
  
  const App = () => {
    const [isLoggedIn, setIsLoggedIn] = useState(false);
  
    const handleLoginSuccess = () => {
      setIsLoggedIn(true);
    };
  
    return (
      <Router>
        <Routes>
          {/*如果未登录直接访问 Home 页面，则跳转至登录页面*/}
          <Route
            path="/"
            element={
              isLoggedIn ? (
                <Navigate to="/home" />
              ) : (
                <Login onLogin={handleLoginSuccess} />
              )
            }
          />
          <Route
            path="/home"
            element={isLoggedIn ? <Home /> : <Navigate to="/" />}
          />
        </Routes>
      </Router>
    );
  };
  
  export default App;
  ```

# `vite.config.js`

Vite 跨域代理 `vite.config.js`，用于直接本地运行（**非容器化部署**）时的前后端通信。

`todo-fullstack-gitops` 项目中的示例：将前端 `/api` 开头的请求转发到 http://localhost:5000 后端服务。

1. 前端请求: `/api/todos`
2. Vite 代理匹配到 `/api` 前缀
3. 转发到: http://localhost:5000/api/todos

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:5000',
        changeOrigin: true
      }
    }
  }
})
```

# 处理方法

## POST 和 GET

源自项目 `student-springboot-react-frontend`

```js
const paperStyle = { padding: "50px 20px", width: 600, margin: "20px auto" };

// POST
const [name, setName] = React.useState("");
const [address, setAddress] = React.useState("");
const handleClick = (e) => {
  e.preventDefault();
  const student = { name, address };
  console.log(student);
  fetch("http://localhost:8080/student/add", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(student),
  }).then(() => {
    console.log("New Student added");
  });
};

// GET
const [students, setStudents] = React.useState([]);
React.useEffect(() => {
  fetch("http://localhost:8080/student/getAll")
    .then((res) => res.json())
    .then((result) => {
      setStudents(result);
    });
});
```
