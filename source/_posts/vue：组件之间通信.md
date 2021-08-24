---
title: vue：组件之间的通信
date: 2019-08-09 17:17:27
tags: vue
category: 技术
---

<meta name="referrer" content="no-referrer"/>

### 一、父-->子

父组件向子组件传递数据通过 props

<!--more-->

```
**父组件代码**
<template>
    <header-box :title-txt="showTitleTxt"></header-box>
</template>
<script>
    import Header from './header'
    export default {
        name: 'index',
        components: {
            'header-box': Header
        },
        data () {
            return {
                showTitleTxt: '首页'
            }
        }
    }
</script>
```

```
**子组件代码**
<template>
    <header>
        {{thisTitleTxt}}
    </header>
</template>
<script>
    export default {
        name: 'header-box',
        props: {
            titleTxt: String
        },
        data () {
            return {
                thisTitleTxt: this.titleTxt
            }
        }
    }
</script>
```

### 二、子-->父

子组件向父组件传递数据用$on和$emit

```
**父组件代码**
<template>
  <typetemplate @change-type="changeType"></typetemplate>
</template>
<script>
  data () {
   return {
    selectType: 0,
  },
  methods: {
   changeType (type) {
    this.type = type
   }
  },
  components: {
　　typetemplate
　}
</script>
```

```
**子组件代码**
<template>
 <div @click="changeData(1)">点击改变数据</div>
</template>
<script>
  data () {
   return {
    type: 0,
  },
  methods: {
    changeData (type) {
      this.type = type
      this.$emit('change-type', type)
   }
  }
</script>
```

### 三、兄弟之间通信

使用 bus 进行通信

```
**main.js**
let bus = new Vue()
Vue.prototype.bus = bus
```

```
**A组件**
<template>
    <header @click="changeTitle">{{title}}</header>
</template>
<script>
export default {
    name: 'header',
    data () {
        return {
            title: '头部'
        }
    },
    methods: {
        changeTitle () {
            this.bus.$emit('toChangeTitle','首页')
        }
    }
}
</script>
```

```
**B组件**
<template>
    <footer>{{txt}}</footer>
</template>
<script>
export default {
    name: 'footer',
    mounted () {
        this.bus.$on('toChangeTitle', function (title) {
            console.log(title)
        })
    },
    data () {
        return {
            txt: '尾部'
        }
    }
}
```
