---
layout: post
title:  "[Swift]LeetCode学习笔记(234) Palindrome Linked List"
date:   2019-11-27 22:10:00 +0800
categories: 算法
---

Given a singly linked list, determine if it is a palindrome.

### Example 1:

```
Input: 1->2
Output: false
```

### Example 2:

```
Input: 1->2->2->1
Output: true
```

Follow up:
> Could you do it in O(n) time and O(1) space?

### 解法一

```swift
class Solution {
    func isPalindrome(_ head: ListNode?) -> Bool {
        guard var head = head else { return true }
        var nums: [Int] = [head.val]
        
        while let next = head.next {
            nums.append(next.val)
            head = next
        }
        return nums == nums.reversed()
    }
}
```

### 思路简述

这题是求一个链表是不是回文的形式，一开始确实有想快慢指针的做法，求出中间点，然后前后比较，但是想了想好像没必要，顺序存进一个数组，然后比较逆序就好，也是O(n)复杂度，并且O(n)的额外空间，从LeetCode 给的结果来看还好。
