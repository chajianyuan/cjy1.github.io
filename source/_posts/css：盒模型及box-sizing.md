---
title: css：盒模型及box-sizing
date: 2019-10-15 22:08:24
tags: css
category: 技术
---

<meta name="referrer" content="no-referrer"/>

<img src="https://github.com/chajianyuan/picture/blob/master/1681617070154_.pic.jpg?raw=true" width="600px" />

<!--more-->

### 一、盒模型

![](https://user-gold-cdn.xitu.io/2017/10/25/9cb491d4bd5d326aeb16632280411283?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

#### 1、IE 盒模型（box-sizing:border-box）

width = 2 x border + 2 x padding + content

height = 2 x border + 2 x padding + content

**实际盒子宽度 = width**

#### 2、标准盒模型（box-sizing:content-box）

width = content

height = content

**实际盒子宽度 = width + 2 x padding + 2 x border**

### 二、box-sizing

css3新增属性，`box-sizing: content-box | border-box`用来设置标准模型和IE模型

### 三、外边距重叠

当两个外边距相遇时，会形成一个外边距，合并后的外边距高度等于合并前两个外边距最大的那一个

> ⚠️ 只有普通文档流中块级元素的**垂直外边距**才会发生合并。