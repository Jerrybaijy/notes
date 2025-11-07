---
title: shell
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - it-basics
  - script
---

# Shell

## Shell

Shell 语言（或称为 Shell Scripting Language）是用于编写 Shell 脚本的编程语言。

Shell 语言不是一种单一的、规范的语言，而是一系列 **Unix-like 操作系统命令行解释器** 所使用的编程语言的总称。最常见和最有影响力的是 **Bourne Shell (sh)** 及其衍生品，如 **Bash**、**Zsh**、**Ksh** 等。

**Shell Script** 是一个包含了一系列 **Shell 命令** 的文本文件。

- `#!/bin/bash`：Shebang，指定解释器。
- `#`，注释，可以在行尾注释。
- **`exec $SHELL`**：执行完毕保持窗口。

# 变量

## 赋值

变量名和等号之间不能有空格。

```bash
NAME="World"
AGE=30
```

## 引用变量

 使用 `$` 符号来引用变量的值。

```bash
NAME="World"
echo "Hello, $NAME"
```

## 环境变量

使用 `export` 关键字将变量提升为环境变量。

```bash
export PATH="/usr/local/bin:$PATH"
```

# 控制结构

## 选择结构

使用方括号 `[ ... ]` 或双层方括号 `[[ ... ]]` 进行条件测试。

```bash
if [ -f "venv/bin/activate" ]; then
    # Linux/macOS/Git Bash
    source venv/bin/activate
elif [ -f "venv/Scripts/activate" ]; then
    # Windows (WSL 或部分环境可能需要)
    source venv/Scripts/activate
else
    echo "错误：无法找到虚拟环境激活脚本。"
    exit 1
fi
```

## 循环结构

```bash
for file in *.log; do
    echo "Processing $file"
done

i=0
while [ $i -lt 5 ]; do
    echo $i
    i=$((i + 1)) # Bash 算术扩展
done
```

# 函数

```bash
my_function() {
    echo "Executing function with argument: $1"
    return 0
}

my_function "test_value"
```

# 关键字

## `echo`

### 基本实现

`echo` 用于在标准输出（终端）上打印文本。

```bash
echo "输出文本"
```

### `-e`

`-e` 选项用于启用 `echo` 命令的**转义功能**。以下是改变输出文本样式的示例：

```bash
echo -e "\033[1;32m输出文本\033[0m"
```

![image-20251107191551704](assets/image-20251107191551704.png)
