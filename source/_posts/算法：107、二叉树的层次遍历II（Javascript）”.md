---
layout: “leetcode算法题
title: 算法：107、二叉树的层次遍历II（Javascript）
date: 2019-03-27 08:51:13
tags: 算法
category: 算法
---

<meta name="referrer" content="no-referrer"/>

题目：给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）
例如：
给定二叉树 [3,9,20,null,null,15,7]

        3
       / \
      9  20
        /  \
       15   7

返回其自底向上的层次遍历为：

```
[
  [15,7],
  [9,20],
  [3]
]
```

<!--more-->

#### 解题思路：

二叉树的层序遍历要用到迭代法，设置一个队列 queue(其实就是一个数组)，把根节点放入 queue 中，当队列不为空时，取出队列元素，然后把这个元素的子节点以数组的形式加入到队列中

```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrderBottom = function(root) {
    let queue=[]; //定义一个队列
    let result=[]; //定义结果
    if(root!==null){
        queue.push(root)
    }
    while(queue.length!==0){
        let len=queue.length;
        let level=[]; //定义叶节点
        for(let i=0;i<len;i++){
            let currentNode=queue.shift(); //设置currentNode为queue中的第一个元素，并将queue中的第一个元素删除
            level.push(currentNode.val);
            if(currentNode.left!==null){
                queue.push(currentNode.left)
            }
            if(currentNode.right!==null){
                queue.push(currentNode.right)
            }
        }
        result.push(level)
    }
    return result.reverse()
};
```
