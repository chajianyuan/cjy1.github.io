---
title: ES7：新特性
date: 2021-08-24 10:36:33
tags: ES
category: 技术
---
ES2016（也就是ES7）中新增了如下特性：
* `Array.prototype.includes`
* `Exponentiation Operator`
<!--more-->

### 一、`Array.prototype.includes`

#### 1. 定义

`includes()`方法用来判断一个数组或字符串中是否包含一个指定的值

**返回值：**如果包含返回`true`，否则返回`false`。

#### 2. 语法

* `arr.includes(valueToFind)`
* `arr.includes(valueToFind, fromIndex)`

```
let arr = [1, 2, 3, 4];
arr.includes(3);        // true
arr.includes(5);        // false
arr.includes(3, 1);     // true
```
##### 1）fromIndex大于等于数组长度

**返回`false`**
```
arr.includes(3, 3);     // false
arr.includes(3, 20);    // false
```
##### 2）计算出的索引小于0

如果`fromIndex`为负值，使用`数组长度 + fromIndex`计算出的索引作为新的`fromIndex`，如果新的`fromIndex`为负值，则搜索整个数组。

```
arr.includes(3, -100);  // true
arr.includes(3, -1);    // false
```

### 二、`Exponentiation Operator`幂运算

幂运算符`**`，相当于`Math.pow()`

```
5 ** 2                  // 25
Math.pow(5, 2)          // 25
```

### 参考

1. [MDN includes地址](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

