---
title: Node：学习koa.js
date: 2020-03-26 09:01:10
tags: koa
category: 技术
---

## 一、优缺点

- **优点：** no callback
- **缺点：** content/express 的中间件基本不能重用，基本要重写；依然需要更多人的支持和学习。

<!--more-->


nidemon依赖可以使node服务器软件边开发边重新启动

ejs 模版引擎

knexjs 链接数据库


```
const Koa = require('koa');
const app = new Koa();

const sleep = timeout => new Promise((resolve) => setTimeout(resolve, timeout));

// 中间件（middleware）
app.use(async(ctx, next) => {
  await sleep();
  // next是一个Promise对象
  await next();
});

app.listen(8080);
```