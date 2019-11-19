---
layout: post
title:  "[Swift]LeetCode学习笔记(20) Valid Parentheses"
date:   2018-02-28 11:00:00 +0800
categories: 算法
---

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

Solution1 (Swift):

```swift
class Solution {
    func isValid(_ s: String) -> Bool {
        let s = Array(s)
        var stack = [String]()

        for c in s {
            switch c {
            case "(":
                stack.append(")")
            case "{":
                stack.append("}")
            case "[":
                stack.append("]")
            default:
                if stack.isEmpty { return false }
                if let pop = stack.popLast(), pop != String(c)   {
                    return false
                }
            }
        }
        return stack.isEmpty
    }
}
```

思路简述：

这题是判断一个只包含 `{}[]()` 的字符串里面，是否所有的括号都能闭合。这一题的解题思路很有意思，每当我们判断有一个前括号的时候，就在一个String 数组里加一个后括号，然后每当遇到一个后括号的时候，就把数组里的最后一个括号pop 出来，看看是否相等。我认为这是所有的办法里最好，最巧妙的。

同时，我想起来某个微博网友遇到的段子，说是去面试的时候遇到了这一题，结果面试官说让括号分别等于1、2、3、-1、-2、-3，然后算和，这是一种非常搞笑的谬误，稍微动动脑子就知道不对，这样的面试最好还是别过，哈哈哈
