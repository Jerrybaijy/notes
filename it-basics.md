---
title: it-basics
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - it-basics
  - web
---

# [API 接口](https://developer.mozilla.org/zh-CN/docs/Web/API)

# GUI

**GUI**（Graphical User Interface，图形用户界面） 是指通过图形元素（窗口、按钮、菜单、图标等）与计算机或软件交互的方式。与 **CLI（命令行界面）**不同，GUI 让用户可以使用鼠标、触摸屏或手势操作，而不需要输入命令行指令。

## GUI 实例

- Windows 资源管理器
- macOS Finder

# 二进制

- **二进制**

  - 十进制为整型数据
  - 二进制、八进制、十六进制都是字符串

# 文件名

- **命名规范**

  - 尽量使用英文命名
  - 完全用小写字母
  - 最好用连字符 (`-`) 而不是下划线 (`_`) 来分隔单词

- **大小写敏感**

  - Linux：敏感
  - Windows：不敏感
    - 同一个目录下，不能同时创建 `Document.docx` 和 `document.docx`。
    - 在 CLI 中，`cp Abc.md Abc1.md` 和 `cp abc.md Abc1.md` 命令等效。

- 以 `.` 开头的文件和目录为隐藏文件

# 转义字符

**转义字符**（escape character）是在计算机中用于处理特殊字符的字符，通常是反斜杠（`\`）。它的作用是使得某些具有特殊意义的字符可以作为普通字符使用，或者是为了表示一些难以直接输入的字符（如换行符、制表符等）。

转义字符主要有以下几个用途：

- **避免冲突**：一些字符在编程或文本处理中有特定的含义，直接使用这些字符可能会产生冲突或错误。通过转义字符，可以避免这些冲突。例如，在代码字符串中直接使用引号会让程序误解字符串的开始和结束，使用 `\"` 可以避免这种误解。
- **表示不可见字符**：某些字符如换行符、制表符等通常不可见，但在程序中却非常重要。使用转义字符可以让这些不可见字符变得可操作。
- **输入特殊符号**：有些符号（如反斜杠、引号、以及一些控制字符）直接输入时可能会出错或无法显示，转义字符提供了一种可靠的方式来表示它们。

## 反斜杠

