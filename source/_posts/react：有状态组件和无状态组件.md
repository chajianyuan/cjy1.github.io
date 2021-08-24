---
title: react：有状态组件和无状态组件
date: 2020-02-11 09:06:30
tags: react
category: 技术
---

<meta name="referrer" content="no-referrer"/>

### 一、React 中创建组件的方式

#### 1、ES5：React.createClass

<!--more-->

#### 2、ES6：React.Component

#### 3、无状态函数

### 一、有状态组件

```
class A extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'hello world'
    }
  }
  render() {
  	const {name} = this.state;
  	const {title} = this.props;
    return(
      <div>
        <div>{name}</div>
        <div>{title}</div>
      </div>
    )
  }
}

export default A;
```

### 二、无状态组件

```
const B = (props)=> {
  const [name, setName] = useState('hello world');
  const {title} = props;
  return(
     <div>
       <div>{name}</div>
       <div>{title}</div>
     </div>
  )
}

export default B;
```

无状态组件主要用来定义模板，接收来自父组件 props 传递过来的数据。

无状态组件应该保持模板的纯粹性，以便组件的复用。
