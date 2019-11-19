---
layout: post
title:  "[Swift]LeetCode学习笔记(112) Path Sum"
date:   2019-10-29 09:00:00 +0800
categories: 算法
---

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

Example:

```
Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

### 解法一

```swift
class Solution {
    func hasPathSum(_ root: TreeNode?, _ sum: Int) -> Bool {
        guard let root = root else { return false }
        let newSum = sum - root.val
        if root.left == nil && root.right == nil {
            return newSum == 0
        }
        return hasPathSum(root.left, newSum) || hasPathSum(root.right, newSum)
    }
}
```


### 思路简述

总的来说，递归的看，这个树中，有没有一个“链路”上的数的和等于目标数字，递归就好了，每次递归的时候剪去当前节点的值