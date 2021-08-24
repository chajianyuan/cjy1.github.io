---
title: css：flex布局
date: 2019-10-13 09:53:53
tags: css
category: 技术
---

<meta name="referrer" content="no-referrer"/>



<!--more-->

### 一、容器的属性

#### 1、flex-direction

定义主轴的方向。

```
.box {
  display: flex;
  flex-direction: row | row-reverse | column | column-reverse;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

#### 2、flex-wrap

定义如果一行排不下，如何换行。

```
.box {
  display: flex;
  flex-direction: row;
  flex-wrap: npwrap | wrap | wrap-reverse;
}
```

![nowrap](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)
![wrap](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)
![wrap-reverse](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)

#### 3、flex-flow

flex-direction 和 flex-wrap 的简写，默认值为 row nowrap。

```
.box {
  display: flex;
  flex-flow：<flex-direction> || <flex-row>;
}
```

#### 4、justify-content

定义了项目在主轴上的对齐方式。

```
.box {
  display: flex;
  justify-content：flex-start | flex-end | center | space-between | space-around;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)

#### 5、align-items

定义了项目在交叉轴上如何对齐。

```
.box {
  display: flex;
  align-items：flex-start | flex-end | center | baseline | stretch;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

#### 6、align-content

定义了多个项目在主轴上的对齐方式。如果只有一个项目则该属性不奏效。

```
.box {
  display: flex;
  align-content：flex-start | flex-end | center | space-between | space-around | stretch;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

### 二、项目的属性

#### 1、order

定义项目的排列顺序。数值越小，排列越靠前，默认值为 0。

```
.box {
  display: flex;
}

.item {
  order： <integer>;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

#### 2、flex-grow

定义项目的放大比例，默认值为 0，即如果存在剩余空间，也不放大。

```
.box {
  display: flex;
}

.item {
  flex-grow：<number>;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)

#### 3、flex-shrink

定义了项目的缩小比例，默认值为 1，即如果空间不足，该项目将缩小。

```
.box {
  display: flex;
}

.item {
  flex-shrink：<number>;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)

#### 4、flex-basis

定义了在分配多余空间之前，项目占据的主轴空间，浏览器根据这个属性，计算主轴是否有多余空间。默认值为 auto，即项目本身的大小。

```
.box {
  display: flex;
}

.item {
  flex-basis：<length> | auto;
}
```

#### 5、flex

flex-grow，flex-shrink，flex-basis 的简写，默认值为 0 1 auto。后两个属性可选。

```
.box {
  display: flex;
}

.item {
  flex：none | <flex-grow> <flex-shrink>? || <flex-basis>;
}
```

#### 6、align-self

允许单个项目有不同于其他项目在交叉轴上的对齐方式，可以覆盖 align-items。默认为 auto，表示继承父元素的 align-items 属性，如果父元素没有 align-items 属性，则等同于 stretch。

```
.box {
  display: flex;
}

.item {
  align-self：auto | flex-start | flex-end | center | baseline | stretch；
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)

### 三、小技巧 💡

#### 1. flex布局实现头部和底部固定，中间滚动布局(少了撑满，多了滚动)

实现思路：

1. 设置最外层为flex布局，方向为纵向
2. 中间的div设置`flex: 1`，撑满除topbar和footer之外的空间

代码实现：
```
<div class="body">
  <div class="topbar">topbar</div>
  <div class="content">contentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontentcontent</div>
  <div class="footer">footer</div>
</div>

.body {
  width: 150px;
  height: 80vh;
  display: flex;
  flex-direction: column;
}

.topbar {
  width: 100%;
  background-color: red;
}

.content {
  width: 100%;
  flex: 1;
  background-color: green;
  overflow-y: scroll;
  word-break: break-all;
}

.footer {
  width: 100%;
  background-color: blue;
}
```

参考资料：[flex 布局实现固定头部和底部，中间滚动布局](https://my.oschina.net/u/4336279/blog/3569932)

参照[阮一峰的 Flex 布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
