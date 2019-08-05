---
layout: post
title:  "LeetCode学习笔记(22) Generate Parentheses"
date:   2018-08-05 08:00:00 +0800
categories: 算法
---

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

Solution 1 (Swift):

```swift
class Solution {
    func generateParenthesis(_ n: Int) -> [String] {
        var result = [String]()
        if (n == 0) {
            return result
        }
        helper(res: &result, present: "", left: n, right: n)
        return result
    }
    
    func helper(res:inout [String], present: String, left: Int, right: Int) {
        if (right == 0) {
            res.append(present)
        }
        if (left > 0) {
            helper(res: &res, present: present + "(", left: left - 1, right: right)
        }
        if (right > left) {
            helper(res: &res, present: present + ")", left: left, right: right - 1)
        }
    }
}
```

思路简述：
这是一个非常巧妙的题目，我很喜欢。上面列出的方法大致可以叫回述法，还剩余空间的时候，我们放一个 `(` 左括号，然后当目前的数量不超出的时候，就可以放一个对应的右括号 `)`
