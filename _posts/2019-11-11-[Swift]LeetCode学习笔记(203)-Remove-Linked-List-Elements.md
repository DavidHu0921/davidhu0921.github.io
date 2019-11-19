---
layout: post
title:  "[Swift]LeetCode学习笔记(203) Remove Linked List Elements"
date:   2019-11-11 00:50:00 +0800
categories: 算法
---

Remove all elements from a linked list of integers that have value val.

### Example:

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

### 解法一

```swift
class Solution {
    func removeElements(_ head: ListNode?, _ val: Int) -> ListNode? {
        var dump = head
        
        while let next = dump?.next {
            if next.val == val {
                dump?.next = next.next
            } else {
                dump = dump?.next
            }
        }
        
        return head?.val == val ? head?.next : head
    }
}
```

### 思路简述

很简单，就是把一个链表中的某个值都删掉，遍历一遍就好了，注意下下个点是空的情况，多生成一个dump 去代表下一个就好了


