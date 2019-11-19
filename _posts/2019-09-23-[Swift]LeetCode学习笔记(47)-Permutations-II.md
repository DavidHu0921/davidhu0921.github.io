---
layout: post
title:  "[Swift]LeetCode学习笔记(47) Permutations II"
date:   2019-09-23 09:00:00 +0800
categories: 算法
---

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

### Example:

```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

### 解法一

```swift
func permuteUnique(_ nums: [Int]) -> [[Int]] {
    var numbers = nums.sorted()
    var temp = [Int]()
    var result = [[Int]]()
    recurse(&numbers, &result, &temp)
    return result
}

func recurse(_ nums :inout [Int],_ result :inout [[Int]] ,_ temp :inout [Int]) {
    if nums.isEmpty {
        result.append(temp)
    }

    for i in 0..<nums.count {
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }
        temp.append(nums[i])
        nums.remove(at: i)
        recurse(&nums, &result, &temp)
        nums.insert(temp.removeLast(), at: i)
    }
}
```

### 思路简述

这题是46题的升级版，问题在于，数字可能重复，因此解也会重复，那么关键在于如何避免这个重复。
为了解决重复的问题，需要第一，把整个数组排序，第二，在递归的时候判断，跟前一个是不是一样，一样就 `continue` 来避免重复的数字元素，剩下的部分就跟46题一样了，非常简单。


