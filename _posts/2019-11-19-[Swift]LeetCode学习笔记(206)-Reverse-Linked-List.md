---
layout: post
title:  "[Swift]LeetCode学习笔记(206) Reverse Linked List"
date:   2019-11-19 23:10:00 +0800
categories: 算法
---

Reverse a singly linked list.

### Example:

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

### Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

```swift
class Solution {
    func reverseList(_ head: ListNode?) -> ListNode? {
        var prev:ListNode? = nil
        var cur = head
        while cur != nil {
            let temp = cur?.next
            cur?.next = prev
            prev = cur!
            cur = temp
        }
        return prev
    }
}
```

### 思路简述

这题有两个主要解法，遍历法非常直接高效，就先写这种了