---
title: script
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - it-basics
  - script
---

# Script

## Script

**脚本**（Script）是一种包含了一系列计算机命令的文本文件，这些命令是按照预定的顺序执行的，目的通常是为了自动化任务或控制程序。

- **解释执行：** 脚本通常不需要经过复杂的“编译”过程。代码是**逐行**由一个名为“解释器”（Interpreter，例如 Bash、Python 解释器）的程序直接读取和执行的。这使得开发和测试周期大大缩短。
- 编写脚本所使用的语言被称为**脚本语言**，如 Shell/Bash、Python、SQL 等。

脚本包含了一系列 `脚本命令`，就像你在命令行里输入它们一样。以下是一个简单的 `Git push` 示例：

```bash
git add .
git commit -m "Daily preservation"
git push
exec $SHELL
```

## 创建脚本

- 以下是一个 Shell 脚本示例。

- 使用记事本创建一个 `.txt` 文件；

- 在记事本中输入想要的命令，以 `Git push` 为例；

  ```bash
  git add .
  git commit -m "Daily preservation"
  git push
  exec $SHELL
  ```

- 保存文件并关闭；

- 将文件后缀名 `.txt` 改为 `.sh`，例如 `python-env.sh`；


## 使用脚本

以下几种方法都可以使用脚本：

- 双击 `python-env.sh` 文件。

- 在 Bash 终端调用 `Bash` 解释器，不可以停在基本激活的 python 虚拟环境。

  ```bash
  # 标准写法
  bash python-env.sh
  
  # 简写
  ./python-env.sh
  ```

- 在 Bash 终端调用 `sh` 解释器，不可以停在基本激活的 python 虚拟环境。

  ```bash
  sh python-env.sh
  ```

- 在 Bash 终端调用 `source`，可以停在基本激活的 python 虚拟环境。

  ```bash
  # 标准写法
  source python-env.sh
  
  # 简写
  . python-env.sh
  ```

##  Shebang

**Shebang** 是一种告诉操作系统内核应该使用哪个**解释器**来执行该文件的机制。

任何类型的脚本都可以使用 Shebang 来指定其解释器。以下是一些常见的例子：

| **脚本类型**   | **Shebang 示例**         | **执行方式**             |
| -------------- | ------------------------ | ------------------------ |
| **Bash Shell** | `#!/bin/bash`            | 使用 Bash 解释器执行     |
| **Python**     | `#!/usr/bin/env python3` | 使用 Python 3 解释器执行 |
| **Perl**       | `#!/usr/bin/perl`        | 使用 Perl 解释器执行     |
| **Node.js**    | `#!/usr/bin/env node`    | 使用 Node.js 解释器执行  |

## 文件后缀名

- 在 Linux/Unix/macOS 环境下
  - 无论脚本文件是否有后缀名，Shell（如 Bash）主要依靠文件内容**首行的 Shebang** 来识别和执行脚本。
  - 提高**可读性**和**可识别性**。用户或文本编辑器可以立即知道这个文件的类型。
- 在 Windows 环境下
  - 系统通过后缀名来匹配对应的解释器或程序。
  - 无法直接通过双击来运行脚本文件。
