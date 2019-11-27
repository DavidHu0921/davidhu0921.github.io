---
layout: post
title:  "[Swift]LeetCode学习笔记(242) Valid Anagram"
date:   2019-11-27 23:10:00 +0800
categories: 算法
---

Given two strings s and t , write a function to determine if t is an anagram of s.

### Example 1:

```
Input: s = "anagram", t = "nagaram"
Output: true
```

### Example 2:

```
Input: s = "rat", t = "car"
Output: false
```

### Note:

> You may assume the string contains only lowercase alphabets.

### Follow up:

> What if the inputs contain unicode characters? How would you adapt your solution to such case?

### 解法一

```swift
class Solution {
    func isAnagram(_ s: String, _ t: String) -> Bool {
        if s.count != t.count {
            return false
        }
        return s.sorted() == t.sorted()
    }
}
```

### 思路简述

先排序再比较，是一个比较慢的方法，更快的应该是用哈希表存一下然后比，后续再优化

