---
title: 总结：css
date: 2019-10-23 14:26:27
tags: 总结
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、css 选择器

[参见总结：css：css 选择器及优先级](https://chajianyuan.github.io/2019/10/19/css%EF%BC%9Acss%E9%80%89%E6%8B%A9%E5%99%A8%E5%8F%8A%E4%BC%98%E5%85%88%E7%BA%A7/)

<!--more-->

## 二、css 的引入方式

[参见总结：css：css 的引入方式]()

## 三、浮动元素（Float）

[参见总结：css：float 和 position](https://chajianyuan.github.io/2019/10/18/css%EF%BC%9Afloat%E5%92%8Cposition/)

## 四、定位属性（position）

[参见总结：css：float 和 position](https://chajianyuan.github.io/2019/10/18/css%EF%BC%9Afloat%E5%92%8Cposition/)

## 五、css 元素哪些可以继承，哪些不可以

可继承的样式：font-size、font-family、color

不可继承的样式：border、padding、margin、width、height

**与字体相关的样式通常可以继承，与尺寸相关的样式通常不能继承。**

## 六、为什么要初始化 css

因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没有初始化 css，往往会导致页面在不同浏览器之间出现差异

当然，初始化样式有时会对 SEO 产生一定一影响，但鱼和熊掌不可兼得，所以在力求影响最小的情况下初始化 css

最简单的初始化方法就是`*{padding: 0; margin: 0}`

## 七、display 属性

[菜鸟教程：CSS display 属性](https://www.runoob.com/cssref/pr-class-display.html)

常用属性值

| 值           | 描述                                                           |
| ------------ | -------------------------------------------------------------- |
| none         | 此元素不会显示，已脱离文档流                                   |
| block        | 块类型，默认宽度为父元素宽度，可设置宽高，换行显示             |
| inline       | 行内元素类型，默认宽度为内容宽度，不可设置宽高，同行显示。     |
| inline-block | 行内块级元素类型，默认宽度为内容宽度，可以设置宽高，同行显示。 |
| list-item    | 像块类型元素一样显示，并添加样式列表标记                       |
| table        | 此元素会作为块级表格显示                                       |
| inherit      | 从父元素继承 display 属性的值                                  |

## 八、行内元素、行内块级元素、块级元素

[参见总结：html：行内元素、行内块级元素、块级元素](https://chajianyuan.github.io/2019/10/15/html%EF%BC%9A%E8%A1%8C%E5%86%85%E5%85%83%E7%B4%A0%E3%80%81%E8%A1%8C%E5%86%85%E5%9D%97%E7%BA%A7%E5%85%83%E7%B4%A0%E3%80%81%E5%9D%97%E7%BA%A7%E5%85%83%E7%B4%A0/)

## 九、盒模型

[参见总结：css：盒模型及 box-sizing](https://chajianyuan.github.io/2019/10/15/css%EF%BC%9A%E7%9B%92%E6%A8%A1%E5%9E%8B%E5%8F%8Abox-sizing/)

## 十、css 单位

[参见总结：css：元素单位的使用](https://chajianyuan.github.io/2019/10/17/css%EF%BC%9A%E5%85%83%E7%B4%A0%E5%8D%95%E4%BD%8D%E7%9A%84%E4%BD%BF%E7%94%A8/)

## 十一、css 常见布局

### 1、水平居中、垂直居中、水平垂直居中

[参见总结：css：水平垂直居中](https://chajianyuan.github.io/2019/10/16/css%EF%BC%9A%E6%B0%B4%E5%B9%B3%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD/)

### 2、单列、两列、三列布局

[参照总结：css：单列、两列、三列布局](https://chajianyuan.github.io/2019/10/27/css%EF%BC%9A%E5%8D%95%E5%88%97%E3%80%81%E4%B8%A4%E5%88%97%E3%80%81%E4%B8%89%E5%88%97%E5%B8%83%E5%B1%80/)

## 十二、css3 新特性

[参见总结：css：css3 属性](https://chajianyuan.github.io/2019/10/19/css%EF%BC%9Acss3%E5%B1%9E%E6%80%A7/)

## 十三、BFC 规范

[参照总结：css：BFC 规范](https://chajianyuan.github.io/2019/10/27/css%EF%BC%9ABFC%E8%A7%84%E8%8C%83/)

## 十四、flex 布局

[参见总结：css：flex 布局](https://chajianyuan.github.io/2019/10/13/css%EF%BC%9Aflex%E5%B8%83%E5%B1%80/)
