---
layout: post
title:  "[Swift]LeetCode学习笔记(189) Rotate Array"
date:   2019-11-03 01:00:00 +0800
categories: 算法
---

Given an array, rotate the array to the right by k steps, where k is non-negative.

### Example 1:

```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

### Example 2:

```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

### Note:

* Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
* Could you do it in-place with O(1) extra 

### 解法一

```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        if k == 0 || nums.count == 0 {
            return
        }

        var i = k
        while i > 0 {
            let num = nums.popLast()
            nums.insert(num!, at: 0)
            i -= 1
        }
    }
}
```


### 解法二

```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        let times = k % nums.count
        let n = nums.count
        nums = Array(nums[n-times..<n]) + Array(nums[0..<n-times])
    }
}
```


### 解法三

```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        let i = k % nums.count
        reverseArray(&nums, 0, nums.count - 1)
        reverseArray(&nums, 0, i-1)
        reverseArray(&nums, i, nums.count - 1)
    }

    func reverseArray(_ array: inout [Int],_ start: Int,_ end: Int) {
        var s = start, e = end
        while s < e {
            let temp = array[s]
            array[s] = array[e]
            array[e] = temp
            s += 1
            e -= 1
        }
    }
}
```

### 思路简述

这题是让你从后往前第k个数的位置翻转一个数组，那么问题清晰了，第一种就是从后往前一个一个pop 然后insert。主要还是insert 效率不太高，所以这个方法最慢。

第二种就是取第k 个之后和k 个之前的颠倒顺序拼一下。最后一种比较tricky，把数组完全倒过来，翻转前k%nums.count 个然后再翻转k%nums.count 往后个。这样不占用任何额外空间就完成了翻转，时间复杂度是O(n)



