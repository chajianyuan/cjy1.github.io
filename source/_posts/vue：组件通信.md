---
title: vue：组件通信
date: 2019-10-19 16:58:21
tags: vue
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 1、props/\$emit（父子组件）

<!--more-->

**props**

父级：父级组件中引用子组件，并将自己 data 下面的 giveChild 数据绑定在 giveChildDate 传给子

```
<myChild :giveChildData="giveChild">{{isMe}}</myChild>

data(){
  return{
    giveChild:'222'
  }
},
components:{
  myChild
}
```

子级：通过 props 接收父级传来的数据，并将接收到的数据显示在自身模板上

```
props:{
      giveChildData:{
         type:String
      }
}

<div>{{giveChildData}}</div>
```

**\$emit**

子级上的点击事件成功后，通过\$emit 将事件和数据发射出去

```
<div @click="sendChildData">点我将子的数据传给父级</div>

data(){
	return{
		childData:111
    }
},
methods:{
	sendChildData(){
		this.$emit('sendChildData',this.childData)
	}
}

```

父级接收到事件后，走自己的事件 getChildData 并进行相关处理、显示。

```
<myChild :giveChildData="giveChild" @sendChildData="getChildData"></myChild>
<div>这是子级传过来的数据 ——> {{isMe}}</div>

data(){
	return{
		giveChild:'222',
		isMe:''
	}
},
methods:{
	getChildData(data){
		this.isMe = data;
	}
},
components:{
	myChild
}
```

## 2、ref 和$parent/$children（父子）

- `ref`：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例
- `$parent` / `$children`：访问父 / 子实例

ref 是被用来给元素或子组件注册引用信息的。引用信息将会注册在父组件的 \$refs 对象上。

父组件

```
<template>
 <div>
  <h1>我是父组件！</h1>
  <child ref="msg"></child>
 </div>
</template>

<script>
 import Child from '../components/child.vue'
 export default {
  components: {Child},
  mounted: function () {
   console.log( this.$refs.msg);
   this.$refs.msg.getMessage('我是子组件一！')
  }
 }
</script>
```

子组件

```
<template>
 <h3>{{message}}</h3>
</template>
<script>
 export default {
  data(){
   return{
    message:''
   }
  },
  methods:{
   getMessage(m){
    this.message=m;
   }
  }
 }
</script>
```

## 3、EventBus（$emit/$ on）（父子、隔代、兄弟）

这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

bus.js

```
 import Vue from 'vue'
 export default new Vue;
```

要通信的组件

```
import Bus from './bus.js'

methods: {
	bus () {
		Bus.$emit('msg', '我要传给兄弟组件们，你收到没有')
	}
}
```

接收通信的组件

```
import Bus from './bus.js'

mounted() {
	let self = this
	Bus.$on('msg', (e) => {
		self.message = e
		console.log(`传来的数据是：${e}`)
	})
}
```

## 4、$attrs/$listeners（隔代）

- `$attrs`：包含了父作用域中不被 prop 所识别 (且获取) 的特性绑定 ( class 和 style 除外 )。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 ( class 和 style 除外 )，并且可以通过 `v-bind="$attrs"` 传入内部组件。通常配合 inheritAttrs 选项一起使用。
- `$listeners`：包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 `v-on="$listeners"` 传入内部组件

## 5、provide/inject（隔代）

祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 inject 来注入变量。 provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

## 6、Vuex（父子、隔代、兄弟）

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

（1）Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

（2）改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

主要包括以下几个模块：

- State：定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation：是唯一更改 store 中状态的方法，且必须是同步函数。
- Action：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
- Module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。
