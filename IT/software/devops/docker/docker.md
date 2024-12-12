# Docker基础

​	Docker 是一个开源的平台，用于开发、交付和运行应用程序。它使用容器技术，通过将应用程序及其依赖项打包到一个容器中，提供了轻量级、可移植和自包含的环境。

## 环境搭建

### Windows 环境

1. 确保 Windows 中已部署WSL

2. 确保 Linux 升级至最新版并运行

3. 确保 Docker Desktop 已安装并运行

4. 启动  `sudo dockerd`


### Linux 环境

1. 下载 Docker 安装脚本并执行：

   ```bash
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   ```

2. 将用户添加到 `docker` 用户组：

   ```bash
   sudo usermod -aG docker $USER
   ```

3. 退出当前终端并重新登录，或者执行下面的命令使用户组更改生效：

   ```bash
   newgrp docker
   ```

4. 验证 Docker 安装：

   ```bash
   docker -v
   ```

5. 启动 Docker

   ```bash
   sudo systemctl start docker
   ```

6. 验证 Docker 服务状态

   ```bash
   sudo systemctl status docker
   ```

7. 将 Docker 添加到开机启动

   ```bash
   sudo systemctl enable docker
   ```

8. 登录

   ```bash
   docker login
   ```

### WSL Ubuntu

1. 更新软件包列表

   ```bash
   sudo apt update
   ```

2. 安装必要的软件包

   ```bash
   sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
   ```

3. 添加 Docker 的官方 GPG 密钥

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. 添加 Docker APT 仓库

   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

5. 再次更新软件包列表，以确保新添加的仓库已经包含在软件包列表中

   ```bash
   sudo apt update
   ```

6. 安装 Docker Engine

   ```bash
   sudo apt install -y docker-ce docker-ce-cli containerd.io
   ```

7. 启动 Docker 服务

   ```bash
   sudo systemctl status docker
   ```

8. 其它同 Linux 安装

## Docker Compose

- Docker Compose 是一个用于管理 Docker 容器的工具。

- Install

  ```bash
  sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  docker-compose --version
  ```

- Command

  ```bash
  # Build and run all containers
  cd $DOCKER_COMPOSE_FOLDER
  docker-compose up
  # Remove all containers
  cd $DOCKER_COMPOSE_FOLDER
  docker-compose down
  ```


## Docker 管理

- **Docker 管理**

  ```bash
  # 查看 Docker 版本信息
  docker -v
  # 显示 Docker 详细版本信息
  docker version
  # 显示 Docker 系统信息
  docker info
  # 登录和登出
  docker login
  docker logout
  ```

## 基本流程

1. 本地已安装并启动登录 Docker
2. 创建项目
5. 项目根目录创建 Dockerfile

4. 终端进入文件夹 HelloDocker 目录
7. 构建推送镜像

   - 手动构建构建镜像保存至本地，加标签，然后手动推送至 DockerHub
   - 通过 GitLab Pipeline 自动构建镜像并自动推送至 DockerHub
8. 运行容器

   - 从本地 image 运行容器
   - 从 DockerHub 拉取 image 运行容器

# [镜像](https://docs.docker.com/reference/cli/docker/image/)

## 镜像基础

- **基础命令**

  ```bash
  # 查看镜像
  docker images
  # 从 Dockerfile 创建镜像
  docker build -t $IMAGE_NAME[:$TAG] $PATH
  # 从容器提交创建镜像
  docker commit $CONTAINER_NAME $IMAGE_NAME[:$TAG]
  # 删除镜像
  docke rmi $IMAGE_NAME[:$TAG]
  # 删除全部镜像
  docker rmi -f $(docker images -aq)
  # 拉取镜像
  docker pull $REPO_NAME/$IMAGE_NAME:$TAG
  # 推送镜像
  docker push $REPO_NAME/$IMAGE_NAME:$TAG
  ```

- **标签**

  ```bash
  # 加标签
  docker tag $IMAGE_NAME:$TAG $REPO_NAME/$IMAGE_NAME:$TAG
  ```

## 其它

# [容器](https://docs.docker.com/reference/cli/docker/container/)

## 容器基础

