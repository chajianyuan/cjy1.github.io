---
title: html：cookie、session、sessionStorage、localStorage详细讲解
date: 2019-10-26 14:45:47
tags: html
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、cookie

### 1、cookie 的来源

cookie 的本质工作并非本地存储，而是“维持状态”。因为**http 协议是无状态的，http 协议本身并不对请求和响应之间的通信状态进行保存**，通常来说，服务器不知道用户上一次做了什么。

<!--more-->

### 2、什么是 cookie 及应用场景

**cookie**是某些网站为了辨别用户身份而存储在本地终端上的数据（通常经过加密）。

cookie 是服务端生成，客户端进行维护和存储。

![](https://user-gold-cdn.xitu.io/2019/3/20/1699babec3c4fcc4?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

cookie 以键值对的形式存在。

**典型的应用场景**

- 记住密码，下次自动登录
- 购物车功能
- 记录用户浏览数据，进行广告（商品）推荐

### 3、cookie 的原理

**cookie 原理**

![](https://user-gold-cdn.xitu.io/2019/3/21/1699f22b7029ca14?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 第一次访问网站时，浏览器发出请求，服务器响应请求后，会在响应头重添加一个 Set-Cookie 选项，将 cookie 放入响应请求中，
- 浏览器收到 Set-Cookie 选项后将它保存在本地
- 在浏览器第二次发起请求时，通过 cookie 请求头部将 cookie 信息发送给服务器，服务端会辨别用户身份。

## 二、session

session 代表着服务器和客户端一次会话的过程。session 对象存储特定用户会话所需的属性及配置信息。这样，当用户在应用程序中的 web 页之间跳转时，存储在 session 对象中的变量将不会丢失，而是在整个会话中一直存在下去。当客户端关闭会话，或者 session 超时失效后会话结束。

## 三、cookie 和 session 的关系

![](https://user-gold-cdn.xitu.io/2019/5/13/16aafb5d90f398e2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 用户第一次请求服务器时，服务器根据用户提交的相关信息，创建对应的 session，请求返回时将此 session 的唯一标识符 sessionID 返回给浏览器，
- 浏览器收到 sessionID 后，将它保存在 cookie 中，同时 cookie 记录 sessionID 属于哪个域名
- 当用户第二次访问服务器时，请求会自动判断此域名下是否存在 cookie 信息，如果存在自动将 cookie 信息也发送给服务端，服务端会从 cookie 中获取 sessionID，再根据 sessionID 查找对应的 session 信息，如果没有找到说明用户没有登录或者登录失效，如果找到 session 证明用户已经登录可执行后面操作

## 四、cookie 和 session 的区别

- **存放位置不同**，cookie 数据保存在客户端的浏览器上，session 数据保存在服务器上；
- **存取方式不同**，cookie 只能是字符串，session 可以是任意数据类型
- **隐私策略不同**，cookie 不是很安全，别人可以分析存放在本地的 cookie 并进行 cookie 欺骗，考虑到安全问题应该使用 session
- **存储大小不同**，单个 cookie 保存的数据不能超过 4K，session 可存储数据远高于 4K
- **有效期不同**，cookie 可以较长时间保存，session 在客户端关闭或者 session 超时都会失效

## 五、localStorage、sessionStorage、cookie 的区别

- **http 请求**
  - cookie 每次都会携带在 HTTP 头中，如果使用 cookie 保存数据过多会带来性能问题
  - sessionStorage 和 localStorage 不会把数据发送给服务器，仅在本地保存
- **存储数据大小**
  - cookie 存储的数据不能超过 4K
  - sessionStorage 和 localStorage 可以达到 5M 或更大
- **数据存储有效期**
  - cookie 在设置的 cookie 过期时间之前有效，如果没有设置，默认是关闭浏览器后失效
  - sessionStroage 仅在关闭当前窗口之前有效，关闭页面或浏览器后会被清除
  - localStorage 始终有效，除非被手动清除
- **易用性**
  - cookie 需要自己封装，原生的 cookie 接口不太友好
  - localStorage 和 sessionStorage：原生接口可以接受，也可以再次封装来对 Object 和 Array 有更好的支持
