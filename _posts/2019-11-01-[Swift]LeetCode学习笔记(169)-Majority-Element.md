---
layout: post
title:  "[Swift]LeetCode学习笔记(169) Majority Element"
date:   2019-11-01 21:10:00 +0800
categories: 算法
---

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

### Example 1:

```
Input: [3,2,3]
Output: 3
```

### Example 2:

```
Input: [2,2,1,1,1,2,2]
Output: 2
```

### 解法一

```swift
func majorityElement(_ nums: [Int]) -> Int {
    var result = 0
    var voting = 0
    for i in nums {
        if voting == 0 {
            result = i
        }
        voting += (result == i) ? 1 : -1
    }
    return result
}
```

### 思路简述

这题比较简单的想法就是多次循环，或者存个字典，进阶一点就用二分法什么的做。但是这个解法是我看别人写的，太牛逼了，叫投票法，每次voting 是0 的时候就把当前数作为候选数，跟候选数一样就+1，不一样就=1，既然最后的结果是众数，要大于n/2，那么最后候选数的voting 一定要大于0。

时间复杂度是O(n)，空间复杂度是O(1)，这个思路实在是太牛逼了
