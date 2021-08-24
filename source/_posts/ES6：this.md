---
title: ES6：this
date: 2019-10-15 15:20:21
tags: ES
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、this 的指向问题

this 代表函数（方法）执行的上下文环境

- this 指向的一定是对象
- this 指向谁不取决于 this 写在哪儿，取决于 this 在哪儿被调用
- 严格模式中：禁止 this 指向全局对象

![](https://user-gold-cdn.xitu.io/2018/11/15/16717eaf3383aae8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

<!--more-->

## 二、箭头函数和普通函数的区别

**箭头函数**

```
let fun1 = ()=>{
  console.log('111')
}
```

**普通函数**

```
function fun2(){
  console.log('222')
}
```

### 1、箭头函数没有原型属性（prototype），所以箭头函数本身没有 this

```
let a = ()=> {};
console.log(a.prototypt); // undefined
```

### 2、箭头函数不绑定 this，会捕获其所在的上下文的 this 值，作为自己的 this 值

### 3、箭头函数不绑定 arguments，取而代之用 rest 剩余参数...解决

```
let B = (b)=>{
  console.log(arguments);
}
B(2,92,32,32);  =>  Uncaught ReferenceError: arguments is not defined

let C = (...c) => {
  console.log(c);
}
C(3,82,32,11323);  =>  [3, 82, 32, 11323]
```

如果箭头函数的 this 指向全局对象，使用`arguments` 会报错；

如果箭头函数的 this 指向一个普通函数，`arguments` 会继承这个普通函数。

### 4、箭头函数通过`call()`或`apply()` 方法调用一个函数时，只传入了一个参数，对`this` 没有影响，不会修改箭头函数的 this 指向

要想修改箭头函数的 this 指向，只需要修改它外层的普通函数 this 指向。

### 5、箭头函数是匿名函数，不能作为构造函数，不能使用 new

```
let Fun1 = ()=>{
  console.log('111')
}
let fc = new Fun1();  =>  Uncaught TypeError: Fun1 is not a constructor
```

### 6、箭头函数不能当做 Generator，不能使用 yield 关键字

## 三、new 的过程

```
var a = new myFunction("Li", "Cherry");

new myFunction{
  var obj = {};
  obj.__proto__ = myFunction.prototype;
  var result = myFunction.call(obj, "Li", "Cherry");
  return typeof result === 'obj' ? result : obj;
}
```

1. 创建一个空对象 obj；
2. 将新创建的空对象的隐式原型（proto）指向其构造函数的显式原型（prototype）；
3. 改变 this 的指向；
4. 如果无返回值或者返回一个非对象值，则将 obj 返回作为新对象；如果返回值是一个新对象的话那么直接返回该对象。

[箭头函数参考文献](https://juejin.im/post/5c76972af265da2dc4538b64)

[new 的过程参考文献](https://juejin.im/post/59bfe84351882531b730bac2)
