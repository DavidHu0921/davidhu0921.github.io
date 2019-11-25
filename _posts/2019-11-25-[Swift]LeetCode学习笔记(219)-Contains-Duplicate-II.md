---
layout: post
title:  "[Swift]LeetCode学习笔记(219) Contains Duplicate II"
date:   2019-11-25 22:30:00 +0800
categories: 算法
---

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

```
Example 1:

Input: nums = [1,2,3,1], k = 3
Output: true
Example 2:

Input: nums = [1,0,1,1], k = 1
Output: true
Example 3:

Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

### 解法一

```swift
class Solution {
    func containsNearbyDuplicate(_ nums: [Int], _ k: Int) -> Bool {
        var s = Set<Int>()   
        
        for i in 0 ..< nums.count {
            if s.contains(nums[i]) {
                return true
            }
            
            s.insert(nums[i])
            
            if s.count > k {
                s.remove(nums[i - k])
            }
        }
        
        return false
    }
}
```

### 思路简述

这题是在 [217题](https://davidwho.me/算法/2019/11/19/Swift-LeetCode学习笔记(217)-Contains-Duplicate/) 的基础上跟进一步，要求两个重复的数之间的index，差距不能大于给定的k，那么最好的办法就是维护一个长度为k 的字典，先进先出队列，就能解决问题。跟217 不一样的是，217 不要求顺序，可以排序完再比，这个不行

