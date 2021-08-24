---
title: css：如何对前端图片主题色进行提取
date: 2021-08-02 11:50:35
tags: css
category: 技术
---

<div style="text-align: center;">
  <img src="https://github.com/chajianyuan/picture/blob/master/Kapture%202021-08-02%20at%2013.48.28.gif?raw=true" width="400px" style="display: inline-block;" />
  <img src="https://github.com/chajianyuan/picture/blob/master/WX20210802-145509@2x.png?raw=true" width="210px" style="margin-left: 10px; display: inline-block;" />
</div>

:question: 如上图electron官网的应用中的app logo在初次渲染的时候获取的是它的主题色，又或者，像网易云音乐切歌的时候背景色也是用的当前歌曲封面的主题色，那么我们该如何获取图片的主题色呢？
<!--more-->

#### 一、背景图使用高斯模糊实现网易云音乐背景模糊

使用css中的[filter属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)

```
filter: blur(20px);
```

[代码参考👉](https://github.com/chajianyuan/cssTest/blob/master/src/ExtractThemeColor/GaussianBlur/style.css#L23)

效果如下：
<img src="https://github.com/chajianyuan/picture/blob/master/WX20210802-145245@2x.png?raw=true" width="300px" />

#### 二、使用canvas

##### 1. 👣 获取图片数据

```
const imgElement = document.querySelector(`.img${index}`);
// 创建画布
const canvas = document.createElement('canvas');
canvas.setAttribute('width', imgElement.width);
canvas.setAttribute('height', imgElement.height);
const context = canvas.getContext('2d');
// 将图片画在画布上
context.drawImage(imgElement, 0, 0);
// 获取像素数据
const imgData = context.getImageData(0, 0, imgElement.width, imgElement.height);
const piexlData = imgData.data;
```

##### 2. 👣 对图片数据进行处理

##### 3. 👣 对颜色列表进行排序

#### 参考

[:bulb: 产品经理：喂那个前端，你从图片提取下主题色](https://mp.weixin.qq.com/s/m7bHjApumqm9HncFHnQm_g)
