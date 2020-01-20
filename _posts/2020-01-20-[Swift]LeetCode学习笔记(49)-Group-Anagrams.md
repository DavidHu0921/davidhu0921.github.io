---
layout: post
title:  "[Swift]LeetCode学习笔记(49) Group Anagrams"
date:   2020-01-20 22:00:00 +0800
categories: 算法
---

Given an array of strings, group anagrams together.

### Example:

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

### Note:

* All inputs will be in lowercase.
* The order of your output does not matter.

### 解法一

```swift
class Solution {
    func groupAnagrams(_ strs: [String]) -> [[String]] {
        var result = [String: [String]]()
        if strs.count == 0 {
            return [[String]]()
        }
        for s in strs {
            let key = String(s.sorted())
            var current = [String]()
            if var arr = result[key] {
                arr.append(s)
                current = arr
            } else {
                current = [s]
            }
            result[key] = current
        }
        return Array(result.values)
    }
}
```

### 思路简述

这一题主要是要new 一个 `[String: [String]]` 的字典，然后把每一个字符取出来，排序一下，这样可以保证一直，对比已经存进去的，有没有那个key，把同样的key 保存在一起，最后一起取出来就好了。这样写效率还挺高的。时间复杂度O(NKlogK)，空间复杂度O(NK)

