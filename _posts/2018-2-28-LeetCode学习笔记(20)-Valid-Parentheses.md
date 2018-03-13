---
layout: post
title:  "LeetCode学习笔记(20) Valid Parentheses"
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

//TODO
