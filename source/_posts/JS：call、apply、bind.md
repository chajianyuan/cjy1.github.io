---
title: JS：call、apply、bind
date: 2019-10-15 16:11:25
tags: javascript
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、call

改变函数的 this 指向，`call()` 第一个参数为 this 要指定的对象，后面可以**接收多个参数列表 **，会**立即调用** 。

**注：** 如果第一个参数为空|null|undefined，则 this 指向 window。

<!--more-->

#### 手撕 call

```
Function.prototype.call = functionl(context){
  if(typeof this != 'function'){
    throw new TypeError('Error');
  }
  context = context || window;
  context.fn = this;
  const args = [...arguments].slice(1);
  const result = context.fn(...args);
  delete context.fn;
  return result;
}
```

**解析**

1. context 为可选参数，如果不传的话默认上下文为 window；
2. 给 context 创建一个 fn 属性，并将值设置为需要调用的函数（因为 call 可以传入多个参数作为调用函数的参数，所以需要将参数剥离出来）；
3. 调用函数并将对象上的函数删除

## 二、apply

和 call 一样，唯一的区别就是调用参数的形式不同，apply 传入的是数组。

#### 手撕 apply

```
Function.prototype.apply = functionl(context){
  if(typeof this != 'function'){
    throw new TypeError('Error')
  }
  context = context || window
  context.fn = this
  let result;
  //处理参数和call有区别
  if(arguments[1]){
    result = context.fn(...arguments[1])
  } else {
    result = context.fn()
  }
  delete context.fn
  return result
}
```

## 三、bind

bind 也是为了改变函数体内部 this 的指向，返回一个函数，稍后调用。

#### 手撕 bind

```
Function.prototype.bind = function(context){
  if(typeof this !== 'function'){
    throw new TypeError('Error')
  }
  const _this = this
  const args = [...arguments].slice(1)
  //返回一个函数
  return function F(){
    //因为返回了一个函数，我们可以new F()，所以需要判断
    if(this instanceof F){
      return new _this(...args,...arguments)
    }
    return _this.apply(context,args.concat(...arguments))
  }
}
```

## 四、区别

### 1、call、apply、bind 的区别

- call 和 apply 改变了函数的 this 指向后便立即执行；
- bind 则是返回改变了上下文之后的一个函数，便于稍后调用。

### 2、call、apply 的区别

call 和 apply 的第一个参数都是 this 要指向的对象，它们两个不同的地方在于第二个参数之后的参数。

- call 从第二个参数开始以参数列表的形式展现；

```
fn.call(obj, arg1, arg2, arg3...);
```

- apply 将除第一个以外的所有参数都放在一个数组中作为第二个参数。

```
fn.apply(obj, [arg1, arg2, arg3...]);
```
