---
title: 网络协议：post和get的区别
date: 2019-10-20 08:43:54
tags: 网络协议
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、post 和 get 的区别

[详见参考](https://mp.weixin.qq.com/s?__biz=MzI3NzIzMzg3Mw==&mid=100000054&idx=1&sn=71f6c214f3833d9ca20b9f7dcd9d33e4#rd)

<!--more-->

## 二、post 提交数据方式

### 1、application/json

这是最常见的 json 格式

```
POST http://www.example.com HTTP/1.1
Content-Type: application/json;charset=utf-8

{"input1":"xxx","input2":"ooo","remember":false}
```

### 2、application/x-www-form-urlencoded

浏览器的原生 form 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded 方式提交

```
POST http://www.example.com HTTP/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

input1=xxx&input2=ooo&remember=false
```

### 3、multipart/form-data

当你需要提交文件、非 ASCII 码的数据或者是二进制流数据，则使用这种提交方式。

```
POST http://www.example.com HTTP/1.1
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryPAlLG7hJKNYc4ft3

------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="text"

demo
------WebKitFormBoundaryPAlLG7hJKNYc4ft3
Content-Disposition: form-data; name="file"; filename="demo.png"
Content-Type: image/png


------WebKitFormBoundaryPAlLG7hJKNYc4ft3--
```

### 4、text/xml

这种直接传的 xml 格式

```
<!--?xml version="1.0"?-->

<methodcall>

<methodname>examples.getStateName</methodname>

<params>

<param>

<value><i4>41</i4></value>

</params>

</methodcall>

------WebKitFormBoundaryrGKCBY7qhFd3TrwA--
```
