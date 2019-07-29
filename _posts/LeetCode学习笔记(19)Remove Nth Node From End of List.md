---
layout: post
title:  "LeetCode学习笔记(19) Remove Nth Node From End of List"
date:   2019-07-29 08:00:00 +0800
categories: 算法
---

Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:

Given n will always be valid.


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
    func removeNthFromEnd(_ head: ListNode?, _ n: Int) -> ListNode? {
        let head = head
        var slow: ListNode? = head
        var fast: ListNode? = head
        
        var count = 0
        while count < n {
            fast = fast?.next
            count += 1
        }
        
        var previous: ListNode? = nil
        while fast != nil {
            fast = fast?.next
            previous = slow
            slow = slow?.next
        }
        
        if slow === head { return slow?.next }
        
        previous?.next = slow?.next
        slow?.next = nil
        return head
    }
}
```

思路简述：

这个问题是给你一个单向的链表，然后删除倒数第n个。那么最最简单的解题思路就是，现遍历一遍，知道这个链表长度的情况下，再遍历一次，然后去掉倒数第二个。

但是这个方法的问题明显，时间复杂度是O(n^2)，那么能不能更快呢？解决办法是快慢指针，一次遍历，快指针比慢指针快n，这样在快指针到链表最后的时候，慢指针的下一个即为倒数第n个，因此把slow.next 指向slow.next.next 就好啦。

同时需要注意的是，swift 的optional 在编译过程中的写法会比其他语言稍微复杂。
