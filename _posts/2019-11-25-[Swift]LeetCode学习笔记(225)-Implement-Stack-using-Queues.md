---
layout: post
title:  "[Swift]LeetCode学习笔记(219) Contains Duplicate II"
date:   2019-11-25 22:30:00 +0800
categories: 算法
---

Implement the following operations of a stack using queues.

* push(x) -- Push element x onto stack.
* pop() -- Removes the element on top of the stack.
* top() -- Get the top element.
* empty() -- Return whether the stack is empty.

###Example:

```
MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
```

### Notes:

```
* You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
* Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
* You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).
```

### 解法一

```swift
class MyStack {
    var array = [Int]()   
    /** Initialize your data structure here. */
    init() {
    }
    
    /** Push element x onto stack. */
    func push(_ x: Int) {
        array.append(x)
    }
    
    /** Removes the element on top of the stack and returns that element. */
    func pop() -> Int {
        return array.isEmpty ? -1 : array.popLast()!
    }
    
    /** Get the top element. */
    func top() -> Int {
        return array.isEmpty ? -1 : array.last!
    }
    
    /** Returns whether the stack is empty. */
    func empty() -> Bool {
        return array.isEmpty
    }
}
```

### 思路简述

就是用数组实现栈，没啥好说的……