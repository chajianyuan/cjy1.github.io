---
title: 总结：html
date: 2019-10-24 21:13:21
tags: 总结
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、HTML 语义化

### 1、含义

语义化的含义就是用正确的标签做正确的事情

<!--more-->

### 2、优势

（1）便于对浏览器、搜索引擎解析

（2）便于盲人浏览网页

（3）便于阅读源代码的人对网站进行分开，维护和理解

### 3、有哪些语义化的标签

< h1 > - < h6 >、< p >、< ul >、< ol >、< li>、< dl>、< dt>、< dd>、< em>、< strong>、< em>、< table>、< thead>、< tbody>、< td>、< th>、< caption>等

## 二、HTML5 新标签

- `header元素`：header 元素代表“网页”或“section”的页眉。
- `footer元素`：footer 元素代表“网页”或“section”的页脚，通常含有该节的一些基本信息，譬如：作者，相关文档链接，版权资料。
- `hgroup元素`：
- `nav元素`：nav 元素代表页面的导航链接区域。用于定义页面的主要导航部分。
- `aside元素`：aside 元素被包含在 article 元素中作为主要内容的附属信息部分，其中的内容可以是与当前文章有关的相关资料、标签、名次解释等。（特殊的 section）
- `section元素`：section 元素代表文档中的“节”或“段”，“段”可以是指一篇文章里按照主题的分段；“节”可以是指一个页面里的分组。section 通常还带标题，虽然 html5 中 section 会自动给标题 h1-h6 降级，但是最好手动给他们降级。
- `article元素`：article 元素最容易跟 section 和 div 容易混淆，其实 article 代表一个在文档，页面或者网站中自成一体的内容，其目的是为了让开发者独立开发或重用。譬如论坛的帖子，博客上的文章，一篇用户的评论，一个互动的 widget 小工具。（特殊的 section）除了它的内容，article 会有一个标题（通常会在 header 里），会有一个 footer 页脚。

## 三、常见浏览器及其内核

|      | Chrome | Firefox | Safari |   IE    | Opera |
| :--: | :----: | :-----: | :----: | :-----: | :---: |
| 内核 | Blink  |  Gecko  | Webkit | Trident | Bink  |

## 四、 < script >和< link >或者是 src 和 href 的区别

1. src 表示来源地址，用在 img、script、iframe 等元素上；
2. href 表示超文本引用，用在 link、a 等元素上；
3. src 的内容是页面必不可少的一部分，表示引入；而 href 的的内容与该页面有关联，表示引用；
4. src 用于替代这个元素，而 href 用于建立这个标签与外部资源之间的关系。

## 五、< head >中都有什么元素

### 1、< base >

为页面上的所有链接规定默认地址或默认目标

通常情况下，浏览器会从当前文档的 URL 中提取相应的元素来填写相对 URL 中的空白。

使用 < base > 标签可以改变这一点。浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL。这其中包括 < a >、< img >、< link >、< form > 标签中的 URL。

```
<base href="http://www.w3school.com.cn/i/" />
<base target="_blank" />
```

### 2、< link >

定义文档与外部资源的关系，最常见的就是链接样式表。

```
<link rel="stylesheet" type="text/css" href="theme.css" />
```

### 3、< script >

用于定义用户脚本，比如 JavaScript。script 元素既可以包含脚本语言，也可以通过 src 属性指向外部脚本文件。必须的 type 属性规定脚本的 MIME 类型

```
<script type="text/javascript">
	document.write("Hello World!")
</script>
```

### 4、< meta >

可提供有关页面的元信息，比如针对搜索引擎和更新频度的描述和关键词。定义了与文档相关联的名称/值对。

`<meta name="keywords" content="HTML,ASP,PHP,SQL">`

### 5、< style >

用于为 html 文档定义样式信息。type 属性是必须的，定义 style 元素的内容，唯一可能的值是“text/css”

```
<style type="text/css">
	h1 {color:red}
	p {color:blue}
</style>
```

### 6、< title >

定义文档的标题，通常是现实在浏览器窗口的标题栏或者是状态栏上。

```
<title>XHTML Tag Reference</title>
```

## 六、本地存储

[参见总结：cookie、session、sessionStorage、localStorage](https://chajianyuan.github.io/2019/10/26/cookie%E3%80%81sessionStorage%E3%80%81localStorage%E8%AF%A6%E7%BB%86%E8%AE%B2%E8%A7%A3/)

## 七、websocket

[参见总结：webSocket 学习](https://chajianyuan.github.io/2019/10/26/webSocket%E5%AD%A6%E4%B9%A0/)

## 八、W3C 标准

w3c 标准不是某一个标准，而是一系列标准的集合，网页主要由三部分组成：结构（structure）、表现（Presentation）、行为（behavior）

### 1、结构标准语言

#### 1.1 可扩展标记语言（XML）

和 HTML 一样，XML 同样来源于标准通用标记语言，可扩展标记语言和标准通用标记语言都是能定义其他语言的语言。XML 最初设计的目的是弥补 HTML 的不足，以强大的扩展性满足网络信息发布的需要，后来逐渐用于网络数据的转换和描述。

#### 1.2 可扩展超文本标记语言（XHTML）

**HTML 和 XHTML 的共同点**

- 所有的标记都必须有一个对应的结束标记
- 所有的标签的元素和属性的名字都必须使用小写
- 所有的 XML 标记都必须合理嵌套
- 所有的属性都必须用“ ”引起来
- 所有的“<”和“&”特殊符号都用编码表示
- 给所有属性赋一个值
- 不要在注释内容中使用“--”
- 图片必须有说明文字

**HTML 和 XHTML 的区别**

- HTML 是一种基于 web 网页的设计语言，XHTML 是一种基于 XML、语法严格、标准的设计语言
- XHTML 元素必须正确的嵌套，元素必须关闭，标签必须小写，必须有根元素；HTML 没有这些限制

### 2、表现标准语言

#### 2.1 层叠样式表（css）

万维网联盟创建 CSS 标准的目的是以 CSS 取代 HTML 表格式布局、帧和其他表现的语言。纯 CSS 布局与结构式 XHTML 相结合能帮助设计师分离外观与结构，使站点的访问及维护更加容易。

### 3、行为标准

#### 3.1 文档对象模型（DOM）

根据 W3C DOM 规范，DOM 是一种与浏览器，平台，语言的接口，使得你可以访问页面其他的标准组件。简单理解，DOM 解决了 Netscaped 的 Javascript 和 Microsoft 的 Jscript 之间的冲突，给予 web 设计师和开发者一个标准的方法，让他们来访问他们站点中的数据、脚本和表现层对象。

#### 3.2 ECMAScript

ECMAScript 是 ECMA(European Computer Manufacturers Association)制定的标准脚本语言（JAVAScript）。

## 九、img 标签上的 title 和 alt 属性的区别

- title 的功能是为元素提供标题信息，即当光标悬浮在标签上后显示的信息
- alt 的功能是图片的替换文案，即当图片不能正常显示的时（如加载失败），用文字代替

## 十、空元素

空元素也就是单标签元素：< br >、< hr >、< img >、< input >、< link >、< meta >
