---
layout: post
title:  "LeetCode学习笔记(110) Balanced Binary Tree"
date:   2019-09-16 09:00:00 +0800
categories: 算法
---

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

### Example 1:

Given the following tree [3,9,20,null,null,15,7]:

```
    3
   / \
  9  20
    /  \
   15   7
```

Return true.

### Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

Return false.

### 解法一：

```swift
class Solution {
    func isBalanced(_ root: TreeNode?) -> Bool {
        guard let root = root else {
            return true
        }
        return dfs(root) != -1
    }

    func dfs(_ root: TreeNode?) -> Int {
        guard let root = root else {
            return 0
        }

        let l = dfs(root.left)
        if l == -1 {
            return -1
        }

        let r = dfs(root.right)
        if r == -1 {
            return -1
        }

        if abs(l - r) < 2 {
            return max(l, r) + 1
        } else {
            return -1
        }
    }
}
```

思路简述：
显然，最容易想到的就是暴力式自顶向下搜一遍，这样的话，最差情况要有O(n^2)的时间复杂度，也就是要全部遍历一边，所以这种情况就很糟糕，就不贴代码了，大家。

那么比较优雅的一种解法就是，从下往上找，当深度差超过2 的时候，就提前终止，因为这个时候已经不满足条件，不是平衡二叉树了，所以这样的情况类似“剪枝”的概念，会省下很多时间。这种情况下，最差最差就是O(n) 的时间复杂度，全遍历一次





