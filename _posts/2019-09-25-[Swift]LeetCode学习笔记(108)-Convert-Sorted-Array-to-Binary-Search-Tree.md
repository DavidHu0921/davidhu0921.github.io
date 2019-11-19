---
layout: post
title:  "LeetCode学习笔记(108) Convert Sorted Array to Binary Search Tree"
date:   2019-09-25 08:00:00 +0800
categories: 算法
---

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

### Example:

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

### 解法一

```swift
class Solution {
    func sortedArrayToBST(_ nums: [Int]) -> TreeNode? {
        if nums.count == 0 {
            return nil
        }

        var array = nums
        return bst(&array, 0, array.count - 1)
    }

    func bst(_ nums:inout [Int], _ left: Int, _ right: Int) -> TreeNode? {
        if left > right {
            return nil
        }

        let mid = left + (right - left)/2
        let node:TreeNode = TreeNode.init(nums[mid])
        node.left = bst(&nums, left, mid-1)
        node.right = bst(&nums, mid+1, right)
        return node
    }
}
```

### 思路简述

这题要求将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。每个节点的左右两个子树的高度差的绝对值不超过 1。

那么就很简单，用递归、二分法就可以解题

