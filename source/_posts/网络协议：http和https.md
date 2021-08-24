---
title: 网络协议：http和https
date: 2020-03-25 08:39:45
tags: 网络协议
category: 技术
---

## 一、http

![](https://user-gold-cdn.xitu.io/2018/6/11/163ef70cbdc63e95?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

HTTP 协议是 Hyper Text Transfer Protocol(超文本传输协议)的缩写，适用于从万维网服务器传输文本到本地浏览器的传送协议。

<!--more-->

### 1、http/1.1 的缺陷

- 高延迟--带来页面加载速度的降低；
- 无状态特性--带来的巨大 HTTP 头部；
- 明文传输--带来的不安全性；
- 不支持服务器推送消息。

### 2、http/2

**新特性：**

- 二进制传输；
- Header 压缩；
- 多路复用；
- Server Push；
- 提高安全性

**缺陷：**

- TCP 以及 TCP+TLS 建立连接的延时；
- TCP 的队头阻塞并没有彻底解决。

### 3、HTTP/3

**QUIC**是基于 UDP 的一个协议，让 http 跑在 QUIC 上而不是 TCP 上。而这个“HTTP over QUIC”就是 HTTP 协议的下一个大版本--HTTP/3。

#### QUIC 新功能

- 实现了类似 TCP 的流量控制、传输可靠性的功能；
- 实现了快速握手功；
- 集成了 TLS 加密功能；
- 多路复用，彻底解决 TCP 中队头阻塞的问题。

## 二、HTTPS

HTTPS（全称：Hyper Text Transfer Protocol over Secure Socket Layer），是以安全为目标的 HTTP 通道，简单讲是 HTTP 的安全版。

**HTTP 和 HTTPS 的区别：**

- HTTP 是明文传输，HTTPS 通过 SSL/TLS 进行了加密；
- HTTP 的端口号是 80，HTTPS 的是 443；
- HTTPS 需要到 CA 申请证书，一般免费证书很少，需要交费；
- HTTPS 的连接很简单，是无状态的；HTTPS 协议是 SSL+HTTP 协议构建的可进行加密传输、身份认证的网络协议，比 HTTP 协议安全。

[掘金：关于 http 协议，你必须要知道的](https://juejin.im/post/5b1e93aa5188257d3914280e)

[掘金：解密 http/2 与 http/3 的新特性](https://juejin.im/post/5d9abde7e51d4578110dc77f)

[掘金：谈谈 HTTPS](https://juejin.im/post/59e4c02151882578d02f4aca)
