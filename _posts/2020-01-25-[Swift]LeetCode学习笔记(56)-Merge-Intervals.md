---
layout: post
title:  "[Swift]LeetCode学习笔记(56) Merge Intervals"
date:   2020-01-25 15:00:00 +0800
categories: 算法
---

Given a collection of intervals, merge all overlapping intervals.

### Example 1:

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

### Example 2:

```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

*NOTE* : input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

### 解法一

```swift
class Solution {
    func merge(_ intervals: [[Int]]) -> [[Int]] {
        guard intervals.count > 1 else {
            return intervals
        }
        
        let sorted = intervals.sorted(by: { $0[0] < $1[0] })
        var result: [[Int]] = [sorted[0]]
        for i in 1..<sorted.count {
            if sorted[i][0] <= result[result.count - 1][1] {
                if sorted[i][1] > result[result.count - 1][1] {
                    result[result.count - 1][1] = sorted[i][1]
                }
            } else {
                result.append(sorted[i])
            }
        }
        return result
    }
}
```

### 思路简述

这一题是比较考验对于方法的规划，经过分析发现，先把所有区间排序，可以满足能合并的区间必然连续的特征，那么针对所有的区间排序后，再比较收尾的数字，就可以得到一个结果，时间复杂度主要就是一次排序O(nlogn)，然后空间复杂度是O(1)
