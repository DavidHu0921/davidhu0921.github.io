---
layout: post
title:  "LeetCode学习笔记(107) Binary Tree Level Order Traversal II"
date:   2019-09-24 08:00:00 +0800
categories: 算法
---

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7]` ,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:

```
[
  [15,7],
  [9,20],
  [3]
]
```

### 解法一

```swift
func levelOrderBottom(_ root: TreeNode?) -> [[Int]] {
    guard let root = root else { return [[Int]]() }
    var ans = [[Int]]()
    var queue = [root]
    while !queue.isEmpty {
        var sub = [Int]()
        let count = queue.count
        for i in 0..<count {
            let curr = queue.removeFirst()
            sub.append(curr.val)
            if let left = curr.left {
                queue.append(left)
            }
            if let right = curr.right {
                queue.append(right)
            }
        }
        ans.insert(sub, at: 0)
    }
    return ans
}
```


### 思路简述

这题就是把二叉树的每一层，同层放在一个数组里，很简单，一个广度优先遍历BFS 解决问题。