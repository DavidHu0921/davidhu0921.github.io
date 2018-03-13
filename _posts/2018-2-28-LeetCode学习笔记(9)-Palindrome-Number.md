---
layout: post
title:  "LeetCode学习笔记(9) Palindrome Number"
date:   2018-02-28 10:00:00 +0800
categories: 算法
---

Determine whether an integer is a palindrome. Do this without extra space.

##Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

Solution1 (Swift):

```swift
class Solution {
    func isPalindrome(_ x: Int) -> Bool {
        var y = x
        if (y < 0 || (y != 0 && y % 10 == 0)) {
            return false
        }

        var rev = 0
        while (y > rev){
            rev = rev * 10 + y % 10
            y = y / 10
        }
        return (y == rev || y == rev/10)
    }
}
```

思路简述：

//TODO
