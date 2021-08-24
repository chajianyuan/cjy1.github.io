---
title: uniapp：APP实现定位
date: 2019-05-12 10:15:55
tags: uniapp
category: 技术
---

<meta name="referrer" content="no-referrer"/>

### 使用高德地图定位

#### 1、先去[高德地图 API](https://lbs.amap.com/dev/key/app)中申请 key 值

![](https://github.com/chajianyuan/picture/blob/master/1.png?raw=true)

<!--more-->

如何获取 SHA1 指纹？

```
cd .android
keytool -list -v -keystore debug.keystore
```

如果出现如下错误
![](https://github.com/chajianyuan/picture/blob/master/2.png?raw=true)
去本地的 jdk 安装目录中的 bin 目录下可以发现 keytool.exe
![](https://github.com/chajianyuan/picture/blob/master/3.png?raw=true)
用命令符输入

```
keytool.exe -list -keystore C:\Users\cjy.android\debug.keystore
```

密钥库口令默认为 android
![](https://github.com/chajianyuan/picture/blob/master/4.png?raw=true)

#### 2、下载[Android 定位 SDK](https://lbs.amap.com/api/android-location-sdk/download)

在代码中引入 SDK 文件

```
import amapFile from '../../utils/amap-wx.js';
```

#### 3、在代码中编写

```
let myAmapFun = new amapFile.AMapWX({ key: '在步骤1中拿到的key值' });
myAmapFun.getRegeo({
  success: data => {
    //成功回调
    this.address = data[0];
  fail: info => {
  //失败回调
  	console.log(JSON.stringify(info));
  }
});
```
