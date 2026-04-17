```yaml
title: cloudflare-warp
author: Jerry.Baijy
tags:
  - it
  - it-basics
  - web
  - cloudfla
```

# Overview

[**Cloudflare WARP**](https://one.one.one.one/) 是一款由 [Cloudflare](https://www.cloudflare.com/zh-cn/) 推出的网络连接优化与安全工具。它建立在 Cloudflare 著名的 **1.1.1.1** 公共 DNS 解析器基础之上，但功能更进一步：1.1.1.1 仅保护你的 DNS 查询，而 WARP 则通过加密隧道保护你设备发出的**所有**互联网流量。可代替 VPN 连接国际互联网。

> [Cloudflare One](https://developers.cloudflare.com/cloudflare-one/)
>
> [小白研究所视频教程](https://www.youtube.com/watch?v=phUqW-pT6_s)
>
> [小白研究所博客教程](https://www.xbiit.net/2026/02/2026-cloudflare-warpvpnvpn.html)

# Config

## 电脑端

- 下载安装 Cloudflare WARP 以后

- 在 `C:\ProgramData\Cloudflare` 目录创建 `mdm.xml` 文件，修改协议：

  ```xml
  <dict>
      <key>warp_tunnel_protocol</key>
      <string>masque</string>
  </dict>
  ```

- 重启电脑生效

## 手机端

- 在 [Cloudflare 控制台](https://dash.cloudflare.com/)创建 zero trust
- 安装 Cloudflare One 并登录 zero trust

# FAQ

## 无法连接

- 至今未找到完全解决的方案
- 一般重启软件或电脑可解决
- 实在不行就重装软件

## 关于 IP

- 官方宣称不隐藏 IP
- 实际使用时，查询自己的 IP 地址一般是美国。
- 同一次连接之内，IP 不会变化。
- 每次连接的 IP 都不一样

## 优点

- 免费，速度快。
- 各个限制地区的网站都能用

## 缺点

- 对国内网站也生效