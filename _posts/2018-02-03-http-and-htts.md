---
title: HTTP和HTTPS
key: 20180203
tags: http https
---

超文本传输协议 (HTTP) 是一个用来通过互联网传输和接收信息的协议。`HTTPS` (基于安全套接字层的超文本传输协议 或者是 `HTTP over SSL`) 是一个 `Netscape` 开发的 `Web` 协议,也可以说：**`HTTPS = HTTP + SSL`**; `HTTPS` 在 `HTTP` 应用层的基础上使用安全套接字层作为子层。

<!--more-->

**不同之处：**

`HTTP` 的 URL 以 `http://` 开头，而 `HTTPS` 的 URL 以 `https://` 开头
{:.warning}

`HTTP` 是不安全的，而 `HTTPS` 是安全的
{:.info}

`HTTP` 标准端口是 `80` ，而 `HTTPS` 的标准端口是 `443`
{:.warning}

在 `OSI 网络模型` 中，`HTTP` 工作于应用层，而 `HTTPS` 工作在传输层
{:.info}

`HTTP` 无需加密，而 `HTTPS` 对传输的数据进行加密
{:.warning}

`HTTP` 无需证书，而 `HTTPS` 需要认证证书
{:.info}