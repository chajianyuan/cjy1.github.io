---
title: JS：数组去重
date: 2019-10-16 21:00:46
tags: javascript
category: 技术
---

<meta name="referrer" content="no-referrer"/>

### 1、ES6 中 Set 去重

set 中成员的值都是唯一的，没有重复的值，set 内部会判断两个值是否不同

<!--more-->

`Array.from(new Set(arr))`

```
let arr = [4,1,2,3,4,2,3]
Array.from(new Set(arr))  =>  [4, 1, 2, 3]
```

### 2、利用 for 嵌套 for，然后用 splice 去重

```
let arr = [4,1,2,3,4,2,3]
function fun(arr){
  for(let i = 0; i < arr.length; i++){
    for(let j = i + 1; j < arr.length; j++){
      if(arr[i] == arr[j]){
        arr.splice(j, 1);
        j--;
      }
    }
  }
  return arr;  =>  [4, 1, 2, 3]
}
```

### 3、利用 indexOf 去重

```
let arr = [4,1,2,3,4,2,3]
function fun(arr){
 let array = []
  for(let i = 0; i <arr.length; i++){
    if(array.indexOf(arr[i]) == -1){
    	array.push(arr[i])
    }
  }
  return array;  => [4, 1, 2, 3]
}
```

### 4、sort()

利用 sort()排序方法，然后根据排序后的结果进行 遍历及相邻元素比对

```
let arr = [4,1,2,3,4,2,3]
function fun(arr){
 arr = arr.sort();
 let array = [arr[0]];
 for(let i = 1; i < arr.length; i++){
   if(arr[i] != arr[i-1]){
     array.push(arr[i])
   }
 }
 return array;  =>  [1, 2, 3, 4]
}
```

### 5、includes

```
let arr = [4,1,2,3,4,2,3];
function fun(arr){
  let array = [];
  for(let i = 0; i < arr.length; i++){
     if(!array.includes(arr[i])){
       array.push(arr[i])
     }
  }
  return array;  =>  [4, 1, 2, 3]
}
```

### 6、hasOwnProperty

利用 hasOwnProperty 判断是否存在对象属性

```
let arr = [4,1,2,3,4,2,3];
function fun(arr){
  let obj = {}
  return arr.filter((item, index, arr)=>{
    return obj.hasOwnProperty(typeof item + item) ? false : (obj[typeof item + item] = true)
  })  =>  [4, 1, 2, 3]
}
```

### 7、filter

```
let arr = [4,1,2,3,4,2,3];
function fun(arr){
  return arr.filter((item, index, arr)=>{
    return arr.indexOf(item, 0) === index
  })  =>  [4, 1, 2, 3]
}
```

### 8、Map

```
let arr = [4,1,2,3,4,2,3];
function fun(arr){
  let map = new Map();
  let array = []
  for(let i of arr){
    if(!map[i]){
      map[i] = i;
      array.push(i)
    }
  }
  return array;  =>  [4, 1, 2, 3]
}
```

### 9、[...new Set(arr)]

```
let arr = [4,1,2,3,4,2,3];
arr = [...new Set(arr)]  =>  [4, 1, 2, 3]
```
