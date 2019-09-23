---
layout: post
title:  "LeetCode学习笔记(46) Permutations"
date:   2019-09-23 08:00:00 +0800
categories: 算法
---

Given a collection of distinct integers, return all possible permutations.

Example:

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 解法一

```swift
func permute(_ nums: [Int]) -> [[Int]] {
    var result = [[Int]]()
    var nums = nums
    recurse(0, &nums, &result)
    return result
}

func recurse(_ first: Int, _ nums: inout [Int], _ result: inout [[Int]]) {
    if first == nums.count {
        result.append(nums)
        return
    }
    for index in first..<nums.count {
        nums.swapAt(first, index)
        self.recurse(first+1, &nums, &result)
        nums.swapAt(first, index)
    }
}
```

### 思路简述

这题很简单，就是列出几个数字可能的、不重复的排列，就递归dfs 好了，按次序交换位置输出。用swift 写很舒服
