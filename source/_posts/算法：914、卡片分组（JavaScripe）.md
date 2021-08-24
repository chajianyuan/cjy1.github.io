---
title: 算法：914、卡片分组（JavaScripe）
date: 2019-03-29 09:53:18
tags: 算法
category: 算法
---

<meta name="referrer" content="no-referrer"/>

给定一副牌，每张牌上都写着一个整数。

此时，你需要选定一个数字 `X`，使我们可以将整副牌按下述规则分成 1 组或更多组：

- 每组都有 `X` 张牌。
- 组内所有的牌上都写着相同的整数。

<!--more-->

仅当你可选的 `X >= 2` 时返回 `true`。

**示例 1：**

```
输入：[1,2,3,4,4,3,2,1]
输出：true
解释：可行的分组是 [1,1]，[2,2]，[3,3]，[4,4]

```

**示例 2：**

```
输入：[1,1,1,2,2,2,3,3]
输出：false
解释：没有满足要求的分组。

```

**示例 3：**

```
输入：[1]
输出：false
解释：没有满足要求的分组。

```

**示例 4：**

```
输入：[1,1]
输出：true
解释：可行的分组是 [1,1]

```

**示例 5：**

```
输入：[1,1,2,2,2,2]
输出：true
解释：可行的分组是 [1,1]，[2,2]，[2,2]

```

**提示：**

1. `1 <= deck.length <= 10000`
2. `0 <= deck[i] < 10000`

**解题思路**

找一个集体公约数，收集每张牌的数量存入新数组 arr，公约数 x 从 2 往上累加，最大不超过 min(arr)，判断 arr[i]能否被 x 整除

```
/**
 * @param {number[]} deck
 * @return {boolean}
 */
var hasGroupsSizeX = function(deck) {
   var obj={},max,min,arr=[],n=0;
    if(deck.length<2){
        return false
    }
    for(var i=0;i<deck.length;i++){
        if(obj[deck[i]]>0){
            obj[deck[i]]+=1;
        }else{
            obj[deck[i]]=1
        }
    }
    for (i in obj){
        arr[n]=obj[i]
        n++
    }
    min=Math.min.apply(null,arr)
    max=Math.max.apply(null,arr)
    if((min===1 && min !=max) || deck.length<2){
        return false
    }
    var x=2,status
    while(min>=x){
        status=0;
        for(var i=0;i<arr.length;i++){
            if(arr[i]%x!=0)
                status=1
        }
        if(status==0)
            return true
        x++
    }
    return false
};
```
