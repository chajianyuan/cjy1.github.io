---
title: 总结：vue
date: 2019-10-24 10:52:09
tags: 总结
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、Vue 生命周期

[参见总结：vue：生命周期](https://chajianyuan.github.io/2019/10/19/vue%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F/)

<!--more-->

## 二、Vue 双向数据绑定原理

[参见总结：vue：双向绑定](https://chajianyuan.github.io/2019/10/19/vue%E5%8F%8C%E5%90%91%E7%BB%91%E5%AE%9A/)

## 三、v-show 和 v-if 的区别

**v-if** 是**真正**的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；也是**惰性的**：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

**v-show** 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 “display” 属性进行切换。

所以，v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。

## 四、MVVM

[掘金：看完这篇关于 MVVM 的文章，面试通过率提升了 80%](https://juejin.im/post/5af8eb55f265da0b814ba766)

## 五、虚拟 DOM

[掘金：揭秘 Vue 中的 Virtual Dom](https://juejin.im/post/5d12c931f265da1bb2773fcc)

## 六、key

![](https://user-gold-cdn.xitu.io/2019/10/31/16e1f60b7d343768?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
![](https://user-gold-cdn.xitu.io/2019/10/31/16e1f6105886daf5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
key 的作用就是在更新组件时判断两个节点是否相同。相同就复用，不相同就删除旧的创建新的。

- key 会用在虚拟 DOM 算法（diff 算法）中，用来辨别新旧节点；
- 不带 key 的时候会最大限度减少元素的变动，尽可能用相同的元素（就地复用）；
- 带 key 的时候，会基于相同的 key 来进行排列（相同的复用）；
- 带 key 还能触发过渡效果，以及触发组件的生命周期。

## 七、nextTick

[掘金：简单理解 Vue 中的 nextTick](https://juejin.im/post/5a6fdb846fb9a01cc0268618)

## 八、template 编译

详情步骤：首先，通过 compile 编译器把 template 编译成 AST 语法树（abstractsyntaxtree 即源代码的抽象语法结构的树状表现形式），compile 是 createCompiler 的返回值，createCompiler 是用以创建编译器的。另外 compile 还负责合并 option。

然后，AST 会经过 generate（将 AST 语法树转化成 renderfuntion 字符串的过程）得到 render 函数，render 的返回值是 VNode，VNode 是 Vue 的虚拟 DOM 节点，里面有（标签名、子节点、文本等等）

## 九、组件间通讯

[掘金：Vue 组件间通信六种方式（完整版）](https://juejin.im/post/5cde0b43f265da03867e78d3)

## 十、父子组件生命周期

### 1、加载渲染过程

```
父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted
```

### 2、子组件更新过程

```
父beforeUpdate->子beforeUpdate->子updated->父updated
```

### 3、父组件更新过程

```
父beforeUpdate->父updated
```

### 4、销毁过程

```
父beforeDestroy->子beforeDestroy->子destroyed->父destroyed
```

## 十一、keep-alive

如果想把切换出去的组件保留在内存中，并保留它的状态或避免重新渲染。为此可以添加一个 keep-alive 指令

`<component:is='curremtView' keep-alive></component>`

## 十二、Vuex

[掘金：从头开始学习 Vuex](https://juejin.im/post/5bbe15dcf265da0a867c57bd)

vuex 是一个状态管理容器(你也可以理解为类似于全局变量),数据的流向是是单向数据流

| vuex      | vue                 |
| --------- | ------------------- |
| state     | data                |
| getters   | computed            |
| mutations | methods（同步操作） |
| actions   | methods（异步操作   |

## 十三、vue版本之间的区别
[参见总结：vue：vue版本之间的区别]()