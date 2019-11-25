---
layout: post
title:  "[Swift]LeetCode学习笔记(231) Power of Two"
date:   2019-11-25 23:55:00 +0800
categories: 算法
---

Given an integer, write a function to determine if it is a power of two.

### Example 1:

```
Input: 1
Output: true 
Explanation: 2^0 = 1
```

### Example 2:

```
Input: 16
Output: true
Explanation: 2^4 = 16
```

### Example 3:

```
Input: 218
Output: false
```

### 解法一

```swift
class Solution {
    func isPowerOfTwo(_ n: Int) -> Bool {
        guard n !=  1 else {return true}
        guard n > 0 else  {return false}
        var n  = n
        while  n % 2 == 0 {
            if n == 2 {
                return true
            } 
            n /= 2 
            if n < 2 {
                return false
            }
        }
        return false
    }
}
```

### 思路简述

这题是说给一个整数n，判定他是不是2的幂数，就用了一个暴力解法，效率并不高。还有一些比较极端的一行数学解法，看不太懂，后续再优化。



