---
layout: post
title:  "LeetCode学习笔记(205) Isomorphic Strings"
date:   2019-11-18 23:10:00 +0800
categories: 算法
---

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

### Example 1:

```
Input: s = "egg", t = "add"
Output: true
```

### Example 2:

```
Input: s = "foo", t = "bar"
Output: false
```

### Example 3:

```
Input: s = "paper", t = "title"
Output: true
```

*Note:*

> You may assume both s and t have the same length.

### 解法一

```swift
class Solution {
    func isIsomorphic(_ s: String, _ t: String) -> Bool {
        if s.count != t.count { return false }
        
        var dic = [Character:Character]()
        let ss : [Character] = Array(s)
        let tt : [Character] = Array(t)
        
        for i in 0..<s.count {
            if let check = dic[ss[i]] {
                if check != tt[i] {
                    return false
                }
            } else {
                if dic.values.contains(tt[i]) { return false }
                dic[ss[i]] = tt[i]
            }
        }
        return true
    }
}
```

### 思路简述

这题就是求一个同构字符串，说人话就是两个字符都要是abb 类似这样的形式，这里面有一个坑就是要注意正反比较，因此顺序比较的时候还要存一个字典，来反过来把t 的和s 同位字符比较。

然后还有一个坑，就是swift 语法的坑，如果用常规的 `let index = s.index(s.startIndex, offsetBy: i)` 来先获取index 再获取char，那么就会超时，我猜是语言的优化问题，如果先转换成array 就没有问题，这里太坑了，搞了好久，因为算法上肯定是没有问题了，但是一到超长字符就出问题，很🌶️🐔

