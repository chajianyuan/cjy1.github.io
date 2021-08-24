---
title: css：瀑布流布局
date: 2021-05-02 20:24:03
tags: css
category: 技术
---

<img src="https://github.com/chajianyuan/picture/blob/master/WX20210515-164933@2x.png?raw=true" width="600px" />
 
 <!--more-->

### 一、实现方式

#### 1. 使用javascript原生实现

* 优点：图片排序是按照图片计算的位置横向排列，位置是计算出来的，比较规范

* 缺点：需要计算，列数 = 浏览器窗口宽度 / 图片宽度，图片定位是根据每一列数据块的高度计算接下来图片的位置

盒子之间的间距建议使用padding，因为需要使用`offsetHeight`计算盒子的高度，`offsetHeight`指包括`padding`，不包括`margin`


js代码实现

```
window.onload = function () {
  waterfall('main', 'box');
  let dataInt = {
    data: [
      {src: '1.jpeg'},
      {src: '2.jpeg'},
      {src: '3.jpeg'}
    ]
  }
  window.onscroll = () => {
    if (checkScrollSlide()) {
      // 将数据块渲染到当前页面的尾部
      for (let i = 0; i < dataInt.data.length; i++) {
        let oParent = document.getElementById('main');
        let oBox = document.createElement('div');
        oBox.className = 'box';
        oParent.appendChild(oBox);
        let oPic = document.createElement('div');
        oPic.className = 'pic';
        oBox.appendChild(oPic);
        let oImg = document.createElement('img');
        oImg.src = `images/${dataInt.data[i].src}`;
        oPic.appendChild(oImg);
      }
      waterfall('main', 'box');
    }
  };
};

const waterfall = (parent, box) => {
  // 将main下的所有class为box的元素取出来
  let oParent = document.getElementById(parent);
  let oBoxs = getByClass(oParent, box);
  // 计算整个页面显示的列数（页面宽/box的宽）
  let oBoxW = oBoxs[0].offsetWidth;
  let cols = Math.floor(document.documentElement.clientWidth / oBoxW);
  // 设置main的宽
  oParent.style.cssText = 'width:' + oBoxW * cols + 'px; margin: 0 auto;';
  let hArr = []; // 存放每一列高度的数组
  for (let i = 0; i < oBoxs.length; i++) {
    if (i < cols) {
      hArr.push(oBoxs[i].offsetHeight);
    } else {
      let minH = Math.min.apply(null, hArr);
      let index = getMinHIndex(hArr, minH);
      oBoxs[i].style.position = 'absolute';
      oBoxs[i].style.top = minH + 'px';
      // oBoxs[i].style.left = oBoxW * index + 'px';
      oBoxs[i].style.left = oBoxs[index].offsetLeft + 'px';
      hArr[index] += oBoxs[i].offsetHeight;
    }
  }
};

// 根据class获取元素
const getByClass = (parent, className) => {
  let boxArr = []; // 用来存储获取到的所有class为box的元素
  let oElements = parent.getElementsByTagName('*');
  for (let i = 0; i < oElements.length; i++) {
    if (oElements[i].className === className) {
      boxArr.push(oElements[i]);
    }
  }
  return boxArr;
};

const getMinHIndex = (arr, val) => {
  let min = arr.findIndex(i => i === val);
  return min;
};

//  检测是否具备了滚动条加载数据块的条件
const checkScrollSlide = () => {
  let oParent = document.getElementById('main');
  let oBoxs = getByClass(oParent, 'box');
  let lastBoxH = oBoxs[oBoxs.length - 1].offsetTop + Math.floor(oBoxs[oBoxs.length - 1].offsetHeight / 2);
  let scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
  let height = document.body.clientHeight || document.documentElement.clientHeight;
  return lastBoxH < scrollTop + height;
}
```

html代码实现

```
<div id="main">
    <div class="box">
      <div class="pic">
        <img src="images/1.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/2.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/3.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/4.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/5.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/6.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/7.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/8.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/9.jpeg" />
      </div>
    </div>
    <div class="box">
      <div class="pic">
        <img src="images/10.jpeg" />
      </div>
    </div>
  </div>
```

css代码实现：

```
body {
  margin: 0;
}

#main {
  position: relative;
}

.box {
  padding: 15px 0 0 15px;
  float: left;
}

.pic {
  padding: 10px;
  border: solid 1px #ccc;
  border-radius: 5px;
  box-shadow: 0 0 5px #ccc;
}

.pic img {
  width: 250px;
  height: auto;
}

```

#### 2. css3多栏布局实现

##### (1) 使用column属性

* 优点：不需要计算，浏览器自动计算，只需设置列宽，性能高

* 缺点：不可横向排列，只能纵向排列，打乱图片的排列顺序

css代码实现：
```
#main {
  -webkit-column-width: 202px;
  -moz-column-width: 202px;
  -moz-column-width: 202px;
  -ms-column-width: 202px;
  /* -webkit-column-count: 5;
  -moz-column-count: 5;
  -moz-column-count: 5;
  -ms-column-count: 5; */
  -webkit-column-gap: 5px;
  -moz-column-gap: 5px;
  -moz-column-gap: 5px;
  -ms-column-gap: 5px;
}
```

##### (2) 使用flex布局

* 优点：可实现横向排列的瀑布流
* 缺点：容器必须有固定高度，并且高度要大于最高的列高

css代码实现：

```
#main {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  /* 容器必须有固定高度
   * 且高度大于最高的列高 */
  height: 2000px;
  width: 500px;
  align-content: space-between;
}

/* 强制换列 */
#main::before,
#main::after {
  content: "";
  flex-basis: 100%;
  width: 0;
  order: 2;
}

.box:nth-child(2n+1) {
  order: 1;
}
.box:nth-child(2n) {
  order: 2;
}

.box {
  width: 32%;
  padding: 10px;
  position: relative;
  border: 1px solid #ccc;
  box-shadow: 0 0 5px #ccc;
  margin-bottom: 10px;
}

.box img {
  width: 100%;
}
```


