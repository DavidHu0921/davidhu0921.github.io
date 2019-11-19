---
layout: post
title:  "LeetCode学习笔记(168) Excel Sheet Column Title"
date:   2019-11-01 00:02:00 +0800
categories: 算法
---

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

### For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```

### Example 1:

```
Input: 1
Output: "A"
```

### Example 2:

```
Input: 28
Output: "AB"
```

### Example 3:

```
Input: 701
Output: "ZY"
```

### 解法一

```swift
class Solution {
    func convertToTitle(_ n: Int) -> String {
        var n = n
        var output = ""

        while n > 0 {
            let u = Unicode.Scalar(((n-1)%26) + 65)
            output = String(Character(u!)) + output
            n = (n-1)/26
        }

        return output 
    }
}
```

### 思路简述

这题很简单，就是不断用26 取余，然后直接用ASC-II 码转换值
可能比较懵的地方在于如何把数字转成字符串，swift 中尤其复杂，特别是还要把 `Character` 转换成 `String` 

给一小段代码，把数字转换成String

```swift
let value = 65
let u = Unicode.Scalar(value)
let str = String(Character(u!))
print(str) // A
```

