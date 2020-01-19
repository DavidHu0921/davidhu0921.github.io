---
layout: post
title:  "[Swift]LeetCode学习笔记(283) Move Zeroes"
date:   2020-01-19 22:30:00 +0800
categories: 算法
---

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

### Example:

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

### Note:

1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

### 解法一

```swift
class Solution {
    func moveZeroes(_ nums: inout [Int]) {
        if nums.count == 0 {
            return
        }
        
        var countZero = 0
        var fast = 0, slow = 0
        for num in nums {
            if num != 0 {
                nums[slow] = num
                slow += 1
            } else {
                countZero += 1
            }
            fast += 1
        }
        
        var indexForEnd = nums.count - 1
        while countZero > 0 {
            nums[indexForEnd] = 0
            indexForEnd -= 1
            countZero -= 1
        }
    }
}
```

### 解法二

```swift
class Solution {
    func moveZeroes(_ nums: inout [Int]) {
        guard nums.count > 0 else { return }
        
        let filteredNums = nums.filter({ $0 != 0 })
        let listOfZeroes = Array(repeating: 0, count: nums.count - filteredNums.count)
        
        nums = filteredNums + listOfZeroes
    }
}
```

### 思路简述

这一题就是要在保留原有非0 数顺序的情况下，把所有的0 移动到最后，并且不能用外的储存空间。
一种是对0计数的同时把非0移动到前面，然后在队尾加0.
第二种就是更简单了，把非0的筛出来，再加上n 个0 的数组，两个方法时间复杂度都是O(n)

