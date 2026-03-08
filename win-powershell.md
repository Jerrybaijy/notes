---
title: win-powershell
author: Jerry.Baijy
tags:
  - it
  - windows
---

# FAQ

## 脚本权限

因为 Windows 出于安全考虑，默认**禁止运行未签名的 PowerShell 脚本**。

```
iex : 无法加载文件 C:\Program Files\nodejs\npm.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 h
ttps:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。
所在位置 行:1 字符: 45
+ iwr -useb https://openclaw.ai/install.ps1 | iex
+                                             ~~~
    + CategoryInfo          : SecurityError: (:) [Invoke-Expression]，PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.InvokeExpressionComman
   d
```

以**管理员身份**运行 PowerShell，执行以下命令，允许运行自己编写的脚本，以及来自互联网但由受信任发布者签名的脚本：

```shell
# 查看当前 PowerShell 的脚本执行策略
Get-ExecutionPolicy
# 如果需要查看所有作用域
Get-ExecutionPolicy -List

# 临时允许（关闭窗口后自动恢复默认安全模式）
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
# 长期允许
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

## 跨环境使用

在 Git Bash 中使用启动一个新的 PowerShell 进程来执行引号内的指令

```bash
powershell -Command "<powershell-command>"
```
