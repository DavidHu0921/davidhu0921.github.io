---
layout: post
title:  "LeetCode学习笔记(125) Valid Palindrome"
date:   2019-10-31 08:00:00 +0800
categories: 算法
---

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.

Example 1:

```
Input: "A man, a plan, a canal: Panama"
Output: true
```


Example 2:

```
Input: "race a car"
Output: false
```

### 解法一

```swift
class Solution {
    func isPalindrome(_ s: String) -> Bool {
        let chars = "a"..."z", nums = "0"..."9"
        let filteredString = [Character](s.lowercased().filter({ chars.contains(String($0)) || nums.contains(String($0)) }))
        if filteredString.isEmpty { return true }

        var firstPoint = 0
        var secondPoint = filteredString.count - 1
        while firstPoint < secondPoint {
            if filteredString[firstPoint] != filteredString[secondPoint] {
                return false
            } else {
                firstPoint += 1
                secondPoint -= 1
            }
        }
        return true
    }
}
```

### 思路简述

先利用swift 的语法糖，filter 过滤一下文字，把非字母和数字过滤掉，同时改大小写。然后用双指针来判断是否是回文



