---
layout: “leetcode算法题
title: 算法：257、二叉树的所有路径（Javascript）
date: 2019-03-27 09:49:48
tags: 算法
category: 算法
---

<meta name="referrer" content="no-referrer"/>

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

```
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

<!--more-->

#### 解题思路：

使用递归思路解决这个问题，对于根节点，如果根节点为空，则返回数组[]，如果为叶子结点，则返回包含此节点的值的数组（这个数组只有一个元素）。如果既不为空也不是叶子结点，则对左右子树递归调用，将两个结果数组拼接起来，最后使用 map 函数来对数组的每个元素进行字符串的操作。

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
 * @return {string[]}
 */
var binaryTreePaths = function(root) {
    if(root === null){
        return []
    }
    if(root.left ===null && root.right===null){
        return [root.val.toString()]
    }
    let left=binaryTreePaths(root.left),
        right=binaryTreePaths(root.right);
    return left.concat(right).map(x=>root.val+'->'+x)
};
```
