---
title: JS：闭包
date: 2021-03-24 09:13:39
tags:
---

<img src="https://github.com/chajianyuan/picture/blob/master/1641616548534_.pic.jpg?raw=true" width="600px" />

<!--more-->

#### MDN对闭包的定义

> 闭包是指那些能够访问自由变量的函数。

❓**自由变量是什么？**

> 自由变量是指能够在函数中使用的，但既不是函数参数也不是函数的局部变量的变量。

对于闭包，我的理解就是当某个函数 A 被调用时，这个函数 A 可以访问它定义时的作用域中的变量。

使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染；缺点是闭包会常驻内存，增加内存使用量，使用不当很容易造成内存泄漏。在 JavaScript 中，函数即闭包，只有函数才会产生作用域。

闭包有 3 个特性：

1. 函数嵌套函数；
2. 在函数内部可以引用外部的参数和变量；
3. 参数和变量不会以垃圾回收机制回收。

```
function a(){
  let name = 'zhangsan';

  function b(){
    console.log(name);
  }

  return b;
}
```

[JavaScript 闭包](https://segmentfault.com/a/1190000006875662)