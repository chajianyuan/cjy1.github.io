---
title: JS：for..in和for..of的区别
date: 2019-10-17 20:50:45
tags: javascript
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 1、for...in

**for...in 主要用于遍历对象，取到的是 key**

<!--more-->

**缺陷**

1. 索引是字符串类型的数字，因而不能直接进行几何运算
2. 遍历顺序可能不是实际的内部顺序
3. for...in 会遍历数组所有的可枚举属性，包括原型

## 2、for...of

**for...of 只能遍历数组，取到的是 value**

## 3、总结

**for...in 遍历对象或返回的是 key**

**for...of 遍历对象会报错，遍历数组返回的是 value**

```
let a = {"one":1,"two":2}
let b = [3,4]

for(let i in a){
	console.log(i)  =>  one  two
}
for(let i of a){
	console.log(i)  =>  Uncaught TypeError: a is not iterable
}

for(let i in b){
	console.log(i)  =>  0  1
}
for(let i of b){
	console.log(i)  =>  3  4
}


```
