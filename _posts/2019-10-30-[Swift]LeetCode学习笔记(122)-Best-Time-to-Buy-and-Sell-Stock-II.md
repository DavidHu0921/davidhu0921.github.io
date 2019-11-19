---
layout: post
title:  "LeetCode学习笔记(122) Best Time to Buy and Sell Stock II"
date:   2019-10-30 11:00:00 +0800
categories: 算法
---

Say you have an array for which the i^th element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

Example 2:

```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

Example 3:

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
        var maxProfit = 0
        for i in 1..<prices.count {
            if prices[i] > prices[i-1] {
                maxProfit += prices[i] - prices[i-1]
            }
        }
        return maxProfit
    }
}
```

### 思路简述

这题跟上题不一样，允许多次买卖，但是不能卖的同时买，所以题目转换一下，理解为，每一段连续上涨区间差值的和，又，很容易得知，多日连续上涨的差值，就是中间每一个交易日上涨的和，所以只要把每一段上涨的值相加就很容易得到答案。我觉得比上一题简单
