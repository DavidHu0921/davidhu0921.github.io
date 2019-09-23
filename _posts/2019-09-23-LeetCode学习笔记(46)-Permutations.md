---
layout: post
title:  "LeetCode学习笔记(46) Permutations"
date:   2019-09-23 08:00:00 +0800
categories: 算法
---

```swift
func permute(_ nums: [Int]) -> [[Int]] {
    var result = [[Int]]()
    var nums = nums
    recurse(0, &nums, &result)
    return result
}

func recurse(_ first: Int, _ nums: inout [Int], _ result: inout [[Int]]) {
    if first == nums.count {
        result.append(nums)
        return
    }
    for index in first..<nums.count {
        nums.swapAt(first, index)
        self.recurse(first+1, &nums, &result)
        nums.swapAt(first, index)
    }
}
```