---
title: vue：vue版本之间的区别
date: 2020-03-27 08:51:17
tags: vue
category: 技术
---

![](https://pic3.zhimg.com/80/v2-120c6f2e62e740210a77ab3c87d65c0e_1440w.jpg)

<!--more-->

- 运行时版本 vue.runtime.js

  - 不支持从 html 获取视图；
  - 不支持 template，需要通过 webpack 的工具 vue-loader 将组件，预编译 template 模板为 render 函数；
  - 没有 complier 编译器，因此代码体积会比完整版小 40%，html 转化成节点。

    `<script src="https://cdn.bootcss.com/vue/2.6.9/vue.runtime.min.js"></script>`

- 完整版 vue.js
  - 支持从 html 获取视图；
  - 支持 template；
  - 有 complier 编译器，而 complier 可以将字符串
    `<script src="https://cdn.bootcss.com/vue/2.6.10/vue.min.js"></script>`
