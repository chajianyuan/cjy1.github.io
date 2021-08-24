---
title: 算法：6、Z字形变换（JavaScript）
date: 2019-03-29 08:56:25
tags: 算法
category: 算法
---

<meta name="referrer" content="no-referrer"/>

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 `"LEETCODEISHIRING"` 行数为 3 时，排列如下：

```
L   C   I   R
E T O E S I I G
E   D   H   N

```

<!--more-->

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"LCIRETOESIIGEDHN"`。

请你实现这个将字符串进行指定行数变换的函数：

```
string convert(string s, int numRows);
```

**示例 1:**

```
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"

```

**示例 2:**

```
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

L     D     R
E   O E   I I
E C   I H   N
T     S     G
```

**解题思路**

1、字符串从上到下排列，到第 numRows 行再向上排，可以看做一个圈，每个圈的元素个数是 numRows\*2-2 个

2、输出的字符串中按行来，从左到右，第一行和最后一行中每一圈只取一个，中间的取两个

**代码**

```
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    var len=s.length;
    var twoRows=2*numRows-2;
    var str=""
    if(len==0 || numRows<=1){
        return s
    }
    for(var i=0;i<numRows;i++){
        for(var j=i;j<len;j+=twoRows){
            str=str.concat(s.charAt(j));
            if(i!=0 && i!=numRows-1 && j-2*i+twoRows<len){
                str=str.concat(s.charAt(j-2*i+twoRows))
            }
        }
    }
    return str
};
```
