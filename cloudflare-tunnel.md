```yaml
title: cloudflare-tunnel
author: Jerry.Baijy
tags:
  - it
  - it-basics
  - web
```

# Cloudflare Tunnel

在不需要购买域名、不需要配置繁琐 SSL 证书的情况下，**Cloudflare Tunnel** 可以让 Web 应用的 HTTP 地址变为 HTTPS 地址。

## 核心优势

- **内网穿透**：服务器无需暴露公网 IP，无需开启防火墙入站端口。
- **自动 HTTPS**：Cloudflare 自动提供受信任的 SSL 证书，彻底解决插件的 `Mixed Content` 拦截问题。
- **成本为零**：不需要购买域名，利用 Cloudflare 提供的免费二级域名。

## 项目背景

Green Assistant 项目运行在阿里云服务器上，前端控制台的访问地址为 `http://<公网 IP>:8081`，由于不是 `https` 安全地址，浏览器禁止插件的脚本向这个地址发请求。

## 安装

- 以阿里云的 RHEL 系统为例

- 前往 [Cloudflare 下载页](https://github.com/cloudflare/cloudflared/releases) 下载，当前为 [cloudflared-fips-linux-x86_64.rpm](https://github.com/cloudflare/cloudflared/releases/download/2026.3.0/cloudflared-fips-linux-x86_64.rpm)

- 将下载的文件传入云服务器，然后安装

  ```bash
  sudo dnf localinstall cloudflared-fips-linux-x86_64.rpm
  ```

## 启动服务

终端会输出一个类似 `https://your-random-site.trycloudflare.com` 的地址。该地址即可代替`http://<公网 IP>:8081`（如 `http://35.101.2.46:8081`）访问目标地址。

### 后台模式

```bash
# 后台启动并将日志写入 tunnel.log
nohup cloudflared tunnel --url http://localhost:8081 > tunnel.log 2>&1 &

# 查看当前分配的随机域名
grep -o 'https://.*\.trycloudflare\.com' tunnel.log
```

> [!Warning]
>后台模式产生的域名在服务器未重启期间有效。如果服务器重启，域名会重新生成。

> [!TIP]
>可以将该服务加入随系统启动

### 前台模式

此模式用于临时测试

```bash
cloudflared tunnel --url http://localhost:<服务端口>
cloudflared tunnel --url http://localhost:8081
```

> [!Warning]
>前台模式产生的域名在 `cloudflared` 进程运行期间有效。如果进程重启，域名会重新生成。

## 固定公网域名

如果你希望域名永远不变（如 `ga.company.com`），请执行以下进阶操作：

- 购买一个永久域名
- **注册账户**：在 [Cloudflare 官网](https://dash.cloudflare.com/) 注册免费账号。
- **创建命名隧道**：
  1. 在 `Zero Trust` 菜单中创建一个 `Tunnel`。
  2. 获取唯一的 **Tunnel Token**。
  3. 在服务器运行 `cloudflared service install <YOUR_TOKEN>` 将其安装为系统服务。
- **绑定域名**：在 Cloudflare 后台将你的域名指向该隧道。
- **效果**：无论服务器如何重启，你的 HTTPS 地址永远固定，用户无需重复登录同步。
