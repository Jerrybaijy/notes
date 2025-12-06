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
---

# React

[**React**](https://zh-hans.react.dev/) 是一个用于构建用户界面的 JavaScript 库，由 Facebook 开发。

## 基本流程

- **创建项目**

  - Node.js 已安装，npm 更新至最新版

  - 创建 React 项目

    ```bash
    npx create-react-app PROJECT_NAME
    ```

  - 安装组件库

  - 编写主程序文件和组件文件

- **本地测试**

  - 后端与数据库已启动

  - 调试源文件

    ```bash
    npm start
    ```

- **生成静态文件**

  - 在项目的根目录中运行 npm 命令，这将项目根目录中生成一个名为 `build` 的静态文件夹。

    ```bash
    npm run build
    ```

  - 将 `.gitignore` 中的 build 注释掉

- **生成 Image**

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

- React 管理

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

# Vite

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

- 源自项目 student-springboot-react-frontend

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

# React 项目

- Student Spring Boot React Full Stack
- Login Flask React
