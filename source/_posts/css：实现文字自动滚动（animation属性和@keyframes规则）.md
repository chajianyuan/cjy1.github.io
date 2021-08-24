---
title: css：实现文字自动滚动（animation属性和@keyframes规则）
date: 2021-01-08 15:48:20
tags:
---

使用css的animation属性和@keyframes规则，实现中奖信息的滚动播报

要创建 css3 动画，需要了解@keyframes 规则

<!--more-->

- @keyframes 规则是创建动画
- @keyframes 规则内指定一个 CSS 样式动画将逐步从目前的样式更改为新的样式

当在 **@keyframes** 创建动画，把它绑定到一个选择器，否则动画不会有任何效果。

指定至少这两个 CSS3 的动画属性绑定向一个选择器：

- 规定动画的名称
- 规定动画的时长

| 属性                      | 描述                                                                                     |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| keyframes                 | 规定动画。                                                                               |
| animation                 | 所有动画属性的简写属性，除了 animation-play-state 属性。                                 |
| animation-name            | 规定 @keyframes 动画的名称。                                                             |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。                                         |
| animation-timing-function | 规定动画的速度曲线。默认是 "ease"。                                                      |
| animation-fill-mode       | 规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。 |
| animation-delay           | 规定动画何时开始。默认是 0。                                                             |
| animation-iteration-count | 规定动画被播放的次数。默认是 1。                                                         |
| animation-direction       | 规定动画是否在下一周期逆向地播放。默认是 "normal"。                                      |
| animation-play-state      | 规定动画是否正在运行或暂停。默认是 "running"。                                           |

```
<div></div>

div{
	width:100px;
	height:100px;
	background:red;
	position:relative;
	animation-name:myfirst;
	animation-duration:5s;
	animation-timing-function:linear;
	animation-delay:2s;
	animation-iteration-count:infinite;
	animation-direction:alternate;
	animation-play-state:running;
}
@keyframes myfirst
{
	0%   {background:red; left:0px; top:0px;}
	25%  {background:yellow; left:200px; top:0px;}
	50%  {background:blue; left:200px; top:200px;}
	75%  {background:green; left:0px; top:200px;}
	100% {background:red; left:0px; top:0px;}
}
```

### animation 和 transition 的异同

**相同：** 功能相同，都是通过改变元素的属性值来实现动画效果的。

**不同：** transition 只能用指定属性的开始值和结束值，然后在这两个属性值之间使用平滑过渡的方式实现动画效果，因此不能实现比较复杂的动画效果；animation 通过定义多个关键帧，以及定义每个关键帧中元素的属性值来实现更为复杂的动画效果。

以react.js为例

JSX部分
```
<div className="prize-info">
  <div className="rowup">
    {
      winners.map(item => <div key={item.nick} className="winner-info">
        <img className="prize-img" src={item.headerpic ? item.headerpic : defaultAvatar} />
        {item.nick}已获得{item.price}元试用资格
      </div>)
    }
  </div>
</div>
```

CSS部分
```
.prize-info {
  background-color: rgba(#FFFFFF, .19);
  border-radius: 0.63rem;
  max-width: 9.5rem;
  margin: 0 auto;
  padding: .15rem .7rem;
  font-size: .55rem;
  overflow: hidden;
  position: relative;
  .winner-info {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: .2rem;
  }
  .prize-img {
    width: .7rem;
    height: .7rem;
    border-radius: 50%;
    border: solid 1px #fff;
    margin-right: .15rem;
  }
}
.prize-info .rowup{
  height: .85rem;
  -webkit-animation: 10s rowup linear infinite normal;
  animation: 10s rowup linear infinite normal;
  position: relative;
}
@keyframes rowup {
  0% {
      -webkit-transform: translate3d(0, 0, 0);
      transform: translate3d(0, 0, 0);
  }
  100% {
      -webkit-transform: translate3d(0, -8em, 0);
      transform: translate3d(0, -8rem, 0);
  }
}

```

待更～（后续会记录使用websocket时时更新数据）