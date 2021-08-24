---
title: vue：双向绑定
date: 2019-10-19 09:30:53
tags: vue
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、Vue 双向数据绑定

![](https://upload-images.jianshu.io/upload_images/8560482-d18d5fe20c1ade5c.png?imageMogr2/auto-orient/strip|imageView2/2/w/730/format/webp)

<!--more-->

vue 双向数据绑定是通过数据劫持和订阅者-发布者模式实现的

1. 实现一个监听器 Observer：对数据进行遍历，包括子属性对象的属性，利用 Object.defineProperty()或 Proxy 对属性都加上 setter 和 getter。这样给这个对象的某个值赋值，就会触发 setter，就能监听到了数据变化；
2. 实现一个解析器 Compile：解析 Vue 模板指令，将模板中的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，调用更新函数进行数据更新；
3. 实现一个订阅者 Watcher：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁，主要的任务是订阅 Observer 中的属性值变化的消息，当收到属性值变化的消息时，触发解析器 Compile 中对应的更新函数
4. 实现一个订阅器 Dep：订阅器采用发布-订阅设计模式，用来收集订阅者 Watcher，对监听器 Observer 和订阅者 Watcher 进行统一管理

**注意：** Object.defineProperty()对数据进行劫持，但是 Object.defineProperty()只能对属性进行数据劫持，不能对整个对象进行劫持，同理无法对数组进行劫持，所以 Vue 框架是通过遍历数组的递归遍历对象，从而达到利用 Object.defineProperty()也能对对象和数组（部分方法的操作）进行监听。

**代码实现：**

```
<body>
  <div id="app">
    <form>
      <input type="text"  v-model="number">
      <button type="button" v-click="increment">增加</button>
    </from>

    <h3 v-bind="number"></h3>
    <form>
      <input type="text"  v-model="count">
      <button type="button" v-click="incre">增加</button>
    </form>
    <h3 v-bind="count"></h3>
  </div>
</body>

<script>
  function myVue(options) {
    this._init();
  }

  myVue.prototype._init = function (options) {
    this.$options = options;
    this.$el = document.querySelector(options.el);
    this.$data = options.data;
    this.$methods = options.methods;

    this._binding = {};
    this._obverse(this.$data);
    this._complie(this.$el);
  }

  myVue.prototype._obverse = function (obj) {
    var _this = this;
    Object.keys(obj).forEach(function (key) {
      if (obj.hasOwnProperty(key)) {
        _this._binding[key] = {
          _directives: []
        };
        console.log(_this._binding[key])
        var value = obj[key];
        if (typeof value === 'object') {
          _this._obverse(value);
        }
        var binding = _this._binding[key];
        Object.defineProperty(_this.$data, key, {
          enumerable: true,
          configurable: true,
          get: function () {
            console.log(`${key}获取${value}`);
            return value;
          },
          set: function (newVal) {
            console.log(`${key}更新${newVal}`);
            if (value !== newVal) {
              value = newVal;
              binding._directives.forEach(function (item) {
                item.update();
              })
            }
          }
        })
      }
    })
  }

  myVue.prototype._complie = function (root) {
    var _this = this;
    var nodes = root.children;
    for (var i = 0; i < nodes.length; i++) {
      var node = nodes[i];
      if (node.children.length) {
        this._complie(node);
      }

      if (node.hasAttribute('v-click')) {
        node.onclick = (function () {
          var attrVal = nodes[i].getAttribute('v-click');
          return _this.$methods[attrVal].bind(_this.$data);
        })();
      }

      if (node.hasAttribute('v-model') && (node.tagName = 'INPUT' || node.tagName == 'TEXTAREA')) {
        node.addEventListener('input', (function(key) {
          var attrVal = node.getAttribute('v-model');
          _this._binding[attrVal]._directives.push(new Watcher(
            'input',
            node,
            _this,
            attrVal,
            'value'
          ))

          return function() {
            _this.$data[attrVal] =  nodes[key].value;
          }
        })(i));
      }

      if (node.hasAttribute('v-bind')) {
        var attrVal = node.getAttribute('v-bind');
        _this._binding[attrVal]._directives.push(new Watcher(
          'text',
          node,
          _this,
          attrVal,
          'innerHTML'
        ))
      }
    }
  }

  function Watcher(name, el, vm, exp, attr) {
    this.name = name;         //指令名称，例如文本节点，该值设为"text"
    this.el = el;             //指令对应的DOM元素
    this.vm = vm;             //指令所属myVue实例
    this.exp = exp;           //指令对应的值，本例如"number"
    this.attr = attr;         //绑定的属性值，本例为"innerHTML"

    this.update();
  }

  Watcher.prototype.update = function () {
    this.el[this.attr] = this.vm.$data[this.exp];
  }

  window.onload = function() {
    var app = new myVue({
      el:'#app',
      data: {
        number: 0,
        count: 0,
      },
      methods: {
        increment: function() {
          this.number ++;
        },
        incre: function() {
          this.count ++;
        }
      }
    })
  }
</script>
```

![](https://user-gold-cdn.xitu.io/2018/4/10/162ad3d5beb544b6?imageslim)

## 二、Proxy 和 Object.defineProperty 优劣势对比

### 1、Proxy 优势

- Proxy 可以直接监听对象而非属性；
- Proxy 可以直接监听数组的变化；
- Proxy 有多达 13 种拦截方法，不限于 apply、ownKeys、deleteProperty、has 等等是 Object.defineProperty 不具备的；
- Proxy 返回的是一个新对象，我们可以只操作新的对象达到目的，而 Object.defineProperty()只能遍历对象属性直接修改；
- Proxy 作为新标准将受到浏览器厂商重点持续的性能优化，也就是传说中的新标准的性能红利

### 2、Object.defineProperty()优势

- 兼容性好，支持 IE9，而 Proxy 存在浏览器兼容性问题，而且无法用 polyfill 磨平，因此要在 vue3.0 才能用 Proxy

[深入浅出 Vue 响应式原理（完整版）](https://juejin.im/post/5d229bfc5188252d707f3ac6)
