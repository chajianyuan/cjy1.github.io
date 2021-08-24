---
title: css：水平垂直居中
date: 2019-10-16 12:15:15
tags: css
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、水平居中

### 1、行内元素

<!--more-->

#### （1）父元素是块级元素

父元素设置`text-align: center`

```
<div class="one">
	<span>我是行内元素</span>
</div>

.one {
	width: 200px;
	height: 100px;
	border: solid 1px red;
	text-align: center;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016123813.png?raw=true)

#### （2）父元素不是块级元素

先将父元素设置为块级元素，再将父元素设置`text-align: center`

```
<span class="one">
	<span>我是行内元素</span>
</span>

.one {
	width: 200px;
	height: 100px;
	border: solid 1px red;
	display: block;
	text-align: center;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016123813.png?raw=true)

### 2、块级元素

#### （1）定宽度

`margin: 0 auto;`

```
<div class="main">
	<div class="one">
		我是有宽度的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
}
.one {
	width: 200px;
	height: 100px;
	margin: 0 auto;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016124428.png?raw=true)

#### （2）不定宽度

1. 设置子元素`display: inline` 或`display: inline-block`;
2. 给父元素设置`text-align: center`

```
<div class="main">
	<div class="one">
		我是没有宽度的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	text-align: center;
}
.one {
	display: inline;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016125427.png?raw=true)

#### （3）使用定位属性

1. 设置父元素为相对定位；
2. 子元素为绝对定位，
3. 设置子元素的 left:50%，即让子元素的左上角水平居中

##### （a） 定宽度

设置绝对子元素的`margin-left: -子元素宽度的一半px` ；或者设置`transform: translateX(-50%)`

```
<div class="main">
	<div class="one">
		我是使用定位属性有宽度的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	position: relative;
}
.one {
	position: absolute;
	left: 50%;
	width: 200px;
	margin-left: -100px;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016131118.png?raw=true)

##### （b）不定宽度

利用 css 新增属性`transform: translateX(-50%)`

```
<div class="main">
	<div class="one">
		我是使用定位属性没有宽度的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	position: relative;
}
.one {
	position: absolute;
	left: 50%;
	width: 200px;
	transform: translateX(-50%);
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016150151.png?raw=true)

#### （4）flex + justify-content

利用 flexbox，只需要给待处理的块状元素的父元素添加属性`dispaly: flex;justify-content: center;`

```
<div class="main">
	<div class="one">
		我是使用flex布局的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	display: flex;
	justify-content: center;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016150717.png?raw=true)

#### （5）flex + margin

父元素设置为 flex 布局，子元素只用 margin 居中。

```
<div class="main">
	<div class="one">
		我是使用flex布局的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	display: flex;
}
.one {
	margin: 0 auto;
}
```

## 二、垂直居中

### 1、单行的行内元素

只需要设置单行行内元素的行高 = 盒子高度即可

```
<div class="main">
	<span class="one">
		我是单行行内元素
	</span>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
}
.one {
	line-height: 300px;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016152131.png?raw=true)

 ### 2、多行的行内元素

给父元素设置`display: table-cell` 和`vertical-align:middle`

```
<div class="main">
	<span class="one">
		我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素我是多行行内元素
	</span>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	display: table-cell;
	vertical-align: middle;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016153152.png?raw=true)

### 3、块级元素

#### （1）使用定位属性

1. 设置父元素为相对定位
2. 设置子元素为绝对定位
3. 设置子元素的`top:50%` ，即让子元素在左上角垂直居中

##### （a）定高度

设置绝对子元素的`margin-top:-子元素高度的一半px` ；或者设置`translateY(-50%)`

```
<div class="main">
	<div class="one">
		我是使用定位属性有高度的块级元素
	</div>
</div>

.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	display: table-cell;
	position: relative;
}
.one {
	height: 100px;
	position: absolute;
	top: 50%;
	margin-top: -50px;
	background-color: green;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016160059.png?raw=true)

##### （b）不定高度

使用 css3 新增属性`transform:translateY(-50%)`

```
<div class="main">
	<div class="one">
		我是使用定位属性没有高度的块级元素
	</div>
</div>
.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	display: table-cell;
	position: relative;
}
.one {
	height: 100px;
	position: absolute;
	top: 50%;
	transform: translateY(-50%);
	background-color: green;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016160537.png?raw=true)

#### （2）使用 flex 布局

使用 flexbox 布局，只需要给待处理的块状元素的父元素添加属性`display:flex; align-items:center;`

```
<div class="main">
	<div class="one">
		我是使用flex布局的块级元素
	</div>
</div>
.main {
	width: 500px;
	height: 300px;
	border: solid 1px red;
	display: flex;
	align-items: center;
}
.one {
	height: 100px;
	background-color: green;
}
```

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720191016162740.png?raw=true)

## 三、水平垂直居中

### 1、绝对定位与负边距

子元素有宽度高度

```
<div class="one">
	<div class="two">
	</div>
</div>

.one {
	position: relative;
}
.two {
	width: 100px;
	height: 100px;
	position: absolute;
	top: 50%;
	left: 50%;
	margin: -50px 0 0 -50px;
}
```

### 2、绝对定位与 margin: auto

父元素必须有高度

```
<div class="one">
	<div class="two">
	</div>
</div>

.one {
	position: relative;
	height: 100px;
}
.two {
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
}
```

### 3、绝对定位+css3

不知道子元素的宽高

```
<div class="one">
	<div class="two">
	</div>
</div>

.one {
	position: relative;
}
.two {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}
```

### 4、flex 布局

```
<div class="one">
	<div class="two">
	</div>
</div>

.one {
	display: flex;
	justify-content: center;
	align-items: center;
}
```

### 5、flex/grid 与 margin: auto

父元素必须有高度

```
<div class="one">
	<div class="two">
	</div>
</div>

.one {
	height: 100px;
	display: grid / flex;
}
.two {
	margin: auto;
}
```

[如何居中一个元素（终结版）](https://juejin.im/post/5bc3eb8bf265da0a8a6ad1ce)
