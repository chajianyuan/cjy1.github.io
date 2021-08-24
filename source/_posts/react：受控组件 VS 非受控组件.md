---
title: react：受控组件 VS 非受控组件
date: 2021-06-04 10:18:23
tags: react
category: 技术
---

#### 一、非受控组件

1. 必须手动操作DOM元素

2. 无法使用setState

<!--more-->

3. 举个 🌰
    * ref

    * defaultValue defaultChecked

    * 文件上传`<input type="file" />`

    * 某些富文本编辑器，需要传入DOM元素
    
    * `<input defaultValue="value" />`，如果想更新defaultValue的值，需要加一个key,`<input defaultValue="value" key="value" />`，❓为什么加一个key，就能更新defalutValue的值了呢？

#### 二、受控组件

1. 受state影响

2. 需要自行监听onChange，更新state

3. 无需手动操作DOM

4. 举个 🌰

    * input 标签中的value属性

      ```
      class Demo extents React.Component {
        constructor() {
          this.state = {
            name: ''
          }
        }

        handleChange = e => {
          this.setstate({
            name: e.target.value
          })
        }

        render() {
          return <input value={this.state.name} onChange={this.handleChange} />
        }
      }
      ```


#### 三、受控组件 vs 非受控组件

1. 优先使用受控组件，符合react设计原则
2. 必须操作DOM元素，再使用非受控组件