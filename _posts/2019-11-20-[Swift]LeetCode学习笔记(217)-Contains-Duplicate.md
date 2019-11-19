---
layout: post
title:  "[Swift]LeetCode学习笔记(217) Contains Duplicate"
date:   2019-11-20 00:20:00 +0800
categories: 算法
---

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

### Example 1:

```
Input: [1,2,3,1]
Output: true
```

### Example 2:

```
Input: [1,2,3,4]
Output: false
```

### Example 3:

```
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### 解法一

```swift
class Solution {
    func containsDuplicate(_ nums: [Int]) -> Bool {
        if nums.count < 2 {
            return false
        }
        
        let arr = nums.sorted()
        for i in 0..<(arr.count - 1) {
            if arr[i] == arr[i+1] {
                return true
            }
        }
        return false
    }
}
```

### 思路简述

这题就是一个数组里，如果有两个一样的数字，就true，全是不重复的就false。硬来查两遍很容易超时，两个解法，一个是先排序后比较前后，还有就是存一个字典去比较。因为swift 的排序是TimSort，又稳又快，所以就用了这样的简单解决办法。存个字典备查也很简单，不赘述

