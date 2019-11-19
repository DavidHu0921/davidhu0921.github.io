---
layout: post
title:  "[Swift]LeetCode学习笔记(91) Decode Ways"
date:   2019-09-17 08:00:00 +0800
categories: 算法
---

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```swift
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a non-empty string containing only digits, determine the total number of ways to decode it.

Example 1:

```
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

Example 2:

```
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

### 解法一：

```swift
func numDecodings(_ s: String) -> Int {
    var arr = s.compactMap { Int(String($0)) }
    var temp = [Int](repeating: 0, count: arr.count + 1)
    
    temp[arr.count] = 1
    var index = arr.count - 1
    
    if index >= 0 && arr[index] > 0 { temp[index] = 1 }
    index -= 1
    
    while index >= 0 {
        if arr[index] == 1 || (arr[index] == 2 && arr[index + 1] <= 6) {
            temp[index] = temp[index + 1] + temp[index + 2]
        } else if arr[index] != 0 {
            temp[index] = temp[index + 1]
        }
        index -= 1
    }
    return temp[0]
}
```

### 思路简述：
这题看起来好像是DFS 问题，实际上跟爬楼梯很像，是个动态规划问题，如果用动态规划来做，就非常舒服，基本上就是个斐波那契数列，但是注意几个边缘case，除了两位数，就是集中在0 上面。一个是0，还有10，还有大于26 的0 结尾的数，只要避开这些数字，题目就跟爬楼梯一样了
