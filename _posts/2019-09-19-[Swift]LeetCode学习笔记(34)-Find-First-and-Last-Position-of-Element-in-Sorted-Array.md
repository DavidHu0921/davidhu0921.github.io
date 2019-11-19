---
layout: post
title:  "[Swift]LeetCode学习笔记(34) Find First and Last Position of Element in Sorted Array"
date:   2019-09-19 08:00:00 +0800
categories: 算法
---

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

### Example 1:

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

### Example 2:

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

### 解法一

```swift
func searchRange(_ nums: [Int], _ target: Int) -> [Int] {
    if nums.count == 0 {
        return [-1, -1]
    }
    
    var lowIndex:Int = 0
    var highIndex:Int = nums.count - 1
    
    var resultLow:Int = -1
    var resultHigh:Int = -1
    
    while lowIndex <= highIndex {
        if (nums[lowIndex] == target && resultLow == -1) {
            resultLow = lowIndex
        } else if (nums[highIndex] == target && resultHigh == -1) {
            resultHigh = highIndex
        } else {
            if (resultLow != -1 && resultHigh != -1) {
                break
            }
            if resultLow == -1 {
                lowIndex += 1
            }
            if resultHigh == -1 {
                highIndex -= 1
            }
        }
    }
    
    return [resultLow, resultHigh]
}
```

### 思路简述

这题要求找到一个数组里第一个和最后一个目标数字的index，而且题目告诉你了要时间复杂度O(log n)，那么就是二分查找了。

用过两个指针，一头一尾开始找，当找到了就停止不继续了，注意边界条件，很简单的题目

