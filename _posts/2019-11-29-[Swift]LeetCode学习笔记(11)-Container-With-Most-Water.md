---
layout: post
title:  "[Swift]LeetCode学习笔记(11) Container With Most Water"
date:   2019-11-29 22:10:00 +0800
categories: 算法
---

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

*Note*: You may not slant the container and n is at least 2.

![图片](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

### Example:

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

### 解法一

```swift
class Solution {
    func maxArea(_ height: [Int]) -> Int {
        var maxWater = 0
        var slowIndex = 0
        var fastIndex = height.count - 1
        
        while slowIndex < fastIndex {
            let tempWater = (fastIndex - slowIndex) * min(height[slowIndex], height[fastIndex])
            maxWater = max(maxWater, tempWater)
            if height[slowIndex] < height[fastIndex] {
                slowIndex += 1
            } else {        
                fastIndex -= 1
            }
        }
        return maxWater
    }
}
```

### 思路简述

还比较简单，木桶原理，算面积，然后双指针，一头一尾查找，然后得到结果。当然那种暴力双循环就不推荐了。双指针是O(n) 的复杂度
