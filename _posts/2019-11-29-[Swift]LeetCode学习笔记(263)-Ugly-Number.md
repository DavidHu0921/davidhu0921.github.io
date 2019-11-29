---
layout: post
title:  "[Swift]LeetCode学习笔记(263) Ugly Number"
date:   2019-11-29 20:30:00 +0800
categories: 算法
---

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include `2, 3, 5`.

### Example 1:

```
Input: 6
Output: true
Explanation: 6 = 2 × 3
```

### Example 2:

```
Input: 8
Output: true
Explanation: 8 = 2 × 2 × 2
```

### Example 3:

```
Input: 14
Output: false 
Explanation: 14 is not ugly since it includes another prime factor 7.
```

### Note:

1. 1 is typically treated as an ugly number.
2. Input is within the 32-bit signed integer range: [−231,  231 − 1].

### 解法一

```swift
class Solution {
    func isUgly(_ num: Int) -> Bool {
        if num < 1 {
            return false
        }
        if num == 1 {
            return true
        }
        var n = num
        while n != 1 {
            let temp = n
            if n % 2 == 0 {
                n = n / 2
            }
            if n % 3 == 0 {
                n = n / 3
            }
            if n % 5 == 0 {
                n = n / 5
            }
            if temp == n {
                return false
            }
        }
        return true
    }
}
```

### 思路简述
题目说明当一个数不能被`2,3,5`整除的时候，就是个丑数。解法比较单一直接，效率也还行，不知道还有没有更好的优化。