- **反斜杠** `\` 是最常见的转义字符，它用来让下一个字符失去其特殊功能。

  ```python
  strr1 = "Hello world!"
  print(strr1)  # Hello world!

  strr2 = "\"Hello,world!\""
  print(strr2)  # "Hello,world!"
  ```

- **说明**：反斜杠本身也需要通过转义来表示。在某些编程语言中，表示一个反斜杠字符本身时需要写成 `\\`。

## 取消转义

- 某些字符串中掺杂转义字符，比如路径、网址等，此时需要取消转义。
- **`\` 方式取消**

  ```python
  # 两个“\”代表双重转义=不转义
  strr = "E:\\labs\\test"
  print(strr)   # E:\labs\test
  ```

- **`r` 方式取消**

  ```python
  # 路径中的 \l 和 \t 都是转义字符
  strr = r"E:\labs\test"
  print(strr)  # E:\labs\test
  ```

## 换行符

- 换行符 `\n` 可以实现一个字符串分两行输出

  ```python
  data = "这是第一行！\n这是第二行！"  # \n换行符
  print(data)
  
  # 这是第一行！
  # 这是第二行！
  ```

## 制表符

- **制表符** `\t` 可以实现字符串中相邻两个字符距离远一些

  ```python
  data = "你是谁？\t离我远一点！"  # \t制表符
  print(data2)  # 你是谁？    离我远一点！
  ```

## Unicode 字符

- **Unicode 字符** `\u` 用于表示一个 Unicode 字符，后面跟上字符的 Unicode 编码。
- 例如，`\u0041` 表示字符 `A`。

## 其它转义字符

- 回车符 `\r`
- 换页符 `\f`
- 垂直制表符 `\v`
- 响铃符 `\a`

# 通配符

- **通配符（Wildcard）** 是一种简化的模式匹配工具，适用于快速查找和文件筛选。
- **通配符**：就是确定要查的到底是几个字。

  - `*` 用于匹配**任意数量的字符**（包括零个字符），不论是字母、数字还是符号。
  - `?` 用于匹配**单个字符**，不论是字母、数字还是符号。比如 `张?郎` 代表要查的是三个字，`张??郎` 代表要查的是四个字。

- **注意**：不同系统或工具的通配符实现可能存在差异。

  - Linux Shell
  - 数据库 SQL 语言

- **应用场景**

  - 文本（字符串）
  - 文件名
  - 数据库
  - 编程
  - Shell 脚本

- **常用通配符**

  <table style="text-align: center;">
    <tr>
      <th>通配符</th>
      <th>功能</th>
      <th>示例</th>
    </tr>
    <tr>
      <td><code>*</code></td>
      <td>匹配任意数量的字符（包括零个字符）</td>
      <td><code>a*</code> 可以匹配 <code>a</code>、<code>abc</code>、<code>apple</code>、<code>a123</code></td>
    </tr>
    <tr>
      <td><code>?</code></td>
      <td>匹配任意单个字符</td>
      <td><code>a?c</code> 可以匹配 <code>abc</code>、<code>adc</code>，但不能匹配 <code>abdc</code></td>
    </tr>
    <tr>
      <td><code>[ ]</code></td>
      <td>匹配括号内的任意一个字符</td>
      <td><code>a[bc]d</code> 可以匹配 <code>abd</code> 或 <code>acd</code></td>
    </tr>
    <tr>
      <td><code>[! ]</code> 或 <code>[^ ]</code></td>
      <td>匹配括号内未出现的任意字符</td>
      <td><code>a[!b]d</code> 或 <code>a[^b]d</code> 匹配 <code>acd</code>，但不匹配 <code>abd</code></td>
    </tr>
    <tr>
      <td><code>{ }</code></td>
      <td>匹配指定的多个字符串</td>
      <td><code>file{1,2,3}.txt</code> 匹配 <code>file1.txt</code>、<code>file2.txt</code>、<code>file3.txt</code></td>
    </tr>
    <tr>
      <td><code>#</code></td>
      <td>在某些工具中表示匹配任意单个数字（如 0-9）</td>
      <td><code>file#</code> 可匹配 <code>file1</code>、<code>file2</code> 等</td>
    </tr>
  </table>

# 占位符

**占位符**（Placeholder）是一种**临时表示**的符号或文本，用于占据待输入的字符位置。

各种环境的占位符风格并不绝对统一，个人按以下习惯进行书写：

- 一般情况：`<container_name>`
- Shell 脚本或环境变量：`$DOCKER_HUB_TOKEN`
- 可选参数：`[option]`

# Unicode 字符

## 全角和半角

[全角和半角](https://zh.wikipedia.org/wiki/全角和半角)是文字的两种显示形式，“全角”指文字字身长宽比为一比一的正方形，而“半角”为宽度为全角一半的文字。

**半角 (Half-width)**

- 字符宽度是**半个方格**，占用约 **一个英文字符**的宽度。
- 用在英文、数字、编程、网址等地方。

**全角 (Full-width)**

- 字符宽度是**一个方格**，占用约**一个汉字**（即**两个英文字符**）的宽度。
- 用在中文排版、特殊对齐时。

**全角与半角切换**

- `Shift + Space`

[Unicode 字符检测](https://www.fileformat.info/info/unicode/char/search.htm?q=)

## Unicode 字符示例

<!-- prettier-ignore -->
| 符号 | 名称 | Unicode 编码 | 宽度 | 输入 | 用法 | 示例 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| \- | Hyphen-Minus<br />连字符-减号 | U+002D | 最短 | <span title="即全键盘0右侧的按键">**半角**模式的**减号键**</span> | **英文排版**的连接符或减号<br /><small title="专业排版使用 U+2212 码减号">[注]</small> | -5<br />well-known |
| － | Full-width Hyphen-Minus<br />全角连字符-减号 | U+FF0D | 汉字宽度 | **全角**模式的**减号键** | **中文排版**的连接符或减号<br /><small title="专业排版使用 U+2212 码减号">[注]</small> | 硫化－催化反应 |
| − | Minus Sigh<br />减号（专业） | U+2212 |  | — | **专业排版**中的减号或负号 | x − y = 5 |
| – | En dash<br />短破折号 | U+2013 | N的宽度 | `Alt + 0150`<br /><small title="小键盘">[注]</small> | 英文范围 | 1990–2000 |
| — | Em dash<br />破折号 | U+2014 | M的宽度 | `Alt + 0150`<br /><small title="小键盘">[注]</small> <small title="传统破折号（Shift + -）的一半">[注]</small> | 中文范围；<br />转折语气、插入语 | 266年—420年 |

# 时间处理

## 时间戳

**时间戳**（Timestamp）是指格林威治时间（GMT）1970 年 01 月 01 日 00 时 00 分 00 秒（北京时间 1970 年 01 月 01 日 08 时 00 分 00 秒）起至现在的总秒数。

- 之后为正数，之前为负数。
- [时间戳查询工具](https://www.epochconverter.com/)

## Day.js

**[Day.js](https://day.js.org/docs/en/display/format)** 是一个轻量级的 **JavaScript 日期处理库**，用于处理日期和时间的格式。如 `YYYY` 表示四位数的年份。

**常用示例**：

<!-- prettier-ignore -->
| 标记符 | 示例 | 含义 |
| :---: | :---: | :---: |
| YYYY | 2024 | 四位数的年份 |
| YY | 24 | 两位数的年份 |
| X | -94353724800 | Unix 时间戳<br />可表示公元前的复数 `-2000` |
| MM | 04 | 两位数的月份（01-12） |
| M | 4 | 月份（1-12） |
| DD | 09 | 两位数的日期（01-31） |
| D | 9 | 日期（1-31） |
| HH | 14 | 24小时制的小时（00-23） |
| mm | 05 | 分钟（00-59） |

## d3-time-format

**[d3-time-format](https://d3js.org/d3-time-format#locale_format)** 是 D3.js 的一个**独立模块**，专门用于日期和时间的解析与格式化。

它和 `dayjs`、`moment.js` 类似，但更偏向于**数据可视化场景**（比如时间轴、坐标轴刻度标签）。

**常用示例**：

<!-- prettier-ignore -->
| 标记符 | 示例 | 含义 |
| :---: | :---: | :---: |
| %Y | 2024 | 四位数的年份 |
| %y | 24 | 两位数的年份 |
| %-Y | 50 | 使用 `-` 取消前导零，<br />显示 `50` 而不是 `0050` |
| %m | 04 | 两位数的月份（01-12） |
| %d | 09 | 两位数的日期（01-31） |
| %H | 14 | 24小时制的小时（00-23） |
| %M | 05 | 分钟（00-59） |
| %a | Tue | 缩写的星期几 |
| %b | Apr | 缩写的月份名称 |

# 固件类型

现代计算机的固件主要有以下两种类型：`传统 BIOS` 和 `UEFI`

## BIOS

**BIOS**（Basic Input/Output System）也常被称为 **传统 BIOS** 或 **Legacy BIOS**，是计算机系统中最早的固件之一。

**BIOS 的局限性：**

- **启动速度慢**：由于 BIOS 是基于 16 位代码，并且采用了传统的启动流程，启动速度相对较慢。
- **容量有限**：BIOS 固件存储空间有限，通常只能存储少量的配置选项和引导程序。
- **硬件支持有限**：BIOS 的设计较早，不能支持现代硬件（如大容量硬盘、复杂的设备接口等），且不支持较大的硬盘（2TB 以上）。

## UEFI

**UEFI**（Unified Extensible Firmware Interface）是 BIOS 的现代替代品。

**UEFI 的优势：**

- **更强的扩展性**：UEFI 使用模块化设计，支持更多的驱动程序和扩展功能。它允许操作系统开发者和硬件厂商定制固件，提供更多特性和功能。
- **更好的兼容性**：UEFI 能够兼容旧版 BIOS 模式（通过“兼容性支持模块”CSM），因此支持使用旧版操作系统（如 Windows 7）启动。
- **更好的安全性**：通过安全启动和其他安全机制，UEFI 能够保护系统免受恶意软件的攻击。

## CSM

**CSM**（Compatibility Support Module），即兼容模式，允许计算机在 UEFI 和 BIOS 之间切换，从而使得支持旧操作系统和硬件的同时，仍然能享受 UEFI 带来的新特性。

# 磁盘分区

## 磁盘分区表类型

硬盘的分区表类型主要有两种：**MBR（Master Boot Record）**和**GPT（GUID Partition Table）**。

### MBR

**MBR（Master Boot Record）**，即**主引导记录**，是一种传统的分区表格式。

- 与**Legacy BIOS**（基本输入输出系统）固件配合使用。
- 传统的分区表格式，最多支持 4 个主分区或 3 个主分区加 1 个扩展分区。
- 每个分区最大支持 2TB 的容量。
- 不支持大于 2TB 的硬盘和更多的分区数。
- 兼容性较好，尤其是在较老的系统中，许多老旧的 BIOS 系统使用 MBR。

### GPT

**GPT（GUID Partition Table）** ，即**GUID 分区表**，是一种现代的硬盘分区表格式，是对传统 MBR（Master Boot Record）分区表的一种改进和替代。

- 与**UEFI**固件配合使用
- 是现代硬盘的分区方式，支持更多分区，最多支持 128 个主分区。
- 支持更大的硬盘（单个分区最大可支持 9.4ZB 的容量，实际硬盘通常限制在几 TB 或几十 TB）。
- 对硬盘的备份和恢复有更好的支持，具有冗余分区表。

一个典型的 Windows 系统 GPT 磁盘的分区布局如下：

```
| ESP分区（FAT32）|  MSR分区（MSR）|  主操作系统分区（NTFS）  |   恢复分区    |
|  100MB-300MB  |  16MB-128MB   |     数十GB-几百GB      |  500MB-几GB  |
```

在**Windows 系统**中，当磁盘使用**GPT**（GUID Partition Table）类型时，通常会有几个与系统相关的重要分区。

- **EFI 系统分区（EFI System Partition，ESP）**

  - **大小**：通常为 100MB 到 300MB 之间，具体取决于系统和配置。
  - **类型**：**FAT32**文件系统。
  - **作用**：这个分区包含了计算机启动所需的引导加载程序（Bootloader），以及其他与启动相关的文件（如 UEFI 固件的启动文件）。它是 UEFI 启动方式所必需的分区，Windows 操作系统和其他操作系统（如 Linux）在此分区中放置自己的引导文件。

- **微软保留分区（Microsoft Reserved Partition，MSR）**

  - **大小**：通常为 16MB 到 128MB。
  - **类型**：没有文件系统，不可直接访问。
  - **作用**：MSR 分区是一个保留分区，用于 Windows 操作系统在 GPT 磁盘上管理和维护其他分区。它并不存储任何用户数据，也不包含操作系统文件，而是为未来的分区调整、配置和一些系统功能（如动态磁盘）保留空间。一般情况下，用户无需关心这个分区。
  - **默认名称**：**Microsoft Reserved Partition**。

- **主操作系统分区（Windows 主分区）**

  - **大小**：根据系统安装大小不同，通常为数十 GB 到几百 GB。
  - **类型**：**NTFS**文件系统。
  - **作用**：这是安装了 Windows 操作系统的主分区，包含所有操作系统文件、用户数据、程序等。一般来说，这是用户访问和操作的分区，它存储着 Windows 的核心文件和大多数应用程序。

- **恢复分区（Recovery Partition）**

  - **大小**：通常为 500MB 到几 GB。
  - **类型**：**NTFS**或**FAT32**文件系统。
  - **作用**：恢复分区包含了 Windows 恢复环境（Windows RE）的文件，用于在系统崩溃或出现严重问题时进行修复。它可以帮助用户重置或恢复系统，或者使用系统修复工具进行恢复操作。
  - **默认名称**：**恢复分区**（在 Windows 中显示为**恢复**或**恢复工具**）。

## 文件系统类型

文件系统类型是操作系统用于组织和存储数据的一种方法。

### NTFS

**NTFS (New Technology File System)**：主要用于 Windows 操作系统，支持大文件、高效的存储管理、权限控制等特性。

### FAT32

**FAT32 (File Allocation Table 32)**：一种较老的文件系统，兼容性较强，但不支持超过 4GB 的文件。

### exFAT

**exFAT (Extended File Allocation Table)**：适用于大文件，特别是在 USB 驱动器和存储卡中使用。

### ext4

**ext4 (Fourth Extended File System)**：常见于 Linux 操作系统，具有高效的性能和稳定性，支持大文件和日志功能。

### HFS+

**HFS+ (Hierarchical File System Plus)**：用于苹果操作系统（macOS），支持元数据和文件权限。

### APFS

**APFS (Apple File System)**：苹果的下一代文件系统，设计用于 SSD 和其他闪存驱动器，支持更高的效率和更好的安全性。

### Btrfs

**Btrfs (B-tree File System)**：Linux 中的一种现代文件系统，提供快照、压缩和去重等功能。

### ReFS

**ReFS (Resilient File System)**：微软开发的一个用于 Windows Server 的文件系统，设计上注重数据完整性和修复能力。
