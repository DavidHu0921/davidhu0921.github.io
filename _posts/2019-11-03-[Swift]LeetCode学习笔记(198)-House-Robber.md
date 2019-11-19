---
layout: post
title:  "[Swift]LeetCode学习笔记(198) House Robber"
date:   2019-11-03 23:00:00 +0800
categories: 算法
---

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### Example 1:

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

### Example 2:

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

### 解法一

```swift
class Solution {
    func rob(_ nums: [Int]) -> Int {
        if nums.count == 0 {
            return 0
        }
        if nums.count == 1 {
            return nums[0]
        }
        var preMax = 0
        var curMax = 0
        for i in nums {
            let temp = curMax
            curMax = max(preMax+i, curMax)
            preMax = temp
        }
        return curMax
    }
}
```

### 思路简述

这题真的easy 吗？看起来挺难的大概意思是，打劫，但是不能连续打劫相邻的，如何利润最大化。

思来想去，还是一个动态规划的问题。在n 的时候，比较n-1 和 （n-2）+n 时候的值，哪个大，所以解题如上。记住要加前面两个判定，swift 可以4ms 跑完。不加的话 8ms 差的非常多。


