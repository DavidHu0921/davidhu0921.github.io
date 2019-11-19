---
layout: post
title:  "LeetCode学习笔记(202) Happy Number"
date:   2019-11-11 00:10:00 +0800
categories: 算法
---

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

### Example: 

```
Input: 19
Output: true
Explanation: 
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

### 解法一

```swift
class Solution {
    func isHappy(_ n: Int) -> Bool {
        var si = Set<Int>(), i = n
        while !si.contains(i) && i != 1 {
            si.insert(i)
            i = String(i).reduce(0, {let j = Int(String($1))!; return $0 + j*j })
        }
        
        return i == 1
    }
}
```

### 思路简述

就是说一个数，不断把每一位平方，然后相加，直到最后等于1，这样的数就是“快乐数”，没想到什么牛b 的解法，暂时按意思做，效率很低，后面再优化



