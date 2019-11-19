---
layout: post
title:  "[Swift]LeetCode学习笔记(415) Add Strings"
date:   2019-10-16 08:00:00 +0800
categories: 算法
---

Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

#### Note:

```
1. The length of both num1 and num2 is < 5100.
2. Both num1 and num2 contains only digits 0-9.
3. Both num1 and num2 does not contain any leading zero.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.
```

### 解法一

```swift
func addStrings(_ num1: String, _ num2: String) -> String {
    var result = [Character]()
    var carry:UInt8 = 0

    var long, short: [Character]

    if num1.count >= num2.count {
        long = num1.reversed()
        short = num2.reversed()
    } else {
        long = num2.reversed()
        short = num1.reversed()
    }

    for index in 0..<long.count {
        let a = long[index].asciiValue! - 48
        var plus: UInt8 = 0

        if index >= short.count {
            plus = (a + carry) % 10 + 48
            carry = (a + carry) / 10
        } else {
            let b = short[index].asciiValue! - 48
            plus = (a + b + carry) % 10 + 48
            carry = (a + b + carry) / 10
        }
        let char = Character.init(Unicode.Scalar.init(plus))
        result.append(char)
    }

    if carry > 0 { result.append("1") }

    return String(result.reversed()) 
}
```

### 思路简述

这题很简单，但是要做好并不容易，主要是把两个只有数字的字符串，当作数字相加，并给出一个字符串的结果。我个人觉得最难的点其实是在swift 下如何转化 `String`、`Character`、`Int` 其中还只能用 `UInt8` 因为题目要求不能用大整型。那么，这一题中，把Character 和ASC II 码互相转化，就是一个特别高效的做法，这题的解法也是超过了100% 的其他解法。

还有需要注意的点就是两个字符串不等长的情况，也要处理。至于处理相加后的进位则是基本功了。最后，全部加玩还有一个1，那就要再加一位。


