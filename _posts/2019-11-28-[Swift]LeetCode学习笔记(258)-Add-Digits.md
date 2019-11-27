---
layout: post
title:  "[Swift]LeetCode学习笔记(258) Add Digits"
date:   2019-11-28 01:10:00 +0800
categories: 算法
---

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

### Example:

```
Input: 38
Output: 2 
Explanation: The process is like: 3 + 8 = 11, 1 + 1 = 2.
             Since 2 has only one digit, return it.
```

### Follow up:
> Could you do it without any loop/recursion in O(1) runtime?

### 解法一

```swift
class Solution {
    func addDigits(_ num: Int) -> Int {
        var sum:Int = 0
        var n = num
        while n != 0 {
            sum = sum + n % 10
            n = n / 10
        }
        
        while sum > 9 {
            return addDigits(sum)
        }
        return sum
    }
}
```

### 思路简述

就很简单，照着题目的意思就写了，递归一下就好了


