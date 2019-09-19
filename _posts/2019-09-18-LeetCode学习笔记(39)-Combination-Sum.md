---
layout: post
title:  "LeetCode学习笔记(39) Combination Sum"
date:   2019-09-19 09:00:00 +0800
categories: 算法
---

Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.


#### Example 1:

```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```


#### Example 2:

```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

### 解法一

```swift
class Solution {
    var array: [Int] = []

    func combinationSum(_ candidates: [Int], _ target: Int) -> [[Int]] {
        self.array = candidates.sorted()
        var answer: [[Int]] = []
        var current: [Int] = []
        dfs(&answer, &current, target, 0)
        return answer
    }

    private func dfs(_ answer: inout [[Int]], _ current: inout [Int], _ remainder: Int, _ start: Int) {
        if remainder < 0 { return }
        if remainder == 0 {
            answer.append(current)
            return
        }

        for i in start..<self.array.count {
            guard array[i] <= remainder else { return }
            current.append(array[i])
            dfs(&answer, &current, remainder-array[i], i)
            current.removeLast()
        }
    }
}
```

### 思路简述

这题可能画图比较清晰，但是我比较懒，大致的思路就是DFS，比如说对于[2,3,6,7] target=7，那么从2 开始，还剩下5 需要凑出来，有2、3、6、7 四种，去掉后两个，因为减完就负数了。然后再往下找，以此类推，画出一个树状图，按照这个树状图去找，然后写出边界条件就好了，是一个典型的DFS 问题。

当然，也可以看作类似爬楼梯的DP 问题，我还没搞明白那个解法，后续可以更新上来
