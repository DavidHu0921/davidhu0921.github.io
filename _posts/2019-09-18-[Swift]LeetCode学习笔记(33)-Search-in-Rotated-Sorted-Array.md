---
layout: post
title:  "LeetCode学习笔记(33) Search in Rotated Sorted Array"
date:   2019-09-18 08:00:00 +0800
categories: 算法
---

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```


Example 2:

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

### 解法一：

```swift
class Solution {
    func search(_ nums: [Int], _ target: Int) -> Int {
        var lowIndex:Int = 0
        var highIndex:Int = nums.count - 1

        while lowIndex < highIndex {
            let midIndex = (lowIndex + highIndex) / 2

            if (nums[0] <= nums[midIndex] && (target > nums[midIndex] || target < nums[0])) {
                lowIndex = midIndex + 1;
            } else if (target > nums[midIndex] && target < nums[0]) {
                lowIndex = midIndex + 1;
            } else {
                highIndex = midIndex;
            }
        }
        return lowIndex == highIndex && nums[lowIndex] == target ? lowIndex : -1;
    }
}
```

### 思路简述

这题不难懂，题目首先就提示你了，时间复杂度要是O(logn)，就是在告诉你要用二分查找，那么问题来了，这题的难点就在于，mid+1 和high 的大小判断上，把这个反转后的情况考虑进去，就很好解决了。

* 如果 target 在[mid+1,high] 序列中，则low = mid+1,否则 high = mid,关键是如何判断 target在[mid+1,high]序列中,具体判断如下：
* 当[0, mid] 序列是升序: nums[0] <= nums[mid], 当target > nums[mid] || target < nums[0] ,则向后规约
* 当[0, mid] 序列存在旋转位: nums[0] > nums[mid],当target < nums[0] && target > nums[mid],则向后规约
* 当然其他其他情况就是向前规约了


