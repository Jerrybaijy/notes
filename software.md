---
title: software
author: Jerry.Baijy
tags:
  - dev
  - software
---

# 通用

## 说明

- 这是一个软件学习笔记的合集。
- 不是特别多的笔记内容都集中在这一个笔记中。
- 每个1级标题都是一个软件，以首字母排序。
  - 实验

## Todo List

- **Daily**
  - [ ] slack dev-misc
- **Shell Script**
  - [ ] Windows
  - [ ] Linux
- **System**
  - [ ] ssh linux
  - [ ] rdp windows
- **Net**
  - [ ] domain name、IP、DNS
  - [ ] server
  - [ ] nslookup

# Mp3tag

[**Mp3tag**](https://www.mp3tag.de/en/) 是一个音乐标签管理工具。

<!-- prettier-ignore -->
| 变量 | 描述 |
| :---: | :---: |
| FILENAME | 文件名 |
| %album% | 唱片集 |
| %title% | 标题 |
| %artist% | 参与创作的艺术家 |
| %genre% | 流派 |
| %comment% | 备注 |
| %track% | 音轨 |
| %year% |年 |
| %_total% | xx/xx 曲目编号字段中的曲目总数 |

# MyDockFinder

[**MyDockFinder**](https://www.mydockfinder.com/) 是一款 Windows 平台上的桌面管理工具，可以设置 MyFinder 和 MyDock。

![image-20250111184147133](assets/image-20250111184147133.png)

## 环境搭建

- Steam 已安装
- 在 Steam 中购买安装 MyDockFinder

# Nexus

[**Winstep Nexus**](https://www.winstep.net/nexus.asp) 是一款功能强大的桌面增强工具，主要用于创建和管理**动态桌面工具栏**（Dock）。相比传统的 RocketDock，Nexus 更允许被高度定制。

- 不支持拖放图标

# Pandoc

[**Pandoc**](https://pandoc.org/) 是一个文档转换工具，支持多种文档格式之间的转换。

## 环境搭建

- [下载 pandoc-3.5-windows-x86_64.msi](https://github.com/jgm/pandoc/releases)
- 修改安装路径

  <img src="assets/image-20241122120939289.png" alt="图片1" style="width: 60%;">

  <img src="assets/image-20241122121208576.png" alt="图片1" style="width: 60%;">

- 点击 `Install` 安装，直到完成
- 验证

  ```bash
  pandoc -v
  ```

## 命令

- **命令**

  ```bash
  # 查看版本
  pandoc -v
  # 帮助
  pandoc --help
  ```

## word 转 MD

- 使用命令行转换

  ```bash
  pandoc 文件名1 -o 文件名2 --extract-media=图片存储路径
  ```

  ```bash
  pandoc 实验.md -o 实验.docx --extract-media=./assets
  ```

  - **`--extract-media`**：可以提取媒体文件并存储到指定路径。

# Podman

[**Podman**](https://podman.io/) 是一个用于管理容器的工具，类似于 Docker。

## 环境搭建

- 安装

  ```bash
  sudo apt install podman
  ```

- 验证

  ```bash
  podman --version
  ```

# Prometheus

[**Prometheus**](https://prometheus.io/) 是一个开源的监控和警报工具，最初由 Sound Cloud 开发。它专为云环境而设计，可以动态发现目标，并收集它们的度量指标，存储这些指标，并提供基于这些指标的警报功能。

## Basics

### Install

- [This part is from NANA, and it is unfinished.](https://www.youtube.com/watch?v=QoDqxm7ybLc)
- **Requirement**
  - Cluster is running.
  - Helm has been installed and the repo 'arldka' is added into local.

- Install

  ```bash
  helm install prometheus arldka/prometheus-operator
  ```

### Install

- [**Source:** This part is from IBM.](https://www.youtube.com/watch?v=VMP48mMBDZw)
- **Requirement:** Git, Docker, Docker Compose
- install

  ```bash
  git clone https://gitlab.com/jerrybai/pmi-prometheus-grafana-sample.git
  cd pmi-prometheus-grafana-sample
  docker-compose up
  ```

- This will build and run 3 containers.
- Access WAS PMI metrics - Prometheus endpoint http://localhost:9080/metrics
- Access Prometheus Server UI [http://localhost:9090](http://localhost:9090/)
- Access Grafana [http://localhost:3000](http://localhost:3000/)

  Login: admin / admin

- Stop

  ```bash
  docker stop grafana prometheus twas_metrics
  ```

- Restart

  ```bash
  docker start grafana prometheus twas_metrics
  ```

# Rainmeter

[**Rainmeter**](https://www.rainmeter.net/) 是一款非常流行的桌面定制软件，主要用于在 Windows 系统上创建并显示动态桌面小部件（Widgets）或皮肤（Skins）。

## 环境搭建

- [官网下载 Rainmeter](https://www.rainmeter.net/)
- 正常安装并运行 Rainmeter
- 关闭所有默认显示的皮肤
- 保存空主题

    <img src="assets/image-20250107211655284.png" alt="image-20250107211655284" style="zoom:50%;" />

## 相关资源

- [致美化](https://zhutix.com/)
- [htvisualskins](https://visualskins.com/)

# Rufus

[**Rufus**](https://rufus.ie/zh/) 是一款轻量级、开源的工具。它可以帮助用户将 ISO 镜像文件（例如操作系统安装盘镜像）写入 U 盘，制作启动 U 盘，类似与 Windows 的 U 盘介质。

## 特点

- 按选项安装 Windows
- 无 PE 启动 U 盘

## 功能说明

- **镜像选项（Windows）**
  - **标准 Windows 安装**：即制作正常启动 U 盘。
  - **Windows To Go**：即把系统安装在 U 盘里，得到一个可以完整运行的 Windows 系统。
    - 当把 U 盘变成 Windows To Go 以后，插入任一台电脑，即可使用这个 Windows 系统。
    - **注意**：这台电脑和 Windows To Go 的引导方式要相同。
    - 当完成初始化设置以后，拔出 U 盘，再次插入电脑，运行 Rufus，即可把 Windows To Go 保存为 VHDX 镜像，供给 Ventoy 使用。

- **持久分区大小（Linux）**：当 Linux 以 Live CD 运行时，用来保存 Live 运行时所做的修改。否则关机后会丢失所有修改。
- **分区类型**
  - **GPT**：对应 UEFI 引导
  - **MBR**：对应传统 BIOS 引导

- **高级设备选项**
  - **显示 USB 外置硬盘**：如果插入的是移动硬盘且无法识别，即可勾选此项。
  - **启用对旧 BIOS 修正**：这是对传统 BIOS 引导的优化，提高兼容性。

- **卷标**：即 U 盘名称
- **高级格式化选项**
  - **创建扩展的标签和图标文件**：把 U 盘图标变成 Rufus

## 使用步骤

- [官网下载 Rufus 工具](https://rufus.ie/zh/)
- 电脑插入已备份的 U 盘（制作时会格式化）
- 双击已下载的 `.exe` 文件，免安装打开工具
- 配置安装选项
  - 选择 U 盘驱动器和 ISO 镜像文件，修改卷标（U 盘名称）

      <img src="assets/image-20250213133434262.png" alt="image-20250213133434262" style="zoom:50%;" />

  - 如果不是老电脑，`分区类型` 和 `目标系统类型` 按工具默认选择即可
  - 点击 `开始`
  - 弹出选项窗口，选择需要的选项，点击 `确定`。

      <img src="assets/image-20250213133611614.png" alt="image-20250213133611614" style="zoom:50%;" />

- Rufus 会将 ISO 镜像文件写入 U 盘并创建启动盘。
- 将 U 盘插入待做系统的电脑，从 U 盘启动做系统（注意此工具不是 PE，只能像 Windows 官网安装介质那样做系统）。

# Trae

[**TRAE**](https://www.trae.ai/) 是由字节跳动推出的一款 IDE。它不仅仅是在传统编辑器上增加 AI 功能，而是从底层开始就以 AI 为核心构建的。

- Chat：使用**自然语言**与 AI 交互
- Builder：使用**内置工具**借助 AI 自动开发
- Builder with MCP：调用**第三方 MCP 工具**借助 AI 自动开发

> [Trae 文档](https://docs.trae.cn/ide/what-is-trae?_lang=zh)

# TranslucentTB

[**TranslucentTB**](https://translucenttb.com/) 是一款免费的 Windows 桌面工具，主要用于自定义 Windows 任务栏的外观，特别是实现任务栏的透明效果。

# Ventoy

## Ventoy 基础

[**Ventoy**](https://www.ventoy.net/cn/index.html) 是一个开源的工具，主要用于创建多重引导 USB 启动盘。与传统的方式不同，Ventoy 不需要你为每个操作系统或工具单独创建启动盘，而是只需将 ISO 文件复制到 USB 驱动器，然后通过 Ventoy 启动这些 ISO 文件。

## 制作 Ventoy U 盘

- 下载并解压 Ventoy。
- 将 USB 驱动器插入电脑，运行 `Ventoy2Disk.exe` 安装到 USB 上。
  - **安全启动**：选中。
  - **分区类型**：GPT。
  - **分区文件系统类型**：Ventoy U 盘的分区类型；为了保证新台式机安装系统成功，选 NTFS。

      <img src="assets/1f24a424ec08957d283e32508eba9ab.png" alt="1f24a424ec08957d283e32508eba9ab" style="zoom:50%;" />

- 将你需要的 ISO 镜像文件直接复制到 USB 驱动器中。
- 重启电脑，选择从 USB 启动，Ventoy 会显示一个菜单让你选择要启动的 ISO 文件。

## 配置 Ventoy U 盘

- 运行 `VentoyPlugson.exe` 配置制作好的 Ventoy U 盘。

## Ventoy 启动菜单

在使用 **Ventoy** 时，选择了一个启动项后进入了如下的菜单：

- **Boot in normal mode**：标准启动模式，适用于大多数操作系统和工具。
- **Boot in wimboot mode**：wimboot 模式，用于从 Windows WIM 文件启动，适用于 Windows PE 或安装镜像。
- **Boot in memdisk mode**：memdisk 模式，将 ISO 文件加载到内存中启动，适用于旧版操作系统或某些特殊工具。
- **File checksum**：文件校验，用于验证 ISO 文件的完整性，确保文件没有损坏。
- **Return to previous menu**：返回到主菜单或前一个菜单，供你重新选择启动选项。

# Wallpaper Engine

[**Wallpaper Engine**](https://www.wallpaperengine.io/zh-hans) 是一款非常流行的桌面壁纸管理工具。

## 环境搭建

- Steam 已安装
- 在 Steam 中购买安装 Wallpaper Engine

## 使用方式

- 在选择 Wallpaper Engine 中选择 `创意工坊`
- 选中喜欢的壁纸，点击 `订阅`。
- 待下载完成，点击 `确认` 即可。


