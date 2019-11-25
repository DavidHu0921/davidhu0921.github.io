---
layout: post
title:  "[Swift]LeetCode学习笔记(226) Invert Binary Tree "
date:   2019-11-25 23:40:00 +0800
categories: 算法
---

Invert a binary tree.

### Example:

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

### Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

### Trivia:

This problem was inspired by this original tweet by Max Howell:

> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.

### 解法一

```swift
class Solution {
    func invertTree(_ root: TreeNode?) -> TreeNode? {
        if root == nil {
            return nil
        }
        
        let temp = root!.left
        root!.left = root!.right
        root!.right = temp
        
        invertTree(root?.left)
        invertTree(root?.right)
        
        return root
    }
}
```

### 思路简述

据说做对了可以进Google;-)
