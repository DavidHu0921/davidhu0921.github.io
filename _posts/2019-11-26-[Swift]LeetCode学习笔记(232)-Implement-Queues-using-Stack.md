---
layout: post
title:  "[Swift]LeetCode学习笔记(232) Implement Queues using Stack"
date:   2019-11-26 00:10:00 +0800
categories: 算法
---

Implement the following operations of a queue using stacks.

* push(x) -- Push element x to the back of queue.
* pop() -- Removes the element from in front of queue.
* peek() -- Get the front element.
* empty() -- Return whether the queue is empty.

### Example:

```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```

### Notes:

* You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
* Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
* You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

### 解法一

```swift
class MyQueue {
    var array = [Int]()
    /** Initialize your data structure here. */
    init() {
    }
    
    /** Push element x to the back of queue. */
    func push(_ x: Int) {
        array.insert(x, at: 0)
    }
    
    /** Removes the element from in front of queue and returns that element. */
    func pop() -> Int {
        return array.isEmpty ? -1 : array.popLast()!
    }
    
    /** Get the front element. */
    func peek() -> Int {
        return array.isEmpty ? -1 : array.last!
    }
    
    /** Returns whether the queue is empty. */
    func empty() -> Bool {
        return array.isEmpty
    }
}
```

### 思路简述

225 的姊妹题，用栈实现队列。不多说，就是插入的时候始终插第一个就好，其他不变
