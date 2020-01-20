---
layout: post
title:  "[Swift]LeetCode学习笔记(48) Rotate Image"
date:   2020-01-19 22:30:00 +0800
categories: 算法
---

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

### Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. *DO NOT* allocate another 2D matrix and do the rotation.

### Example 1:

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```


### Example 2:

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

### 解法一

```swift
class Solution {
    func rotate(_ matrix: inout [[Int]]) {
        let n = matrix.count
        for i in 0..<(n+1)/2 {
            for j in 0..<n/2 {
                let temp = matrix[n - 1 - j][i]
                matrix[n - 1 - j][i] = matrix[n - 1 - i][n - j - 1];
                matrix[n - 1 - i][n - j - 1] = matrix[j][n - 1 - i];
                matrix[j][n - 1 - i] = matrix[i][j];
                matrix[i][j] = temp;
            }
        }
    }
}
```

### 思路简述

这一题乍一看好像没什么头绪，仔细分析一下，其实就是按位置转换，时间复杂度基本上就是O(n^2)，不需要额外的空间，原地换位置就好了
