---
layout: post
title:  "[Swift]LeetCode学习笔记(118) Pascal's Triangle"
date:   2019-10-30 08:00:00 +0800
categories: 算法
---

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

![image](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.


### 解法一

```swift
class Solution {
    func generate(_ numRows: Int) -> [[Int]] {
        if numRows == 0 {
            return [[Int]]()
        }
        if numRows == 1{
            return [[1]]
        }
        if numRows == 2{
            return [[1],[1,1]]
        }
        var triangle = [[1],[1,1]]
        for row in 2..<numRows{
            var newRow:[Int] = [Int]()
            newRow.append(1)
            var i = 1
            while i < row{
                newRow.append(triangle[row-1][i-1] + triangle[row-1][i])
                i += 1
            }
            newRow.append(1)
            triangle.append(newRow)
        }
        return triangle
    }
}
```

### 思路简述

就是解杨辉三角，没啥好说的，注意效率，我看那种先把一排填满1 的实在很迷惑，头尾加一就完事了，何必在遍历一遍……