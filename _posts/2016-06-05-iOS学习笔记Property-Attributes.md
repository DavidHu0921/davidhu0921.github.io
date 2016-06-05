---
layout: post
title:  "iOS学习笔记Property Attributes"
date:   2016-06-05 19:00:00 +0800
categories: iOS学习笔记
---

[原文链接](http://stackoverflow.com/questions/9859719/objective-c-declared-property-attributes-nonatomic-copy-strong-weak)

看到这篇StackOverflow上的回答对于Property Attributes的理解特别好，翻译记录下来，加深印象。并没有授权，如果侵权请告知我删除本文。

**Nonatomic**

`nonatomic` 是为了在多线程的时候使用。如果我们在声明的时候设置了nonatomic 这个属性， 那么另外一个线程想获取这个对象的时候就可以获取到这个对象并且在给出结果的时候遵循多线程原理。

**Copy**

`copy` 需要在对象可变的时候用。当你想用这个对象当前的值的时候用这个，当然你也不想这个值反映了任何别的对象持有者对他的改变。你需要在不用这个对象的时候释放它，因为你持有了这个对象。

**Assign**

`Assign` 恰恰和 `copy` 相反。当调用一个 `assgin` 的属性的时候，它会返回一个真实数据的关系。一般来说，在你用一些原始类型（如float, int, BOOL...）时会用到这个属性。

**Retain**

`retain` 在你的属性时一个只想指向对象的指针的时候用。`@synthesize` 生成的setter 方法会持有（换句话说，增加引用计数）对象。你需要在不用这个对象的时候释放它。用retain 会增加引用技术病在自动释放池中占据内存。

**Strong**

`strong` 是retain 的一种替代，是Objective-C ARC（Automated Reference Counting，自动引用计数）的一部分。在非ARC 代码中，strong至少retain 的一个代名词。

这有个学习iOS5中`strong` 和`weak` 很好的网站。
 [原文链接](http://www.raywenderlich.com/5677/beginning-arc-in-ios-5-part-1)

**Weak**

`weak` 跟`strong` 很像，除了它不会对引用计数加一。它不会成为对象的持有者而只是持有一个关联对象。如果对象的关联数量降为0，即使你还有指向那里，但是还是会被从内存中清除。
