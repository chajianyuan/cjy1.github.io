---
title: css：css小技巧
date: 2021-04-16 15:08:58
tags: css
category: 技术
---

这篇文章记录在实践中用到的一些css小技巧:high_brightness:

<!--more-->

#### 1. :paw_prints: 文本省略

* 两行或多行省略
```
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
/*! autoprefixer: off */
-webkit-box-orient: vertical;
```
* 一行省略
```
overflow: hidden;
white-space: nowrap;
text-overflow: ellipsis;
```
一行省略除了使用上面代码中的方法，还可以将多行省略代码中的限制行数设置为1

#### 2. :paw_prints: 将网站文字变成繁体字

```
document.body.style.fontVariantEastAsian='traditional';
```

