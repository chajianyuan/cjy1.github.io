---
title: react：setState
date: 2021-03-28 18:35:14
tags: react
category: 技术
---

<img src="https://github.com/chajianyuan/picture/blob/master/1671616928038_.pic.jpg?raw=true" width="600px" />
<img src="https://github.com/chajianyuan/picture/blob/master/1671616928038_.pic.jpg?raw=true" width="600px" />

<!--more-->

### 一、setState的执行过程

![](https://user-gold-cdn.xitu.io/2019/2/23/169197bbdc7ae14e?imageView2/0)

:information_desk_person: 简单描述：

1. 将`setState`传入`partialState`参数存储在当前组件实例的state暂存队列中；
2. 判断当前React是否处于批量更新状态，如果是，将当前组件加入待更新的组件队列中；
3. 如果未处于批量更新状态，将批量更新状态标识设置为`true`，用事务再次调用上一步方法，保证当前组件加入了待更新组件队列中；
4. 调用事务的`waper`方法，遍历待更新组件队列依次执行更新；
5. 执行生命周期`componentWillReceiveProps`；
6. 将组件的state暂存队列中的`state`进行合并，获得最终要更新的state对象，并将队列置为空；
7. 执行生命周期`componentShouldUpdate`，更具返回值判断是否要继续更新；
8. 执行生命周期`componentWillUpdate`；
9. 执行真正的更新`render`；
10. 执行生命周期`componentDidUpdate`。

[:dizzy: setState源码地址](https://github.com/facebook/react/blob/main/packages/react/src/ReactBaseClasses.js#L57)


### 二、:question: setState是同步还是异步，setState内部又是如何实现的呢？

#### 1. 假设我们有如下五种`setState`使用场景

初始化
```
constructor() {
  super();
  this.state = {
    count: 0
  };
}
```

##### （1）合成事件

```
handleClick = () => {
  this.setState({count: this.state.count + 1});
  console.log('合成事件 -> count', this.state.count);
}
```

setState的执行过程



##### （1）`setState`只传一个参数，且参数类型为对象

```
componentDidMount() {
  this.setState({count: this.state.count + 1});
  console.log('outside -> count', this.state.count); // outside -> count 0
}
```
此时，我们拿到的`count`并不是更新之后的，所以这种方式的setState是**异步**的

##### （2）`setState`只传一个参数，且参数类型为函数

```
componentDidMount() {
  this.setState(prevState => {
    console.log('prevState -> count', prevState.count); // prevState -> count 0
    return {
      count: prevState.count + 1
    }
  });
}
```
此时，`prevState`拿到的是上一次更新之后的state, 所以这种方式的setState是**异步**的

##### （3）`setState`传两个参数，第一个是对象，第二个是函数

```
this.setState({
  count: this.state.count + 1
}, () => {
  console.log('setState -> count', this.state.count); // setState -> count 1
});
```
此时拿到的`count`是更新之后的值，所以这种方式的setState获取到的值是**同步**的

##### （4）使用setTimout

```
setTimeout(() => {
  this.setState({count: this.state.count + 1});
  console.log('setTimeout -> count', this.state.count); // setTimeout -> count 1
}, 0);
```
此时拿到的`count`是更新之后的值，所以这种方式的setState获取到的值是**同步**的

##### （5）使用自定义dom事件

```
const element = document.querySelector('.test');
element.addEventListener('click', e => {
  this.setState({count: this.state.count + 1});
  console.log('event -> count', this.state.count); // event -> count 1
});
```
此时拿到的`count`是更新之后的值，所以这种方式的setState获取到的值是**同步**的

#### 2. :punch: 总结

**setState可能是同步，也可能是异步**

* setTimeout、自定义dom事件是同步更新的
* 钩子函数、合成事件中是异步更新的

<!-- legacy模式命中batchedUpdates时异步
legacy模式未命中batchedUpdates时同步
ConCurrent模式都是异步的 -->

### 三、:question: setState为什么是异步的

我们先介绍一个概念：批处理（batchedUpdates），批处理就是当同时多次调用setState时，只有一次生效

Dan的解释是👇

#### 1. 不能保证内部的一致性

现在的React提供的对象（state、props、refs）在内部是一致的，所以即使state是同步更新，props也不是同步更新的（只有在渲染父组件的时候，props才会更新）。

#### 2. 影响性能

如果state是同步更新的话，那么每一次state更新完，都要重新渲染页面，会造成很大的性能问题

### 四、:question: setstate是如何实现异步更新的

#### 1. 合成事件中的setState

```
qq
```

### 五、例子

接下来我们来验证一下我们的学习成果，下面代码执行后的打印结果依次是什么呢？

```
componentDidMount() {
  this.setState({count: this.state.count + 1});
  console.log('outside1 -> count', this.state.count);

  this.setState({count: this.state.count + 1});
  console.log('outside2 -> count', this.state.count);

  this.setState(prevState => {
    console.log('prevState -> count', prevState.count)
    return {
      count: prevState.count + 1
    }
  });

  this.setState({
    count: this.state.count + 1
  }, () => {
    console.log('setState -> count', this.state.count)
  });

  setTimeout(() => {
    this.setState({count: this.state.count + 1});
    console.log('setTimeout -> count', this.state.count);
  }, 0);

  const element = document.querySelector('.test');
  element.addEventListener('mouseover', e => {
    this.setState({count: this.state.count + 1});
    console.log('自定义dom -> count', this.state.count);
  });
}

handleClick = () => {
  this.setState({count: this.state.count + 1});
  console.log('合成事件 -> count', this.state.count);
}
```

答案在这儿

```
outside1 -> count   0
outside2 -> count   0
prevState -> count  1
setState -> count   1
setTimeout -> count 2
自定义dom -> count   3
合成事件 -> count    3
```

> 自定义dom事件比合成事件先执行

### 参考文献
[:bulb: 【React深入】setState的执行机制](https://juejin.cn/post/6844903781813993486)
[:bulb: 听Dan说：setState() 为什么是异步的](https://github.com/facebook/react/issues/11527)
[:bulb: 你真的理解setState吗？](https://juejin.cn/post/6844903636749778958#heading-7)