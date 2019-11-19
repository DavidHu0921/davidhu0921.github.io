---
layout: post
title:  "LeetCode学习笔记(1) Two Sum"
date:   2018-02-28 09:01:00 +0800
categories: 算法
---

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

Swift 解法1：

```swift
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        for x in 0 ..< nums.count{
        for y in x+1 ..< nums.count{
            if(target==nums[x]+nums[y]){
                return [x,y]
            }
        }
    }
    return [0];
    }
}
```

Swift 解法2：

```swift
func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var array: [Int] = []
        for i in 0...nums.count {
            let n = nums[i]
            let j = target - n
            if array.contains(j) {
                guard let m = array.index(of: j) else { return [0] }
                return [m, i]
            }
            array.append(n)
        }
        return [0]
    }
```

Swift 解法3:
```swift
// 更新到swift5
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var dict = [Int: Int]()
        
        for (index, one) in nums.enumerated() {
            let two:Int = target - one
            if let lastIndex = dict[two] {
                return [lastIndex, index]
            }
            dict[one] = index
        }
        
        return []
    }
}
```

思路简述：

//TODO
