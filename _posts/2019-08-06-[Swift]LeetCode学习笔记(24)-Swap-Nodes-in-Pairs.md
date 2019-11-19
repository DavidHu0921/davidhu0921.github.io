---
layout: post
title:  "[Swift]LeetCode学习笔记(24) Swap Nodes in Pairs"
date:   2019-08-06 08:00:00 +0800
categories: 算法
---

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.


Example:

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
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
    func swapPairs(_ head: ListNode?) -> ListNode? {
        guard let temp = head?.next, let node = head else { return head }
        
        node.next = swapPairs(temp.next)
        temp.next = node
        return temp
    }
}
```

思路简述：
这题标了一个中等难度，实际上很简单，翻转xxx 一类的问题基本上解法都是一样的。这题是交换一个链表中前后两个节点，比如1-2，3-4换位置。是换节点，不是换节点的值。

就很简单用个递归解决问题，把next.next 传下去，然后把当前节点和next 互换。这题用swift 的语法糖 `guard let` 来做特别合适，代码量很小，非常优雅。

