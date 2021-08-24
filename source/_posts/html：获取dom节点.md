---
title: html：获取dom节点
date: 2021-04-26 23:51:19
tags: html
category: 技术
---

### 一、通过元素类型的方式

#### 1. getElementById

**:leaves: 通过id名称获取dom节点，返回一个dom节点**

```
document.getElementById('id名称');
```

![](https://github.com/chajianyuan/picture/blob/master/WX20210427-000254@2x.png?raw=true)

> ⚠️ 如果存在多个同名id，只取第一个

<!--more-->

#### 2. getElementsByName

**:leaves: 通过name属性名称获取dom节点，返回一个类数组**

```
document.getElementsByName('name')
```

![](https://github.com/chajianyuan/picture/blob/master/WX20210427-000305@2x.png?raw=true)

#### 3. getElementsByTagName

**:leaves: 通过标签名称获取dom节点，返回一个类数组**

```
document.getElementsByTagName('div')
```

#### 4. getElementsByClassName

**:leaves: 通过类名获取dom节点，返回一个类数组**

```
document.getElementsByClassName('class')
```

#### 5. documentElement

**:leaves: 获取html节点**

```
document.documentElement
```

![](https://github.com/chajianyuan/picture/blob/master/WX20210427-000615@2x.png?raw=true)

#### 6. body

**:leaves: 获取body节点**

```
document.body
```

#### 7. querySelector

**:leaves: 通过选择器获取一个元素**

```
document.querySelector('.ouvJEz')
```

![](https://github.com/chajianyuan/picture/blob/master/WX20210427-000934@2x.png?raw=true)

#### 8. querySelectorAll

**:leaves: 通过选择器获取一组元素**

```
document.querySelectorAll('.ouvJEz')
```

![](https://github.com/chajianyuan/picture/blob/master/WX20210427-001002@2x.png?raw=true)


### 练习

[来做一个练习题吧🎁](https://github.com/chajianyuan/htmlTest/issues/1)