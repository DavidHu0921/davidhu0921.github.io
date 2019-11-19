---
layout: post
title:  "[Swift]LeetCode学习笔记(204) Count Primes"
date:   2019-11-18 22:10:00 +0800
categories: 算法
---

Count the number of prime numbers less than a non-negative number, n.

### Example:

```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

### 解法一

```swift
class Solution {
    func countPrimes(_ n: Int) -> Int {
        guard n >= 2 else { return 0 }
        
        var arr = Array(repeating: true, count: n)
        arr[0] = false
        arr[1] = false
        var count = 0
        
        for i in 2..<n {
            guard arr[i] == true else { continue }
            count += 1
            
            var j = i * i
            while j < n {
                arr[j] = false // mark any multiple of i to false
                j += i
            }
        }
        
        return count
    }
}
```

### 思路简述

这题主要是说给定一个数n，输出n 以内的素数个数。主要是用到了 [埃拉托斯特尼筛法](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) 这题是一个swift 版本的实现
