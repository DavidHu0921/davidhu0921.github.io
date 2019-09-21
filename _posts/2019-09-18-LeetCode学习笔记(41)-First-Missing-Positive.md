---
layout: post
title:  "LeetCode学习笔记(41) First Missing Positive"
date:   2019-09-21 08:00:00 +0800
categories: 算法
---

Given an unsorted integer array, find the smallest missing positive integer.

### Example 1:

```
Input: [1,2,0]
Output: 3
```

### Example 2:

```
Input: [3,4,-1,1]
Output: 2
```

### Example 3:

```
Input: [7,8,9,11,12]
Output: 1
```

### Note:

Your algorithm should run in O(n) time and uses constant extra space.


### 解法一

```swift
func firstMissingPositive(_ nums: [Int]) -> Int {
        var status = [Int].init(repeating: 0, count: nums.count)
    
        nums.forEach { (num) in
            if num > 0 && num <= nums.count {
                status[num-1] = num
            }
        }

        for i in 0..<status.count {
            if status[i] == 0 {
                return i+1
            }
        }

        return status.count+1
    }
```

### 思路简述

这题看似很简单，题目描述是：输出漏掉的第一个正整数。但是实际上做起来很难，因为题目限定了只能是O(n)，然后存贮空间只能是常数级别的。

解题也十分巧妙，因为首先，一个非常重要的知识点，就是，根据抽屉原理，当一个数组长度为n 的时候，最大的返回值只能是n+1. 那么第一步就是把等长n 的数组，全部填上0。然后第二步，我觉得是最最精髓的，就是把对应Index 的填上对应的值。然后第三部，剩下的数组中，第一个为0 的Index+1 就是缺失的。如果全都没有，那就是n+1 的情况，返回就好了。

实在是太巧妙的题目和解答

