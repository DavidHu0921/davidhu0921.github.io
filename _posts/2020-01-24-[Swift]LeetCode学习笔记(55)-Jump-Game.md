---
layout: post
title:  "[Swift]LeetCode学习笔记(55) Jump Game"
date:   2020-01-24 23:00:00 +0800
categories: 算法
---

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

### Example 1:

```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

### Example 2:

```
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```

### 解法一

```swift
class Solution {
    func canJump(_ nums: [Int]) -> Bool {
        if nums.count == 0 {
            return false
        }
        var lastPos = nums.count - 1
        for i in stride(from: (nums.count - 1), through: 0, by: -1) {
            print(i)
            if (i + nums[i]) >= lastPos {
                lastPos = i
            }
        }
        return lastPos == 0
    }
}
```

### 思路简述

[详细分析](https://leetcode-cn.com/problems/jump-game/solution/tiao-yue-you-xi-by-leetcode/)

这题是一题设置的非常巧妙的动态规划问题，最简单的做法当然是从头开始，递归、穷举到最后一位。但是这样的话，最差情况就是从头到尾来一遍，显然会超时。

好一点的做法是自顶向下或者自底向上，都是在某一位得到true 的时候做一个“剪枝”的事情，减少复杂度。

最好的当然还是“贪心法”，从右向左，我们只需要找到第一个标记为 GOOD 的坐标（由跳出循环的条件可得），也就是说找到最左边的那个坐标。如果我们用一个单独的变量来记录最左边的 GOOD 位置，我们就可以避免搜索整个数组。

