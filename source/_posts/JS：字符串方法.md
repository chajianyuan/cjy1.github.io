---
title: JS：字符串方法
date: 2020-11-11 15:59:47
tags: javascript
category: 技术
---

```
let str = 'My name is Lily';
```
### 一、提取字符串方法

#### 1. charAt()

`charAt` 获取字符串的某个字符。

<!--more-->

```
str.charAt(3)  // "n"
```

还有一种方式是把字符串当成一个类似数组的对象，对其中的每个字符进行索引。

```
str[3]  // "n"
```

#### 2. charCodeAt()

`charCodeAt()`方法返回0到65535之间的整数，表示给定索引处的UTF-16代码单元。

**返回值：** 指定index处字符的UTF-16代码单元值的一个数字；如果index超出范围，`charCodeAt()`返回NaN。

```
str.charCodeAt(3)  // 110
```
### 二、提取部分字符串

#### 3. slice

`slice()`提取字符串的某个部分并在新字符串中返回被提取的部分

该方法设置两个参数：起始索引和终止索引

如果某个参数为负数，则从字符串的结尾开始计数

如果省略第二个参数，则裁剪字符串的剩余部分

#### 4. subString

`subString()`类似于`slice()`

不同之处在于`subString()`不支持参数为负数

#### 5. subStr

`subStr()`类似于`slice()`

不同之处在于`subStr`第二个参数规定被提取部分的长度

如果第一个参数为负数，则从字符串的末尾开始计算

### 三、替换字符串内容

#### 6. replace

`replace()`方法用一个值替换在字符串中指定的值

`replace()`方法不会改变调用它的字符串，返回一个新字符串

`replace()`默认只替换首个匹配

`replace()`对大小写敏感

如需执行大小写不敏感的替换，则使用正则表达式`/i`

```
str = "Please visit Microsoft!";
var n = str.replace(/MICROSOFT/i, "W3School");
```

如需替换所有匹配，则使用正则表达式的`g`

```
str = "Please visit Microsoft and Microsoft!";
var n = str.replace(/Microsoft/g, "W3School");
```
### 四、转换为大写和小写

#### 7. toUpperCase

`toUpperCase()`把字符串转换为大写

#### 8. toLowerCase

`toLowerCase()`把字符串转换为小写

### 五、字符串转数组

#### 9.split

### 六、查找字符串中的字符串

#### 10. indexOf()

`indexOf()` 方法返回调用它的String对象中第一次出现的指定值的索引，从fromIndex开始查找，如果没有找到该值，返回-1。

**参数：**

* searchValue：要被查找的字符串值，如果`searchValue`是空字符串，则返回`fromIndex`
* fromIndex：要开始查找的位置（数字），默认值是0

```
str.indexOf('a')  // 4
```

#### 11. lastIndexOf()

`lastIndexOf()`方法返回调用它的String对象中的指定值最后一次出校的索引，在一个字符串中的指定位置处从后向前搜索，如果没有找到则返回-1。

**参数：**

* searchValue：要被查找的字符串值，如果`searchValue`是空字符串，则返回`fromIndex`
* fromIndex：要开始查找的位置（数字），默认值是`+Infinity`，如果`fromIndex >= str.length`，则会搜索整个字符串；如果`fromIndex < 0`，则等同于`fromIndex == 0`

```
str.lastIndexOf('a')  // 4
```

#### 12. search

`search()`方法搜索特定值的字符串，并返回匹配的位置

⚠️ 注意：indexOf()和search()方法的区别在于

* search()方法无法设置第二个参数
* indexOf()方法无法设置更强大的搜索值（正则表达式）

### 七、其他

#### 13. includes()

`includes()` 方法用于判断一个字符串是否包含在另一个字符串中，根绝结果返回true或false。

**返回值：** true或false

```
str.includes('abc')  // false
```
#### 14. concat()

`concat()`方法将一个或多个字符串与原字符串链接合并，形成一个新的字符串并返回。

**返回值：** 一个新的字符串

**不会改变原字符串**

**性能：** 强烈建议使用赋值操作符（+， +=）代替concat方法。

```
str.concat(', too')  // "My name is Lily, too"
"".concat({})        // "[object Object]"
"".concat([])        // ""
"".concat(null)      // "null"
"".concat(4, 5)      // "45"
```

#### 15. String.fromCharCode()

`String.fromCharCode()`方法返回由指定的UTF-16代码单元序列创建的字符串。

**返回值：** 一个长度为N的字符串，由N个指定的UTF-16代码单元组成。

```
String.fromCharCode(189, 43, 190, 61)  // "½+¾="
```
#### 16. String.fromCodePoint()

`String.fromCodePoint()`静态方法返回使用指定的代码点序列创建的字符串。

**返回值：** 使用指定的Unicode 编码位置创建的字符串。

```
String.fromCodePoint(189, 43, 190, 61)  // "½+¾="
```

#### 17. codePointAt()

`codePointAt()`方法返回一个Unicode编码点值的非负整数。

**返回值：** 在字符串中的给定索引的编码单元体现的数字，如果在索引处没有找到该元素则返回`undefined`。

```
str.codePointAt(3)  // 110
```

#### 18. endsWith()

`endsWith()`方法用来判断当前字符串是否是以另外一个给定的子字符串结尾的，根据结果返回true或false。

**参数：**

* 第一个参数：当前字符串
* 第二个参数：字符串的长度，默认是当前字符串的长度

**返回值：** true或false

```
str.endsWith('ly')  // true
```


#### 19. localeCompare()

`localeCompare()`方法返回一个数字来指示一个参考字符串是否在排序顺序前面或之后与给定字符串相同。

**返回值：** 如果引用字符存在于比较字符之前为`负数`；如果引用字符存在于比较字符之后则为`正数`；相等的时候返回0。

#### 20. match()

`match()`方法检索返回一个字符串匹配的正则表达式的结果。

**参数：** 一个正则表达式对象，如果传入一个非正则表达式对象，则会隐式地使用`new RegExp(obj)`将其转换成一个`RegExp`；如果没有给出任何参数直接使用match()方法，则会得到一个包含空字符串的Array: [""]。

**返回值：** 
* 如果使用g标识，则将返回与完整正则表达式匹配的所有结果，但不会返回捕获组。
* 如果未使用g标志，则返回第一个完整匹配及其相关的捕获组（Array）。

#### 21. matchAll()

` matchAll()`方法返回一个包含所有匹配正则表达式的结果及分组捕获数组的迭代器。

**参数：** 正则表达式对象，注意：正则表达式必须是设置了全局模式的g的形式，否则会抛出异常。

**返回值：** 一个迭代器（迭代器是符合迭代器协议的一个对象）。

#### 22. normalize()

`normalize()`会按照指定的一种Unicode正规形式将当前字符串正规化。（如果该值不是字符串，则首先将其转换为一个字符串）

#### 23. length

`length`属性返回字符串的长度

#### 24. trim

`trim()`删除字符串两端的空白符

#### 25. 属性访问

```
let str = 'school';
str[0]
```



