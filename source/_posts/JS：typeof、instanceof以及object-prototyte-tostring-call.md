---
title: JS：typeof、instanceof以及Object.prototyte.toString.call()
date: 2019-10-13 14:11:06
tags: javascript
category: 技术
---

<meta name="referrer" content="no-referrer"/>

## 一、数据类型

### 1、基本数据类型

<!--more-->

number、string、Boolean、undefined、null、Symbol（ES6中新增）、BigInt（ES10中新增）

> BigInt 可以表示任意大的整数（ > 2^53 -1）

### 2、引用数据类型

Object(Array、Function、Date。。。)

### 3、基本数据类型和引用数据类型的区别

（1）基本数据类型的值不可变，引用数据类型的值可变；

（2）基本数据类型存储的是值，引用数据类型存储的是地址（指针）；

（3）基本数据类型的比较是值得比较，引用数据类型的比较是地址的比较；

（4）基本数据类型的值保存在栈中；引用数据类型的值保存在堆中，指针保存在栈中，这个指针指向堆中的值。

## 二、判断数据类型的方法

### 1、typeof

- **对于基本数据类型，除了 null 输出为 object，其他的都是正确的类型；**
- **对于引用数据类型，除了 function 输出为 function，其他的都是 object**

#### （1）原理

js 在底层存储变量的时候，会在变量的机器码的低位 1-3 位存储其类型信息

- 000：对象
- 010：浮点数
- 100：字符创
- 110：布尔
- 1：整数
- null：所有机器码均为 0
- undefined：用-2^30 整数来表示

**因为 null 的所有机器码都为 0，所以 typeof 就把他当做了对象来看待**

#### （2）实现

typeof 可以判断一个变量的类型，

```
typeof 1               =>  "number"
typeof "1"             =>  "string"
typeof undefined       =>  "undefined"
typeof true            =>  "boolean"
typeof Symbol()        =>  "symbol"
typeof 11n             =>  "bigint"
typeof null            =>  "object"
typeof []              =>  "object"
typeof {}              =>  "object"
typeof function a(){}  =>  "function"
```

### 2、instanceof

语法：`数据 instanceof 数据类型`，返回 true 或 false

#### （1）作用

- **判断一个实例是否属于某种类型；**
- **判断一个实例是否是其父类型或者祖先类型的实例。**

#### （2）原理

instanceof 在查找的过程中会遍历左边变量的原型链，直到找到右边变量的 prototype，如果查找失败则返回**false **

#### （3）实现

```
[] instanceof Array             =>  true
[] instanceof Object            => true
'' instanceof String            => false
new String() instanceof String  => true
let a = {}
a instanceof Object             => true
function b(){}
b instanceof Function           => true
```

### 3、Object.prototype toString.call()

语法：`Object.prototype.toString.call(数据)`返回`[object 数据类型]`

```
Object.prototype.toString.call({})            =>  "[object Object]"
Object.prototype.toString.call([])            =>  "[object Array]"
Object.prototype.toString.call(function(){})  =>  "[object Function]"
Object.prototype.toString.call('')            =>  "[object String]"
Object.prototype.toString.call(1)             =>  "[object Number]"
Object.prototype.toString.call(true)          =>  "[object Boolean]"
Object.prototype.toString.call(null)          =>  "[object Null]"
Object.prototype.toString.call(undefined)     => "[object Undefined]"
Object.prototype.toString.call()              => "[object Undefined]"
Object.prototype.toString.call(new Date())    =>  "[object Date]"
Object.prototype.toString.call(/at/)          =>  "[object RegExp]"
```

## 三、类型转换

### 1、类型转换

| 原始值          | 转换目标 |                      结果 |
| --------------- | :------: | ------------------------: |
| number          | Boolean  | 除了 0、-0、NaN 都为 true |
| string          | Boolean  |         除了空串都为 true |
| undefined、null | Boolean  |                     false |
| 引用类型        | Boolean  |                      true |
| number          |  string  |                    5=>'5' |

| Boolean、函数
、symbol |string |'true' |
|数组 |string |[1,2]=>'1,2' |
|对象 | string|'[object Object]' |
|string |number |'1'=>1,'a'=>NaN |
|数组 |number |空数组=>0,存在一个元素且为数字=>数字,其他=>NaN |
| null|number |0 |
|除了数组的引用类型 |number | NaN|
|symbol | number|报错 |

### 2、四则运算

- 加法运算

  - 其中一方为字符串，会把另外一方也转成字符串；
  - 如果一方不是字符串或数字，将它转换为数字或字符串；

  ```
  1 + '1' => '11'
  true + true => 2
  4 + [1,2,3] =>'41,2,3'
  ```

- 除了加法以外，只要其中一方是数字，另一方也转成数字。
