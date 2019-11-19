---
layout: post
title:  "[Swift]LeetCode学习笔记(121) Best Time to Buy and Sell Stock"
date:   2019-10-30 10:00:00 +0800
categories: 算法
---

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

Example 2:

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

### 解法一

```swift
class Solution {
    func maxProfit(_ prices: [Int]) -> Int {
        if prices.count < 2 {
            return 0
        }
        var minPrice = Int.max
        var maxProfit = 0

        for i in 0..<prices.count {
            if prices[i] < minPrice {
                minPrice = prices[i]
            } else if prices[i] - minPrice > maxProfit {
                maxProfit = prices[i] - minPrice
            }
        }
        return maxProfit
    }
}
```

### 思路简述

就很简单，判断一个区间内最合适的买入卖出点，求最大获取的差价。

当然你可以用快慢指针，这个是最容易想到的解法，但是问题非常明显，一个从大到小的数组你怎么办？时间复杂度是 `O(N * (N - 1))`，这显然不是我们想要的。

所以仔细想想，我们只需要关注最低价，和差价的最大值就好，这样只要存两个变量，遍历一次就行了。
