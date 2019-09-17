---
layout: post
title:  "LeetCode学习笔记(17) Letter Combinations of a Phone Number"
date:   2019-09-16 08:00:00 +0800
categories: 算法
---

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

## Example:


```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```


## Note:
Although the above answer is in lexicographical order, your answer could be in any order you want.


# 解法一：

```swift
let arr: [String: String] = ["0": " ", "1": " ","2": "abc", "3": "def", "4": "ghi", "5": "jkl", "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"]
var result: [String] = []

func letterCombinations(_ digits: String) -> [String] {
    if digits.contains("0") || digits.contains("1") || digits.isEmpty { return [] }
    let strArr = Array(digits)
    solve(index: 0, path: "", length: digits.count, string: strArr)
    return result
}

func solve(index: Int, path: String, length: Int, string: [Character]) {
    if index == length { result.append(path); return }
    let key = string[index]

    guard let value = arr[String(key)] else { return solve(index: index + 1, path: path, length: length, string: string) }
    let keyArray = Array(value)
    for char in keyArray {
        let value = String(char)
        solve(index: index + 1, path: path+value, length: length, string: string)
    }
}
```

# 解法二：

```swift
func letterCombinations(_ digits: String) -> [String] {
    if digits.count == 0 {
        return []
    }
    let numLetterCombos: [Int: [String]] =
        [0:[], 1:[], 2:["a", "b", "c"], 3:["d", "e", "f"], 4:["g", "h", "i"], 5:["j", "k", "l"], 6:["m", "n", "o"], 7:["p", "q", "r", "s"], 8:["t", "u", "v"], 9:["w", "x", "y", "z"]]
    
    var results: [String] = [""]
    var remaining = Int(digits) ?? 0
    
    while remaining > 0 {
        let mod = remaining % 10
        remaining /= 10
        var newResults: [String] = []
        for s in numLetterCombos[mod]! {
            for r in results {
                newResults.append("\(s)\(r)")
            }
        }
        results = newResults
    }
    
    return results
}
```

## 思路简述


这题特别有意思，也特别“实用”，简单描述题目就是在九宫格键盘的情况下，列出数字组合里所有可能的字母组合结果。比如输入“23”，输出 `["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]` 

那么这题其实就是一个多重循环的结构，可以选择深度优先或者广度优先。深度优先就是解法一，遍历到最后一个节点，然后添加，一个个加过去。广度优先我觉得显然更好，就是解法二，比如“23”的情况，可以先便利第一层"a", "b","c"，然后把第二层叠加上去，反过来也一样，顺序不重要。但是说实话解法二是我看LeetCode 给出的，简直是神仙做法，并非我的智商范围内，列出来给大家学习交流，类似树形原理如图：

![img](https://pic.leetcode-cn.com/38567dcbb6401d88946ca974aacffb5ab27cb1ad54056f02b59016c0cc68b40f-file_1562774451350)



