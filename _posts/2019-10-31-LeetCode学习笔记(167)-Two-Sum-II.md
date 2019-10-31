---
layout: post
title:  "LeetCode学习笔记(167) Two Sum II"
date:   2019-10-31 22:40:00 +0800
categories: 算法
---

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

### Note:

```
* Your returned answers (both index1 and index2) are not zero-based.
* You may assume that each input would have exactly one solution and you may not use the same element twice.
```

### Example:

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

### 解法一

```swift
class Solution {
    func twoSum(_ numbers: [Int], _ target: Int) -> [Int] {
        if numbers.count == 0 || numbers.count == 1 || (numbers.count == 2 && (numbers[0] + numbers[1] != target)) {
            return []
        }
        var smallIndex = 0
        var bigIndex = numbers.count - 1

        while smallIndex < bigIndex {
            if numbers[smallIndex] + numbers[bigIndex] == target {
                return [smallIndex+1, bigIndex+1]
            } else if numbers[smallIndex] + numbers[bigIndex] > target {
                bigIndex -= 1
            } else if numbers[smallIndex] + numbers[bigIndex] < target {
                smallIndex += 1
            }
        }

        return []
    }
}
```

### 思路简述

这题就是两数之和的进化版，给定数组是排好序的，那么就超级简单了，直接上双指针，一头一尾，不断往中间迫近就好了，知道输出正确答案，没有就输出空。

