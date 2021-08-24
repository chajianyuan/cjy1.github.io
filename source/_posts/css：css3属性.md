---
title: css：css3属性
date: 2019-10-19 11:55:08
tags: css
category: 技术
---

<meta name="referrer" content="no-referrer"/>

[参照掘金](https://juejin.im/post/5a0c184c51882531926e4294#heading-11)

<!--more-->

## 1、过渡（transition）

参照[菜鸟教程|css3 过渡](https://www.runoob.com/css3/css3-transitions.html)

CSS 过渡是元素从一种样式逐渐改变为另一种的效果，要实现这一点，必须规定两项内容：

- 指定要参加效果的 CSS 属性
- 指定效果的持续时间

| 属性                       | 描述                                       |
| -------------------------- | ------------------------------------------ |
| transition                 | 简写属性，用于在一个属性中设置四个过渡属性 |
| transition-property        | 规定应用过渡的 CSS 属性的名称              |
| transition-duration        | 定义过渡效果花费的时间。默认是 0           |
| transition-timing-function | 规定过渡效果的时间曲线。默认是“ease”       |
| transition-delay           | 规定过渡效果何时开始。默认是 0             |

```
<div></div>

div{
	width:100px;
	height:100px;
	background:red;
	transition-property:width;
	transition-duration:1s;
	transition-timing-function:linear;
	transition-delay:2s;
	/* Safari */
	-webkit-transition-property:width;
	-webkit-transition-duration:1s;
	-webkit-transition-timing-function:linear;
	-webkit-transition-delay:2s;
}
div:hover{
	width:200px;
}
```

## 2、动画（animation）

参考[菜鸟教程|css3 动画](https://www.runoob.com/css3/css3-animations.html)

## 3、形状转换（transform）

参照[菜鸟教程|css3 transform](https://www.runoob.com/cssref/css3-pr-transform.html)

transform 适用于 2D 或 3D 转换的元素

`transform: none|transform-functions;`

| 值                                                                        | 描述                                    |
| ------------------------------------------------------------------------- | --------------------------------------- |
| none                                                                      | 定义不进行转换。                        |
| matrix(_n_,_n_,_n_,_n_,_n_,_n_)                                           | 定义 2D 转换，使用六个值的矩阵。        |
| matrix3d(_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_,_n_) | 定义 3D 转换，使用 16 个值的 4x4 矩阵。 |
| translate(_x_,_y_)                                                        | 定义 2D 转换。                          |
| translate3d(_x_,_y_,_z_)                                                  | 定义 3D 转换。                          |
| translateX(_x_)                                                           | 定义转换，只是用 X 轴的值。             |
| translateY(_y_)                                                           | 定义转换，只是用 Y 轴的值。             |
| translateZ(_z_)                                                           | 定义 3D 转换，只是用 Z 轴的值。         |
| scale(_x_[,*y*]?)                                                         | 定义 2D 缩放转换。                      |
| scale3d(_x_,_y_,_z_)                                                      | 定义 3D 缩放转换。                      |
| scaleX(_x_)                                                               | 通过设置 X 轴的值来定义缩放转换。       |
| scaleY(_y_)                                                               | 通过设置 Y 轴的值来定义缩放转换。       |
| scaleZ(_z_)                                                               | 通过设置 Z 轴的值来定义 3D 缩放转换。   |
| rotate(_angle_)                                                           | 定义 2D 旋转，在参数中规定角度。        |
| rotate3d(_x_,_y_,_z_,_angle_)                                             | 定义 3D 旋转。                          |
| rotateX(_angle_)                                                          | 定义沿着 X 轴的 3D 旋转。               |
| rotateY(_angle_)                                                          | 定义沿着 Y 轴的 3D 旋转。               |
| rotateZ(_angle_)                                                          | 定义沿着 Z 轴的 3D 旋转。               |
| skew(_x-angle_,_y-angle_)                                                 | 定义沿着 X 和 Y 轴的 2D 倾斜转换。      |
| skewX(_angle_)                                                            | 定义沿着 X 轴的 2D 倾斜转换。           |
| skewY(_angle_)                                                            | 定义沿着 Y 轴的 2D 倾斜转换。           |
| perspective(_n_)                                                          | 为 3D 转换元素定义透视视图。            |

`transform:rotate(30deg);`

![](https://user-gold-cdn.xitu.io/2017/11/15/15fbf4073fe59bee?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
