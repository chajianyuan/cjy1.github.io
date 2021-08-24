---
title: html：行内元素、行内块级元素、块级元素
date: 2019-10-15 21:42:11
tags: html
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、行内元素

可以通过`display: inline`设置

<!--more-->

**特点**

1. 设置宽高无效
2. 对 margin 仅设置左右有效，设置 padding 有效，即会撑大空间
3. 不会自动换行

**举例**

< span >、< b >、< i >、< a >、< sub >、< sup >、< br >

## 二、行内块级元素

可以通过`display: inline-block`设置

**特点**

1. 可以设置宽高
2. 设置 margin、padding 都有效
3. 不自动换行，默认排序从左到右

**举例**

< img >、< input >、< td >

## 三、块级元素

可以通过`display: block`设置

**特点**

1. 可以设置宽高
2. 设置 margin、padding 都有效
3. 能自动换行，多个块级元素写在一起默认从上到下

**举例**

< p >、< div >、< ul >、< li >、< h1 >-< h6 >、< ol >
