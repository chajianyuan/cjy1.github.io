---
title: css：BFC规范
date: 2019-10-27 11:00:05
tags: css
category: 技术
---

<meta name="referrer" content="no-referrer"/>

### 一、定义

BFC（Block formatting context，块级格式化上下文），他是一个独立的渲染区域，只有 Block-level box 参与，他规定了内部的 Block-level box 如何布局，并且与这个区域外部毫不相干。通俗的讲，BFC 是一个容器，用于管理块级元素。

### 二、BFC 触发方式

- float 为 left|right
- overflow 为 hidden|auto|scroll
- display 为 table-cell|table-caption|inline-block
- position 为 absolute|fixed

### 三、特性

#### 1. 阻止垂直外边距重叠

（1）两个兄弟元素垂直边距重叠

```
<div class="content1"></div>
<div class="content2"></div>

.content1 {
  width: 100px;
  height: 100px;
  background: red;
  margin: 10px;
  overflow: hidden;
}

.content2 {
  width: 200px;
  height: 200px;
  background: green;
  margin: 20px 10px;
}
```
![](https://github.com/chajianyuan/picture/blob/master/1721617073209_.pic.jpg?raw=true)

**解决办法：** 让两个元素不处于同一个BFC

```
<div class="box1">
  <div class="content1"></div>
</div>
<div class="content2"></div>

.box1 {
  overflow: hidden;
}

.content1 {
  width: 100px;
  height: 100px;
  background: red;
  margin: 10px;
  overflow: hidden;
}

.content2 {
  width: 200px;
  height: 200px;
  background: green;
  margin: 20px 10px;
}
```

![](https://github.com/chajianyuan/picture/blob/master/1731617073258_.pic.jpg?raw=true)

#### 2. 父子元素垂直边距重叠

```
<div class="box1">
  <div class="content1"></div>
</div>

.box1 {
  margin: 20px;
}

.content1 {
  width: 100px;
  height: 100px;
  background: red;
  margin: 10px;
}
```

![](https://github.com/chajianyuan/picture/blob/master/1701617072889_.pic.jpg?raw=true)

**解决办法：** 父元素形成一个BFC

```
<div class="box1">
  <div class="content1"></div>
</div>

.box1 {
  margin: 20px;
  overflow: hidden;
}

.content1 {
  width: 100px;
  height: 100px;
  background: red;
  margin: 10px;
}
```
![](https://github.com/chajianyuan/picture/blob/master/1711617073145_.pic.jpg?raw=true)

#### 2. BFC不会重叠浮动元素

可以创造自适应两栏布局

```
<div class="box1">
  <div class="content1">
    我是浮动元素
  </div>
  <div class="content2">
    哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈
  </div>
</div>

.box1 {
  margin: 20px;
  width: 350px;
}

.content1 {
  width: 100px;
  height: 100px;
  background: red;
  float: left;
}

.content2 {
  overflow: hidden;
}
```

![](https://github.com/chajianyuan/picture/blob/master/1751617076427_.pic.jpg?raw=true)

#### 3. 清除浮动

将父元素创造为BFC，避免高度塌陷

```
<div class="box1">
  <div class="content1">
    我是浮动元素
  </div>
  <div class="content2">
    哈哈哈
  </div>
</div>

.box1 {
  margin: 20px;
  background: yellow;
  overflow: hidden;
}

.content1 {
  width: 100px;
  height: 100px;
  background: red;
  float: left;
}

.content2 {
  float: left;
}
```

![](https://github.com/chajianyuan/picture/blob/master/1761617076728_.pic.jpg?raw=true)


[参考：深入理解 BFC](https://juejin.im/post/5bc33d0d6fb9a05d1658afc7)
