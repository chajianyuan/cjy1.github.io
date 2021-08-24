---
title: 总结：javascript
date: 2019-10-24 21:23:10
tags: 总结
categories: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、数据类型及检测

[参见总结：JS：typeof、instanceof 以及 Object.prototyte.toString.call()](https://chajianyuan.github.io/2019/10/13/JS%EF%BC%9Atypeof%E3%80%81instanceof%E4%BB%A5%E5%8F%8Aobject-prototyte-tostring-call/)

<!--more-->

## 二、原型与原型链、继承

[参见总结：JS：原型、原型链继承](https://chajianyuan.github.io/2019/10/15/JS%EF%BC%9A%E5%8E%9F%E5%9E%8B%E3%80%81%E5%8E%9F%E5%9E%8B%E9%93%BE%E7%BB%A7%E6%89%BF/)

## 三、闭包

## 四、浅拷贝和深拷贝

[参见总结：JS：赋值、深拷贝和浅拷贝](https://chajianyuan.github.io/2020/02/24/JS%EF%BC%9A%E8%B5%8B%E5%80%BC%E3%80%81%E6%B7%B1%E6%8B%B7%E8%B4%9D%E5%92%8C%E6%B5%85%E6%8B%B7%E8%B4%9D/)

## 五、防抖和节流

防抖：事件被触发 n 秒之后再执行回调，如果在这段时间之内又被触发，则重新计时。

节流：规定在单位时间之内只能触发一次，如果触发了多次只有一次生效。

[7 分钟理解 JS 的节流、防抖及使用场景](https://juejin.im/post/5b8de829f265da43623c4261)

[2019 面试准备 - JS 防抖与节流](https://juejin.im/post/5c87b54ce51d455f7943dddb#chapter-three-one)

## 六、数组方法、数组去重

[参见总结：JS：数组方法](https://chajianyuan.github.io/2019/10/14/JS%EF%BC%9A%E6%95%B0%E7%BB%84%E6%96%B9%E6%B3%95/)

[参见总结：JS：数组去重](https://chajianyuan.github.io/2019/10/16/JS%EF%BC%9A%E6%95%B0%E7%BB%84%E5%8E%BB%E9%87%8D/)

## 七、作用域和作用域链

## 八、this 的指向和 new 的过程

[参见总结：ES6：this](https://chajianyuan.github.io/2019/10/15/ES6%EF%BC%9Athis/)

## 九、JavaScript 有哪些垃圾回收机制？

1. 标记清除（mark and sweep）

   这是 JavaScript 最常见的垃圾回收方式。当变量进入执行环境的时候,比如在函数中声明一个变量，垃圾回收器将其标记为"进入环境"。当变量离开环境的时候（函数执行结束），将其标记为“离开环境”。

   垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量，以及被环境中变量所引用的变量（闭包）的标记。在完成这些之后仍然存在的标记就是要删除的变量。

2. 引用计数

   在低版本的 IE 中经常发生内存泄漏，很多时候就是因为它采用引用计数的方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数。当声明了一个变量并将一个引用类型赋值给该变量的时候，这个值的引用次数就加 1,。如果该变量的值变成另外一个，则这个值得引用次数减 1，当这个值得引用次数变为 0 的时候，说明没有变量在使用，这个值没法被访问.因此，可以将它占用的空间回收，这样垃圾回收器会在运行的时候清理引用次数为 0 的值占用的空间。

   在 IE 中虽然 JavaScript 对象通过标记清除方式进行垃圾回收，但是 BOM 与 DOM 对象是引用计数的方式回收垃圾的。也就是说，只要涉及 BOM 和 DOM，就会出现循环引用问题。

## 十、列举几种类型的 DOM 节点

- 整个文档是一个文档（Document）节点
- 每个 HTML 标签是一个元素（Element）节点
- 每一个 HTML 属性是一个属性（Attribute）节点
- 包含在 HTML 元素中的文本是文本（Text）节点

## 十一、谈谈 script 标签中 defer 和 async 属性的区别

1. defer 属性规定是否延迟执行脚本，直到页面加载为止。async 属性规定脚本一旦可用，就异步执行；
2. defer 并行加载 JavaScript 文件，会按照页面上 script 标签的顺序执行。async 并行加载 JavaScript 文件，下载完成立即执行，不会按照页面上 script 标签的顺序执行。

## 十二、encodeURI()和 decodeURI()的作用是什么？

encodeURI()用于将 URL 转换为十六进制编码，而 decodeURI()用于将编码的 URL 转换成正常的 URL。

## 十三、为什么不建议在 JavaScript 中使用 innerHTML？

通过 innerHTML 修改内容，每次都会刷新，因此很慢。在 innerHTML 中没有验证的机会，因此更容易在文档中插入错误代码，使网页不稳定。

## 十四、在 DOM 操作中怎样创建、添加、移除、替换、插入和查找节点？

1. 创建节点

```
createDocumentFragment() // 创建一个DOM片段
createElement()  //创建一个具体的元素
createTextNode()  //创建一个文本节点
```

2.添加、移除、替换、插入节点

```
appendChild()
removeChild()
replaceChild()
insertBefore()
```

3. 查找节点

```
getElementByTagName()  //通过标签名称查找节点
getElementByName()  //通过元素的name属性查找节点（IE容错能力较强，会得到一个数组，其中包括id等于name值得节点）
getElementById()  //通过元素Id查找节点，具有唯一值
```

## 十五、null 和 undefined 的区别是什么？

null 是一个表示“无”的对象，转为数值时为 0；undefined 是一个表示“无”的原始值，转为数值时为 NaN。

当声明的变量还未初始化时，变量的默认值为 undefined。

null 用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。

undefined 表示“缺少值"，即此处应该有一个值，但是还没有定义，典型用法是：

1. 如果变量声明了，但是没有赋值，它就等于 undefined；
2. 当调用函数时，如果没有提供应该提供的参数，该参数就等于 undefined；
3. 如果对象没有赋值，该属性的值为 undefined；
4. 当函数没有返回值时，默认返回 undefined。

null 表示“没有对象”，即此处不应该有值，典型用法是：

1. 作为函数的参数，表示该函数的参数不是对象；
2. 作为对象原型链的终点。

## 十六、JavaScript 延迟加载的方式有哪些？

包括 defer 和 async，动态创建 DOM（创建 script，插入 DOM 中，加载完毕后回调，按需异步载入 JavaScript）。

## 十七、call、apply、bind

[参见总结：JS：call、apply、bind](https://chajianyuan.github.io/2019/10/15/JS%EF%BC%9Acall%E3%80%81apply%E3%80%81bind/)

## 十八、哪些操作会造成内存泄漏？

内存泄漏指不再拥有或需要任何对象（数据）之后，它们仍然存在于内存中。

**提示：** 垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的唯一引用是循环的，那么该对象占用的内存立即被回收。

如果 settimeout 的第一个参数使用字符串而非函数，会引发内存泄漏。

闭包、控制台日志，循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）等会造成内存泄漏。

## 十九、列举 IE 与 Firefox 的不同之处。

不同之处如下。

1. IE 支持 currentStyle，Firefox 使用 getComputStyle；
2. IE 使用 innerText，Firefox 使用 textContent;
3. 在透明度过滤镜方面，IE 使用 filter:alpha(opacity = num); Firefox 使用-moz-opacity:num；
4. 在事件方面，IE 使用 attachEvent；Firefox 使用 addEventListener；
5. 对于鼠标位置：IE 使用 event.clientX；Firefox 使用 event.pageX；
6. IE 使用 event.srcElement；Firefox 使用 event.target。
7. 要消除 list 圆点，IE 中仅需使 margin：0 即可达到最终效果，Firefox 中需要设置 margin：0，padding：0，list-style：none；
8. css 圆角：IE7 以下不支持圆角。

## 二十、如何实现异步编程？

1. 通过回调函数，优点是简单、容易理解和部署；缺点是不利于代码的阅读和维护，各个部分之间高度耦合（Coupling），流程混乱，而且每个任务只能指定一个回调函数。
2. 通过事件监听，可以绑定多个事件，每个事件可以指定多个回调函数，而且可以“去耦合”（Decoupling），有利于实现模块化；缺点是整个程序都要变成事件驱动型，运行流程会变得恨不清晰。
3. 采用发布/订阅方式，性质与“事件监听”类似，但是明显优于后者；
4. 通过 Promise 对象实现，Promise 对象是 CommonJS 工作组提出的一种规范，旨在为异步编程提供统一接口。它的思想是，每一个异步任务返回一个 Promise 对象，该对象有一个 then 方法，允许指定回调函数。

## 二十一、请解释一下 JavaScript 的同源策略。

同源策略是客户端脚本（尤其是 JavaScript）的重要安全度量标准。它最早出自 Netscape Navigator 2.0，目的是防止某个文档或脚本从多个不同源装载。

这里的同源策略指的是协议、域名、端口相同。同源策略是一种安全协议。指一段脚本只能读取来自同一来源的窗口和文档的属性。

## 二十二、为什么要有同源限制？

我们举例说明，比如一个黑客，他利用 Iframe 把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名、密码登录时，他的页面就可以通过 JavaScript 读取到你表单上 input 的内容，这样黑客就会轻松得到你的用户名和密码。

## 二十三、map,filter 和 reduce

[参见总结：JS：map、filter、reduce]()

## 二十四、前端模块化

[参见总结：JS：前端模块化](https://chajianyuan.github.io/2019/10/20/JS%EF%BC%9A%E5%89%8D%E7%AB%AF%E6%A8%A1%E5%9D%97%E5%8C%96/)

## 二十五、数组方法

[参见总结：JS：数组方法]()
