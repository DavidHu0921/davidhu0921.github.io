---
layout: post
title:  "LeetCode学习笔记(7) Reverse Integer"
date:   2018-02-28 09:00:00 +0800
categories: 算法
---

Given a 32-bit signed integer, reverse digits of an integer.

###Example 1:

```
Input: 123
Output:  321
```

###Example 2:

```
Input: -123
Output: -321
```

###Example 3:

```
Input: 120
Output: 21
```

###Note:
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

Swift 解法：

```swift
class Solution {
    func reverse(_ x: Int) -> Int {
        var i: Int = 0
        var y: Int = x
        while y != 0 {
            let temp: Int = i * 10 + y % 10
            if temp / 10 != i {
                return 0
            }
            i = temp
            y /= 10
        }
        if abs(i) > 2147483647 {
            return 0
        }
        return i
    }
}
```

思路简述：

//TODO
