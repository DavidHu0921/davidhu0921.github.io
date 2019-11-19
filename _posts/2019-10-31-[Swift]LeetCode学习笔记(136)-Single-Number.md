---
layout: post
title:  "[Swift]LeetCode学习笔记(136) Single Number"
date:   2019-10-31 22:00:00 +0800
categories: 算法
---

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Example 1:

```
Input: [2,2,1]
Output: 1
```

Example 2:

```
Input: [4,1,2,1,2]
Output: 4
```

### 解法一

```swift
class Solution {
    func singleNumber(_ nums: [Int]) -> Int {
        if nums.count == 1 {
            return nums[0]
        }
        let array = nums.sorted()
        if array[0] != array[1] {
            return array[0]
        }
        if array[nums.count - 2] != array[nums.count - 1] {
            return array[nums.count - 1]
        }
        for i in 1 ..< (array.count - 1) {
            if (array[i] == array[i - 1]) || (array[i] == array[i + 1]) {
                continue
            } else {
                return array[i]
            }
        }
        return 0
    }
}
```


### 解法二

```swift
class Solution {
    func singleNumber(_ nums: [Int]) -> Int {
        var a = 0
        for i in nums {
            a ^= i
        }
        return a
    }
}
```

### 思路简述

本题就是说，在一个数组里，只有一个数字是单独的，其他都是成对出现的，那么这种情况下，如何更快用更少额外空间的做出这题。

第一种解法非常直接且傻瓜，排序后，如果某一个数字跟他前后的都不一样，那么就是他了。但是很显然这样的时间复杂度非常高，sort + 一次遍历，时间复杂度最差是 O(nlogn + n)。

第二种就是碉堡了，直接用数学原理解决了，异或规则：

> 如果我们对 0 和二进制位做 XOR 运算，得到的仍然是这个二进制位
`a⊕0=a`

> 如果我们对相同的二进制位做 XOR 运算，返回的结果是 0
`a⊕a=0`

> XOR 满足交换律和结合律
`a⊕b⊕a=(a⊕a)⊕b=0⊕b=b`

由此易得解法二
