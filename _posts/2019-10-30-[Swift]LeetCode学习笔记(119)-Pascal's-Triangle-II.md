---
layout: post
title:  "[Swift]LeetCode学习笔记(119) Pascal's Triangle II"
date:   2019-10-30 09:00:00 +0800
categories: 算法
---

Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.

![image](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:

```
Input: 3
Output: [1,3,3,1]
```

Follow up:
Could you optimize your algorithm to use only O(k) extra space?


### 解法一

```swift
class Solution {
    func getRow(_ rowIndex: Int) -> [Int] {
      var row: [Int] = []
      var pre1: Int = 0
      var pre2: Int = 0
      for i in 0...rowIndex {
          row.append(1)
          for j in 0...i {
              switch j {
                  case 0:
                      pre1 = 1
                  case i:
                      break
                  default:
                      pre2 = pre1
                      pre1 = row[j]
                      row[j] = pre1 + pre2
              }
          }
      }
      return row
  }
}
```

### 解法二

```swift
class Solution {
    func getRow(_ rowIndex: Int) -> [Int] {
        if rowIndex == 0 {
            return [1]
        }
        var line:[Int] = [Int]()
        var pre = 1
        line.append(1)
        for k in 1...rowIndex {
            let cur = pre * (rowIndex - k + 1) / k
            line.append(Int(cur))
            pre = cur
        }
        return line
    }
}
```

### 思路简述

这一题是上一题杨辉三角的进化版，但是只要求某一行，不用输出全部。因此第一种解法很容易理解，就是把第一个第二个相加等于后一个。[第二种解法](https://leetcode-cn.com/problems/pascals-triangle-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--28/) 看这个链接最后一部分，直接使用了杨辉三角的数学公式算到答案，很简单直接，需要一定的数学功底。

有一点值得注意的是，这题对空间复杂度有额外要求，因此不能先用上一题的步骤求出全集再取某一行，这样不能满足空间复杂度O(k) 的要求


