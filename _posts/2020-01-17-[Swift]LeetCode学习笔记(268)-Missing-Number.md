---
layout: post
title:  "[Swift]LeetCode学习笔记(268) Missing Number"
date:   2020-01-17 22:30:00 +0800
categories: 算法
---

Given an array containing n distinct numbers taken from `0, 1, 2, ..., n` , find the one that is missing from the array.

### Example 1:

```
Input: [3,0,1]
Output: 2
```

### Example 2:

```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

### Note:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

### 解法一

```swift
class Solution {
    func missingNumber(_ nums: [Int]) -> Int {
        let arr = nums.sorted()
        var miss = 0
        for n in arr {
            if miss == n {
                miss += 1
            } else {
                break
            }
        }
        return miss
    }
}
```

### 解法二

```swift
class Solution {
    func missingNumber(_ nums: [Int]) -> Int {
        var s = Set<Int>()
        for n in nums {
            s.insert(n)
        }
        var miss = 0
        for _ in nums {
            if s.contains(miss) {
                miss += 1
            } else {
                break
            }
        }
        return miss
    }
}
```

### 思路简述

这题是从0开始，按顺序找缺失了某个数，当然很自然的想到，可以用排序后的数组做，就是一，时间复杂度是O(nlogn)，还有就是用字典做，时间复杂度是O(n)。还有其他的解法，比这两个更快，但是太针对这一题了，没有共性，暂时不研究
