---
layout: post
title:  "[Swift]LeetCode学习笔记(50) Pow(x, n)"
date:   2020-01-23 23:00:00 +0800
categories: 算法
---

Implement pow(x, n), which calculates x raised to the power n (x^n).

### Example 1:

```
Input: 2.00000, 10
Output: 1024.00000
```

### Example 2:

```
Input: 2.10000, 3
Output: 9.26100
```

### Example 3:

```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2^-2 = (1/2)^2 = 1/4 = 0.25
```

### Note:

```
-100.0 < x < 100.0
n is a 32-bit signed integer, within the range [−2^31, 2^31 − 1]
```

### 解法一

```swift
class Solution {
    func myPow(_ x: Double, _ n: Int) -> Double {
        var N:CLongLong = CLongLong(n)
        var X = x
        if N < 0 {
            X = 1/x
            N = -N
        }
        return fastPow(X, N)
    }
    func fastPow(_ x: Double, _ n: CLongLong) -> Double {
        if n == 0 {
            return 1.0
        }
        let half: Double = fastPow(x, n/2)
        if n % 2 == 0 {
            return half * half
        } else {
            return half * half * x
        }
    }
}
```

### 思路简述

* 时间复杂度：O(log⁡n). 每一次我们使用公式 (x^n)^2=x^(2∗n)，n 都变为原来的一半。因此我们需要至多O(log⁡n) 次操作来得到结果。

* 空间复杂度：O(logn). 每一次计算，我们需要存储 x(n/2) 的结果。我们需要计算O(logn) 次，所以空间复杂度为 O(log⁡n)。

