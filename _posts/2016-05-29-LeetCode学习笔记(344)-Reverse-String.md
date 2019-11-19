---
layout: post
title:  "[Swift]LeetCode学习笔记(344) Reverse String"
date:   2016-05-29 23:22:46 +0800
categories: 算法
---

开始慢慢学习算法，所以开始刷LeetCode 题，每次做完会留个blog 做学习笔记记录下来。

知乎上轮子哥给了建议，从接受率最高的来做，这样会比较简单，从易到难有助于提升信心一直做下去。

所以理所当然从[344. Reverse String](https://leetcode.com/problems/reverse-string/)开始刷。

那么为了更接近底层（或者说装逼）选择了C，虽然大学都在用，但是真的有些忘了，因此造成了一些麻烦。先上代码：

```
char* reverseString(char* s) {
    if (!*s){
        return s;
    }
    char t;
    size_t len = strlen(s) - 1;
    size_t i;
    size_t j = len;

    for(i = 0; i < len; i++){
	    t = s[j];
	    s[j] = s[i];
    	s[i] = t;
	    j--;

        if(j == (len / 2)){
           break;
        }
    }
    return s;
}
```
接下来说说思路，其实注意点就两个：1、最最初级的想法就是把最后/最前的字符调到最前/最后的位置，稍微改进一下就是同时调换头尾，这样时间复杂度一下子减少一半。2、前面判断非空的真的非常非常重要，不然不会提及通过，会造成`Last executed input:
""` 的报错。原因是`size_t len = strlen(s) - 1;` 中`strlen()` 这个方法不能对空指针进行判断。这个坑感谢陈琦同学的解答，学习了。

总的来说这段代码跑了4ms，当然后续还看到了花式玩指针的解法，但是暂时看不懂，以后再优化。

那么作为一个在写iOS的程序员，当然要试试Swift（感谢LeetCode）提供了这个选择。那么在Swift 2.x 下代码是这样的：

```
class Solution {
    func reverseString(s: String) -> String {
        return String(s.characters.reverse())
    }
}
```
虽然Swift 做完一门新语言，有很多现代语言的优势和各种新特性，一行就解决了，但不得不说的是效率实在太差，耗时：572ms。显然简单的方法不是最好的。后续会更新一个效率更高的优化解法。
