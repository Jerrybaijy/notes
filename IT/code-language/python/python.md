**参考**：

> [我要自学网：燎原《Python编程入门2021新版教程》](https://www.51zxw.net/List.aspx?cid=929)
>
> [B站：银角大王-武沛齐《精品 Python全套教程》](https://www.bilibili.com/video/BV1zd4y1y7px/?spm_id_from=333.337.search-card.all.click&vd_source=02dd98cfbf740b256dca0ec3e66776e6)

# Python 基础

## 环境搭建

1. 以 Python3.9.2 为例

2. 双击解压包 python-3.9.2-amd64 运行

3. 勾选 `Add Python 3.9 to PATH`

   <img src="assets/image-20231026224146549.png" alt="图片1" style="zoom:33%;" />

4. 安装成功，点击 `Close`

   <img src="assets/image-20231026224550908.png" alt="图片1" style="zoom: 33%;" />

## 配置

- **关于安装目录**
  - `Lib`：存放模块
  - `site-packages`：存放第三方模块
  
- **帮助**

  - Python 已加入环境变量
  - 进入终端
  - **列出模块中的函数**

    ```python
    > python
    > import urllib
    > dir(urllib)
    ```
  
  - **查看完整的python内置函数清单**

    ```python
    > dir(__builtins__)
    ```
  
  - **查看某个函数的文档帮助信息**

    ```python
    > help(sum)
    ```
  

## Pip

- Pip 是 Python 的包管理工具
- **常用命令**

  ```bash
  # 查看 pip 版本
  pip --version
  # 升级 pip
  python -m pip install --upgrade pip
  
  # 查看 pip 下载源
  pip config get global.index-url
  # 设置 pip 下载源
  pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/
  
  # 查看已经安装的第三方模块
  pip list
  # 安装模块（选项为指定下载源）
  pip install [-i https://pypi.tuna.tsinghua.edu.cn/simple] $MODULE_NAME
  # 卸载第三方模块
  pip uninstall $MODULE_NAME
  # 显示模块信息
  pip show $MODULE_NAME
  ```

## 编辑器

### IDLE

- **IDLE**（Integrated Development and Learning Environment，集成开发和学习环境），是一款 Python 自带的 IDE，稳定但界面不好；
- 打开 `IDME`，新建文件，新窗口编写代码，原窗口运行代码；

- 保存代码为文件，文件后缀名 `.py`，注意先保存后执行；

- 光标在“编写代码”窗口，按 `F5` 运行代码，“运行代码”窗口有显示运行结果。

### Pycharm

PyCharm 是由 JetBrains 开发的一款 Python IDE。它提供了丰富的功能和工具，包括代码编辑器、调试器、版本控制工具、代码分析、自动完成、重构、单元测试等，以帮助开发者提高 Python 开发的效率和质量。

PyCharm 有商业版和社区版两个版本。

#### 安装

1. [官网下载社区免费版 `PyCharm Community Edition`](https://www.jetbrains.com/pycharm/download/?section=windows)

2. 勾选如图 2 项

3. 继续安装直到 `Finish`

   <img src="assets/image-20231026230614766.png" alt="图片1" style="zoom:50%;" />


####  破解

1. [官网下载商业版 `Pycharm Professional`](https://www.jetbrains.com/pycharm/download/?section=windows)；
2. 默认安装，安装完成后不要立即运行；
3. 以下破解方法来源于 [`小墨の博客`](https://www.only4.work/blog/?id=473)；
4. 博客地址或网盘下载并解压激活工具 `【请解压】JetBrains 2023.1 永久激活插件`；
5. 为了避免路径问题，请将解压后的文件夹到本地一个没有中文以及特殊符号的路径下，且配置后不能移动和删除；

   <img src="assets/image-20231026232300636.png" alt="图片1" style="zoom: 50%;" />

6. `jetbra` > `scripts` > 双击运行 `install-all-users.vbs` 脚本 > 出现 `done` 弹框，说明成功；
7. 由于存在环境变量配置，插件安装之后，需要重启电脑才会生效。
8. 重启后，在博客内获取激活码；
9. 最后一次获取到的是：

   ```
   # Pycharm
   EUWT4EE9X2-eyJsaWNlbnNlSWQiOiJFVVdUNEVFOVgyIiwibGljZW5zZWVOYW1lIjoic2lnbnVwIHNjb290ZXIiLCJhc3NpZ25lZU5hbWUiOiIiLCJhc3NpZ25lZUVtYWlsIjoiIiwibGljZW5zZVJlc3RyaWN0aW9uIjoiIiwiY2hlY2tDb25jdXJyZW50VXNlIjpmYWxzZSwicHJvZHVjdHMiOlt7ImNvZGUiOiJQU0kiLCJmYWxsYmFja0RhdGUiOiIyMDI1LTA4LTAxIiwicGFpZFVwVG8iOiIyMDI1LTA4LTAxIiwiZXh0ZW5kZWQiOnRydWV9LHsiY29kZSI6IlBDIiwiZmFsbGJhY2tEYXRlIjoiMjAyNS0wOC0wMSIsInBhaWRVcFRvIjoiMjAyNS0wOC0wMSIsImV4dGVuZGVkIjpmYWxzZX0seyJjb2RlIjoiUFBDIiwiZmFsbGJhY2tEYXRlIjoiMjAyNS0wOC0wMSIsInBhaWRVcFRvIjoiMjAyNS0wOC0wMSIsImV4dGVuZGVkIjp0cnVlfSx7ImNvZGUiOiJQV1MiLCJmYWxsYmFja0RhdGUiOiIyMDI1LTA4LTAxIiwicGFpZFVwVG8iOiIyMDI1LTA4LTAxIiwiZXh0ZW5kZWQiOnRydWV9LHsiY29kZSI6IlBDV01QIiwiZmFsbGJhY2tEYXRlIjoiMjAyNS0wOC0wMSIsInBhaWRVcFRvIjoiMjAyNS0wOC0wMSIsImV4dGVuZGVkIjp0cnVlfV0sIm1ldGFkYXRhIjoiMDEyMDIyMDkwMlBTQU4wMDAwMDUiLCJoYXNoIjoiVFJJQUw6MzUzOTQ0NTE3IiwiZ3JhY2VQZXJpb2REYXlzIjo3LCJhdXRvUHJvbG9uZ2F0ZWQiOmZhbHNlLCJpc0F1dG9Qcm9sb25nYXRlZCI6ZmFsc2V9-FT9l1nyyF9EyNmlelrLP9rGtugZ6sEs3CkYIKqGgSi608LIamge623nLLjI8f6O4EdbCfjJcPXLxklUe1O/5ASO3JnbPFUBYUEebCWZPgPfIdjw7hfA1PsGUdw1SBvh4BEWCMVVJWVtc9ktE+gQ8ldugYjXs0s34xaWjjfolJn2V4f4lnnCv0pikF7Ig/Bsyd/8bsySBJ54Uy9dkEsBUFJzqYSfR7Z/xsrACGFgq96ZsifnAnnOvfGbRX8Q8IIu0zDbNh7smxOwrz2odmL72UaU51A5YaOcPSXRM9uyqCnSp/ENLzkQa/B9RNO+VA7kCsj3MlJWJp5Sotn5spyV+gA==-MIIETDCCAjSgAwIBAgIBDTANBgkqhkiG9w0BAQsFADAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBMB4XDTIwMTAxOTA5MDU1M1oXDTIyMTAyMTA5MDU1M1owHzEdMBsGA1UEAwwUcHJvZDJ5LWZyb20tMjAyMDEwMTkwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCUlaUFc1wf+CfY9wzFWEL2euKQ5nswqb57V8QZG7d7RoR6rwYUIXseTOAFq210oMEe++LCjzKDuqwDfsyhgDNTgZBPAaC4vUU2oy+XR+Fq8nBixWIsH668HeOnRK6RRhsr0rJzRB95aZ3EAPzBuQ2qPaNGm17pAX0Rd6MPRgjp75IWwI9eA6aMEdPQEVN7uyOtM5zSsjoj79Lbu1fjShOnQZuJcsV8tqnayeFkNzv2LTOlofU/Tbx502Ro073gGjoeRzNvrynAP03pL486P3KCAyiNPhDs2z8/COMrxRlZW5mfzo0xsK0dQGNH3UoG/9RVwHG4eS8LFpMTR9oetHZBAgMBAAGjgZkwgZYwCQYDVR0TBAIwADAdBgNVHQ4EFgQUJNoRIpb1hUHAk0foMSNM9MCEAv8wSAYDVR0jBEEwP4AUo562SGdCEjZBvW3gubSgUouX8bOhHKQaMBgxFjAUBgNVBAMMDUpldFByb2ZpbGUgQ0GCCQDSbLGDsoN54TATBgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMCBaAwDQYJKoZIhvcNAQELBQADggIBABqRoNGxAQct9dQUFK8xqhiZaYPd30TlmCmSAaGJ0eBpvkVeqA2jGYhAQRqFiAlFC63JKvWvRZO1iRuWCEfUMkdqQ9VQPXziE/BlsOIgrL6RlJfuFcEZ8TK3syIfIGQZNCxYhLLUuet2HE6LJYPQ5c0jH4kDooRpcVZ4rBxNwddpctUO2te9UU5/FjhioZQsPvd92qOTsV+8Cyl2fvNhNKD1Uu9ff5AkVIQn4JU23ozdB/R5oUlebwaTE6WZNBs+TA/qPj+5/we9NH71WRB0hqUoLI2AKKyiPw++FtN4Su1vsdDlrAzDj9ILjpjJKA1ImuVcG329/WTYIKysZ1CWK3zATg9BeCUPAV1pQy8ToXOq+RSYen6winZ2OO93eyHv2Iw5kbn1dqfBw1BuTE29V2FJKicJSu8iEOpfoafwJISXmz1wnnWL3V/0NxTulfWsXugOoLfv0ZIBP1xH9kmf22jjQ2JiHhQZP7ZDsreRrOeIQ/c4yR8IQvMLfC0WKQqrHu5ZzXTH4NO3CwGWSlTY74kE91zXB5mwWAx1jig+UXYc2w4RkVhy0//lOmVya/PEepuuTTI4+UJwC7qbVlh5zfhj8oTNUXgN0AOc+Q0/WFPl1aw5VV/VrO8FCoB15lFVlpKaQ1Yh+DVU8ke+rt9Th0BCHXe0uZOEmH0nOnH/0onD
   
   # IDEA
   6G5NXCPJZB-eyJsaWNlbnNlSWQiOiI2RzVOWENQSlpCIiwibGljZW5zZWVOYW1lIjoic2lnbnVwIHNjb290ZXIiLCJhc3NpZ25lZU5hbWUiOiIiLCJhc3NpZ25lZUVtYWlsIjoiIiwibGljZW5zZVJlc3RyaWN0aW9uIjoiIiwiY2hlY2tDb25jdXJyZW50VXNlIjpmYWxzZSwicHJvZHVjdHMiOlt7ImNvZGUiOiJQU0kiLCJmYWxsYmFja0RhdGUiOiIyMDI1LTA4LTAxIiwicGFpZFVwVG8iOiIyMDI1LTA4LTAxIiwiZXh0ZW5kZWQiOnRydWV9LHsiY29kZSI6IlBEQiIsImZhbGxiYWNrRGF0ZSI6IjIwMjUtMDgtMDEiLCJwYWlkVXBUbyI6IjIwMjUtMDgtMDEiLCJleHRlbmRlZCI6dHJ1ZX0seyJjb2RlIjoiSUkiLCJmYWxsYmFja0RhdGUiOiIyMDI1LTA4LTAxIiwicGFpZFVwVG8iOiIyMDI1LTA4LTAxIiwiZXh0ZW5kZWQiOmZhbHNlfSx7ImNvZGUiOiJQUEMiLCJmYWxsYmFja0RhdGUiOiIyMDI1LTA4LTAxIiwicGFpZFVwVG8iOiIyMDI1LTA4LTAxIiwiZXh0ZW5kZWQiOnRydWV9LHsiY29kZSI6IlBHTyIsImZhbGxiYWNrRGF0ZSI6IjIwMjUtMDgtMDEiLCJwYWlkVXBUbyI6IjIwMjUtMDgtMDEiLCJleHRlbmRlZCI6dHJ1ZX0seyJjb2RlIjoiUFNXIiwiZmFsbGJhY2tEYXRlIjoiMjAyNS0wOC0wMSIsInBhaWRVcFRvIjoiMjAyNS0wOC0wMSIsImV4dGVuZGVkIjp0cnVlfSx7ImNvZGUiOiJQV1MiLCJmYWxsYmFja0RhdGUiOiIyMDI1LTA4LTAxIiwicGFpZFVwVG8iOiIyMDI1LTA4LTAxIiwiZXh0ZW5kZWQiOnRydWV9LHsiY29kZSI6IlBQUyIsImZhbGxiYWNrRGF0ZSI6IjIwMjUtMDgtMDEiLCJwYWlkVXBUbyI6IjIwMjUtMDgtMDEiLCJleHRlbmRlZCI6dHJ1ZX0seyJjb2RlIjoiUFJCIiwiZmFsbGJhY2tEYXRlIjoiMjAyNS0wOC0wMSIsInBhaWRVcFRvIjoiMjAyNS0wOC0wMSIsImV4dGVuZGVkIjp0cnVlfSx7ImNvZGUiOiJQQ1dNUCIsImZhbGxiYWNrRGF0ZSI6IjIwMjUtMDgtMDEiLCJwYWlkVXBUbyI6IjIwMjUtMDgtMDEiLCJleHRlbmRlZCI6dHJ1ZX1dLCJtZXRhZGF0YSI6IjAxMjAyMjA5MDJQU0FOMDAwMDA1IiwiaGFzaCI6IlRSSUFMOi0xMDc4MzkwNTY4IiwiZ3JhY2VQZXJpb2REYXlzIjo3LCJhdXRvUHJvbG9uZ2F0ZWQiOmZhbHNlLCJpc0F1dG9Qcm9sb25nYXRlZCI6ZmFsc2V9-SnRVlQQR1/9nxZ2AXsQ0seYwU5OjaiUMXrnQIIdNRvykzqQ0Q+vjXlmO7iAUwhwlsyfoMrLuvmLYwoD7fV8Mpz9Gs2gsTR8DfSHuAdvZlFENlIuFoIqyO8BneM9paD0yLxiqxy/WWuOqW6c1v9ubbfdT6z9UnzSUjPKlsjXfq9J2gcDALrv9E0RPTOZqKfnsg7PF0wNQ0/d00dy1k3zI+zJyTRpDxkCaGgijlY/LZ/wqd/kRfcbQuRzdJ/JXa3nj26rACqykKXaBH5thuvkTyySOpZwZMJVJyW7B7ro/hkFCljZug3K+bTw5VwySzJtDcQ9tDYuu0zSAeXrcv2qrOg==-MIIETDCCAjSgAwIBAgIBDTANBgkqhkiG9w0BAQsFADAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBMB4XDTIwMTAxOTA5MDU1M1oXDTIyMTAyMTA5MDU1M1owHzEdMBsGA1UEAwwUcHJvZDJ5LWZyb20tMjAyMDEwMTkwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCUlaUFc1wf+CfY9wzFWEL2euKQ5nswqb57V8QZG7d7RoR6rwYUIXseTOAFq210oMEe++LCjzKDuqwDfsyhgDNTgZBPAaC4vUU2oy+XR+Fq8nBixWIsH668HeOnRK6RRhsr0rJzRB95aZ3EAPzBuQ2qPaNGm17pAX0Rd6MPRgjp75IWwI9eA6aMEdPQEVN7uyOtM5zSsjoj79Lbu1fjShOnQZuJcsV8tqnayeFkNzv2LTOlofU/Tbx502Ro073gGjoeRzNvrynAP03pL486P3KCAyiNPhDs2z8/COMrxRlZW5mfzo0xsK0dQGNH3UoG/9RVwHG4eS8LFpMTR9oetHZBAgMBAAGjgZkwgZYwCQYDVR0TBAIwADAdBgNVHQ4EFgQUJNoRIpb1hUHAk0foMSNM9MCEAv8wSAYDVR0jBEEwP4AUo562SGdCEjZBvW3gubSgUouX8bOhHKQaMBgxFjAUBgNVBAMMDUpldFByb2ZpbGUgQ0GCCQDSbLGDsoN54TATBgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMCBaAwDQYJKoZIhvcNAQELBQADggIBABqRoNGxAQct9dQUFK8xqhiZaYPd30TlmCmSAaGJ0eBpvkVeqA2jGYhAQRqFiAlFC63JKvWvRZO1iRuWCEfUMkdqQ9VQPXziE/BlsOIgrL6RlJfuFcEZ8TK3syIfIGQZNCxYhLLUuet2HE6LJYPQ5c0jH4kDooRpcVZ4rBxNwddpctUO2te9UU5/FjhioZQsPvd92qOTsV+8Cyl2fvNhNKD1Uu9ff5AkVIQn4JU23ozdB/R5oUlebwaTE6WZNBs+TA/qPj+5/we9NH71WRB0hqUoLI2AKKyiPw++FtN4Su1vsdDlrAzDj9ILjpjJKA1ImuVcG329/WTYIKysZ1CWK3zATg9BeCUPAV1pQy8ToXOq+RSYen6winZ2OO93eyHv2Iw5kbn1dqfBw1BuTE29V2FJKicJSu8iEOpfoafwJISXmz1wnnWL3V/0NxTulfWsXugOoLfv0ZIBP1xH9kmf22jjQ2JiHhQZP7ZDsreRrOeIQ/c4yR8IQvMLfC0WKQqrHu5ZzXTH4NO3CwGWSlTY74kE91zXB5mwWAx1jig+UXYc2w4RkVhy0//lOmVya/PEepuuTTI4+UJwC7qbVlh5zfhj8oTNUXgN0AOc+Q0/WFPl1aw5VV/VrO8FCoB15lFVlpKaQ1Yh+DVU8ke+rt9Th0BCHXe0uZOEmH0nOnH/0onD
   ```

   <img src="assets/image-20231026232934381.png" alt="图片1" style="zoom:50%;" />

10. 此时运行 PyCharm Professional，在 `activation code` 选项下，填入最新激活码，点击 `Activate` 就能完成激活了；
11. 注意激活以后，不要移动或删除激活插件文件夹；
12. 查看激活状态：`Help` > `About`

    <img src="assets/image-20231026233121030.png" alt="图片1" style="zoom:50%;" />

#### 配置

- **快捷键**：`Ctrl + Alt + S` > `File` > `Settings`

- **自动保存**：`Ctrl + Alt + S` > `Appearance & Behavior` > `System Settings` > `Autosave`

- **缩进**
  1. `Main menu` > `Settings` > `Editor` > `Code Style` > `Python`
  2. 设置 `Tab size` `Indent` `Continuation indent` 三项为 `2`
  
- **鼠标滚轮**
  1. `Main menu` > `Settings` > `Editor` > `General` > `Mouse Control` 选项
  2. `Change font size with Ctrl + Mouse Wheel` 打上对勾
  3. `All editors` 打勾

- **设置代码字体大小**
  1. `Main menu` > `Settings` > `Editor` > `Font`
  
  2. `Size = 24`，`Line Height = 1.2`
  
  3. 如果设置不生效，`Main menu` > `Settings` > `Editor` > `Color Scheme` > `Color Scheme Font` > 取消勾选  `Use color scheme font instead of the default`
  
- **汉化**
  1. `Main menu` > `Settings` > `Plugins`，搜索 `Chinese`，`Install` 安装汉化包。软件重启即汉化版
  
- **代码格式化**

  1. `Main menu` > `Settings` > `Editor` > `Code Style` > `Python` > `Space` 选项卡
  2. `在命名形参中的 = 周围` 和 `在关键字实参中的 = 周围` 两项打勾，保存。
  3. 编辑完代码按 `Ctrl + Shift + L`，可实现自动更正空格格式。注意注释部分不会被更正

- **安装主题**：`主菜单` > `设置` > `外观与行为` > `外观` > `获取更多主题`

- **创建文件**

  1. `项目路径右键` > `New` > `Python Fire` > 给文件命名 > `Enter`；
  2. 编写代码，自动保存；
  3. 运行：（1、项目栏，2、右键，3、快捷键）快捷键：`Ctrl + Shift + F10`。

- **同一项目添加多个文件夹**

  1. `Settings` > `Project` > `Project Structure`
  2. 右侧 `Add Content Root` > `选择要添加的文件夹` > `OK`

- **将 Terminal 默认项切换至 cmd**
  1. Terminal 可以模拟 cmd
  2. `Settings` > `Tools` > `Terminal` > `Shell path` 下拉菜单，`切换至 cmd`
  
- **无法调用第三方模块**

  1. `Settings` > `Project：当前文件名` > `Python Interpreter` > `右侧Add Interpreter` > `Existing` > `右侧…`
  2. 找到 `python.exe/` 将 `python.exe` 拖入窗口 > `OK`


#### 创建项目

- 项目环境

  - **`Previously configured interpreter`**：已存在环境，使用全局的 Python 解释器，正常无法使用虚拟环境的依赖。
  
  - **`Viutualenv`**：虚拟环境，与全局环境隔离，不影响全局，可以使用全局环境依赖。
  
    <img src="assets/image-20240322004048261.png" alt="图片1" style="zoom:50%;" />
  

### Sublime

Sublime- Text 是一个用 C++ 和 Python 开发的跨平台文本编辑器。除了 Python 之外，它还提供对其他语言的支持。Sublime 有自己的包管理器，开发者可以用来安装组件，插件和额外样式。与 PyCharm、VS Code 不同，Sublime Text 并没有集成开发环境，而是作为一个纯粹的编辑器，提供了快速、便捷的编辑功能。特点：第三方，轻量化，界面好，支持常见所有语言。

- **安装 Sublime**
  
  1. 默认所有选项安装 Sublime
  2. Sublime 原生环境不支持 `input` 语句的执行，所以要安装 `SublimeREPL` 插件。
  
- **安装 SublimeREPL 插件**
  
  1. `Ctrl+shift+P` 打开命令面板，输入 `install`，选择 `Package Control：Install Package`
  
    - 程序包控件，安装程序包，需要等待一下，看左下角有 `=` 左右动；
    - 注意，如果没有这个选项，需要先安装 `Package Control`，点击 `Install Package Control`，等待安装，提示安装成功后再重新按 `Ctrl+shift+P` 选择 `Package Control：Install Package`；
  
  2. 过一会 `=` 消失，弹出窗口，搜索 `SublimeREPL`，点击下载；
  
  3. 安装成功后，在 `Tools` 选项里出现 `SublimeREPL`，表明安装成功；
  
  4. 设置快捷键
  
  	- 首先点击首选项 `preference`
  
  	- 其次打开快捷键设置 `key bindings`
  
  	- 在两个中括号之间那行，粘贴输入下面代码
  
  		```json
  		{"keys": ["f5"],
  		"caption": "SublimeREPL: Python - RUN current file",
  		"command": "run_existing_window_command",
  		"args": {
  		"id": "repl_python_run",
  		"file": "config/Python/Main.sublime-menu"}}
  		```
  
  	- 关闭快捷键设置页面，重启 `Sublime` 软件。
  
  	  - 需要注意，`input` 语句在 Sublime 中执行，需要按快捷键 `F5`，并且新跳出一个窗口显示。
  
- **卸载 SublimeREPL 插件**
	1. `Ctrl+shift + p`，输入框中输入`remove package`；
	2. 下面会有提示，直接点击或者输入后回车。

- **创建文件**
	- 右下角单击选择 `Python`；

	- 编写代码，保存：`文件名.py`；
	- 运行：`Ctrl + B`（第一次选择 `Python`）。

## 代码规范

- 除以下规范，其余同编程语言通用规范。

- **缩进**：敏感

  - Python 最具特色的就是使用缩进来表示代码块，不需要使用大括号 **`{}`** 。

  - 缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数。

- **分号**：每行代码结束不使用分号

## 标识符

- 除以下规范，其余同编程语言通用规范。
- **规范**
  - 只能含有字母、数字、下划线，且不能以数字开头

  - 大小写敏感

  - 不能是关键字和保留字
  
- **命名习惯**
  - **变量名**：小蛇形，例 `max_length`。
  - **函数名**：小蛇形，例 `max_length`；Python 中可以使用中文作为变量名。
  - **类名**：大驼峰，例 `MyFirstJavaClass`。
  - **文件名**：Python 文件名不要使用 `-`，因为将文件作为模块引入时，如果模块名中包含破折号，可能会导致一些问题。
  - **环境变量**：大蛇形，例 `MAX_LENGTH`。

## 注释

- **单行注释**：`Ctrl + /`

  ``` python
  # 这是一个单行注释
  a = 5
  b = 6
  print(a + b)
  '''
  多行注释第一行
  多行注释第二行
  多行注释第三行
  '''
  ```

## 变量

- Python 无需使用关键字声明变量

## 输入与输出

- **input() 输入**：`input()` 的返回结果为 `字符串`

  ```python
  uname = input("请输入用户名")  # 提示并输入
  print("你的用户名：" + uname)  # 返回结果
  ```

  ```python
  input("按回车继续")  # 程序停顿，按回车继续
  ```

- **print() 输出**

  ```python
  print("a")  # a
  ```
  
  - **说明**
  	- 如果输出内容为字符串，加 `双/单引号`。
  	- `a` 可以是拼接数据
  	- `print("内容", end = "")`：多行 `print` 显示结果不换行

## 其它基础

- **pass**：什么都不执行，补充代码完整性。
- Python 中二、八、十六进制之间不能直接转换，需通过十进制。

### 数据的拼接

此部分不要作为所有代码语言通用学习内容，只是为了留存最初学编程时的困惑。

- **数据的拼接**

	- 数据的拼接就是通过拼接方式，将多个数据拼接成一整个数据。
	- 相同类型数据可以用逗号和加号拼接；
	- 不同数据类型只能用逗号拼接；
	- 字符串的拼接效率很低，尽量将字符串加到空列表，再通过 `"".join(LIST)` 拼接。

- **`+` 操作符**：只能拼接字符串，且拼接结果仍是字符串，显示结果无间隔。

	```python
	a1 = "张三"
	a2 = "李四"
	c = a1 + "爱" + a2
	print(c)  # 张三爱李四
	```

- **`,` 拼接**：实质不是拼接，只是用在将多个数据打印在一句话内，拼接结果是一个元组，直接打印拼接内容显示结果有间隔。

	```python
	name = "张三"
	age = 22
	data = "我叫", name,"今年",age,"岁"
	print(data) # ('我叫', '张三', '今年', 22, '岁')
	print("我叫", name,"今年",age,"岁") # 我叫 张三 今年 22 岁
	```

- **`f-string` 拼接，推荐**

	```python
	name = "张三"
	age = 22
	hobby = "看书"
	data = f"我叫{name}，今年{age}岁，爱好是{hobby}"
	print(data)  # 我叫张三，今年22岁，爱好是看书
	```

- **其它拼接方式**

	```python
	# format 函数拼接
	s1 = "hello!{}{}{}".format("张三","李四",666)  # 可拼接 int 类型 666
	print(s1)  # hello!张三李四666
	
	# 使用 % 拼接
	s1 = "hello!%s%s%s"%("张三", "李四", 666)
	print(s1)  # hello!张三李四666
	```

# 数据类型

## 内置数据类型

- **数字类型**
	- **`int`**：整型
	- **`float`**：浮点型
	- **`complex`**：复数
- **布尔类型**
	- **`bool`**：布尔型
- **序列类型**
	- **`str`**：字符串
	- **`list`**：列表
	- **`tuple`**：元组
	- **`range`**：范围
- **集合类型**
	- **`set`**：集合
	- **`frozenset`**：冻结集合
- **映射类型**
	- **`dict`**：字典
- **二进制类型**
	- **`bytes`**：字节
	- **`bytearray`**：字节数组
	- **`memoryview`**：内存视图
- **空值类型**
	- **`NoneType`**：空值，只有一个值 `None`。
- **函数和对象类型**
  - **`object`**：对象
  - **`function`**：函数（属于特殊的对象）
  - **`module`**：模块（属于特殊的对象）

- **自定义类型**
  - 使用类（`class`）可以定义自定义数据类型。

## 整型 `int`

- **定义**：表示整数，属于不可变数据类型。

	```python
	a = 5
	b = 128
	print(a * 2 + b + 5) # 143
	```

## 浮点型 `float`

- **定义**：表示小数，属于不可变数据类型。

  ```python
  c = 3.14
  d = 5.5
  print(c + d) # 8.64
  ```

- **说明**：浮点数参与数学运算可能会产生误差。

## 布尔型 `bool`

- Python 中布尔值首字母**大写**：`True` 和 `False`。

## 字符串 `str`

### 字符串基础

- Python 中字符串作为值，原变量的值不支持修改，处理之后的值可作为新值赋给新的变量，详见数据类型的特殊说明；
- 特性：只可存放普通字符；元素可重复；有序索引（下标）；可切片；元素不支持修改；
- **常用功能**

  ```python
  # 其它公共功能：...
  
  lst = ["中国", ["上海", "北京", "深圳"], 123]
  strr = " ad min.123 "
  
  len(strr)  # 获取长度
  
  strr[0]  # 索引
  
  lst[0][1]  # 多级索引
  
  strr[0:6:2]  # 切片
  
  if "中国" in strr:  # in 包含
      pass
  
  strr.replace("a", "A")  # 替换
  
  strr.split(".", 1)  # 切割
  
  strr.strip()  # 去除空格/换行
  
  strr.upper()  # 转大写
  
  strr.startswith("a")  # 判断开头
  
  strr.isdecimal()  # 判断数字
  ```

### 获取长度 `len`

- **语法**：`len(STR)`，返回 `int`。

  ``` python
  len_a = len("中国江西联通")
  print(len_a)  # 6
  print(type len_a)  # <class 'int'>
  ```

### 索引

- **一级索引**：`STR/CONTAINER[INDEX]`，字符串返回 `str`，容器返回元素。

  ``` python
  #       0 1 2 3 4 5，正向索引号
  #      -6-5-4-3-2-1，逆向索引号
  strr = "中国江西联通"
  print(strr[0])  # 中
  print(strr[-6])  # 中
  print(type(strr[0]))  # <class 'str'>
  ```

- **多级索引**：`STR/CONTAINER[INDEX1][INDEX2]...`

  ``` python
  lst = ["中国", ["上海", "北京", "深圳"], 123]
  data1 = lst[1][0]
  data2 = lst[1][0][0]
  print(data1)  # 上海
  print(data2)  # 上
  ```

- **实际示例**

  ``` python
  strr = "中国江西联通"
  index = 0  # index为索引号
  while index < len(strr):
      data = strr[index]
      print(data)
      index += 1
  # 依次打印“中国江西联通”
  ```

### 遍历

详见 [for 循环](#for 循环)

### `in` 包含

- **定义**：`in` 包含
- **语法**：`STR in STR`

  ``` python
  strr = "中国联通"
  res = "中国" in strr
  print(res)  # True
  
  # use
  if "中国" in strr:
      pass
  ```

### 切片

- **语法**：`STR[INDEX_START:INDEX_END:STEP_VALUE]`，返回 `str`。

  ``` python
  #      0 1 2 3 4 5，正向索引号
  strr = "中国江西联通"
  print(strr[2:4])  # 江西
  print(strr[0:6:2])  # 中江联
  print(strr[2:])  # 江西联通
  print(strr[:4])  # 中国江西
  ```

### 切割 `split`

- `STR.split("SEPARATOR"[, MAX_SPLIT])`，返回 `list`。

  ``` python
  # 切割后会得到一个列表
  
  strr = "马化腾,40,XXXX@qq.com"
  res1 = strr.split(",")  # 把所有序列都切割，分别放入子字符串，逗号是切割标识依据
  res2 = strr.split(".")  # "."为切割标识
  res3 = strr.split(",", 1)  # 从左到右，保留几个单独子字符串，剩余放进另一个子字符串
  res4 = strr.rsplit(",", 1)  # 从右到左，保留几个单独元素，剩余放进另一个子字符串
  
  print(res1)  # ['马化腾', '40', 'XXXX@qq.com']
  print(res1[1])  # 40  # 拿到单独一个元素
  print(res2)  # ['马化腾,40,XXXX@qq', 'com']
  print(res3)  # ['马化腾', '40,XXXX@qq.com']
  print(res4)  # ['马化腾,40', 'XXXX@qq.com']
  ```

### 合并 `f-string`

- **语法**：`f"{任意数据类型}{任意数据类型}..."`，返回 `str`。

	```python
	name = "张三"
	age = 22
	hobby = "看书"
	data = f"我叫{name}，今年{age}岁，爱好是{hobby}"
	print(data)  # 我叫张三，今年22岁，爱好是看书
	```

### 模版字符串 `f-string`

- Python 中不支持反引号表示模版字符串，而是使用 `f-string` 代替。
- **跨行输出**

	```python
	# 用双引号包围的字符串，每行后面加反斜杠，可以分多行书写，但在一行输出
	a = "今天天气真不错\
	真不错啊\
	真不错"
	print(a)  # 天气真不错真不错啊真不错
	
	# 用三个双引号包围的字符串，分多行书写，在多行输出
	b = f"""今天天气真不错
	真不错啊
	真不错"""
	print(b)  # 分多行输出
	# 天气真不错
	# 真不错啊
	# 真不错
	```

- **嵌套变量 + 拼接**

	```python
	a = "你好"  # a 可以是任意数据类型
	b = f"{a}世界"
	print(b)  # 你好世界
	```

### 替换 `replace`

- **语法**：`STR.replace("STR_OLD", "STR_NEW")`，返回 `str`。

  ``` python
  strr = " 中国 联通 联通 "
  res = strr.replace("联通", "移动")
  print(res)  # " 中国 移动 移动 "
  ```

### 去空格、换行 `strip`

- **语法**：`STR.strip()`，返回 `str`。

  ```python
  strr = " 中国 联通 "
  
  res1 = strr.strip()  # 去除开头和接尾空格
  print(res1)  # "中国 联通"
  
  res2 = strr.lstrip()  # 去除开头空格
  print(res2)  # "中国 联通 "
  
  res3 = strr.rstrip()  # 去除接尾空格
  print(res3)  # " 中国 联通"
  ```

  ```python
  strr = "中国联通\n"
  print(strr)  # 中国联通（后面有换行）
  
  res4 = strr.strip()
  print(res4)  # 中国联通（后面没有换行）
  ```

- **说明**：`strip()` 不能去除中间的空格，去除中间空格应使用 `STR.replace(" ", "")`，将空格替换成空白。

### 转大小写

- **语法**

  - **转大写**：`STR.upper()`，返回 `str`。
  - **转小写**： `STR.lower()`，返回 `str`。

  ``` python
  strr = "abc"
  res = strr.upper()
  print(res)  # ABC
  ```

### 判断起始 `startwith`

- **语法**：`STR.startswith()`，返回 `str`。

  ``` python
  strr = "中国联通"
  res = strr.startswith("中国")
  print(res)  # True
  ```

### 判断数字 `isdecimal`

- **语法**：`STR.isdecimal()`，返回 `bool`。

  ``` python
  strr = "中国联通"
  res = strr.isdecimal()
  print(res)  # False
  ```

### 找下标 `find`

- **语法**：`STR.find("匹配项")`，返回 `int`。

	```python
	data = "中国江西联通中国"
	
	# 第一个匹配项
	print(data.find("国"))  # 1
	print(type(data.find("国")))  # <class 'int'>
	
	# 最后一个匹配项
	print(data.rfind("国"))  # 7
	
	# 错误的匹配项
	print(data.rfind("海"))  # -1
	```

## 列表 `list`

### 列表基础

- **特性**：详见 [`code-general` - `列表（数组）`](../code-general/code-general.md#列表（数组）)
- **语法**：`[ITEM1, ITEM2, ...]`

  ``` python
  lst = ["中国", "上海", 123]
  print(lst)  # ['中国', '上海', 123]
  print(type(lst))  # <class 'list'>
  ```

- **公共功能**

  - 以下功能详见字符串
  - 获取长度 `.length`
  - 索引
  - 遍历 `for-in 语句`
  - `in` 包含
  - 嵌套
  - 切片 `.slice()`
  - 合并 `.concat()`

- **其它功能**

  ```python
  lst = [1, 2, 3, 4]
  
  lst[0] = 5  # 修改
  
  lst.append(5)  # 追加
  
  lst.insert(1, "北京")  # 插入
  
  lst.remove(1)  # 删除
  
  lst.clear()  # 清空
  
  lst.reverse()  # 反转
  
  sorted(lst)  # 排序
  
  strr = "_".join(lst)  # join 连接
  ```

### 列表修改元素 `索引`

- **语法**：`LIST[INDEX] = ITEM_NEW`

  ``` python
  lst = [1, 2, 3, 4]
  lst[0] = 5
  print(lst)  # [5, 2, 3, 4]
  ```

### 列表追加元素 `append`

- **语法**：`LIST.append(ITEM_NEW)`

  ``` python
  lst = [1, 2, 3, 4]
  lst.append(5)
  lst.append(6)
  print(lst)  # [1, 2, 3, 4, 5, 6]
  ```

- **说明**：`append()` 方法每次只能追加1个元素

### 列表插入元素 `insert`

- **语法**：`LIST.insert(INDEX, ITEM_NEW)`

  ``` python
  lst = [1, 2, 3, 4]
  lst.insert(0, 5)  # 在第0索引号，插入 5
  print(lst)  # [5, 1, 2, 3, 4]
  ```

- **说明**：`insert()` 方法每次只能插入1个元素

### 列表删除元素 `remove`

- **语法**：`LIST.remove(ITEM)`

  ``` python
  lst = [1, 2, 3, 4]
  lst.remove(1)
  print(lst)  # [2, 3, 4]
  ```

- **说明**：`remove()` 方法每次只能删除1个元素

### 列表清空 `clear`

- **语法**：`LIST.clear()`

  ``` python
  lst = [1, 2, 3, 4]
  lst.clear()
  print(lst)  # []
  ```

### 列表反转 `reverse`

- **语法**：`LIST.reverse()`

  ``` python
  lst = [1, 2, 3, 4]
  lst.reverse()
  print(lst)  # [4, 3, 2, 1]
  ```

### 列表升序 `sorted`

- **语法**：`sorted(LIST[, OPTION])`

  ```python
  # 升序
  lst1 = [21, 21, 31, 32, 33, 5454, 46, 65, 6]
  res1 = sorted(lst1)
  print(res1)  # [6, 21, 21, 31, 32, 33, 46, 65, 5454]
  
  # 降序
  lst2 = [21, 21, 31, 32, 33, 5454, 46, 65, 6]
  res2 = sorted(lst2, reverse = True)  # 降序，增加反转为真
  print(res2)  # [5454, 65, 46, 33, 32, 31, 21, 21, 6]
  ```

- **说明**：默认按首字的 ASCII 码转十进制的大小排序，如果首字相同，则逐一往后对比。
- **扩展**：自定义排序标准，`sorted(列表名, key = 排序依据函数)`

  ```python
  list_name = ["2.提升", "1.基础", "10.总结", "3.高阶"]
  
  # 排序依据key  key值为lambda表达式：将前面的数字转整型作为返回值
  list_sorted = sorted(list_name, key = lambda x: int(x.split(".")[0]))
  
  print(list_sorted)  # ['1.基础', '2.提升', '3.高阶', '10.总结']  否则正常排序10应在2前面
  ```

### 列表连接 `join`

- **语法**：`"[SEPARATOR]".join(LIST)`

  ``` python
  lst = ["中国", "江西", "联通"]
  str = "_".join(lst)  # "_"为分隔符
  print(str)  # 中国_江西_联通
  print(type(str))  # <class 'str'>
  ```

- **说明**：在 Python 中，列表中所有元素必须是字符串。

## 元组 `tuple`

- **特性**：详见 [`code-general` - `元祖`](../code-general/code-general.md#元祖)
- **语法**：`(ITEM1, ITEM2, ...)`

  ``` python
  tpl = ("中国", "上海", 123)
  print(tpl)  # ('中国', '上海', 123)
  print(type(tpl))  # <class 'tuple'>
  ```

- **说明**：如果元组中只有一个元素，应该在后面多加一个逗号，否则会等同于给变量赋值，得到的结果就不是元组了

  ``` python
  tpl1 = ("中国")
  print(tpl1)  # 中国
  
  tpl2 = ("中国",)
  print(tpl2)  # ('中国',)
  ```
  
- **说明**：虽然元祖是不可变数据，但如果元组内部嵌套容器，该容器内部的元素可以修改

  ``` python
  tpl1 = ("中国", ["北京", "上海"], 123)
  tpl1[1][0] = "深圳"
  print(tpl1)  # ('中国', ['深圳', '上海'], 123)
  ```
  
- **元组公共功能**

	- 以下功能详见字符串
	- 获取长度 `.length`
	- 索引
	- 遍历 `for-in 语句`
	- `in` 包含 
	- 嵌套

## 集合 `set`

- **特性**：详见 [`code-general` - `集合`](../code-general/code-general.md#集合)
- **语法**：`{ITEM1, ITEM2, ...}`

  ```python
  st = {"中国", "上海", 123}
  print(st)  # {123, '上海', '中国'}
  print(type(st))  # <class 'seta'>
  ```

- **去重复值**：`set(CONTAINER)`

  ```python
  # 将其它容器转换成集合，再转换回该容器
  
  lst1 = [1, 2, 1, 1323, 2121, 2, 32323, 23, 23, 23]
  st = set(lst1)  # 将 list 转换成 set
  lst2 = list(st)  # 将 set 转换成 list
  print(lst1)  # [1, 2, 1, 1323, 2121, 2, 32323, 23, 23, 23]
  print(st)  # {1, 2, 32323, 2121, 1323, 23}
  print(lst2)  # [1, 2, 32323, 2121, 1323, 23]
  ```

- **集合运算**

  ```python
  st1 = {1, 2, 3, 4, 5, 6}
  st2 = {7, 8, 9, 4, 5, 6}
  
  # 获取交集，不能用加号
  print(st1 & st2)  # {4, 5, 6}
  
  # 获取并集
  print(st1 | st2)  # {1, 2, 3, 4, 5, 6, 7, 8, 9}
  
  # 获取差集
  print(st1 - st2)  # {1, 2, 3}
  ```

## 字典 `dict`

- **特性**：详见 [`code-general` - `字典`](../code-general/code-general.md#字典)
- **语法**：`{"KEY1": "VALUE1", "KEY1": "VALUE1", ...}`

  ```python
  dict_a = {"A": 1,"B": 2,"C": 3}
  print(dict_a)  # {'A': 1, 'B': 2, 'C': 3}
  print(type(dict_a))  # <class 'dict'>
  ```

- **公共功能**

  - 以下功能详见字符串
  - 获取长度 `.length`
  - 索引（用键作为索引）
  - 遍历 `for-in 语句`（获取到键）
  - `in` 包含 （判断键）
  - 嵌套

- **常用功能**

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  
  value = dict_a.get("name")  # 获取值
  
  dict_a["hobby"] = "reading"  # 修改值
  
  dict_a["gender"] = "male"  # 增加元素，就是给一个原本不存在的键赋值
  
  dict_a.pop("hobby")  # 删除元素
  
  for key in dict_a.keys():  # 获取所有键
      print(key)
  
  for value in dict_a.values():  # 获取所有值
      print(value)
  
  for key, value in dict_a.items():  # 获取所有键和值
      print(key, value)
  ```

### 获取值 `get`

- **语法**：`DICT.get("KEY")`

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  value = dict_a.get("name")
  print(value)  # ZhangSan
  ```

- **扩展**：`DICT[KEY]`，通过索引键获取值

	```python
	dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
	value = dict_a["name"]
	print(value)  # ZhangSan
	```

### 修改值

- **语法**：`DICT[KEY] = "VALUE"`，通过索引键修改值

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  dict_a["hobby"] = "reading"
  print(dict_a)  # {'name': 'ZhangSan', 'age': 18, 'hobby': 'reading'}
  ```

### 增加元素

- `$DICT[$KEY] = "$VALUE"`，即给一个原本不存在的键赋值

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  dict_a["gender"] = "male"
  print(dict_a)  # {'name': 'ZhangSan', 'age': 18, 'hobby': 'playBall', 'gender': 'male'}
  ```

### 删除元素 `pop`

- **语法1**：`$DICT.pop("$KEY")`

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  dict_a.pop("hobby")
  print(dict_a)  # {'name': 'ZhangSan', 'age': 18}
  ```

- **语法2**：`del $DICT["$KEY"]`

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  del dict_a["hobby"]
  print(dict_a)  # {'name': 'ZhangSan', 'age': 18}
  ```

### 获取所有键 `keys`

- **语法**：`DICT.keys()`

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  for x in dict_a.keys():
      print(x)  # 依次打印 name age hobby
  
  # v = dict_a.keys()
  # print(v)  # dict_keys(['name', 'age', 'hobby'])
  # print(type(v))  # <class 'dict_keys'>
  ```

- **扩展**：遍历

	```python
	dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
	for key in dict_a:
	    print(key)  # 依次打印 name age hobby
	```

### 获取所有值 `values`

- **语法**：`DICT.values()`

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  for value in dict_a.values():
      print(value)  # 依次打印 ZhangSan 18 playBall
  
  # value = dict_a.keys()
  # print(value)  # dict_keys(['name', 'age', 'hobby'])
  # print(type(value))  # <class 'dict_keys'>
  ```

- **扩展**：索引 + 遍历

	```python
	dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
	for key in dict_a:
	    print(dict_a[key])
	```

### 获取所有键和值 `items`

- **语法**：`DICT.items()`

  ```python
  dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
  for key, value in dict_a.items():
      print(key, value)  # name ZhangSan  age 18  hobby playBall
  
  # value = dict_a.items()
  # print(value)  # dict_items([('name', 'ZhangSan'), ('age', 18), ('hobby', 'playBall')])
  # print(type(value))  # <class 'dict_items'>
  ```

- **扩展**：索引 + 遍历

	```python
	dict_a = {"name": "ZhangSan", "age": 18, "hobby": "playBall"}
	for key in dict_a:
	    print(key, dict_a[key])
	```

### 构造字典

- 构造字典
  
  ```python
  name = "ZhangSan"
  age = 18
  hobby = "playBall"
  dict_a = {"name": name, "age": age, "hobby": hobby}
  print(dict_a)  # {'name': 'ZhangSan', 'age': 18, 'hobby': 'playBall'}
  print(type(dict_a))  # <class 'dict'>
  ```

## 数据类型的转换

### int()

- **语法**：`int(ITEM)`，返回 `<class 'int'>`。

  ```python
  # 将整数型的字符串转换成整型
  data1 = int("123")
  print(data1)  # 123
  print(type(data1))  # <class 'int'>
  
  # 将浮点型转换成整型
  data2 = int(3.14)
  print(data2)  # 3
  print(type(data2))  # <class 'int'>
  ```

### float()

- **语法**：`float(ITEM)`，返回 `<class 'float'>`。

  ```python
  # 将小数型的字符串转换成浮点型
  data1 = float("3.14")
  print(data1)  # 3.14
  print(type(data1))  # <class 'float'>
  
  # 将整型转换成浮点型
  data2 = float(3)
  print(data2)  # 3.0
  print(type(data2))  # <class 'float'>
  ```

### str()

- **语法**：`str(ITEM)`，返回 `<class 'str'>`。

  ```python
  strr = str(123)
  print(strr)  # 123
  print(type(strr))  # <class 'str'>
  ```

### bool()

- **语法**：`bool(ITEM)`，返回 `<class 'bool'>`。

  ```python
  data1 = bool(12)
  data2 = bool("hello")
  data3 = bool(None)
  data4 = bool(0)
  data5 = bool("")  # []  {}  ()空容器
  print(data1)  # True
  print(data2)  # True
  print(data3)  # False
  print(data4)  # False
  print(data5)  # False
  ```

- **说明**：表示空意义的数据（`0`、`None`、空字符串和空容器）将被转成 `False`，其他数据都会转成 `True`。

## 数据的可变性

- 关于数据的可变性，详见[`code-general` - 数据的可变性](../code-general/code-general.md#数据的可变性)

- **不可变数据类型**

	- **`int`**：整型
	- **`float`**：浮点型
	- **`str`**：字符串
	- **`tuple`**：元组
	- **`frozenset`**：冻结集合
	- **`bytes`**：字节序列

- **可变数据类型**

	- **`list`**：列表
	- **`dict`**：字典
	- **`set`**：集合
	- **`bytearray`**：字节数组


# 运算符

## 算术运算符

- **`+`**：加
- **`-`**：减
- **`*`**：乘
- **`/`**：除
- **`**`**：幂
- **`//`**：向下取整除（除法保留整数）
- **`%`**：取模（除法获取余数）

### 求平均值

- 用户输入任意5个数，for 循环求他们的平均值

	```python
	total = 0
	for x in range(1, 6):
	  num = int(input("请输入第" + str(x) + "个数："))
	  total += num
	print("平均数为：", total / 5)
	```

- 用户输入任意个数，求他们的平均值

	```python
	total = 0
	count = 0  # 计算循环执行的次数（记录数的个数）
	i = 1
	while i <= 3:
	  num = int(input("请输入第" + str(count + 1) + "个数："))
	  total += num
	  count += 1
	  msg = int(input("继续请按1，结束请按2："))
	  if msg == 2:
	    i = 4  # 改变i，让循环结束
	print("总数为：", total, "次数为：", count, "平均数为：", total / count)
	```

### 折纸厚度

- 一张纸的厚度大约是0.08mm，对折多少次之后能达到珠穆朗玛峰的高度（8848米）?

	```python
	p = 0.08
	m = 8848000
	count = 0  # 记录对折次数
	while p < m:
	  p = p * 2  # 对折
	  count += 1
	print(count)  # 27
	```

### 鸡兔同笼

- 今有鸡兔同笼，上有三十五头，下有九十四足，问鸡兔各几只？

	```python
	for chicken in range(0, 36):
	  rabbit = 35 - chicken
	  if chicken * 2 + rabbit * 4 == 94:
	    print(chicken, rabbit)  # 23 12
	```

### 百钱买百鸡

- 5文钱可以买一只公鸡，3文钱可以买一只母鸡，1文钱可以买3只雏鸡。现在用100文钱买100只鸡，那么各有公鸡、母鸡、雏鸡多少只？

	```python
	for g in range(0, 21):
	  for m in range(0, 34):
	    c = 100 - g - m
	    if g + m + c == 100 and g * 5 + m * 3 + c / 3 == 100:
	      print(g, m, c)  # 0 25 75 / 4 18 78 / 8 11 81 / 12 4 84
	```

## 赋值运算符

- **基本赋值运算符**

	- **`=`**：赋值

- **复合赋值运算符**

	- **`+=`**：加赋值
	- **`-=`**：减赋值
	- **`*=`**：乘赋值
	- **`/=`**：除赋值
	- **`**=`**：幂赋值
	- **`%=`**：求余赋值
	- **`//=`**：取整除赋值
	- Python 中没有以下复合赋值运算符
		- **`++`**：自增，即在自身的基础加1
		- **`--`**：自减，即在自身的基础减1
		- **`%=`**：求余赋值
		- **`??=`**：空赋值
		-  `<<=`：左移赋值
		-  `>>=`：右移赋值
		- `>>>=`：无符号右移赋值

- **解构赋值运算符**

	```python
	a, b, c = 1, 2, 3  # 将值 1, 2, 3 分别赋给 a, b, c
	print(a, b, c)  # 输出: 1 2 3
	```

- **函数默认参数赋值**

	```python
	def greet(name="Guest"):
	  print(f"Hello, {name}")
	
	greet()  # 输出: Hello, Guest
	greet("Alice")  # 输出: Hello, Alice
	```

- **示例**

	``` python
	a = 11
	a += 3  # 在 a 的基础上再加 3 ，相当于 a = a + 3
	print(a)  # 14
	```

	```java
	public class Main {
	  public static void main(String[] args) {
	    int a = 11;
	    a++; // 相当于 a = a + 1
	    System.out.println(a); // 12
	  }
	}
	```

	``` python
	a = 11
	a %= 3  # a=a/3之后再求余
	print(a)  # 2
	```

	``` python
	a = 11
	a //= 3  # a=a/3之后再取整
	print(a)  # 3
	```

	```python
	a = 11
	a **= 3  # a = a的3次方 
	print(a)  # 1331
	```

## 关系运算符

- **关系运算符**：用来检查两个值之间的关系是否成立，关系运算符运算的结果是**布尔值**

	- **`>`**：大于

	- **`<`**：小于

	- **`>=`**：大于等于

	- **`<=`**：小于等于

	- **`==`**：相等（值相等，类型忽略，返回 `真`）
	- **`!=`**：不等（值不相等，类型忽略，返回 `真`）

	- Python 中没有以下关系运算符
		- **`===`**：全等（值相等，类型也相同，返回 `真`）
		- **`!==`**：不全等（值和类型至少有一个相等，返回 `真`）

## 逻辑运算符

- **`not`**：非
- **`and`**：与
- **`or`**：或

## 三元条件运算符

- 在 Python 中，并没有类似于其他语言中的三元条件运算符，提供了一个 **条件表达式**。

- **语法**：`true_value if 条件表达式 else false_value`

	```python
	x = 10
	y = 5
	
	# 如果 x 大于 y，返回 "x is greater", 否则返回 "y is greater"
	result = "x is greater" if x > y else "y is greater"
	
	print(result)  # 输出: x is greater
	```

## 运算符优先级

1. **括号** `()`
2. **一元运算符** `+x`, `-x`, `~x`, `not x`
3. **算数运算符**
	1. **指数运算符** `**`
	2. **乘法、除法、取余、取整除** `*`, `/`, `//`, `%`
	3. **加法、减法** `+`, `-`
4. **位移运算符** `<<`, `>>`
5. **按位与** `&`
6. **按位异或** `^`
7. **按位或** `|`
8. **比较运算符** `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in`
9. **逻辑运算符** `and`, `or`
10. **条件运算符** `if else`
11. **赋值运算符** `=`, `+=`, `-=`, `*=`, `/=`, `//=`, `%=` 等
12. **逗号运算符** `,`

# 控制结构

## 选择结构

- Python 中有 `if` 和 `三元表达式` 两种选择结构。

### `if`

- **语法**

  ```python
  if 条件表达式:
      执行语句
  ```

  ```python
  money = int(input("请输入你的存款："))
  if money >= 100:
      print("恭喜你！可以买宝马了！")  # print 前默认有一个缩进，表示与 if 的从属关系
      print("真开心！")  # 同一条件下的所有 print 缩进要统一
  ```

- **说明**

	- 执行语句前有一个缩进，表示与 if 的从属关系；
	- 同一条件下的所有执行语句缩进要统一。


### `if-else`

- **语法**

  ```python
  if 条件表达式:
      执行语句A
  else:
      执行语句B
  ```

  ```python
  money = int(input("请输入你的存款："))
  if money >= 100:
      print("恭喜你！可以买宝马了！")
  else: # else 与 if 缩进相同
      print("继续上班！")
  ```

- **说明**：`else` 缩进与 `if` 相同，表示与 `if` 的并列关系。

### `if-elif-else`

- **语法**

  ```python
  if 条件表达式1:
      执行语句A
  elif 条件表达式2:
      执行语句B
  elif 条件表达式3:
      执行语句C
  else:
      执行语句D
  ```
  
  ```python
  money = int(input("请输入你的存款："))
  if money >= 100:
      print("恭喜你！可以买宝马了！")
  elif money >= 50:  # elif 缩进与 if 相同
      print("买丰田！")
  elif money >= 20:
      print("买二手车！")
  else:
      print("继续上班！")
  ```

### 选择结构嵌套

- **语法**

  ```python
  if 条件表达式1:
      执行语句A
      if 条件表达式2:
          执行语句A
  else:
      执行语句C
  ```
  
  ```python
  money = int(input("请输入存款金额（万）？"))
  day = int(input("今天是星期几（1-7）？"))
  if money >= 100:
      print("恭喜你！可以买宝马了！")
      if day <= 5:  # 此处的 if 在第一个 if 的基础下，所以缩进要降一个等级
          print("周末去提车！")
      else:  # 此处的 else 在第一个 if 的基础下，与第二个 if 同级
          print("今天下午就去提车！")
  elif money >= 50:
      print("买丰田！")
  elif money >= 20:
      print("买二手车！")
  else:
      print("继续上班！")
  ```

### 三元表达式

- **语法**：`真值 if 条件表达式 else 假值`

	```python
	money = int(input("请输入你的存款："))
	print("恭喜你！可以买宝马了！" if money >= 100 else "继续上班！")
	```

### 练习

#### 特价菜

- 根据用户输入星期几，输出特价菜是什么。

  ```
  星期一特价菜：水煮鱼
  星期二特价菜：烧排骨
  星期三，四特价菜：宫爆鸡丁
  星期五，六特价菜：清蒸鲈鱼
  其它：干锅肥肠
  ```

  ```python
  day = int(input("请输入星期几？（1-7）"))
  if day == 1:
      print("星期一特价菜：水煮鱼")
  elif day == 2:
      print("星期二特价菜：烧排骨")
  elif day == 3 or day == 4:
      print("星期三、四特价菜：宫爆鸡丁")
  elif day == 5 or day == 6:
      print("星期五、六特价菜：清蒸鲈鱼")
  else:
      print("星期日特价菜：干锅肥肠")
  ```

#### 成绩单

- 根据输入判断学生的成绩等级

  ```
  如果成绩>=90分，则输出“优秀”;
  如果成绩>=80分，则输出“良好”;
  如果成绩>=60分，则输出“中等”;
  否则，输出“差”
  ```

  ```python
  score = int(input("请输入考生成绩："))
  if score >= 90:
      print("优秀")
  elif score >= 80:
      print("良好")
  elif score >= 60:
      print("中等")
  else:
      print("差")
  ```

#### 保险柜

- 现在有一个银行保险柜，有两道密码。想拿到里面的钱必须两次输入的密码都要正确。

  ```
  如果第一道密码都不正确，那直接把你拦在外面；
  如果第一道密码输入正确，才能有权输入第二道密码。
  只有当第二道密码也输入正确，才能拿到钱！(两道密码自己设)(嵌套 if)
  ```

  ```python
  password1 = "123"
  password2 = "abc"
  
  pwd1 = input("请输入第一道密码：")
  if pwd1 == password1:
      print("第一道密码输入正确！")
      pwd2 = input("请输入第二道密码：")
      if pwd2 == password2:
          print("恭喜你，输入正确！拿到5毛钱！")
      else:
          print("很遗憾！第二道密码错误！")
  else:
      print("第一道密码输入错误，请出去吧！")
  ```

#### 商品管理系统

- 为一家超市开发一个简易的收银系统（以3-5种商品为例）

  ```
  使用变量保存：商品编号 商品价格 商品名字
  提示用户输入商品编号和数量,然后显示总价多少钱
  提示用户输入付款金额,然后显示找零金额。
  ```

  ```python
  num1 = "1001"
  price1 = 7
  name1 = "苹果"
  
  num2 = "1002"
  price2 = 4
  name2 = "香蕉"
  
  num3 = "1003"
  price3 = 5
  name3 = "梨子"
  
  # 提前声明变量保存需要的商品价格和名称
  num = input("请输入商品编号：")
  count = int(input("请输入商品数量："))
  
  price = 0
  name = ""
  
  if num == num1:
      price = price1
      name = name1
  elif num == num2:
      price = price2
      name = name2
  elif num == num3:
      price = price3
      name = name3
  else:
      print("没有此商品！")
  if price != 0:
      amount = price * count
      print("您当前购买的是：", name, ",单价：", price, "元,数量：", count, "件,金额：", amount, "元！")
      money = float(input("请输入付款金额："))
      if money < amount:
          print("金额不足！")
      else:
          print("付款：", money, "元！找零：", money - amount, "元！")
  ```

## 循环结构

- Python 中有 `for` 和 `while` 两种循环结构。

### `for`

- Python 中并没有像 JS 中那样严格意义的 `for` 语句，而是使用 `for-in` 语句集合了 JS 中 `for`、`for-in` 和 `for-of` 的全部功能。

#### `for-in`

- Python 中，`for-in` 语句用于遍历**可迭代对象**（如字符串、列表、元组、字典和集合等），可迭代对象有几个元素，就会执行几次循环体，每次循环时从中取出的一个元素，将赋值给该变量。

- **语法**

  ```python
  for 变量 in 可迭代对象:
    循环体
  ```

  ```python
  lst = ["中国", "上海", 123]
  for data in lst:
    print(data)
  ```

- **说明**：遍历字典获取到的是 `键`，再利用索引可获取到 `值`。

  ```python
  dict_a = {"name": "Jerry", "age": 18, "hobby": "football"}
  for key in dict_a:
      print(key)  # 依次输出name  age  hobby
  print(key, dict_a[key])  # 依次输出name Jerry  age 18  hobby football
  ```

#### 遍历序列

- `range 序列`：生成一个 a 到 b 的序列，左闭右开。
- **语法**：`range (结束值) | (开始值, 结束值, 步长)`

  - 包含开始值，不包含结束值，即左闭右开；
  - 步长可省略，默认为 1，步长不可为 0。

  ```python
  for i in range(10):
  	  print(i)  # 依次打印从0到9
  
  for i in range(10):
  	  print("Hello world!")  # 依次输出 10 次 Hello world!
  ```

- **扩展**：利用遍历序列和索引，从而达到遍历可迭代对象的目的

	```python
	lst = ["中国", "上海", 123]
	for i in range(len(lst)):
	  print(lst[i])
	```

#### 遍历嵌套容器

- **示例**

  ```python
  reward_list = [
      ("三等奖", 5, "ipad"),
      ("二等奖", 3, "iPhone"),
      ("一等奖", 1, "马尔代夫"),
      ("特等奖", 1, "一套房")
  ]
  
  for title, count, detail in reward_list:  # 元素可写成 (title, count, detail)
      print(title)  # 三等奖  二等奖  一等奖  特等奖
      print(title, count)  # 三等奖 5  二等奖 3  一等奖 1  特等奖 1
  ```

#### 冒泡排序

- 冒泡排序：从第一个元素开始，往后比较相邻两个元素，按照需求进行交换（升序或降序），经过多轮比较完成的排序。

  ```python
  # 升序排列示例
  
  lista = [5, 2, 3, 4, 1]
  for x in range(1, len(lista)):  # x是比较的轮数，从1到4
      for y in range(0, len(lista) - x):  # y是每轮每次比较的前一位索引号
          if lista[y] > lista[y + 1]:  # 通过比较大小判断两个数是否交换
              # 两个数交换
              c = lista[y]  # 引入第三方变量
              lista[y] = lista[y + 1]
              lista[y + 1] = c
  print(lista)  # [1, 2, 3, 4, 5]
  ```

### `while`

- **语法**

  ```python
  while 条件表达式:
    循环体
  ```
  
  ```python
  i = 1
  while i <= 10:
      print("第", i, "次打印：Hello World!")
      i = i + 1  # 条件迭代
  ```

- **死循环**

  ```python
  while True:
      循环体
  ```

### 循环结构嵌套

- **示例**

  ```python
  for year in range(1, 11):
      print("----------第", year, "年到了！")
      for month in range(1, 13):
          print("第", year, "年，第", month, "月，还款1000元！")
  ```
  
- **遍历多维容器**

  ```python
  lst1 = [1, 213, 13, 232, 3, 43, 3, 3]
  lst2 = [21, 13, 243, 4, 54, 6]
  lst3 = [23, 545, 465, 65, 6565, 76]
  lst4 = [lst1, lst2, lst3]
  
  for lstx in lst4:
      for a in lstx:
          print(a)  # 获取结果为：前3个列表的各个值
  ```

### 跳转结构

Python 中有 `continue`、`break`、`return` 三种跳转结构。

- **`continue` 和 `break` 示例**

  ```python
  for year in range(1, 11):
      if year == 5:
          print("第5年疫情原因，今年不用还款了！")
          # 此处如果没有continue，会同时正常显示：第五年到了，还款1.2万
          continue  # 第5年不用还，本次循环结束，进入下一次该循环，第6年。
      if year == 6:
          print("第", year, "年到了！还款2.4万！")
          continue  # 第6年还2.4万，本次循环结束，进入下一次该循环，第7年。
      if year == 8:
          print("第8年，提前还清，以后都不用还了！")
          break  # 从第9年不用再还款了，当前循环结束
      print("第", year, "年到了！还款1.2万！")
  ```

- `return`：详见[返回值](#返回值)

# 文件读写

## 文件读写基础

- **基础步骤**

  ```python
  data = "Hello world!"  # 确认要写入的内容并用data接收
  data = data.encode(utf-8)  # 将“青海联通”编码，转为字节型数据
  f = open (r"demo.txt", "a")  # 获取文件对象
  f.write(data)  # 写入
  # f.flush()  # 将数据强刷进硬盘，防止关闭文件前电脑死机数据不保存
  f.close()  # 关闭文件，不关不影响程序运行，但会耗内存
  ```

- **文件**

  - **文本文件**：也称字符型文件，只保存字符串的文本文档，如 txt，JSON，css 等。文本文件从本质上也是二进制文件。

  - **二进制文件**：也称字节型文件，可以保存任意格式的多媒体数据，如图片，音频，视频等。

- **文件路径**

  - 路径加 r 取消转义
  - 绝对/相对路径
  - 路径可以是变量，尤其是以文件名的相对路径

- **访问模式**

  - 读：r / rb
  - 写：w / wb
  - 追加：a
  - 文本文件为 r / w，二进制文件为 rb / wb。

## 读文件

- **基本示例**

  ```python
  f = open(r"demo.txt", "r", encoding = "utf-8")  # 二进制文件访问模式为 rb，不解码
  data = f.read()
  f.close()
  ```
  
- **读大体积文本文件**

  ```python
  f = open(r"demo.txt", "r", encoding = "utf-8")
  for line in f:  # 防止一次性读完，内存不够，所以逐行读
      data = line
  f.close()
  ```
  
- **读大体积二进制文件**

  ```python
  import os
  
  total_size = os.stat(r"英雄.mp4").st_size  # 获取总字节数
  f = open(r"英雄.mp4", "rb")
  has_read_size = 0
  while has_read_size < total_size:
      chunk = f.read(3)  # 每次读3个字节，防止一次性读完，内存不够
      print(chunk)
      has_read_size += len(chunk)
  f.close()
  ```

## 写文件

- 如果文件不存在，则创建新文件再写入；如果存在，则直接写入。

  - 覆盖写入 `w/wb`

  - 追加写入 `a/ab`

- **基本示例**

  ```python
  data = "你好，长春！" 
  f = open(r"demo.txt", "w"或"a", encoding = "utf-8")
  f.write(data)
  f.close()
  ```

## `with open()` 语句

- 使用 `with open()` 语句简化读写操作，且不必关闭

  ```python
  # 读
  with open(r"demo.txt", "r", encoding="utf-8") as f:
      data = f.read()
  
  # 写
  with open(r"demo.txt", "a", encoding="utf-8") as f:
      f.write("Hello world!")
  ```

## 文件处理

### 批量写入

- 批量写入示例

  ```python
  dict_a = {"zhangsan": 111, "lisi": 222, "wangwu": 333}
  for user, pwd in dict_a.items():
      with open(r"demo.txt", "a", encoding="utf-8") as f:
          line = "{}-{}\n".format(user, pwd)
          f.write(line)
  ```

### 复制粘贴

- 复制粘贴示例

  ```python
  with open(r"cat.jpg", "rb") as file1, open(r"cat-2.jpg", "wb") as file2:  # 用逗号连接，同时执行两次读写
      data = file1.read()
      file2.write(data)
  ```

### 处理 TXT 文件

- 要求：得到一个 TXT 文件，把文件名和网址作为键值对放入一个字典中

  ```
  # file.txt
  # 开头多个换行
  123.jpg,汽车,https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg
  
  456.jpg,卡车,https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg
  
  789.jpg,轿车,https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg
  # 结尾多个换行
  ```
  
  ```py
  with open(r"file.txt", "r", encoding="utf-8") as f:
      # 获取到去除首尾空白行的文件内容
      data = f.read().strip()
  
  # 根据"\n"切割，获取到一个列表，文件每行内容为列表的一个元素
  lst = data.split("\n")
  dict_a = {}
  for line in lst:
      # 去除中间空白行
      if not line:
          continue
      # 根据","切割原列表的元素，切割之后的部分组成一个新列表，每个信息为新列表的一个元素
      list_new = line.split(",")  # ['zhangsansan', '123', '19999999999'] for 循环3次，分别得到3个列表
      # 向字典添加键值对
      dict_a[list_new[0]] = list_new[2]
  print(dict_a)
  ```

- 要求：得到一个 TXT 格式的字幕文件，只提取字幕部分

  ```txt
  Dialogue: 0,0:00:33.27,0:00:34.96,Default,NTP,0,0,0,,即使哥伦布在海上迷失\N{\rEng}So, even Columbus got lost,
  Dialogue: 0,0:00:34.96,0:00:36.68,Default,NTP,0,0,0,,没成为首位发现美洲大陆的人\N{\rEng}and wasn't the first who discovered America,
  # 删除“}”之前多余内容，变成如下
  So, even Columbus got lost,
  and wasn't the first who discovered America,
  ```

  ```python
  # 读取文件内容
  with open(r'hanchi_original.txt', 'r', encoding='utf-8') as file:
      lines = file.readlines()
  
  # 提取“}”后面的内容
  extracted_lines = [line.split('}', 1)[1].strip() if '}' in line else '' for line in lines]
  
  # 写入新文件
  with open(r'hanchi_new.txt', 'w', encoding='utf-8') as output_file:
      output_file.write('\n'.join(extracted_lines))
  ```


### 下载图片

- **语法**

  ```python
  import requests
  res = requests. get("$URL")  # 发送请求并用res接收数据
  data = res.content  # content解码
  # 接下来进行文件读写处理数据
  ```
  
- **下载图片示例**

  ```python
  import requests
  
  url = " https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg"
  data = requests.get(url)
  image = data.content
  
  with open("Benz.png", "wb") as f:
      f.write(image)
  ```

- **批量下载图片示例**

  ```
  # file.txt
  # 开头多个换行
  123.jpg,汽车,https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg
  456.jpg,卡车,https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg
  789.jpg,轿车,https://club2.autoimg.cn/album/g26/M0A/2C/E9/userphotos/2023/09/03/22/820_ChxkjmT0lFqAcBBbAAvcbidXiqQ277.jpg
  # 接尾多个换行
  ```
  
  ```python
  import requests
  
  # 处理文件，详见处理 txt 文件
  with open(r"file.txt", "r", encoding="utf-8") as f:
      data = f.read()
  data = data.strip()
  lst = data.split("\n")
  dict_a = {}
  for row in lst:
      list_new = row.split(",")
      dict_a[list_new[0]] = list_new[2]
  
      # 详见下载图片
      # 批量下载，list_new[2]为之前获取到的 url
      data = requests.get(list_new[2])
      image = data.content
      # list_new[0]为之前获取到的文件名
      with open(list_new[0], "wb") as f:
          f.write(image)
  ```

# 函数

## 创建函数

### `def` 语句

- **语法**

	```python
	def 函数名(形参列表):
	    函数体
	    return 返回值
	```

	```python
	def get_sum(a, b):
	    result = a + b
	    return result
	
	res = get_sum(1, 1)
	print(res)  # 2
	print(type(get_sum))  # <class 'function'>
	```

### 匿名函数

- **语法**：`函数名 = lambda 形参列表: 返回值`

	```python
	get_sum = lambda x, y: x + y
	
	res = get_sum(1, 1)
	print(res)  # 2
	print(type(get_sum))  # <class 'function'>
	```

### `__init__` 方式

- **语法**

	```python
	class 类名:
	    def __init__(self, 形参列表):
	        self.形参列表 = 形参列表
	
	对象名 = 类名(实参列表)
	print(对象名.形参)
	```

	```python
	class Person:
	    def __init__(self, name, age):
	        self.name = name
	        self.age = age
	
	# 创建对象时，构造函数会被调用
	person = Person("Alice", 25)
	print(person.name)  # 输出：Alice
	print(person.age)   # 输出：25
	```

## Python 函数说明

### 返回值

- 函数末尾没有 `return` 或 `return` 没有赋值，则默认返回 None；

### `global`

- global

  - 关键字 `global` 的作用就是将局部变量作用到全局。
  - 如果局部变量和全局变量重名，经 `global` 后，原全局变量的值将更改。

- **示例**

  ```python
  v1 = 1  # 全局变量
  v2 = 2  # 全局变量
  v3 = 3  # 全局变量
  
  
  def func():
      v2 = 3  # 与全局变量同名的局部变量
      global v3  # 通过global，将局部变量 v3 改为全局变量
      v3 = 4  # 通过global，将全局变量 v3 的值改为 4
      v4 = 4  # 局部变量
      print(v1)  # 1  获取全局变量 v1 的值
      print(v2)  # 3  优先获取局部变量 v2 的值
      print(v3)  # 4  获取全局变量 v3 的新值
      print(v4)  # 4  取局部变量 v4 的值
  
  
  func()  # 1 3 4 4
  print(v1)  # 1  获取全局变量 v1 的值
  print(v2)  # 2  获取全局变量 v2 的值
  print(v3)  # 4  获取全局变量 v3 的新值
  print(v4)  # 报错  函数外部不能直接调用未经 global 的局部变量
  ```

## 内置函数

### 数学运算函数

- 部分

  ```python
  abs(-10)  # 10  求绝对值
  pow(2, 5)  # 32  求幂次方  等同于2 ** 5
  sum([11, 22])  # 33 求和及平均数 sum/len
  divmod(98, 10)  # (9, 8)  求商和余数  <class 'tuple'>
  round(3.1415, 2)  # 3.14  保留小数位
  max([1,2,3])  # 3 求最大值
  min([1,2,3])  # 1 求最小值
  len("name")  # 4  求长度
  range()  # 循环序列 详见 for 循环
  sorted()  # 升序  降序加reverse = True
  reversed()  # 反转
  enumerate()  # 枚举
  ```

- **sum()  求和**

  用来求和及平均数

  ```python
  # 求和
  lista = [21, 21, 31, 32, 33, 5454, 46, 65, 6]
  print(sum(lista))
  
  # 求平均数
  listb = [21, 21, 31, 32, 33, 5454, 46, 65, 6]
  print(sum(listb) / len(listb))
  ```
  
- **round() 保留小数位**

  ```python
  # 保留指定的小数位，末位后面四舍五入
  round(a,n)  # a为欲处理的数，n为保留的位数
  ```

  ```python
  a = 15.3
  b = 3
  c = a / b
  print(round(c, 1))  # 5.1
  print(round(3.1415926, 4))  # 3.1416  四舍五入
  ```


- **reversed() 序列反转**

  将序列中的排序进行反转

  ```python
  lista=[21, 21, 31, 32, 33, 5454, 46, 65, 6]
  new_list = reversed(lista)
  for x in new_list:
  	print(x)  # 依次打印反转后的各个元素  如果直接print(new_list)会得到迭代器
  ```

- **enumerate() 枚举**

  将元素加编号逐一列举

  ```python
  goods = ["电脑", "手机", "汽车"]
  for index, item in enumerate(goods, 1):  # index序号  1：从1号开始
      print(index, item)  # 依次打印1 电脑  2 手机  3 汽车
  ```

### 数据类型函数

- **部分**

  ```python
  int("90")  # 90  转整型
  float("90")  # 90.0  转浮点型
  str(90)  # '90'  转字符串
  bool(0)  # False  转换为布尔类型
  list((1, 2, 3))  # [1, 2, 3]  转列表
  tuple([1, 2, 3])  # (1, 2, 3)  转元组
  dict([('a', 1), ('b', 2), ('c', 3)])  # {'a': 1, 'b': 2, 'c': 3}  转字典
  set([1, 4, 2, 4, 3, 5])  # {1, 2, 3, 4, 5}  转集合
  
  iter(iterable)  # 返回一个可迭代的对象。 iter([1,2,3]) > <list_iterator object at 0x0000000003813B00>
  enumerate(iterable) : 返回一个枚举对象。
  bin(int) : 转换为2进制。 bin(1024) > '0b10000000000'
  oct(int) : 转换为8进制。 oct(1024) > '0o2000'
  hex(int) : 转换为16进制。hex(1024) > '0x400'
  chr(int) : 转换数字为相应ASCI码字符。 chr(65) > 'A'
  ord(str) : 转换ASCI字符为相应的数字。 ord('A') > 65
  
  all([0, 11, 22])  # False  检测列表中元素是否全部是True
  any([0, 11, 22])  # True  检测列表中元素是否有True
  bin(90)  # 0b1011010  十进制转二进制
  oct(90)  # 0o132  十进制转八进制
  hex(90)  # 0x5a  十进制转十六进制
  int("0b1011010", base = 2)  # 90  二进制转十进制  八、十六进制同理
  chr(65)  # 'A'  十进制 转ASCII码字符
  ord('A')  # 65  ASCII码字符转十进制
  bytes('abc', 'utf-8')  # b'abc'  将str转换成字节类型
  ```

### 操作型函数

- 部分

  ```python
  print()  # 输出。
  input()  # 输入。
  type(1)  # <class 'int'>  获取数据类型。
  id(4)  # 140725468128136  获取id
  print(__file__)  # 获取当前操作文件的路径（此处不是在cmd中）
  hash('python')  # 7070808359261009780  计算一个对象的hash值
  callable(func)  # True/False 判断func是否可执行，即是不是函数
  eval() : 执行一个表达式，或字符串作为运算。 eval('1+1') > 2
  exec() : 执行python语句。 exec('print("Python")') > Python
  
  filter(func, iterable) : 通过判断函数fun，筛选符合条件的元素。
  filter(lambda x: x>3, [1,2,3,4,5,6]) > <filter object at 0x0000000003813828>
  
  map(func, *iterable) : 将func用于每个iterable对象。
  map(lambda a,b: a+b, [1,2,3,4], [5,6,7]) > [6,8,10]
  
  zip(*iterable) : 将iterable分组合并。返回一个zip对象。
  list(zip([1,2,3],[4,5,6])) > [(1, 4), (2, 5), (3, 6)]
  
  help()：调用系统内置的帮助系统。
  isinstance()：判断一个对象是否为该类的一个实例。
  issubclass()：判断一个类是否为另一个类的子类。
  globals() : 返回当前全局变量的字典。
  next(iterator[, default]) : 接收一个迭代器，返回迭代器中的数值，如果设置了default，则当迭代器中的元素遍历后，输出default内容。
  ```
  
- **id() 获取id**

  获取一个数据的id，判断两个变量是不是同一个变量

  ```python
  a = 5
  b = "5"
  print(id(a))  # 获取结果为：140725472125864
  print(id(b))  # 获取结果为：140718218251616
  ```

# 模块

模块是 Python 中最高级别组织单元，它将程序代码和数据封装起来以便重复使用。

模块中包含了某一类业务中多个函数和属性。模块也称包或者库。

## 自定义模块

- **创建模块**

  项目已创建 > 在项目中创建包/py文件，在 `.py文件` 中写模块

- **引入和使用模块**

  引入模块本质上就是在一个 Python 文件中引入另一个 Python 文件

  -  模块文件在以下目录时，调用和使用方法

  ```
  - 当前运行文件同级目录
  - 内置模块目录根目录
  - 第三方模块根目录
  - 以上三个目录依次查找
  ```

  ```
  import 模块名
  使用：模块名.函数名()
  ```

  -  模块文件在以下目录时，调用和使用方法

  ```
  - 模块文件与主文件不在同一目录
  - 内置模块的子模块
  - 第三方模块的子模块
  ```

  ```
  - 推荐用法
  	- from 同级文件夹.文件夹2…文件夹n import 模块名
  	- 使用：模块名.函数名()
  
  - 另一用法，繁琐
  	- import 同级文件夹.文件夹2…文件夹n.模块名
  	- 使用：同级文件夹.文件夹2…文件夹n.模块名.函数名()
  ```

  - 设置别名

  ```
  - 引入的模块在文档中还可以设置别名
  - improt 模块名 as 别名
  ```

- **\__name__**

  ```
  - 每个模块中都有一个__name__内部变量
  	- 当运行此模块时，__name__ = "__main__"
  	- 当导入此模块时，__name__ = "模块名"
  
  当直接执行当前文件时才运行接下来的语句，如果引用当前文件到另一个文件，那么在另一个文件中不执行当前文件接下来的语句。一般放在项目主函数中。
  ```

  ```python
  def run():
      print("程序启动")
  
  if __name__ == 'main':
      run()
  ```

## 内置模块

- 内置模块就是 Python 自带的模块。

- 内置模块存放路径：C:\Users\39331\AppData\Local\Programs\Python\Python311\Lib

### random 生成随机数

- **抽取**

  抽取原则：随机抽取对原数据没有影响，原数据不会更改

  ```python
  import random
  
  random(a, b)  左闭右闭
  random.randint(1, 10)  # 随机抽取整数
  random.uniform(1, 10)  # 随机抽取浮点数
  random.random()  # 随机抽取0到1的浮点数
  random.choice([1, 132, 32, 43, 43, 454])  # 随机抽取一个元素
  random.sample([1, 132, 32, 43, 43, 454], 2)  # [1, 43]  随机抽取2个元素
  ```

  ```python
  # 抽奖实例
  
  import random  # 引入随机数模块
  
  print("正在抽奖.......")
  r = random.randint(1, 1000)
  print("----------您的抽奖号码是：", r)
  if r == 1:
    print("*******恭喜你，获得一等奖笔记本电脑！")
  elif 10 <= r <= 19:
    print("*******恭喜你，获得二等奖 冰箱！")
  elif 100 <= r <= 149:
    print("*******恭喜你，获得三等奖 音响！")
  else:
    print("******* 谢谢惠顾！")
  ```

- **打乱次序**

  打乱次序以后，原数据会更改

  ```python
  import random
  num_list = [1, 132, 32, 43, 43, 454]
  random.shuffle(num_list)
  print(num_list)  # [1, 43, 32, 132, 454, 43]
  ```

### time 时间处理

- Basic func

  ```python
  ```
  
  
  
- **获取时间戳**

  time.time()

  表示当前时间距离 1970 年元旦 0 时的秒数

  ```python
  import time
  
  time_stamp = time.time()
  print(time_stamp)  # 1697600152.2022958
  print(type(time_stamp))  # <class 'float'>
  ```

- **程序休眠**

  time.sleep() 

  程序休眠，用来处理程序停顿、定时程序

  ```python
  import time
  time.sleep(2)  # 程序休眠2秒
  ```

- **其它用法**

  ```
  - time.localtime() 获取当前日期时间
  - time.strftime() 获取特定格式的日期时间字符串
  - ("%Y-%m-%d----%H:%M:%S", time.localtime()) 获取特定格式的日期时间字符串
  	- 不常用，str表示字符串，f表示转换format
  ```

### datetime 日期时间

- **获取当前时间**

  datetime.now()

  ```python
  from datetime import datetime  # 第二个datetime是第一个的子模块
  
  time_date = datetime.now()
  print(time_date)  # 2023-10-18 09:07:47.664739
  print(type(time_date))  # <class 'datetime.datetime'>
  ```

- **获取指定时间**

  ```python
  from datetime import datetime
  
  data = datetime(2023, 10, 18, 9, 10, 55)
  print(data)  # 2023-10-18 09:10:55
  print(type(data))  # <class 'datetime.datetime'>
  ```

- **时间增量**

  timedelta()

  从当前时间往后/往前多长时间是什么时间

  ```python
  from datetime import datetime
  from datetime import timedelta
  
  res = datetime.now() + timedelta(days = 50)  # days  hours  minutes  seconds
  print(res)  # 2023-12-07 12:18:27.026529
  print(type(res))  # <class 'datetime.datetime'>
  ```

- **时间差**

  end_date - start_date

  ```python
  from datetime import datetime
  
  start_string = "2023-10-18 08:10:08"
  start_date = datetime.strptime(start_string, "%Y-%m-%d %H:%M:%S")
  end_string = "2024-06-18 16:15:15"
  end_date = datetime.strptime(end_string, "%Y-%m-%d %H:%M:%S")
  
  time_delta = end_date - start_date  # 两个时间的差
  print(time_delta)  # 244 days, 8:05:07
  print(type(time_delta))  # <class 'datetime.timedelta'>
  print(time_delta.seconds)  # 29107  # 切换成秒
  print(type(time_delta.seconds))  # <class 'int'>
  ```

### 时间格式的转换

- 三种时间格式：时间戳 time.time()、当前时间 datetime.now()、字符串

- 三种格式以 datetime 为核心相互转换

#### datetime 和字符串

- **datetime 转字符串**

  ```python
  from datetime import datetime
  
  time_string = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
  print(time_string)  # 2023-10-18 11:06:11
  print(type(time_string))  # <class 'str'>
  ```

- **字符串转 datetime**

  ```python
  from datetime import datetime
  
  time_string = "2023-10-18 11:06:11"
  time_date = datetime.strptime(time_string, "%Y-%m-%d %H:%M:%S")
  print(time_date)  # 2023-10-18 11:06:11
  print(type(time_date))  # <class 'datetime.datetime'>
  ```

#### datetime 和时间戳

- **datetime 转时间戳**

  ```python
  from datetime import datetime
  
  time_stamp = datetime.now().timestamp()
  print(time_stamp)  # 1697599215.415559
  print(type(time_stamp))  # <class 'float'>
  ```

- 时间戳转 datetime

  ```python
  from datetime import datetime
  import time
  
  time_date = datetime.fromtimestamp(time.time())
  print(time_date)  # 2023-10-18 11:06:11
  print(type(time_date))  # <class 'datetime.datetime'>
  ```

### os 路径/创建文件夹

#### 获取路径

- **路径拼接**

  ```python
  import os
  
  file_path = os.path.join("python", "Python笔记2", "7.1.模块_时间处理.py")
  print(file_path)  # x1\x2\x3  自动拼接，系统不同，斜杠不同  Mac和Linux为x1/x2/x3
  print(type(file_path))  # <class 'str'>
  ```

- ```
  关于__file__
  
  __file__指的是脚本所在的路径，有可能是相对路径
  ```

- **获取当前文件绝对路径**

  ```python
  import os
  
  abs_path = os.path.abspath(__file__)
  print(abs_path)  # E:\文件\工作\程序员\python\Python笔记2\7.2.函数_路径.py
  print(type(abs_path))  # <class 'str'>
  ```

- **获取当前文件父级目录**

  ```python
  import os
  
  father_path = os.path.dirname(__file__)
  print(father_path)  # E:\文件\工作\程序员\python\Python笔记2
  print(type(father_path))  # <class 'str'>
  ```

- **获取当前文件父级目录的绝对路径**

  ```python
  import os
  
  base_dir = os.path.dirname(os.path.abspath(__file__))
  print(base_dir)  # E:\文件\工作\程序员\python\Python笔记2
  print(type(base_dir))  # <class 'str'>
  
  file_path = os.path.join(base_dir, "a1.txt")  # 获取到当前具体文件的绝对路径
  ```

#### 判断路径是否存在

- 语法

  ```python
  import os
  
  base_dir = os.path.dirname(os.path.abspath(__file__))
  file_path = os.path.join(base_dir, "a1.txt")
  res = os.path.exists(file_path)
  print(res)  # False
  ```

- 应用

  ```python
  if not os.path.exists("path"):
      pass
  ```

#### 创建文件夹

- 语法

  ```python
  import os
  
  base_dir = os.path.dirname(os.path.abspath(__file__))
  folder_path = os.path.join(base_dir, " xx/xx/xx ")
  if not os.path.exists(folder_path):
      os.makedirs(folder_path)
  ```

### urllib 爬虫

- **`request.urlopen($URL)`**

  ```python
  # 爬取网页并存入本地 html 文件
  
  from urllib import request
  
  url = "http://www.baidu.com"  # 注意 https: 和 http:
  data = request.urlopen(url).read()  # data 为变量，发送请求并读取数据
  print(data.decode())  # decode()解码：将二进制转换成字符，此行可以没有
  
  with open(r"8888.html", "wb") as f:  # f 为变量，创建一个文件，等待写入
      f.write(data)  # 将 data 获取到的数据写到 f 中
  ```


### JSON 数据

#### JSON 语法

​	在 Python 中 JSON 数据本质上是一个固定格式的字符串。使用键值对的方式表示一个业务对象（类似于字典）。

- 创建一个 TXT 文件

  ```python
  with open(r"users.txt", "w") as f:
      users = '[{"name":"zhangsan","pwd":"123"},{"name":"lisi","pwd":"123"},{"name":"wangwu","pwd":"123"}]'
      f.write(users)
  ```
  
  ```
  [{"name":"zhangsan","pwd":"123"},{"name":"lisi","pwd":"123"},{"name":"wangwu","pwd":"123"}]
  ```
  
- Python 中保存一个对象

  ```json
  '{"键1": "值1", "键2": "值2", ....}'
  ```

  ```
  - a = '{"键1": "值1", "键2": "值2", ....}'
  - a为接收变量，整个 json 数据用单引号包围，但不包含单引号；
  - 如果 Python 数据键是单引号，转换后会自动变成双引号。
  - 序列化支持以下类型
  ```
  
  |   Python    | JSON     |
  | :---------: | -------- |
  |    dict     | object   |
  | list, tuple | array    |
  |     str     | string   |
  | int, float  | number   |
  |    True     | true     |
  |    False    | false    |
  |    None     | null     |
  |  '单引号'   | "双引号" |
  
- Python 中保存多个对象

  ```json
  '[{"键1": 值1, "键2": 值2}, {"键1": 值1, "键2": 值2}, …]'
  ```

#### Python 转 JSON

- 即序列化，实际就是将字典或者列表嵌套字典转成字符串。

- **`json.dumps($DATA_PYTHON)`**

  ```python
  import json
  
  data_python = {"user": "张三", "pwd": "123", "num": 100}  # Python 格式的字典
  data_json = json.dumps(data_python, ensure_ascii = False)  # 将 Python 格式转换成 JSON 格式
  print(data_json)  # {"user": "张三", "pwd": "123", "num": 100}, 但注意这是一个字符串。
  print(type(data_json))  # <class 'str'>
  ```

  解释：

  - 禁止使用 `str()` 将 Python 数据转换成字符串，否则获取结果花括号里面会变单引号。
  - `ensure_ascii=False` 表示禁止 Ascii 转换，就是禁止将中文的“张三”转换成字节。


#### JSON 转 Python

- 即反序列化，实际就是将字符串转成字典或者列表嵌套字典。

- **`json.loads($DATA_JSON)`**

  ```python
  import json
  
  data_json = '{"user": "张三", "pwd": "123", "num": 100}'  # JSON 格式的字符串
  data_python = json.loads(data_json)  # 将 JSON 格式转换成 Python 格式
  print(data_python)  # {'user': '张三', 'pwd': '123', 'num': 100}
  print(type(data_python))  # <class 'dict'>
  ```

#### JSON 模拟数据库

- 详见 Projects > Login And Sign Up


### hashlib 加密

​	hashlib 模块可实现 md5 加密，md5 无法解密。

- **语法**

  ```python
  import hashlib
  
  data = "admin"
  obj = hashlib.md5()
  obj.update(data.encode('utf-8'))  # 括号里必须是字节
  res = obj.hexdigest()
  print(res)  # 21232f297a57a5a743894a0e4a801fc3  加密字符
  ```

- 注册案例

  ```python
  import hashlib
  
  # 输入
  user = input("请输入用户名：")
  pwd = input("请输入密码：")
  
  # 加密密码
  obj = hashlib.md5("88888".encode('utf-8')) # 加盐
  obj.update(pwd.encode('utf-8'))  # 括号里必须是字节
  pwd_md5 = obj.hexdigest()
  
  # 写入文件
  with open("db.txt", 'a', encoding = 'utf-8') as f:
      line = "{}|{}\n".format(user, pwd_md5)
      f.write(line)
  ```

### socket 网络传输

​	socket 是对 TCP/IP 协议的封装，socket 本身是一个调用接口（API），方便程序员用 socket 使用 TCP/IP 协议簇，实现网络通信。

​	不同编程语言，使用 socket 的语法有所不同，但基本过程类似。

- **名词解释**

  ```
  - 通信选择
      - UNIX  本机通信
      - AF_INET  IPV4通信
      - AF_INET6  IPV6通信
  - 通信协议
      - SOCK_STREAM  TCP协议，面向连接
      - SOCK_DGRAM  UDP协议，面向非连接，速度快，可靠性差
  ```

- **引入方式**

  frome socket import*

- ```
  以下没学完！！！！！！！！！！！
  ```

- **客户端** 

- **服务端**

## 第三方模块

​	第三方模块是由第三方个人或者组织使用 Python 开发，需要先下载安装才能使用的工具包。

​	第三方模块安装的失败率很高，应该多试几次。

### 第三方模块的安装

​	第三方模块存放路径：C:\Users\39331\AppData\Local\Programs\Python\Python311\Lib \site-packages

- **pip 安装**

  ```bash
  pip install $MODULE_NAME
  ```
  
- **网上下载**

  ```
  - 在网上https://pypi.python.org，下载下来
      - cp311代表Python的版本3.11
      - win_amd64代表Windows 64位系统
      - 下载.whl文件或者压缩包.tar.gz文件，选择其中一个安装
  - .whl文件的安装方法
      - cmd进入whl文件所在目录
      - 在.whl文件所在文件夹空白处，Shift+右键—在此处打开powershell窗口
      - 在powershell中执行： pip install 文件名（包含后缀）
  - 压缩包的安装方法
      - 解压安装包
      - cmd进入setup.py文件所在目录
      - 在setup.py文件所在文件夹空白处，Shift+右键—在此处打开powershell窗口
      - 在powershell中输入： python setup.py install，回车
  ```

- **在 Pycharm 中安装**

  ```
  - 在创建项目时，需要选择系统环境，否则通过其它方式安装的模块，可能无法使用。
  - Settings—Project:Pycharm Project—Python Interpreter—点加号，搜索模块
  - 选中要安装的模块
  - 点方框——Install Packge
  ```

### flask-cors 允许跨域

​	在默认情况下，浏览器会阻止跨源的 HTTP 请求，以保护用户的安全和隐私。因此，当你在 localhost 的端口 3000 上运行的前端应用尝试向 localhost 的端口 5000 上运行的后端应用发送请求时，由于跨域限制，浏览器会拒绝这些请求。要解决这个问题，你需要在后端应用中配置 CORS，允许来自前端应用的跨源请求。在 Flask 中，你可以使用 flask_cors 库来处理跨域请求。请注意，这样配置会允许来自任何域的跨源请求，因此在生产环境中应谨慎使用，最好限制允许的来源。

- 应用

  ```python
  from flask import Flask
  from flask_cors import CORS
  
  app = Flask(__name__)
  CORS(app)  # 允许所有域的跨域请求，即允许前端的 3000 端口访问后端的 5000 端口
  ```

# 对象

## 创建对象

### 字面量方式

- **语法**：模拟对象字面量

	```python
	# 使用字典模拟对象
	person = {
	    "name": "Alice",  # 定义 name 属性
	    "age": 25,        # 定义 age 属性
	    "introduce": lambda: print(f"My name is {person['name']}, and I am {person['age']} years old.")  # 定义方法
	}
	
	# 调用方法
	person["introduce"]()  # 输出: My name is Alice, and I am 25 years old.
	```

### 面向对象方式

- **语法**

	```python
	# 定义类
	class Person:
	    # 构造函数
	    def __init__(self, name, age):
	        self.name = name  # 初始化 name 属性
	        self.age = age    # 初始化 age 属性
	
	    # 定义方法
	    def introduce(self):
	        print(f"My name is {self.name}, and I am {self.age} years old.")
	
	# 创建对象
	person1 = Person("Alice", 25)
	person2 = Person("Bob", 30)
	
	# 调用方法
	person1.introduce()  # 输出: My name is Alice, and I am 25 years old.
	person2.introduce()  # 输出: My name is Bob, and I am 30 years old.
	```

# 面向对象

## 面向对象基础

- **语法**

  ```python
  # 定义类
  class Person:
      # 构造函数
      def __init__(self, name, age):
          self.name = name  # 初始化 name 属性
          self.age = age    # 初始化 age 属性
  
      # 定义方法
      def introduce(self):
          print(f"My name is {self.name}, and I am {self.age} years old.")
  
  # 创建对象
  person1 = Person("Alice", 25)
  person2 = Person("Bob", 30)
  
  # 调用方法
  person1.introduce()  # 输出: My name is Alice, and I am 25 years old.
  person2.introduce()  # 输出: My name is Bob, and I am 30 years old.
  ```


- **银行卡示例**

  ```python
  # 编写一个银行卡类
  # 属性：银行名称，卡号，密码，姓名，余额
  # 方法：登录，存款
  
  # 定义类
  class Card():
      # 构造函数
      def __init__(self, num, pwd, user, balance):
          self.bank_name = "Python Bank"  # 初始化 bank_name 属性
          self.num = num  # 初始化 num 属性
          self.pwd = pwd  # 初始化 pwd 属性
          self.user = user  # 初始化 user 属性
          self.balance = balance  # 初始化 balance 属性
  
      # 定义方法
      def longin(self):
          unum = input("请输入卡号：")
          upwd = input("请输入密码：")
          if unum == self.num and upwd == self.pwd:
              print("验证成功！")
              return unum
          else:
              print("验证失败！")
              return None
  
      def deposit(self):
          if self.longin():  # 类的内部可以调用其它函数
              money = float(input("请输入存款金额："))
              self.balance += money
              print("存款成功！存入", money, "元！余额", self.balance, "元！")
  
  # 创建对象
  c1 = Card("1001", "123", "张三", 0)
  c2 = Card("1002", "123", "张三", 0)
  
  # 调用方法
  c1.deposit()
  c2.deposit()
  ```

## 面向对象三大特性

### 类的封装

- 封装

  ```
  - 封装就是把对象的某个属性，只能通过类内部的方法访问，而不能从外部直接调用。
  - 方法：在定义类属性时，把“self.属性”改成“self.__属性”，然后把该属性的操作创建到一个方法内。
  ```

- 将数据封装到对象

  ```python
  class Foo:
      def __init__(self, name, age):
          self.name = name
          self.age = age
  obj = Foo("Jerry", 30)
  ```

- 将同一类方法封装到类

  ```py
  class Message:
      def email(self):
          pass
      def wechat(self):
          pass
      def sms(self):
          pass
  
  class FileHandler:
      def txt(self):
          pass
      def excel(self):
          pass
      def word(self):
          pass
  ```

### 类的继承

- 子类自动拥有父类的属性和方法。

- 语法

  ```python
  class Base:
      def func1(self):
          pass
  
  class Son(Base):
      def func2(self):
          pass
  
  obj = Son()  # 创建子类对象
  obj.func1()  # 子类自动拥有父类的属性和方法
  ```

  ```
  - 子类必须自动拥有父类属性和方法，但父类不拥有子类的属性和方法。
  - 当子类和父类拥有相同属性和方法时，子类只调用自己，而不调用父类。
  - 创建子类对象时，要填写父类的各个属性。
  - 在python中，一个父类可以有多个子类，一个子类也可以有多个父类。
  - 所有类的最终父类是object，如果不填写父类，系统默认为父类就是object。
  ```

### 类的多态

​	支持传入多种类型参数

## 类的特殊成员

- **\__new__构造对象**

  ```
  - 构造对象，实际就是创建对象省略的那两步。
  - 用在想让初始化对象之前做一点操作，可以使用此方法。
  ```

  ```python
  class Foo:
      def __new__(self,*args,**kwargs):
          object=object.__new__(self) # 创建的空对象
          return object
  ```

- **\__call__对象执行方法**

  ```
  普通对象自身没有方法，不能使用“对象名()”执行方法，只能通过“对象名.方法名()”调用类的方法，但此种模式可以让对象直接通过“对象名()”去执行一个定义好的自己的方法。
  ```

  ```python
  class Foo:
      def __call__(self,*args,**kwargs):
          print("1111")
  obj = Foo()
  obj() #获取结果为：1111。
  ```

# 异常处理

# 操作 MySQL

## Syntax

- SQL syntax in Python

  ```python
  sql = "show databases;"
  ```

  解释：

  - 结尾不加分号也行
  - 整个 sql 语句用双引号包围
  - 当作为数据的值时，应该使用单引号

- Commit SQL syntax template

  ```python
  cursor.execute("$SQL_SYNTAX")
  
  # 1. 如果是查询业务，则执行 fetchall
  result = cursor.fetchall()
  print(result)
  
  # 2. 如果是增删改业务，则执行 commit
  conn.commit()
  ```

## About DictCursor

- 引入 DictCursor

  ```python
  import pymysql
  from pymysql.cursors import DictCursor  # 引入 DictCursor
  
  # 连接方式
  cursor = conn.cursor(cursor=DictCursor)
  ```

  ```
  # 查询结果：每行数据都放在各自字典中，所有行都放在一个列表中，即列表嵌套字典，列名为字典的键，数据为字典的值。
  [{'id': 8, 'username': 'zhangsansan', 'password': '123', 'mobile': '19999999999'}, {'id': 9, 'username': 'lisisi', 'password': '123', 'mobile': '18888888888'}, {'id': 10, 'username': 'wangwuwu', 'password': '123', 'mobile': '16666666666'}]
  ```

- 不引入 DictCursor

  ```python
  import pymysql
  
  # 连接方式
  cursor = conn.cursor()
  ```

  ```
  # 查询结果：每行数据都放在各自元组中，所有行都放在一个大元组中，即元组嵌套元组。
  ((8, 'zhangsansan', '123', '19999999999'), (9, 'lisisi', '123', '18888888888'), (10, 'wangwuwu', '123', '16666666666'))
  ```

## Operate MySQL

### An operation

- 此例作为 Python 操作 MySQL 的样板文件，可以替换中间 `文件处理` 和 `执行sql` 部分。

  ```python
  # 1.引入 pymysql 和 DictCursor
  # 确保第三方模块 pymysql、DictCursor 已安装
  import pymysql
  from pymysql.cursors import DictCursor  # 引入 DictCursor，查询结果为列表嵌套字典
  
  # 2.连接 MySQL 服务器
  # 将连接部分写在循环以外，防止频繁连接
  # 确保已创建数据库 db_test 和数据表 tb_test (四列：id, username, password, mobile)
  conn = pymysql.Connect(
      host="localhost",  # 主机地址，如果要连接远程数据库，需填写对应数据库地址
      port=3306,  # 端口号，注意数字是整型
      user="root",
      password="123456",
      charset="utf8",  # 文件编码
      database="db_test"  # 可提前连接某个特定数据库，以减少后期进入数据库的步骤
  )
  print("MySQL已连接.....")
  cursor = conn.cursor(cursor=DictCursor)  # 创建游标对象（连接方式 DictCursor，查询结果为列表嵌套字典）
  
  # 3.增删改查（以导入数据为例）
  # 3.文件处理
  # 确保已创建 users.txt 文件（zhangsan,123,19999999999...）
  # 关于文件处理，详见：处理 TXT 文件
  with open('users.txt', 'r', encoding='utf-8') as f:
      data = f.read().strip()
  lst = data.split("\n")
  for line in lst:
      if not line:
          continue
      list_new = line.split(",")  # ['zhangsansan', '123', '19999999999'] for 循环3次，分别得到3个列表
  
      # 4.执行sql
      # 不要直接将用户输入的值直接写入 sql 语句，防止 SQL 注入攻击。
      sql = "insert into tb_test(username, password, mobile) values(%s, %s, %s)"  # %s 占位符
      cursor.execute(sql, list_new)  # 将用户输入的值以列表的形式传递给 cursor.execute() 方法
      conn.commit()
      print("导入数据成功！")
  
  # 5.关闭游标对象和连接
  # 将关闭连接部分写在循环以外，防止频繁连接
  cursor.close()
  conn.close()
  print("MySQL 已断开连接！")
  ```

### Multiple operations

- 当需要多次连接 MySQL 时，可以将连接和断开连接封装成函数，以免冗余。

  ```python
  import pymysql
  from pymysql.cursors import DictCursor
  
  
  # 连接 MySQL
  def conn_mysql():
      return pymysql.Connect(
          host="localhost",
          port=3306,
          user="root",
          password="123456",
          charset="utf8",
          database="db_test"
      )
  
  
  # 断开 MySQL
  def close_conn_mysql(conn, cursor):
      cursor.close()
      conn.close()
  
  # 以查询数据为例
  conn = conn_mysql()  # 调用连接 MySQL 函数
  cursor = conn.cursor(cursor=DictCursor)
  cursor.execute("select * from tb_test")
  result = cursor.fetchall()
  close_conn_mysql(conn, cursor)  # 调用断开 MySQL 函数
  ```

## Database

- **查询所有数据库**

  ``` python
  cursor.execute("show databases;")
  result = cursor.fetchall()  # 接收查询结果
  print(result)
  ```

- **进入数据库**

  ``` python
  cursor.execute("use $DATABASE;")
  ```

- **创建数据库**

  ``` python
  cursor.execute("create database $DATABASE default charset=utf8;")
  conn.commit()  # 执行conn，提交数据
  print("创建数据库成功！")
  ```

- **删除数据库**

  ``` python
  cursor.execute("drop database $DATABASE;")
  conn.commit()
  print("删除成功！")
  ```


## Table

- **查询所有数据表**

  ``` python
  cursor.execute("show tables;")
  result = cursor.fetchall()
  print(result)
  ```

- **创建数据表**

  ``` python
  # 一般以id作为主键
  sql = """
  create table tb2(
    	id bigint unsigned primary key auto_increment not null,
      name varchar(16),
      mobile char(11),
      email varchar(128),
      salary decimal(10, 2),
      ctime datetime
  )default charset=utf8;"""
  cursor.execute(sql)
  conn.commit()
  print("创建数据表成功！")
  ```

- **删除数据表**

  ``` python
  cursor.execute("drop table $TABLE")
  conn.commit()
  print("删除数据表成功！")
  ```

## Row

- **增加数据行**

  ``` python
  sql = "insert into tb_test(name, mobile, email, salary, ctime) values('zhaoliu', '18888888888', 'x@qq.com', 1000, '2023-11-01 12:30:30');"
  cursor.execute(sql)
  conn.commit()
  print("增加数据行成功！")
  ```

  ``` python
  # 增加多行数据行
  
  sql = """insert into tb_test(name, mobile, email, salary, ctime) values
      ('mayun', '18888888888', 'x@qq.com', 1000, '2023-11-01 12:30:30'),
      ('zhangsan', '18888888888', 'x@qq.com', 1000, '2023-11-01 12:30:30'),
      ('lisi', '18888888888', 'x@qq.com', 1000, '2023-11-01 12:30:30');"""
  cursor.execute(sql)
  conn.commit()
  print("增加数据行成功！")
  ```

- **删除数据行**

  ``` python
  sql = "delete from tb_test where name='zhangsan';"
  cursor.execute(sql)
  conn.commit()
  print("删除数据行成功！")
  ```

  - 删除所有数据行

  ``` python
  cursor.execute("delete from tb_test;")
  conn.commit()
  print("删除所有数据行成功！")
  ```

## Data

- **查询所有数据**

  ``` python
  cursor.execute("select * from tb_test;")
  result = cursor.fetchall()
  print(result)
  ```

- **查询特定数据**

  ``` python
  sql = "select id from tb_test where name = 'zhaoliu';"
  cursor.execute(sql)
  result = cursor.fetchall()
  print(result)
  ```

- **查询第一行数据**

  ``` python
  # fetchone在Python中查询结果是一个字典
  sql = "select * from tb_test where name = 'lisi';"
  cursor.execute(sql)
  result = cursor.fetchone()
  print(result)
  ```

- **修改数据**

  ``` python
  sql = "update tb_test set mobile = '1999998888' where name = 'zhangsan';"
  cursor.execute(sql)
  conn.commit()
  print("修改数据成功！")
  ```

  - **修改多个数据（某行）**

  ``` python
  sql = "update tb_test set name = 'zhaoliu',mobile = '1999999999' where name = 'zhangsan';"
  cursor.execute(sql)
  conn.commit()
  print("修改某行数据成功！")
  ```
  
  - **修改多个数据（某列）**
  
  ``` python
  sql = "update tb_test set mobile = '1999998888';"
  cursor.execute(sql)
  conn.commit()
  print("修改某列数据成功！")
  ```

## Instance

### Add Data Manually

- 在程序中循环手动输入数据，添加至数据库

  ```python
  # 1.引入 pymysql 和 DictCursor
  import pymysql
  from pymysql.cursors import DictCursor
  
  # 2.连接 MySQL 服务器
  # 确保已创建数据库 db_test 和数据表 tb_test (四列：id, username, password, mobile)
  conn = pymysql.Connect(
      host="localhost",
      port=3306,
      user="root",
      password="123456",
      charset="utf8",
      database="db_test"
  )
  print("MySQL 已连接.....")
  cursor = conn.cursor(cursor=DictCursor)
  
  # 3.文件处理
  # 关于文件处理，详见：处理 TXT 文件
  while True:
      username = input("请输入用户名：")
      if username.upper() == "Q":
          break
      password = input("请输入密码：")
      phone = input("请输入手机号：")
  
      # 4.执行 sql
      # 关于执行 sql，详见 Operate MySQL
      sql = "insert into tb_test(username, password, mobile) values(%s, %s, %s)"
      cursor.execute(sql, [username, password, phone])
      conn.commit()
      print("添加数据成功！")
  
  # 5.关闭游标对象和连接
  cursor.close()
  conn.close()
  print("MySQL 已断开连接！")
  ```

### Import Data

- 在程序中从文件获取数据，导入至数据库

  ```
  # users.txt
  # 开头多个换行
  zhangsansan,123,19999999999
  
  lisisi,123,18888888888
  
  wangwuwu,123,16666666666
  # 结尾多个换行
  ```

  ```python
  # 1.引入 pymysql 和 DictCursor
  import pymysql
  from pymysql.cursors import DictCursor
  
  # 2.连接 MySQL 服务器
  # 确保已创建数据库 db_test 和数据表 tb_test (四列：id, username, password, mobile)
  # 确保已创建 users.txt 文件（zhangsan,123,19999999999...）
  conn = pymysql.Connect(
      host="localhost",
      port=3306,
      user="root",
      password="123456",
      charset="utf8",
      database="db_test"
  )
  print("MySQL 已连接.....")
  cursor = conn.cursor(cursor=DictCursor)
  
  # 3.文件处理
  # 确保已创建 users.txt 文件（zhangsan,123,19999999999...）
  # 关于文件处理，详见：处理 TXT 文件
  with open('users.txt', 'r', encoding='utf-8') as f:
      data = f.read().strip()
  
  lst = data.split("\n")
  for line in lst:
      if not line:
          continue
      list_new = line.split(",")  # ['zhangsansan', '123', '19999999999'] for 循环3次，分别得到3个列表
  
      # 4.执行sql
      # 关于执行 sql，详见操作 MySQL
      sql = "insert into tb_test(username, password, mobile) values(%s, %s, %s)"
      cursor.execute(sql, list_new)
      conn.commit()
      print("导入数据成功！")
  
  # 5.关闭游标对象和连接
  cursor.close()
  conn.close()
  print("MySQL 已断开连接！")
  ```

### Export Data

- 在程序中从数据库获取数据（列表嵌套字典），导出至文件

  ```python
  # 1.引入 pymysql 和 DictCursor
  import pymysql
  from pymysql.cursors import DictCursor
  
  # 2.连接 MySQL 服务器
  # 确保已创建数据库 db_test 和数据表 tb_test (四列：id, username, password, mobile)
  conn = pymysql.Connect(
      host="localhost",
      port=3306,
      user="root",
      password="123456",
      charset="utf8",
      database="db_test"
  )
  print("MySQL 已连接.....")
  cursor = conn.cursor(cursor=DictCursor)
  
  # 3.执行sql
  # 关于执行 sql，详见操作 MySQL
  sql = "select id, username, password, mobile from tb_test"
  cursor.execute(sql)
  user_list = cursor.fetchall()  # [{},{}...]
  
  # 4.关闭游标对象和连接
  cursor.close()
  conn.close()
  print("获取数据成功！")
  print("MySQL 已断开连接！")
  
  # 5.文件处理
  for user in user_list:
      line = "{}, {}, {}\n".format(user['username'], user['password'], user['mobile'])
      with open('users.txt', 'a', encoding='utf-8') as f:
          f.write(line)
  print("导出数据成功！")
  ```


# 了解网络编程

# 了解多线程

# Flask 框架

Flask 是一个轻量级的 Python Web 框架，适用于构建小型到中型规模的 Web 应用程序和 API。它由 Armin Ronacher 创建，基于 Werkzeug 和 Jinja2。Flask 的设计目标是简单而灵活，使得开发者能够快速地构建 Web 应用。

## 环境搭建

- 安装 Flask

  ```bash
  # 查看 flask
  pip show flask
  # 安装 flask
  pip install Flask
  ```

## 基本项目

<div style="display: flex; justify-content: left;">
    <img src="assets/image-20240322141019074.png" alt="图片1" style="width: 40%;">
</div>

1. [**来源**：B 站武沛齐《精品 Python 全套课程》P19 10-1 前端开发 - 01:05:36](https://www.bilibili.com/video/BV1zd4y1y7px?p=19&vd_source=02dd98cfbf740b256dca0ec3e66776e6)

2. **说明**

   1. 这是一个没有前端框架和数据库的 Flask 简介项目
   2. 此项目没有整理至《projects》，没有存储至 Git 托管平台

3. Pycharm 创建 Flask 项目

4. 在项目根目录创建后端主程序文件 app.py

   ```python
   from flask import Flask, render_template, request
   
   app = Flask(__name__)
   
   
   # 定义初始页面路由，返回至 register.html 页面
   @app.route("/register")
   def register():
       return render_template("register.html")
   
   
   # 定义 submit 路由，返回至 login.html 页面
   @app.route("/register_ok", methods=["POST"])
   def register_ok():
       # 1.接收用户提交数据
       # 左侧 user 为要存入数据库的变量名，右侧 user 为 form 表单提交数据的变量名
       user = request.form.get("user")
       pwd = request.form.get("pwd")
       role = request.form.get("role")
       gender = request.form.get("gender")
       others = request.form.get("others")
       # 接收复选框  request.args.getlist()
       hobby = request.form.getlist("hobby")
   
       # 2.保存数据
       with open("users.txt", "a", encoding="utf-8") as f:
           line = "{}|{}|{}|{}|{}|{}\n".format(user, pwd, role, gender, hobby, others)
           f.write(line)
       return render_template("login.html")
   
   
   if __name__ == '__main__':
       app.run()
   ```

5. 在 templates 文件夹创建前端文件 register.html, login.html

   - register.html

     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <title>Title</title>
     </head>
     <body>
     <!--定义submit路由和HTTP协议-->
     <form action="/register_ok" method="POST">
         <div>
             <!--"user"作为接收用户输入内容的变量-->
             用户名：<input type="text" placeholder="请输入用户名" name="user">
         </div>
     
         <div>
             密码：<input type="text" placeholder="请输入密码" name="pwd">
         </div>
     
         <div>
             角色：
             <!--"role"作为接收用户选择内容的变量-->
             <select name="role">
                 <option value="teacher">老师</option>
                 <option value="student">学生</option>
             </select>
         </div>
     
         <div>
             性别：
             男<input type="radio" name="gender" value="male"/>
             女<input type="radio" name="gender" value="female"/>
         </div>
     
         <div>
             爱好：
             篮球<input type="checkbox" name="hobby" value="basketball"/>
             足球<input type="checkbox" name="hobby" value="football"/>
             游泳<input type="checkbox" name="hobby" value="swim"/>
         </div>
     
         <div>
             其它：<textarea name="others"></textarea>
         </div>
     
         <input type="submit" value="注册">
     </form>
     </body>
     </html>
     ```

   - login.html

     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <title>login</title>
     </head>
     <body>
     <h1>注册完成，请登录</h1>
     </body>
     </html>
     ```

6. 运行项目，手动进入 register 页面：http://127.0.0.1:5000/register

7. 输入信息，点击注册

   1. 程序会自动在项目根目录创建一个 users.txt 文件，并将用户提交信息存储在文件中。
   2. 页面自动跳转至 login 页面。

## 项目

- Login Flask React

# Django 框架

​	Django 是一个用于构建 Web 应用程序的高级 Python Web 框架。它由 Adrian Holovaty 和 Simon Willison 创建，遵循了“Don't repeat yourself”（不要重复你自己）和“Convention over Configuration”（约定大于配置）等软件设计原则。Django 提供了一套功能强大而完整的工具，使得开发者能够更快速地构建复杂的 Web 应用。

## 创建项目-cmd

- 正常情况通过 pycharm 创建项目

- cmd 中安装 Django 及创建项目

  - 安装 django
  - 进入项目目录
  - 创建项目

  ```
  >pip install django
  >e:回车   进入E盘
  >cd 文件\工作\Pycharm项目\Web开发\Web开发文件笔记   进入想放项目的文件夹
  >django-admin startproject 项目名
  ```

  ```
  - 项目名
  	- manage.py       # 管理当前项目
  	- 项目名
  		- setting.py  # 一部分项目配置
  		- wsgi.py
  		- asgi.py     # 启动项目，接收浏览器发送的请求
  		- urls.py     # 对应关系   浏览器->函数
  ```

  - 启动和关闭项目

  ```
  >进入项目目录
  >python manage.py runserver
  
  关闭：Ctrl + c
  ```

## Django 知识点

- **快速编写一个网站**

  ```python
  from django.contrib import admin
  from django.urls import path
  from django.shortcuts import HttpResponse
  
  def home(request):
      # 1.去request中可以获取请求的数据
      # 2.做一些业务处理
      # 3.给浏览器返回内容
      return HttpResponse("成功")
  
  urlpatterns = [
      path('xxx/xxx/', home),
  ]
  ```

- **app**

  app就是存放不同功能文件的文件夹

  - **创建 app**

    终端terminal

  ```
  >python manage.py startapp app名字
  ```

  ```
  - day15
  	- app01   【所有功能放在一起管理】
  		- views.py   【视图函数：接收请求处理业务逻辑】
  		- models.py  【创建数据库表结构，操作表中数据】
  		- migrations  【数据库相关】
  		- tests.py    【单元测试】
  		- apps.py     【配置】
  		- admin.py    【django内置后台管理】
  ```

  - **注册 app**

    settings.py

  ```python
  -> INSTALLED_APPS = [
      ...
      'app01.apps.App01Config',
  ]
  ```

  - **app 创建文件夹**

  ```
  - day15
  	- app  【所有功能放在一起管理】
  		- static  【存放静态资源】
  			- 详见静态资源
  		- templates  【存放html文件】
  			- html模板
  ```

- **views**

  存放视图函数的文件

  ```python
  # views.py
  
  from django.shortcuts import render
  from django.shortcuts import HttpResponse
  
  def home(request):
      return HttpResponse("成功")
  ```

- **urls**

  存放路径的文件

  ```python
  # urls.py
  
  from django.urls import path
  from app01 import views
  
  urlpatterns = [
      # 访问xxx/xxx/路径，执行home函数
      path('xxx/xxx/', views.home),
  ]
  ```

## html 模板

​	html 模板就是存放 html 文件的文件夹

### 模板位置

- urls.py 配置

  ```python
  from django.contrib import admin
  from django.urls import path
  from app01 import views
  
  urlpatterns = [
      path('xxx/xxx/', views.home),
      path('admin/', admin.site.urls),
  ]
  ```

- views.py 配置

  ```python
  from django.shortcuts import render
  
  def home(request):
      return render(request, 'home.html')
  ```

- 位置1，推荐

  - 确保app01已注册
  - Django去settings.py文件中 INSTALLED_APPS（已注册的所有app）依次寻找templates模板
  - 在app01里创建templates文件夹，里面创建名为home的html文件

- 位置2，不推荐

  - Django优先去settings.py文件中  TEMPLATES -> 'DIRS': [], 寻找templates模板
  - 在项目根目录创建templates文件夹，里面创建名为home的html文件

  ```
  settings.py配置
  import os
  
  -> TEMPLATES -> 'DIRS': [os.path.join(BASE_DIR, 'templates'),],
  ```

### 模板语法

- 基本语法

  - urls.py

  ```python
  from django.urls import path
  from app01 import views
  
  urlpatterns = [
      path('index/', views.index),
  ]
  ```

  - views.py

  ```python
  from django.shortcuts import render
  def index(request):
      data = "中国联通"
      return render(request, 'index.html', {"v1": data})
  ```

  - index.html

  ```html
  <body>
  <!-- html里的变量加双层花括号-->
  <div>{{ v1 }}</div>
  </body>
  ```

- **模板 for 循环**

  - 以列表为例，其它容器同理
  - urls.py同基本语法

  - views.py

  ```python
  def index(request):
      lst = ["张三", "李四", "王五"]
      return render(request, 'index.html', {"v1": data, "v2": lst})
  ```

  - index.html

  ```html
  <body>
  <ul>
      {% for item in v2 %}
          <li>{{ item }}</li>
      {% endfor %}
  </ul>
  </body>
  ```

- **模板索引**

  - 以列表为例，其它容器同理

  - urls.py 和 views.py同基本语法

  - views.py

    v2[0] > v2.0

  ```python
  <div>{{ v2.0 }}</div>
  <div>{{ v2.1 }}</div>
  <div>{{ v2.2 }}</div>
  ```

  - 获取元素对应关系

  ```
  Python-----------html模板
  list[0]----------list.0
  dict["name"]-----dict.name
  dict.keys()------dict.keys
  ```

## 静态资源

​	静态资源：图片、CSS、JavaScript、及插件

### 静态资源位置

- 存储位置思路与html模板相同

- 位置1  推荐

  - 确保app已注册
  - Django去settings.py文件中 INSTALLED_APPS（已注册的所有app）依次寻找templates模板
  - 在app01里创建templates文件夹，里面创建名为static的文件夹

  - static里创建如下文件夹

  ```
  - app01
  	- static
          - CSS      放CSS
          - images   放图片
          - js       放js
          - plugins  放插件
  ```

- 位置2  不推荐

  - Django 优先去 settings.py 文件中  TEMPLATES -> 'DIRS': [], 寻找 templates 模板
  - 在项目根目录创建 templates 文件夹，里面创建名为 static 的文件夹

  ```
  settings.py添加
  import os
  
  STATICFILES_DIRS = (
      os.path.join(BASE_DIR, 'static'),
  )
  ```

### 静态资源引入

- static 里创建如下文件夹

  ```
  - CSS      放CSS
  - images   放图片
  - js       放js
  - plugins  放插件
  ```

- 引入方式

  ```html
  <!-- 顶部引入static文件夹 -->
  {% load static %}
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>login页面</title>
      <link rel="stylesheet" href="{% static 'plugins/bootstrap/css/bootstrap.css' %}">  <!-- head引入其它插件 -->
  </head>
  <body>
  	<!-- 引入图片同理 -->
      <img src="{% static 'images/demo1.png' %}">
      
      <a class="btn btn-danger">删除</a>
  </body>
  </html>
  ```

  - 在顶部引入static文件夹确保系统能找到路径，输入路径时才能有提示。
  - 引入路径时 src="{% static '...' %}"
  - 定义 class 方式不变

## 请求与相应

- **请求与响应**

  <div style="display: flex; justify-content: left;">
      <img src="assets/image-20231104113148646.png" alt="图片1" style="width: 100%;">
  </div>

- **获取请求**

  ```python
  def login(request):
      # 1.1获取请求方式  GET/POST
      print(request.method)
      # 在pycharm底部可以看见用户请求数据的方式GET/POST
  
      # 1.2获取URL中传递的参数  浏览器地址由.../login/变为.../login/?n1=111&n2=222&n3=333
      print(request.GET)# <QueryDict: {'n1': ['111'], 'n2': ['222'], 'n3': ['333']}>
  
      # 1.3单独获取URL中传递的某个参数
      print(request.GET.get("n1"))  # 111
  
      # 1.4获取请求体中传递的数据
      print(request.POST)
  ```

- **响应**

  ```python
  from django.shortcuts import render
  from django.shortcuts import HttpResponse
  from django.shortcuts import redirect
  
  def login(request):
      # 2.1返回一个字符串
      return HttpResponse("你好")
  
      # 2.2返回一个html页面 + 数据渲染
      return render(request, 'login.html')
  
      # 2.3返回一个重定向
      return redirect("http://www.baidu.com")
  ```

- 案例：登录

  ![image-20231104133452264](assets/image-20231104133452264.png)

  views.py

  ```python
  from django.shortcuts import render
  from django.shortcuts import HttpResponse
  from django.shortcuts import redirect
  
  def login(request):
      # 浏览器上输入地址/跳转
      # Django默认传递方式为GET
      if request.method == "GET":
          return render(request, 'login.html')
  
      # 否则就是以POST方式提交
      user = request.POST.get("username")
      pwd = request.POST.get("password")
  
      if user == "root" and pwd == "123":
          # 登录成功，跳转到百度首页
          return redirect("http://www.baidu.com")
  
      else:
          # 登录失败，依然返回登录页面
          # 向html传入占位符error的值
          return render(request, "login.html", {"error":"用户名或密码错误"})
  ```

  login.html

  ```html
  {% load static %}
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>login页面</title>
      <link rel="stylesheet" href="{% static 'plugins/bootstrap/css/bootstrap.css' %}">
  </head>
  <body>
  <h1>用户登录</h1>
  <form action="/login/" method="post">
      <!-- 校验，否则无法提交 -->
      {% csrf_token %}
  
      <input type="text" name="username" placeholder="用户名"/>
      <input type="password" name="password" placeholder="密码"/>
      <input type="submit" value="提交"/>
  
      <!-- 错误提示，占位符error -->
      <span style="color: red;">{{ error }}</span>
  </form>
  
  </body>
  </html>
  ```

## 数据库操作

- Django 操作数据库流程

  <div style="display: flex; justify-content: left;">
      <img src="assets/无标题-2023-11-04-1411.png" alt="图片1" style="width: 80%;">
  </div>	

- 路径配置

  ![image-20231105095347102](assets/image-20231105095347102.png)

  settings.py

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': BASE_DIR / 'db.sqlite3',
      }
  }
  ```

### 查看数据库

- sqlite 驱动

  - 下载驱动https://github.com/xerial/sqlite-jdbc/releases

    <div style="display: flex; justify-content: left;">
        <img src="assets/image-20231104193510562.png" alt="图片1" style="width: 80%;">
    </div>	

    <div style="display: flex; justify-content: left;">
        <img src="assets/image-20231104193729867.png" alt="图片1" style="width: 80%;">
    </div>	

  - 将下载好的sqlite-jdbc-3.43.0.0.jar文件放入如下路径C:\Users\39331\AppData\Roaming\JetBrains\PyCharm2023.2\jdbc-drivers\Xerial SQLiteJDBC\3.43.0\org\xerial\sqlite-jdbc\3.43.0.0
  - 配置

    ![image-20231104194439218](assets/image-20231104194439218.png)

    ![image-20231104194617754](assets/image-20231104194617754.png)

    ![image-20231104194803561](assets/image-20231104194803561.png)

    ![image-20231104195036183](assets/image-20231104195036183.png)

- 查看数据库

  ![image-20231104195320024](assets/image-20231104195320024.png)

  ![image-20231104195722346](assets/image-20231104195722346.png)

### 创建数据表

- 创建类

  ![image-20231104151521903](assets/image-20231104151521903.png)

  models.py

  ```python
  from django.db import models
  
  class UserInfo(models.Model):
      username = models.CharField(verbose_name = "用户名", max_length = 16)
      password = models.CharField(verbose_name = "密码", max_length = 16)
      age = models.IntegerField(verbose_name = "年龄")
  ```

  ```
  - 确保app01已经在settings中注册
  - 创建类以后就会自动生成db.sqlite3，这就是此项目的数据库
  	- 存放在项目根目录db.sqlite3
  - 表名  app名_类名
  - Django默认在第一列创建id，且主键、自增、不重复
  - CharField属性里必须写最大长度
  - verbose_name为了提示开发者，备忘
  ```

- 创建表

  ![image-20231104153624882](assets/image-20231104153624882.png)

  - 终端中先后执行

  ```
  python manage.py makemigrations
  python manage.py migrate
  ```

  - 方法2

    Pycharm --> 工具 --> 运行manage.py任务（Ctrl+Alt+R）

    先后输入执行makemigrations和migrate

### 删除数据表

- 删除表

  ![image-20231104155211390](assets/image-20231104155211390.png)

  ```
  - 将models.py中该表的类注释或者删除
  - 终端中先后执行
      - python manage.py makemigrations
      - python manage.py migrate
  ```

### 删除数据列

- 删除列

  ![image-20231104160037026](assets/image-20231104160037026.png)

  ```
  - 将models.py中此类的该列注释或者删除
  - 终端中先后执行
      - python manage.py makemigrations
      - python manage.py migrate
  ```

### 增加数据行

- ![image-20231104225748556](assets/image-20231104225748556.png)

- **urls.py**

  ```python
  from django.urls import path
  from app01 import views
  
  urlpatterns = [
      path('demo/', views.demo),
  ]
  ```

- **models.py**

  ```python
  from django.db import models
  
  class UserInfo(models.Model):
      username = models.CharField(verbose_name = "用户名", max_length = 16)
      password = models.CharField(verbose_name = "密码", max_length = 16)
      age = models.IntegerField(verbose_name = "年龄")
  ```

- **views.py**

  models.UserInfo.objects.create(增加内容)

  ```python
  from django.shortcuts import HttpResponse
  
  def demo(request):
      from app01 import models
     
  	# 增加数据
      models.UserInfo.objects.create(username = "root", password = "123", age = 19)
      
      return HttpResponse("测试")
  # 访问demo页面就会触发增加数据行
  # 刷新并查看数据表得以验证已经增加数据
  ```

### 删除数据行

- **urls.py 和 models.py 同增加数据行**

- **views.py**

  models.UserInfo.objects.filter(条件1, 条件2...).delete()

  ```python
  from django.shortcuts import HttpResponse
  
  def demo(request):
      from app01 import models
      
      # 删除数据行
      models.UserInfo.objects.filter(age = 20, username = "root").delete()
      
      return HttpResponse("测试")
  # 访问demo页面就会触发删除age = 20且username = "root"的数据行
  # 刷新并查看数据表得以验证已经删除数据
  ```

  ```python
  # 删除全部数据行
  models.UserInfo.objects.all().delete()
  ```

### 修改数据列

- **urls.py 和 models.py同增加数据行**

- **views.py**

  models.UserInfo.objects.all().update(修改内容1, 修改内容2...)

  ```python
  from django.shortcuts import HttpResponse
  
  def demo(request):
      from app01 import models
      
      # 删除数据列
      models.UserInfo.objects.all().update(username = "zhangsan", age = 90)
      
      return HttpResponse("测试")
  # 访问demo页面就会触发修改所有username都是zhangsan，所有的age都是90
  # 刷新并查看数据表得以验证已经修改数据列
  ```

### 修改数据

- **urls.py 和 models.py 同增加数据行**

- **views.py**

  models.UserInfo.objects.filter(条件).update(修改内容1, 修改内容2...)

  ```python
  from django.shortcuts import HttpResponse
  
  def demo(request):
      from app01 import models
      
      # 修改数据
      models.UserInfo.objects.filter(id = 2).update(username = "lisi", age = 80)
      
      return HttpResponse("测试")
  # 访问demo页面就会触发将id = 2的username修改为lisi，age修改为80
  # 刷新并查看数据表得以验证已经修改数据
  ```

### 查询数据

- **urls.py 和 models.py 同增加数据行**

- **views.py**

  models.UserInfo.objects.filter(条件1, 条件2...)

  ```python
  from django.shortcuts import HttpResponse
  
  def demo(request):
      from app01 import models
      
      # 查询并接收数据
      res = models.UserInfo.objects.filter(username = "zhangsan", age = 90)
      print(res)  # QuerySet类型：[obj1, obj2]
      
      # 遍历
      for obj in res:
          print(obj.id, obj.username, obj.password, obj.age)
          # 3 zhangsan 123 90
      
      return HttpResponse("测试")
  # 访问demo页面就会触发查询username = "zhangsan"且age = 90的数据行
  ```

  ```python
  # 查询所有条件数据
  models.UserInfo.objects.all()
  ```

### 案例：页面展示数据库

- <div style="display: flex; justify-content: left;">
      <img src="assets/image-20231105001327278.png" alt="图片1" style="width: 100%;">
  </div>

- **urls.py**

  ```python
  from django.urls import path
  from app01 import views
  
  urlpatterns = [
      path('user/list/', views.user_list),
      path('user/delete/', views.user_delete),
  ]
  ```

- **models.py**

  只要数据库里有数据，不写也行

  ```python
  from django.db import models
  
  class UserInfo(models.Model):
      username = models.CharField(verbose_name = "用户名", max_length = 16)
      password = models.CharField(verbose_name = "密码", max_length = 16)
      age = models.IntegerField(verbose_name = "年龄")
  ```

- **views.py**

  ```python
  from app01 import models
  from django.shortcuts import render
  from django.shortcuts import redirect
  
  def user_list(request):
      lst = models.UserInfo.objects.all()
      return render(request, "user_list.html", {"lst": lst})
  
  def user_delete(request):
      uid = request.GET.get('uid')
      models.UserInfo.objects.filter(id = uid).delete()
      return redirect("/user/list/")
  ```

- **user_list.html**

  ```html
  {% load static %}
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>user_list</title>
      <link rel="stylesheet" href="{% static 'plugins/bootstrap/css/bootstrap.css' %}">
  </head>
  <body>
  
  <div class="container">
      <h1>用户列表</h1>
      <table class="table table-bordered">
          <thead>
          <tr>
              <th>ID</th>
              <th>用户名</th>
              <th>密码</th>
              <th>年龄</th>
          </tr>
          </thead>
          <tbody>
          {% for obj in lst %}
              <tr>
                  <td>{{ obj.id }}</td>
                  <td>{{ obj.username }}</td>
                  <td>{{ obj.password }}</td>
                  <td>{{ obj.age }}</td>
                  <td>
                      <a href="/user/delete/?uid={{ obj.id }}" class="btn btn-danger btn-xs">删除</a>
                  </td>
              </tr>
          {% endfor %}
          </tbody>
      </table>
  </div>
  </body>
  </html>
  ```

## 综合案例

### 创建项目

- 创建项目、创建 app 并注册、引入 static、创建 templates

### 表结构

- 表结构

  ![image-20231105125801723](assets/image-20231105125801723.png)

  ```python
  from django.db import models
  
  # app01_Admin
  class Admin(models.Model):
      """ 管理员表 """
      username = models.CharField(verbose_name = "用户名", max_length = 16)
      password = models.CharField(verbose_name = "密码", max_length = 64)
  
  # app01_DepartMent
  class DepartMent(models.Model):
      """ 部门表 """
      title = models.CharField(verbose_name = "标题", max_length = 16)
  
  # app01_AssetSet
  class AssetSet(models.Model):
      """ 资产表 """
      name = models.CharField(verbose_name = "名称", max_length = 32)
      price = models.IntegerField(verbose_name = "价格")
      category = models.SmallIntegerField(verbose_name = "资产类型",choices = ((1, "办公类"), (2, "3C类"), (3, "房产类"),))                                                       
      # 外键             # DepartMent类                     
      depart = models.ForeignKey(verbose_name = "所属部门", to = "DepartMent", to_field = "id",on_delete = models.CASCADE)# 级联删除
  ```

### 用户登录

- 手动创建 2 个管理员
- 为了赶进度，停止本案例的学习。B 站

# Python Scripts

## Music Crawler

1. 抓包

   <div style="display: flex; justify-content: left;">
       <img src="assets/image-20240405214854742.png" alt="图片1" style="width: 50%;">
   </div>

   1. 浏览器打开音乐播放页面
   2. `F12` 进入开发者工具
   3. 如上图找到“请求网址”
   4. 此网址可以打开直接下载，也可以放在下面脚本中获取音乐文件

2. Script

   ```python
   import requests
   
   # 抓包获取音乐的链接
   url = "$URL"
   
   # get()向服务器发送get请求  .content获取二进制数据（.text 获取文本数据）
   data = requests.get(url).content
   
   # 写入到本地
   with open(r"E:\labs\以后的以后.mp4", "wb") as f:
       f.write(data)
   ```


# 实验

```python
a=3
if a==5:
  c=6
c=7
if a==6:
  if c==7:
    e=8
```
