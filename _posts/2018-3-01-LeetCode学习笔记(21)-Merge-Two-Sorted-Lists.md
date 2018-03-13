---
layout: post
title:  "LeetCode学习笔记(21) Merge Two Sorted Lists"
date:   2018-03-01 08:00:00 +0800
categories: 算法
---

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

Solution1 (Swift):

```swift
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init(_ val: Int) {
 *         self.val = val
 *         self.next = nil
 *     }
 * }
 */
class Solution {
    func mergeTwoLists(_ l1: ListNode?, _ l2: ListNode?) -> ListNode? {
        guard let n1 = l1 else { return l2 }
        guard let n2 = l2 else { return l1 }

        if n1.val < n2.val {
            n1.next = mergeTwoLists(n1.next, n2)
            return n1;
        } else {
            n2.next = mergeTwoLists(n2.next, n1);
            return n2;
        }
    }
}
```

思路简述：

//TODO
