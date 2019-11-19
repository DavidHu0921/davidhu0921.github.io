---
layout: post
title:  "[Swift]LeetCode学习笔记(172) Factorial Trailing Zeroes"
date:   2019-11-02 00:00:00 +0800
categories: 算法
---

Given an integer n, return the number of trailing zeroes in n!.

### Example 1:

```
Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

### Example 2:

```
Input: 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```

Note: Your solution should be in logarithmic time complexity.

### 解法一

```swift
class Solution {
    func trailingZeroes(_ n: Int) -> Int {
        var n = n
        var num = 0
        while n > 0 {
            num += n/5
            n = n/5
        }
        return num
    }
}
```

### 思路简述

这题求的是末尾有几个0，经过数学分析可以得，主要是看有几个10 作为因子，最后乘完末尾就会有几个0. 进一步说，因为 `10=2*5`，而2 在阶乘里远比5多，多的用不完，所以也就转换成了含有几个有5 的因子，同时5 是质数，很好算，直接用数学求解就可以了。

