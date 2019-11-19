---
layout: post
title:  "LeetCode学习笔记(111) Minimum Depth of Binary Tree"
date:   2019-10-29 08:00:00 +0800
categories: 算法
---

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.

Example:

```
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
```

return its minimum depth = 2.


### 解法一

```swift
class Solution {
    func minDepth(_ root: TreeNode?) -> Int {
        guard let root = root else { return 0 }
    
        if root.left == nil && root.right == nil {
            return 1
        }

        var depth:Int = Int.max
        if root.left == nil {
            depth = min(depth, minDepth(root.right))
        } else if root.right == nil {
            depth = min(depth, minDepth(root.left))
        } else {
            depth = min(minDepth(root.left), minDepth(root.right))
        }

        return depth + 1
    }
}
```

### 思路简述

这题就二叉树最小深度，递归取较小值就好