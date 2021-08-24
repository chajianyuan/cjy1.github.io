---
title: JS：scrollWidth、offsetWidth、clientWidth
date: 2020-11-03 22:01:56
tags: javascript
category: 技术
---
### Element.clientWidth

内联元素以及没有css样式的元素的`clientWidth`值为0。 `Element.clientWidth`属性表示元素的内部宽度。

<!--more-->

该属性包括内边距padding，但不包括边框border、外边距margin和垂直滚动条（如果有的话）。

⚠️ 当在根元素（< html >元素）上使用`clientWidth`(或者在< body >上，如果文档是在怪异模式下)，将返回viewport的宽度（不包含任何滚动条）。

> 这个属性会进行四舍五入并返回整数，如果需要小数形式的值，则使用`element.getBoundingClientRect()`。

### Element.scrollWidth

`Element.scrollWidth`这个只读属性是元素内容宽度的一种度量，包括由于overflow溢出而在屏幕上不可见的内容。

scrollWidth值等于元素在不使用水平滚动条的情况下适合视口中的所有内容所需的最小宽度。

宽度的测量与`clientWidth`相同：它包括元素的内边距，但是不包括边框、外边距或垂直滚动条（如果存在）。它还可以包括伪元素的宽度，例如`::before`或`::after`。如果元素的内容可以适合而不需要水平滚动条，则其`scrollWidth`等于`clientWidth`。

> 1. 这个属性会进行四舍五入并返回整数，如果需要小数形式的值，则使用`element.getBoundingClientRect()`。
> 2. 谷歌获取的`Element.scrollWidth`和IE、火狐下获取的`Element.scrollWidth`并不相同。

### Element.offsetWidth

`Element.offsetWidth`是一个只读属性，返回一个元素的布局宽度。

`Element.offsetWidth`是测量包含元素的边框（border）、水平线上的内边距（padding）、垂直方向上的滚动条、以及css设置的的宽度（width）值。

⚠️ 各浏览器的offsetWidth可能有所不同。

> 这个属性会进行四舍五入并返回整数，如果需要小数形式的值，则使用`element.getBoundingClientRect()`。