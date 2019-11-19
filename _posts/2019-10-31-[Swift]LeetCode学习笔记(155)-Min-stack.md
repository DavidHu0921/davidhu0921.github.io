---
layout: post
title:  "[Swift]LeetCode学习笔记(155) Min Stack"
date:   2019-10-31 22:40:00 +0800
categories: 算法
---

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

```
push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
```

### Example:

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

### 解法一

```swift
class MinStack {
    var data = [(val: Int, min: Int)]()
    
    init() { }
    
    func push(_ x: Int) {
        data.append((x, min(data.last?.min ?? x, x)))
    }
    
    func pop() {
        data.popLast()
    }
    
    func top() -> Int {
        return data.last!.val
    }
    
    func getMin() -> Int {
        return data.last!.min
    }
}
```

### 思路简述

这题有点意思了，有那么一点系统设计的味儿了，主要就是设计一个实现了 `push/pop/top/getMin` 这四个方法的堆栈。

其中最难的是获取最小值，而且要求在常数世界内能获取到，因此我们选择在插入的时候，用原组去把最小的那个记录在最后，这样在pop 的时候也不会影响，去最小值的时候直接取就好了。如果不这样做，还需要再设计一个存取最大最小值的数组，然后在插入、删除的时候去同步，很麻烦。

