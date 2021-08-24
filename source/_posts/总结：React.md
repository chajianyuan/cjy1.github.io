---
title: 总结：React
date: 2020-03-09 10:52:51
category: 技术
tags: 总结
---

<meta name="referrer" content="no-referrer"/>

## 一、当调用 setState 的时候,发生了什么？

当调用 setState 时，React 做的第一件事就是将传递给 setState 的对象合并到组件的当前状态，这将启动一个称为和解的过程，和解的最终目标是，根据这个新的状态以最有效的方式更新 DOM。为此，React 将构建一个新的 React 虚拟 DOM 树（可以将其视为页面 DOM 元素的对象表示方式）。

<!--more-->

一旦有了这个 DOM 树，为了弄清 DOM 是如何响应新的状态而改变的，React 会将这个新树与上一个虚拟 DOM 树比较。

这样做，React 会知道发生的确切变化，并且通过了解发生的变化后，在绝对必要的情况下进行更新 DOM，即可将因操作 DOM 而占用的空间最小化。

## 二、在 React 中元素（element）和组件（component）有什么区别？

简单的说，在 React 中元素（虚拟 DOM）描述了你在屏幕上看到的 DOM 元素。换个说法就是，在 React 中元素是页面中 DOM 元素的对象表示方式，在 React 中组件是一个函数或一个类，它可以接受输入并返回一个元素。

> 提醒：工作中，为了提高开发效率，通常使用 JSX 语法表示 React 元素（虚拟 DOM）。在编译的时候，把它转化成一个 React.creatElement 调用方法。

## 三、什么时候使用类组件（Class Component）？什么时候使用功能组件（Functional Component）？

如果使用组件具有状态（state）或生命周期方法，请使用类组件；否则使用功能组件。

## 四、什么是 React 的 refs？为什么它们很重要？

refs 允许你直接访问 DOM 元素或组件实例，为了使用它们，可以向组件添加一个 ref 属性。

如果该属性的值是一个回调函数，它将接受底层的 DOM 元素或组件的已挂载实例作为其第一个参数。可以在组件中存储它。

```
export class App extends Component {
  showResult() {
    console.log(this.input.value);
  }
  render() {
    return(
      <div>
        <input type="text" ref={ input => this.input = input} />
        <button onClick={ this.showResult.bind(this) }> 展示结果 </button>
      </div>
    )
  }
}
```

如果该属性值是一个字符串，React 将会在组件实例化对象的 refs 属性中，存储一个同名属性，该属性是对这个 DOM 元素的引用，可以通过原生的 DOM API 操作它。

```
export class App extends Component {
  showResult() {
    console.log(this.refs.username.value)
  }
  render() {
    return (
      <div>
        <input type="text" ref="username" />
        <button onClick={this.showResult.bind(this)}>展示结果</button>
      <div>
    )
  }
}
```

## 五、React 中的 key 是什么？为什么它们很重要？

key 可以帮助 React 跟踪循环创建列表中的虚拟 DOM 元素，了解哪些元素已更改、添加或删除。

每个绑定 key 的虚拟 DOM 元素，在兄弟元素之间都是独一无二的。在 React 的和解过程中，比较新的虚拟 DOM 树与上一个虚拟 DOM 树之间的差异，并映射到页面中。key 使 React 处理列表中虚拟 DOM 时更加高效，因为 React 可以使用虚拟 DOM 上的 key 属性，快速了解元素是新的，还是需要删除的，还是修改过的。如果没有 key，React 就不知道列表中虚拟 DOM 元素与页面中的哪个元素相对应，所以在创建列表的时候，不要忽略 key。

## 六、如果创建了类似于下面的 Icketang 元素，那么该如何实现 Icketang 类？

```
<Icketang username="雨夜清荷">
  {user => user ? <Info user={user} /> : <Loading />}
</Icketang>
import React, {Component} from "react";
export class Icketang extends Component {
  // 请实现代码
  constructor(props) {
    super(props);
    this.state = {
      user: props.user
    }
  }
  componentDidMount() {
    // 模拟异步获取数据操作，更新状态
    setTimeout(()=> this.setState({
      user: '爱创课堂'
    }), 2000)
  }
  render() {
    return this.props.children(this.state.user)
  }
}
class Loading extends Component {
  render() {
    return <p>Loading...</p>
  }
}
class Info extends Component {
  render() {
    return <h1>{this.props.user}</h1>
  }
}
```

## 七、约束性组件（controlled component）与非约束性组件（uncontrolled component）有什么区别？

在 React 中，组件负责控制和管理自己的状态。

如果将 HTML 中的表单元素（input、select、textarea 等）添加到组件中，当用户与表单发生交互时，就设计表单数据存储问题。根据表单数据存储问题。根据表单数据的存储位置，将组件分成约束性组件和非约束性组件。

约束性组件（controlled component）就是由 React 控制的组件。
