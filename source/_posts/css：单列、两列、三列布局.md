---
title: css：单列、两列、三列布局
date: 2019-10-27 17:06:35
tags: css
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、单列布局

![](https://user-gold-cdn.xitu.io/2018/11/7/166ed4e13cc2753f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

<!--more-->

### 1、header,content 和 footer 等宽的单列布局

先通过对 header,content,footer 统一设置`width:1000px`或者`max-width:1000px` （这两者的区别是当屏幕小于 1000px 时，前者会出现滚动条，后者则不会，显示实际宽度），然后设置`margin:auto` 实现居中即可得到

```
<div class="header"></div>
<div class="content"></div>
<div class="footer"></div>
<style>
	.header,
	.content,
	.footer {
		margin: 0 auto;
		max-width: 1000px;
	}
	.header {
		height: 100px;
		background-color: green;
	}
	.content {
		height: 200px;
		background-color: blue;
	}
	.footer {
		height: 100px;
		background-color: red;
	}
</style>
```

### 2、header 与 footer 等宽，content 略窄的单列布局

header、footer 的内容宽度不设置，块级元素充满整个屏幕，但 header、content、footer 的内容区设置同一个 width，并通过 margin：0 auto 实现居中

```
<div class="header">
	<div class="nav"></div>
</div>
<div class="content"></div>
<div class="footer"></div>
<style>
	.header,
	.content,
	.footer,
	.nav {
		margin: 0 auto;
	}
	.header {
		max-width: 1000px;
		height: 100px;
		background-color: green;
	}
  .nav {
		max-width: 800px;
		height: 10px;
		background-color: yellow;
	}
	.content {
		width: 500px;
		height: 200px;
		background-color: blue;
	}
	.footer {
		max-width: 1000px;
		height: 100px;
		background-color: red;
	}
</style>
```

## 二、两列布局

### 1、利用 float 配合 margin 实现

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <div class="box">
      <div class="left">left</div>
      <div class="right">right</div>
    </div>
    <style>
      .box {
        overflow: hidden;
        height: 100%;
      }
      .box > div {
        height: 100%;
      }
      .left {
        float: left;
        background-color: red;
        width: 100px;
      }
      .right {
        background-color: blue;
        margin-left: 100px;
      }
    </style>
  </body>
</html>
```

### 2、利用 float 配合 overflow 实现

如果是普通的两列布局，**浮动+普通元素的 margin ** 便可以实现，但如果是自适应的两列布局，利用**float+overflow:hidden** 便可以实现，这种办法主要是通过 overflow 触发 BFC，因为 BFC 不会重叠浮动元素，由于设置 overflow:hidden 并不会触发 IE6-浏览器的 laslayout 属性，所以需要设置 zoom:1 来兼容 IE6-浏览器

```
    <div class="parent">
      <div class="left">
        <p>left</p>
      </div>
      <div class="right">
        <p>right</p>
      </div>
    </div>
    <style>
      .parent {
        background-color: aqua;
        overflow: hidden;
        zoom: 1;
      }
      .left {
        float: left;
        background-color: red;
      }
      .right {
        overflow: hidden;
        background-color: blue;
      }
    </style>
```

## 3、使用 flex 实现

```
    <div class="parent">
      <div class="left">
        <p>left</p>
      </div>
      <div class="right">
        <p>right</p>
      </div>
    </div>
    <style>
      .parent {
        background-color: aqua;
        display: flex;
      }
      .left {
        background-color: red;
      }
      .right {
        flex: 1;
        background-color: blue;
      }
    </style>
```

### 4、grid 布局

Grid 布局，是一个基于网格的二维布局系统，目的是用来优化用户界面设计。

```
    <div class="parent">
      <div class="left">
        <p>left</p>
      </div>
      <div class="right">
        <p>right</p>
      </div>
    </div>
    <style>
      .parent {
        background-color: aqua;
        display: grid;
        grid-template-columns: auto 1fr;
      }
      .left {
        background-color: red;
      }
      .right {
        background-color: blue;
      }
    </style>
```

## 三、三列布局

**特征：中间列自适应宽度，旁边两侧固定宽度**

### 1、圣杯布局

#### 1.1 特点

比较特殊的三栏布局，同样也是两固定宽度，中间自适应，唯一的区别是 dom 结构必须是先写中间列部分，这样实现中间列可以优先加载。

#### 1.2 实现步骤

- 三个部分都设定为左浮动，否则左右两边内容上不去，就不可能和中间列同一行，然后设置 center 的宽度为 100%（实现中间列内容自适应），此时，left 和 right 部分会跳到下一行。

  ![](https://user-gold-cdn.xitu.io/2018/10/18/16682cae82722a6a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 通过设置 margin-left 为负值让 left 和 right 部分回到与 center 部分同一行

  ![](https://user-gold-cdn.xitu.io/2018/10/18/16682c1d72a1ea68?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 通过设置父容器的 padding-left 和 padding-right，让左右两边留出间隙

  ![](https://user-gold-cdn.xitu.io/2018/10/18/16682c473f605745?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 通过设置相对定位，让 left 和 right 部分移动到两边

  ![](https://user-gold-cdn.xitu.io/2018/10/17/16682bf3615502c2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

#### 1.3 缺点

- center 部分的最小宽度不能小于 left 部分的宽度，否则 left 部分会掉到下一行

- 如果其中一列内容高度拉长，其他两列的背景并不会自动填充（借助等高布局正 padding+负 padding 可解决）

  ![](https://user-gold-cdn.xitu.io/2018/11/8/166f229b862b187f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

```
    <div class="container">
      <div class="center">圣杯布局</div>
      <div class="left"></div>
      <div class="right"></div>
    </div>
    <style>
      .left,
      .center,
      .right {
        float: left;
        height: 100px;
      }
      .container {
        padding-left: 100px;   //为左右栏腾出空间
        padding-right: 100px;
      }
      .left {
        width: 100px;
        background-color: red;
        margin-left: -100%;
        position: relative;
        left: -100px;
      }
      .center {
        background-color: yellow;
        width: 100%;
      }
      .right {
        width: 100px;
        margin-left: -100px;
        position: relative;
        right: -100px;
        background-color: blue;
      }
    </style>
```

### 2、双飞翼布局

#### 2.1 特点

同样是三栏布局，在圣杯布局基础上进一步优化，解决了圣杯布局错误问题，实现了内容与布局的分离。而且任何一栏都可以是最高栏，不会出问题。

#### 2.2 实现步骤（前两步与圣杯布局）

- 三个部分都设定为左浮动，然后设置 center 的宽度为 100%，此时，left 和 right 部分会跳到下一行
- 通过设置 margin-left 为负值让 left 和 right 部分回到与 center 部分同一行
- center 部分增加一个内层 div，并设`margin：0 200px`；

#### 2.3 缺点

多加一层 dom 树节点，增加渲染树生成的计算量

```
    <div class="container">
      <div class="main col">
        <div class="main_inner">main</div>
      </div>
      <div class="left col">left</div>
      <div class="right col">right</div>
    </div>
    <style>
      body,
      html,
      container {
        height: 100%;
        padding: 0;
        margin: 0;
      }
      .col {
        float: left; /*把left和right定位到左右不分*/
      }
      .main {
        width: 100%;
        height: 100%;
        background-color: red;
      }
      /*处理中间栏被遮盖问题*/
      .main_inner {
        margin: 0 200px 0 100px;
      }
      .left {
        width: 100px;
        height: 100%;
        margin-left: -100%;
        background-color: green;
      }
      .right {
        width: 200px;
        height: 100%;
        margin-left: -200px;
        background-color: blue;
      }
    </style>
```

**对比圣杯布局和双飞翼布局**

（1）都是左右栏定宽，中间自适应的三栏布局，中间栏都放在文档流前面，保证先行渲染

（2）解决方案基本相似：都是三栏全部设置左浮动`float: left` ，然后分别解决中间栏内容被覆盖问题

（3）解决中间栏内容被覆盖问题时，圣杯布局设置父元素的 padding，双飞翼布局在中间栏外面嵌套了一个 div，并设置 margin，实际上双飞翼布局就是圣杯布局的改进方案

### 3、flex 布局

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <div class="container">
      <div class="left">left</div>
      <div class="main">main</div>
      <div class="right">right</div>
    </div>
    <style>
      .container {
        display: flex;
      }
      .left {
        width: 200px;
        background-color: red;
      }
      .main {
        flex: 1;
        overflow: hidden; // 避免中间内容溢出
        background-color: blue;
      }
      .right {
        width: 200px;
        background-color: green;
      }
    </style>
  </body>
</html>
```

### 4、流体布局

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <div class="left"></div>
    <div class="right"></div>
    <div class="main"></div>
    <style>
      .left,
      .right,
      .main {
        height: 200px;
      }
      .left {
        float: left;
        width: 100px;
        background-color: red;
      }
      .right {
        float: right;
        width: 100px;
        background-color: green;
      }
      .main {
        background-color: blue;
        margin-left: 100px;
        margin-right: 100px;
      }
    </style>
  </body>
</html>
```

**缺点**：主要内容无法最先加载，当页面内容较多时会影响用户体验

### 5、BFC 三栏布局

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <div class="left"></div>
    <div class="right"></div>
    <div class="main"></div>
    <style>
      .left,
      .right,
      .main {
        height: 200px;
      }
      .left {
        float: left;
        width: 100px;
        background-color: red;
      }
      .right {
        float: right;
        width: 100px;
        background-color: green;
      }
      .main {
        background-color: blue;
        overflow: hidden;
      }
    </style>
  </body>
</html>

```

[几种常见的 CSS 布局](https://juejin.im/post/5bbcd7ff5188255c80668028)
