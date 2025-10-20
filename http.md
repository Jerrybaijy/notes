---
title: http
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - web
---

# HTTP

[**HTTP**](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)（**H**yper**T**ext **T**ransfer **P**rotocol，超文本传输协议），是一种用于分布式、协作式和超媒体信息系统的应用层协议，旨在使客户端（通常是浏览器）能够和服务器进行通信和数据交换，是万维网数据通信的基础。

# 请求方法

[**HTTP 请求方法**](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Reference/Methods)定义了浏览器将如何发送表单数据以及服务器应该如何处理这些数据。

## GET

**[GET 方法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)**

当使用 `GET` 方法提交表单时，表单数据会附加在 URL 的末尾（query string），并以键值对的形式出现。这种方式适合用于获取数据，但不适合包含敏感信息，因为数据会明文显示在 URL 中。GET 方法通常用于数据检索，而不涉及对服务器上数据的修改。

## POST

**[POST 方法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST)**

使用 `POST` 方法提交表单时，表单数据会包含在表单体内，而不会显示在 URL 中。这种方式更适合用于提交敏感信息和对服务器上数据进行修改。POST 方法通常用于表单提交，文件上传等需要传输大量数据或包含敏感信息的场景。传递文件必须使用 `POST` 形式传递。
