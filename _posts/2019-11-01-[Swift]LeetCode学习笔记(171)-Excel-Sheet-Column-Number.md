---
layout: post
title:  "[Swift]LeetCode学习笔记(171) Excel Sheet Column Number"
date:   2019-11-01 23:30:00 +0800
categories: 算法
---

Given a column title as appear in an Excel sheet, return its corresponding column number.

### For example:

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```

### Example 1:

```
Input: "A"
Output: 1
```

### Example 2:

```
Input: "AB"
Output: 28
```

### Example 3:

```
Input: "ZY"
Output: 701
```

### 解法一

```swift
class Solution {
    func titleToNumber(_ s: String) -> Int {
        if s.count == 0 {
            return 0
        }

        var result = 0
        for char in s {
            result = Int(char.asciiValue! - 64) + (26 * result)
        }
        return result
    }
}
```

### 思路简述

这题就是168 的逆向版本，非常简单，把字母拆开用ASC-II 值乘回去就好了


