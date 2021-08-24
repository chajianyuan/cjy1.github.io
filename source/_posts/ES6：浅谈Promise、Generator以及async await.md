---
title: ES6：浅谈Promise、Generator以及async await
date: 2019-10-12 19:23:00
tags: ES
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、Generator

### 1、基本概念

Generator 函数是 ES6 提供的一种异步编程解决方案，执行 Generator 函数会返回一个**遍历器对象**。形式上，Generator 函数是一个普通函数，但是有两个特征：

​ （1）function 关键字和函数名之间有一个星号（\*）；

​ （2）函数体内部使用 yield 表达式。

### 2、实现

```
function* hello(x){
  let y = 2 * (yield(x+1));
  let z = yield(y / 3);
  return (x+y+z);
}
let fun = hello(5);
cosnole.log(fun.next())     //=>{value:6, done:false}
cosnole.log(fun.next(12))   //=>{value:8, done:false}
cosnole.log(fun.next(13))   //=>{value:42, done:false}
```

（1）执行第一个 next 时，**x=5**，函数执行到 yield(x+1)，所以返回 5+1=6；

（2）执行第二个 next 时，**x = 5**，传入的参数会代替 yield(x+1)的位置，即 yield(x+1) = 12，所以**y = 2 \* 12 = 24**，函数执行到 yield(y / 3)，所以返回 y / 3 = (2 \* 12) / 3 = 8;

（3）执行第三个 next 时，**x = 5**，**y = 2 \* 12 = 24**，传入的参数会代替 yield(y / 3)的位置，即**z = 13**，所以最终返回 x + y + z = 5 + 24 + 13 = 42。

[从 for of 聊到 Generator](https://juejin.im/post/5c40484bf265da61171cfb4d)

## 二、Promise

### 1、基本概念

Promise 是异步编程的一种解决方案，简单来说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。

### 2、特点

（1）**对象的状态不会受外界的影响**。Promise 对象代表一个异步操作，有三种状态：pending（进行中）、fufilled（已成功）、rejected（已失败），只有异步操作的结果才能决定最后的状态。

（2）**一旦该状态改变，就不会再变，任何时候都可以得到这个结果**。状态的改变只能由 pending->fulfilled（resolved）和 pending->rejected.

### 3、优缺点

**优点**：

​ （1）可以将异步操作的流程表达出来，避免了层层嵌套的回调函数；

​ （2）Promise 对象提供统一的接口，使得异步操作更加容易。

**缺点**：

​ （1）无法取消 Promise，一旦新建他就会立即执行，无法中途取消 ；

​ （2）如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部；

​ （3）当处于 pending 状态时，不知道目前进行到了哪个阶段（是刚刚开始还是即将结束）。

### 4、原理

Promise 对象是一个构造函数，用来生成 Promise 实例，这个实例一旦创建就会立即执行，实例中接收一个执行函数作为参数，这个执行函数有两个函数类型形参（resolve 和 reject），resolved 函数的作用是将 Promie 对象的状态从“未完成”到“成功”，在异步函数成功时调用，并将异步操作的结果作为参数传递出去；rejected 函数的作用是将 Promise 对象的状态从“未完成”到“失败”，在异步函数失败时调用，并将异步操作报出的错误作为参数传递出去。

Promise 实例生成后，可以用 then 方法分别指定 resolved 状态和 rejected 状态的回调函数。

**真正的链式 Promise 是指在当前 promise 达到 fulfilled 状态后，即开始进行下一个 Promise。**

```
new Promise((resolve,reject)=>{
  resolve(1)
}).then(value=>{
  console.log(value)
})
```

### 5、手撕 Promise

```
const PENDING = 'pending';     // 首先创建三个常量来表示状态，
const RESOLVED = 'resolved';
const REJECTED = 'rejected';

function MyPromise(fn){
  const that = this;   // 在函数体内部创建常量that，因为代码可能会异步执行，用于获取正确的this对象；
  this.state = PENDING;    // 一开始Promise状态应该是pending；
  that.value = null;    // value变量用于保存resolve或者reject中传入的值
  that.resolvedCallbacks = [];    // 用于保存then中的回调函数，因为当执行完Promise时状态可能还是等待
  that.rejectedCallbacks = [];    // 中，这时候应该把then中的回调保存起来用于状态改变时用

  /**
  首先两个函数都得判断当前状态是否为等待状态，只有等待状态才可以改变状态；
  将当前状态改变为对应状态，并且将传入的值赋给value；
  遍历回调数组并执行
  */
  function resolve(value){
    if(that.state == PENDING){
      that.state = RESOLVED;
      that.value = value;
      that.resolvedCallbacks.map(item=>item(that.value));
    }
  }
  function reject(value){
    if(that.state == PENDING){
      that.state = REJECTED;
      that.value = value;
      that.rejectedCallbacks.map(item=>item(that.value));
    }
  }

  /**
  执行传入的参数并且将之前两个函数当做函数传进去；
  可能执行函数过程中会遇到错误，需要捕获错误并执行到reject函数
  */
  try{
    fn(resolve, reject)
  } catch(e){
    reject(e)
  }
}

/**
首先判断两个参数是否为函数类型，因为这两个参数是可选参数；
当参数不是函数类型的时候，需要创建一个函数赋值给对应的参数，同时也实现了透传
*/
MyPromise.prototype.then = function(onFulfilled,onRejected){
  const that = this;
  onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : v=> v;
  onRejected = typeof onRejected === 'function' ? onRejected : r=> {throw r};
  if(that.state === PENDING){
    that.resolvedCallbacks.push(onFulfilled);
    that.rejectedCallbacks.push(onRejected)
  }
  if(that.state === RESOLVED){
    onFulfilled(that.value);
  }
  if(that.state === REJECTED){
    onRejected(that.value);
  }
}
```

[面试精选之 Promise](https://juejin.im/post/5b31a4b7f265da595725f322)

## 三、async、await

### 1、基本概念

async 其实就是 Generator 函数的语法糖。async 就是将函数返回值使用 Promise.resolve()包裹一下，和 then 中处理返回值一样，并且 await 只能配套 async 使用。

**特点 **

​ （1）内置执行函数

​ asyns 函数的执行和普通函数的一样`asyncFun()`

​ （2）更好的语义

​ async 表示函数里有异步操作，await 表示紧跟在后面的表达式需要等待结果。

​ （3）更广泛的运用性

​ async 函数的 await 命令后面，可以是 Promise 对象和原始类型的值（数值、字符串、布尔值，但这时等同于同步操作）

​ （4）返回值是 Promise

​ 可以使用 then 指定下一步的操作。

### 2、用法

async 函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当函数执行的时候，一旦遇到`await` 就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

```
function timeout(ms){
  return new Promise((resolve)=>{
    setTimeout(resolve,ms)
  })
}
async function asyncPrint(value, ms){
  await timeout(ms);
  console.log(value);
}
asyncPrint('hello world', 50)
```

等同于

```
async function timeout(ms){
  await new Promise((resolve)=>{
    setTimeout(resolve,ms)
  })
}
async function asyncPrint(value, ms){
  await timeout(ms);
  console.log(value);
}
asyncPrint('hello world', 50)
```

[理解 async/await](https://juejin.im/post/596e142d5188254b532ce2da)