- **基础命令**

  ```bash
  # 查看容器
  docker ps [-a] # -a表示全部，包含未运行
  # 创建容器
  docker create $IMAGE
  # 启动容器
  docker start $CONTAINER_NAME
  # 创建并启动容器
  docker run [-d] [-it] --name $CONTAINER_NAME $IMAGE
  # 重启容器
  docker restart $CONTAINER_NAME
  # 停止容器
  docker stop $CONTAINER_NAME
  # 删除容器
  docker rm $CONTAINER_NAME
  # 删除全部容器
  docker rm $(docker ps -aq)
  ```

## 其它

- **其它命令**

  ```bash
  # 查看容器日志
  docker logs [OPTIONS] $CONTAINER
  # 检查容器详细信息
  docker inspect [OPTIONS] $CONTAINER [CONTAINER...]
  ```
  
- **进入容器执行**

  ```bash
  docker exec [OPTIONS] CONTAINER [COMMAND] [ARG...]
  # eg：进入容器的 shell 环境
  docker exec -it jerry-container /bin/sh
  # eg：进入容器的 bash 环境
  docker exec -it jerry-container bash
  ```

- [**复制文件**](https://docs.docker.com/reference/cli/docker/container/cp/)

  在容器和本地文件系统之间复制，容器之间不能直接复制

  ```bash
  docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH
  ```


# 命令选项

- **-a (--all)**：

  - 对于镜像：列出本地所有镜像，包括中间层
  - 对于容器：显示所有容器（否则仅显示运行容器）

- [**-c (--change)**](https://docs.docker.com/reference/cli/docker/container/commit/#change)：将 Dockerfile 指令应用于创建的镜像

- **[-d (--detach)](https://docs.docker.com/reference/cli/docker/container/run/#detach)**：在后台运行容器，不占用终端

- [**-e (--env ; --env-file)**](https://docs.docker.com/reference/cli/docker/container/run/#env)：设置环境变量

- [**--entrypoint /bin/sh**](https://docs.docker.com/compose/compose-file/05-services/#entrypoint)：设置容器的入口点，后面的值 `/bin/sh` 表示启动容器后直接进入 Shell 环境。

- [**-f (--force)**](https://docs.docker.com/reference/cli/docker/container/rm/#force)：强制删除运行中的容器

- **-it**：(-i 和 -t 的组合)

  - [**-t (--tty)**](https://docs.docker.com/reference/cli/docker/container/run/#tty)：分配一个伪终端 (TTY) 给容器，这样可以在容器中执行交互式的命令
  - [**-i (--interactive)**](https://docs.docker.com/reference/cli/docker/container/run/#interactive)：让容器的标准输入保持打开，以便我们可以与容器进行交互

- [**--name**](https://docs.docker.com/reference/cli/docker/container/run/#name)：命名容器

- [**-p (--publish)**](https://docs.docker.com/reference/cli/docker/container/run/#publish)：端口映射

  ```bash
  -p $HOST_PORT:$CONTAINER_PORT
  # eg
  -p 80:8080
  ```

- [**`-t $IMAGE_NAME[:$TAG]`**](https://docs.docker.com/reference/cli/docker/image/build/#tag)：命名镜像（-t / --tag），可一次使用多个 `-t`

# [Dockerfile](https://docs.docker.com/reference/dockerfile/#dockerfile-reference)

​	Dockerfile 文件用于构建 docker 镜像，文件中包含了镜像的各种配置信息。

## 命令说明

- **常用命令**

  ```dockerfile
  FROM node:latest
  WORKDIR /app
  COPY ./build .
  RUN npm install -g http-server
  CMD ["http-server", "-p", "8080"]
  ```

- **FROM**：基础镜像

- **WORKDIR**：工作目录

  - 如该目录不存在，WORKDIR 会自动创建
  - 工作目录是进入容器的默认目录，后续指令的工作目录
  - 每一个 RUN 命令都是新建的一层，只有通过 WORKDIR 创建的目录才会一直存在
  - 可以有多个 WORKDIR，对应多阶段的命令

- **EXPOSE**：对外暴露出的端口（只是声明）

- **ADD**：从本地复制文件到容器（还可从 URL 下载）

- **COPY**：从本地复制文件到容器

- **ENV**：设置环境变量

  - `ENV $KEY $VALUE`

- **CMD**：指定容器创建时的默认命令。（可以被覆盖）

- **ENTRYPOINT**：指定容器创建时的默认命令。（不可以被覆盖）

## 相关项目

- Dockerfile Build Image

## 手动训练

1. 这个训练用于手动模拟 Dockerfile 文件创建一个容器化应用的过程。

2. 下载 main.go 至本地 hello 文件夹

   - **文件来源**：[GoogleCloudPlatform/kubernetes-engine-samples/quickstarts/hello-app/](https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/tree/da3e2c22c727e3b6d72d4eea04c19335db0727cb/quickstarts/hello-app)

   - 与 Dockerfile Build Image 项目使用相同文件

   - Linux 下载

     ```bash
     curl -O https://raw.githubusercontent.com/GoogleCloudPlatform/kubernetes-engine-samples/main/quickstarts/hello-app/main.go
     ```

   - main.go

     ```go
     package main
     
     import (
     	"fmt"
     	"log"
     	"net/http"
     	"os"
     )
     
     func main() {
     	mux := http.NewServeMux()
     	mux.HandleFunc("/", hello)
     
     	port := os.Getenv("PORT")
     	if port == "" {
     		port = "8080"
     	}
     
     	log.Printf("Server listening on port %s", port)
     	log.Fatal(http.ListenAndServe(":"+port, mux))
     }
     
     func hello(w http.ResponseWriter, r *http.Request) {
     	log.Printf("Serving request: %s", r.URL.Path)
     	host, _ := os.Hostname()
     	fmt.Fprintf(w, "你好, 世界!\n")
     	fmt.Fprintf(w, "Version: 1.0.0\n")
     	fmt.Fprintf(w, "Hostname: %s\n", host)
     }
     ```

   - Dockerfile

     ```dockerfile
     FROM golang:1.21.0 as builder
     WORKDIR /app
     RUN go mod init hello-app
     COPY *.go ./
     RUN CGO_ENABLED=0 GOOS=linux go build -o /hello-app
     
     FROM gcr.io/distroless/base-debian11
     WORKDIR /
     COPY --from=builder /hello-app /hello-app
     ENV PORT 8080
     USER nonroot:nonroot
     CMD ["/hello-app"]
     ```

3. 模拟 Dockerfile

   ```bash
   #本地全程都在 hello 目录下操作
   
   # 编译环境
   # 创建编译环境容器
   docker run -d -it --name builder golang:1.21.0
   # 进入编译环境容器的 bash 环境
   docker exec -it builder /bin/sh
   # 进入根目录
   cd /
   # 创建工作目录app
   mkdir app
   # 模块化
   go mod init hello-app
   # 退出编译环境容器
   exit
   # 复制 main.go 至容器内的工作目录 app
   docker cp *.go builder:/app
   # 进入编译环境容器
   docker exec -it builder bash
   cd /app
   # 编译你的 Go 应用程序为静态 Linux 可执行文件。然后，你将编译好的可执行文件保存为 /hello-app。
   CGO_ENABLED=0 GOOS=linux go build -o /hello-app
   exit
   
   
   # 生产环境
   # 创建生产环境：通过将应用程序从 builder 镜像中复制到这个镜像中，并设置相应的运行时配置，最终生成的镜像将是一个精简的、只包含应用程序和运行时环境的最小化镜像，从而降低了攻击面和维护成本。
   # 由于不允许运行，我使用了一个新image
   docker run -d -it -p 80:8080 --name runner debian
   # 从编译环境中复制应用程序 hello-ap 到生产环境，由于容器之间不能直接复制，所以以本机作为中转
   docker cp builder:/hello-app .
   docker cp hello-app runner:/hello-app
   
   # 进入生产环境容器的 bash 环境
   docker exec -it runner bash
   # 暴露生产环境的8080端口
   export PORT=8080
   # 添加nonroot用户
   adduser --disabled-password --gecos "" nonroot
   # 运行应用程序
   /hello-app
   ```

4. 访问应用

   ```bash
   # 在容器内访问应用，新建终端，容器环境内有 curl 工具
   curl http://127.0.0.1:8080
   # 在Linux中访问应用
   curl http://127.0.0.1:80
   ```

5. 如果想把 runner 容器 commit 成 Image

   ```bash
   # 创建 Image
   docker commit -c 'ENTRYPOINT ["/hello-app"]' runner $IMAGE_NAME
   # 运行新容器
   docker run -d -it -p 80:8080 --name $CONTAINER_NAME $IMAGE_NAME
   # 随后即可访问
   ```

# 其它



