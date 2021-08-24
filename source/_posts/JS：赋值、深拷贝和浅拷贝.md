---
title: JS：赋值、深拷贝和浅拷贝
date: 2020-02-24 08:46:35
tags: javascript
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、浅拷贝和深拷贝

浅拷贝和深拷贝只针对 object 和 array 这种引用数据类型。

<!--more-->

**浅拷贝：** 只复制某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存。

**深拷贝：** 会创造一个一模一样的新对象，新对象和原对象不共享内存，修改新对象不会改到原对象。

## 二、赋值和浅拷贝

**赋值：** 当把某个对象赋值给一个新的变量时，赋的是该对象在栈中的地址，而不是堆中的数据。

```
var a ={
  name: "zhangsan",
  scores: [100, 99]
}
var b = a;
```

其实是将对象 a 在栈中的指针 a 赋值给了对象 b,指针 a 和指针 b 指向的是同一个堆中的数据，那么其中一个数据改变时，另外一个也会改变。

**浅拷贝：** 浅拷贝会创建一个新的对象，但它是按位拷贝对象，即如果原对象的属性是基本类型，则拷贝的是基本数据类型的值；如果原对象的属性是引用数据类型，则拷贝的是引用类型的指针。

![](https://user-gold-cdn.xitu.io/2018/12/23/167da74d45d3103b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## 三、浅拷贝的实现方式

### 1、Object.assign()

```
var obj = {
  a: {
    a: 'zhangsan',
    b: 'lisi'
  }
}
var copyObj = Object.assign({}, obj)
```

### 2、Array.prototype.concat()

```
var obj = {
  a: {
    a: 'zhangsan',
    b: 'lisi'
  }
}
var copyObj = obj.concat();
```

### 3、Array.prototype.slice()

```
var obj = {
  a: {
    a: 'zhangsan',
    b: 'lisi'
  }
}
var copyObj = obj.slice();
```

## 四、深拷贝的实现方式

### 1、JSON.parse(JSON.stringify())

```
var obj = {
  a: {
    a: 'zhangsan',
    b: 'lisi'
  }
};

var copyObj = JSON.parse(JSON.stringify(obj));
```

### 2、手写递归方法

遍历对象、数组直到里面都是基本数据类型，然后再去复制。

### 3、函数库 lodash

```
var _ = require('lodash');
var obj = {
  a: {
    a: 'zhangsan',
    b: 'lisi'
  }
};
var copyObj = _.cloneDeep(obj);
```

[浅拷贝与深拷贝](https://juejin.im/post/5b5dcf8351882519790c9a2e)
