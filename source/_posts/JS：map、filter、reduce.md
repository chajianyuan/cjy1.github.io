---
title: JS：map、filter、reduce
date: 2020-03-22 09:28:46
tags: javascript
category: 技术
---

### 1、map

```
let arr = [1,2,3]
arr.map((item, index, array)=> item = item+1)  => [2, 3, 4]
```

<!--more-->

`map`的回调函数可接受三个参数，遍历原数组，对每个元素进行操作，返回一个新数组。

### 2、filter

```
let arr = [1,2,3]
arr.map((item, index, array)=> item != 2)  => [1, 3]
```

`filter` 的回调函数也可以接受三个参数，在遍历原数组事，将返回值为 true 的元素放在新数组中，返回新数组。

### 3、reduce

```
let arr = [1,2,3]
arr.map((acc, current) => acc+ current, 0)  => 6
```

`reduce`接收两个参数，分别是回调函数和初始值。
