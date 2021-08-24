---
title: ES6：let、const、var
date: 2019-10-14 18:08:43
tags: ES
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、var

`var`用来声明变量

- 存在变量提升;
- 可以重复声明
- 使用`var`声明的变量会被提升到作用域顶部

<!--more-->

```
//变量提升:变量还未声明但能使用
console.log(a)   =>  undefined
var a = 1;
```

## 二、let

`let`是 ES6 中提出的用于声明变量

- 不存在变量提升，也就是说被`let` 声明的变量不会提升到作用域顶部，如果还未声明便使用会报错（**Uncaught ReferenceError**）

  **let 到底存在变量提升吗？**

  - var 声明的创建、初始化和赋值过程

    ```
    function fn() {
      var x = 1;
      var y = 2;
    }
    fn();
    ```

    执行 fn 过程：

    1. 进入 fn，为 fn 创建一个环境；
    2. 找到 fn 中所有用 var 声明的变量，在这个环境中创建这些变量（x 和 y）；
    3. 将这些变量初始化为 undefined；
    4. 开始执行代码
    5. 将 x 赋值为 1，将 y 赋值为 2。

    **var 声明在代码执行前就会创建变量，并将其初始化为 undefined。**

  - function 声明的创建 初始化和赋值过程

    ```
    fn2();
    function fn2() {
      consle.log(2)
    }
    ```

    JS 引擎执行过程：

    1. 找到所有用 function 声明，在环境中创建这些变量；
    2. 将这些变量初始化并赋值；
    3. 开始执行 fn2()。

    **function 声明会在代码执行之前就创建、初始化并赋值。**

  - let 声明的创建、初始化和赋值过程

    ```
    {
      let x = 1;
      x = 2;
    }
    ```

    {}里面的执行过程：

    1. 找到所有用 let 声明的变量，在环境中创建这些变量；
    2. 开始执行代码（注意：现在还没有初始化）；
    3. 执行 x=1，将 x 初始化为 1（这并不是一次赋值，如果代码是 let x，就将 x 初始化为 undefined）;
    4. 执行 x = 2，对 x 进行赋值。

  **所以综上，**

  **1. let 的创建过程被提升了，但是初始化没有提升。**

  **2. var 的创建和初始化都被提升了。**

  **3. function 的创建、初始化和赋值都被提升了。**

  ![](https://pic1.zhimg.com/80/v2-9c8c4a0a3ce5402b1a74f488d79c74d0_hd.jpg)

- 暂时性死区

- 块级作用域

  ```
  var li = document.querySelectorAll('li');
  // 代码段1
  for(var i = 0; i < li.length; i++) {
    li[i].onClick=function() {
      console.log(i)
    }
  }

  //代码段2
  for(let i = 0; i < li.length; i++) {
    li[i].onClick=function() {
      console.log(i)
    }
  }
  ```

  **为什么代码段 1 会打印出 5 个 5，而代码段 2 会打印出 0、1、2、3、4？**

  猜测：

  1. for(let i = 0; i < li.length; i++)这句话的圆括号之间，有一个隐藏的作用域

  2. for(let i = 0; i < li.length; i++) {循环体}在每次执行循环体之前，JS 引擎会把 i 在循环体的上下文中重新声明及初始化一次

  3. 近似把代码 2 理解为

     ```
     for(let i = 0; i < li.length; i++) {
       let i = 隐藏作用域中的i
       li[i].onClick=function() {
         console.log(i)
       }
     }
     ```

* 不可重复声明

## 三、const

`const` 是 ES6 提出的用于声明变量

- 声明必须赋值，一旦声明便不可更改
- 其他和`let` 一致

## 四、块级作用域

### 为什么需要块级作用域

- 内层变量可能覆盖外层变量
- 用来计数的循环变量泄露为全局变量

[我用了两个月的时间才理解 let](https://zhuanlan.zhihu.com/p/28140450)
