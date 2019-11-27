---
layout: post
title:  "[Swift]LeetCode学习笔记(257) Binary Tree Paths"
date:   2019-11-27 23:10:00 +0800
categories: 算法
---

Given a binary tree, return all root-to-leaf paths.

*Note*: A leaf is a node with no children.

### Example:

```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

### 解法一

```swift
class Solution {
    func binaryTreePaths(_ root: TreeNode?) -> [String] {
        var paths = [String]()
        var p = ""
        buildPaths(root, &p, &paths)
        return paths
    }
    
    func buildPaths(_ node: TreeNode?, _ path: inout String, _ paths: inout [String]) {
        guard let node = node else { return }
        var p = path + String(node.val)
        
        if (node.left == nil) && (node.right == nil) {
            paths.append(p)
        } else {
            p = p + "->"
            buildPaths(node.left, &p, &paths)
            buildPaths(node.right, &p, &paths)
        }
    }
}
```

### 思路简述

典型的一个递归，把文字加上去，还不够快，还能更精简后续优化，不难懂，随便看看就能理解的

