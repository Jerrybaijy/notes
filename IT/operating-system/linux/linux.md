# Linux 基础

Linux 是一个开源的类 Unix 操作系统内核。它是一个多用户、多任务、支持多种处理器架构的操作系统。

## 环境搭建

### 在 Windows 中搭建

- 在 Windows 中搭建 Linux 有以下方法：虚拟机、WSL、Live CD/USB、远程服务器。
- 接下来使用 WSL 方法。
- 确保 WSL 已安装，详见 [`Windows` > `WSL`](../windows/windows.md#WSL)。
- 在 Microsoft Store 中选择的 Linux 发行版，例如 "Ubuntu 20.04 LTS"。
- 安装完成后，点击启动，设置用户名和密码。
  - **注意**：即使你输入密码，也不会在屏幕上显示，就像没输入一样。

### 在裸机上安装

- 以 Ubuntu 为例，并且抹掉整个硬盘。

- [官网下载 Ubuntu Desktop 的 ISO 文件](https://ubuntu.com/download/desktop)。

- [下载 Rufus，制作启动 U 盘](https://rufus.ie/zh/)。

    <img src="assets/image-20250208202758425.png" alt="image-20250208202758425" style="zoom:50%;" />

- 重启电脑，进入 U 盘启动。

- 选择 `Try Or Install Ubuntu`，进入类似 PE 的 Ubuntu 系统。

- 右下角双击 `Install Ubuntu` 图标。

- 安装过程中会询问如何分区，如果想把整个磁盘作为 Ubantu 的运行磁盘，选择擦掉即可，安装程序会自动分区。

- 安装完成后，手动重启，根据提示，应先拔掉 U 盘，然后按 `Enter` 重启。

- 重启后即可进行初始设置。

## Zsh

- Zsh（Z Shell）是一种命令行解释器，也是一种交互式的 Unix shell，它是 Bash 的替代品。

- 安装 Zsh

  ```bash
  # 安装
  sudo apt install zsh
  # 设置 Zsh 为默认 shell
  chsh -s $(which zsh)
  ```

- 安装 Oh-My-Zsh 插件

  ```bash
  # 下载
  wget https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh
  # 安装
  sh install.sh
  ```


- 安装 Zsh 主题和插件

  ```bash
  # PowerLevel10k主题
  git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
  # zsh-autosuggestions自动提示插件
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  # zsh-syntax-highlighting语法高亮插件
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```

- 编辑 `~/.zshrc` 文件启用插件和主题

  ```shell
  # 修改主题
  ZSH_THEME="powerlevel10k/powerlevel10k"
  
  # 启用插件
  plugins=(
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
  )
  ```

- 重启终端，启动 PowerLevel10k 配置向导

  ```bash
  p10k configure
  ```

## 路径

- **目录结构**：`/Home/USER_NAME/...`
- **路径分隔符**：正斜杠 `/`
- **Linux 特有路径（区别于 Windows）**
  - Home目录：`cd` 或 `/Home`
  - 上一次的工作目录：`cd -`

- 其它详见 [`web-basics` > `路径`](../../web-basics/web-basics.md#路径)

# 包管理工具

Linux 包管理工具用于简化和管理软件包的安装、更新、卸载和依赖管理。不同的 Linux 发行版采用不同的包管理工具和格式，但它们的目标是相同的，即简化系统和应用软件的管理。

## apt

**`apt`** 是基于 Debian 的包管理工具，用于管理 `.deb` 格式的包（如 Ubuntu、Debian 等系统）。

Ubuntu 默认使用 `apt` 作为包管理工具。

`apt` 常用命令包括：

- `sudo apt update`：更新软件包列表。
- `sudo apt upgrade`：升级已安装的包。
- `sudo apt install <package>`：安装软件包。
- `sudo apt remove <package>`：卸载软件包。

## snap

**`snap`** 也是一种包管理系统，专门用于管理和安装 **Snap 包**，它是一个跨发行版的包管理工具。

## dpkg

`dpkg` 是一个较底层的工具，`apt` 会调用 `dpkg` 来安装 `.deb` 包文件，`dpkg` 通常用来手动安装单个 `.deb` 包，但不管理依赖关系。

## 其它

# 系统管理

## 服务管理 systemctl

- 开机启动

    ```bash
    # 设置开机启动
    sudo systemctl enable $APP
    
    # 禁用开机启动
    sudo systemctl disable $APP
    
    # 查看开机启动
    sudo systemctl is-enabled $APP
    ```

- 运行和停止

    ```bash
    # 运行应用
    sudo systemctl start $APP
    
    # 停止应用
    sudo systemctl stop $APP
    
    # 查看应用状态
    sudo systemctl status $APP
    ```

- 其它服务管理

    ```bash
    # 以超级权限执行命令（让普通用户变成root用户）
    sudo $COMMAND
    ```

## 用户管理 usermod

- 修改用户组

    ```bash
    sudo usermod -aG docker jerry
    ```

    - 默认情况下，只有 `root` 用户或使用 `sudo` 前缀才能运行某些命令，如 `docker`。将当前用户加入 `docker` 组以后，可以不使用 `sudo` 来执行 Docker 命令。
    - 修改用户组以后，需退出当前终端并注销系统重新登录，使用户组生效。如果不想注销，可以直接在终端中使用 `newgrp docker` 命令，这个命令会让你切换到新的组，并使更改立即生效。但关闭当前终端再进入时，还是会失效，除非注销重新登录。

- 其它用户管理命令

    ```bash
    # 查看当前用户
    whoami
    
    # 创建用户
    sudo adduser $NEW_USER
    
    # 切换用户
    su - $USER
    ```

# Curl

`curl` 是一个用于与网络服务器进行数据交换的命令行工具。

## 下载文件

- 下载并显示文件内容

    ```bash
    curl http://example.com/file.txt
    ```

- 下载的文件，并按原文件名保存

    ```bash
    curl -O http://example.com/file.txt
    ```

- 下载的文件，并按指定路径和文件名保存

    ```bash
    curl -o myfile.txt http://example.com/file.txt
    ```

## 上传文件

- 上传文件

    ```bash
    curl -X POST -F "file=@myfile.txt" http://example.com/upload
    ```

# 文件

## 文件基础

- **基础命令**

  ```bash
  # 查看文件
  cat $FILE
  # 创建文件
  touch $FILE
  # 编辑文件
  nano $FILE
  vim $FILE
  # 删除文件
  rm $FILE
  # 复制文件
  cp $FILE $DES_PATH
  ```

- **文本搜索**

  ```bash
  grep CONTENT
  ```

- 替换

  `sed`：流编辑器，用于对文本进行流式处理；`-i`：在原文件修改；`s`：替换；`g` ：全局替换

  ```bash
  sed -i 's/SOURCE_CONTENT/NEW_CONTENT/g' 'PATH/FILE'
  # eg
  sed -i 's/aaa/bbb/g' './html.py' # 将当前文件夹下的html.py文件中的aaa替换成bbb
  ```

- `echo`：快速向文件添加内容

  ```bash
  echo "[CONTENT]" > [FILE]
  # eg
  echo "Hello World!" > demo.txt
  ```

- 查找文件

  ```bash
  find PATH OPTION COMMAND
  # eg
  find . -name jquery* -print # 查找当前目录下所有文件名以jquery开头的文件，并打印路径
  ```

## Vim

**Vi**（Vi IMproved）是 Unix 系统上最早的文本编辑器之一，**Vim**（Vi IMproved）是 Vi 的增强版。

### Basics

- Basics

  ```bash
  # show version
  vi / vim
  # open / create file
  vim $FILE
  # into insert mode
  i
  # back to command mode
  `Esc`
  # exit
  :q
  # save and exit
  :wq
  ```

### Command mode

- Default enter into command mode.

  ![image-20240406160608629](assets/image-20240406160608629.png)

- `Esc`: Back to command mode

- `dd`: Cut cursor line. `2dd`: Cut cursor and next line

- `yy`: Copy cursor line. `2yy`: Copy cursor and next line

- `p`: Paste at next line of cursor. `2p`: Paste at next line of cursor 2 times

- `Ctrl + F`: Page Up. `Ctrl + U`: Page Up Half.

- `Ctrl + B`: Page Down. `Ctrl + D`: Page Down Half.

### Insert mode

- Into insert mode
  - `i`: before cursor
  - `I`: line beginning
  - `a`: after cursor
  - `A`: line end
  - `o`: next new line
  - `O`: previous new line
- Edit
  - `^`: jump to line beginning
  - `$`: jump to line end

### Last line mode

- `:`: Into last line mode
- `:q`: exit
- `:wq`: save and exit
- `:set nu`: show line number
- `:set nonu`: close line number

# 文件夹

## 文件夹基础

- **基础命令**

  ```bash
  # 创建文件夹
  mkdir [PATH] FOLDER_NAME
  # 删除空文件夹
  rmdir [PATH] FOLDER_NAME
  # 删除非空文件夹
  rm -r [PATH] FOLDER_NAME
  # 列出文件夹内容
  ls [-al] # -al列出隐藏内容
  ```

# 命令选项

- `-rf` 选项是 `-r` 和 `-f` 的组合

  `-r` 选项，以确保递归删除子目录和文件。

  `-f` 选项，强制删除。

# 其它

- **`|`**：管道符，命令输出传递；eg：打开 `tmp` 文件夹中的 `html.py` 文件，然后找出字符串 `jquery-1.11.3.min.js`

  ```bash
  cat /tmp/html.py | grep jquery-1.11.3.min.js
  ```

# 解决方法

## 密码反馈

在 Linux 终端中，默认情况下，输入密码时是不可见的，这是出于安全性考虑。然而，如果你想让密码在输入时可见，有一些方法可以实现。

- 打开 sudoers 文件：`sudo visudo`

- 找到 `Defaults   env_reset` 行，添加 `pwfeedback`，如下

  ```bash
  Defaults env_reset,pwfeedback
  ```

- 这将启用密码反馈功能，使得在输入密码时可以看到 * 星号，但仍然不是明文显示。


## 安装软件

- 官网下载软件的 `.deb` 安装包

- 终端进入 `下载` 目录

   ```bash
   sudo dpkg -i [软件名]
   # eg
   sudo dpkg -i google-chrome-stable_current_amd64.deb
   ```


## 更新下载源

- 当执行 `sudo apt update` 时，提示以下信息

    ```bash
    E: 仓库 “file:/cdrom noble Release” 不再含有 Release 文件。
    N: 无法安全地用该源进行更新，所以默认禁用该源。
    N: 参见 apt-secure(8) 手册以了解仓库创建和用户配置方面的细节。
    ```

- 错误信息表明，系统无法从指定的仓库（`file:/cdrom noble Release`）获取 `Release` 文件，因此该源被禁用。这通常发生在你尝试从一个无效或不可用的源更新软件包时。

- 右键打开 `/etc/apt/sources.list` 文件，检查是否有指向 `file:/cdrom` 的源。

- 如果发现 `file:/cdrom` 相关的行，可以将其注释掉（在行首添加 `#`）或删除，然后保存。

- 重新更新。

