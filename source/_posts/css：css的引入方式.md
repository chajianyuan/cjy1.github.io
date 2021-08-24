---
title: css：css的引入方式
date: 2020-03-22 09:48:54
tags: css
category: 技术
---

### 1、css 的引入方式有三种

（1）行内式将样式写在元素的 style 属性里面

（2）内嵌式将样式写在< style >元素里面

（3）外链式指通过 link 标签引入 css 文件

<!--more-->

### 2、link 和@import 引入样式文件的区别

（1）加载资源的限制

link 是 XHTML 的标签，除了加载 css 文件之外，还能加载 RSS 等其他事务，如加载模板等；

@import 只能加载 css 文件

（2）加载方式

用 link 引用 css，在页面载入时同时加载，即同步加载；

用@import 引用 css，则需要等到网页完全载入后，再加载 css 文件，即异步加载

（3）兼容性

link 是 XHTML 标签，没有兼容问题

@import 是在 css2.1 中提出的，不支持低版本的浏览器

（4）改变样式

link 的标签是 DOM 元素，支持使用 JavaScript 控制 DOM 和修改样式

@import 是一种方法，不支持控制 DOM 和修改元素
