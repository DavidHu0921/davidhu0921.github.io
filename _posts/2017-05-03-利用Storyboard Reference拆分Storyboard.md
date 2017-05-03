---
layout: post
title:  "利用Storyboard Reference拆分Storyboard"
date:   2017-05-03 09:00:00 +0800
categories: iOS学习笔记
---

自从nib和之后的storyboard 出现以来，iOS开发就一直有流派之争，时至今日，还有非常多的开发坚持纯代码的去写UI界面。但我认为，目前storyboard 已经变得非常强大，可以适用非常多的场景，使用纯代码去构建非常非常复杂的界面的使用场景已经不多了。

但是在这个争论过程中反复被提及的一点就是storyboard 在多人团队协作过程中，特别容易因为git merge 引发大量冲突惨案，那么接下来就简单说说最近做的一个新项目是如何利用Storyboard Reference 对项目的Storyboard 进行拆分的。

![Methods in Xcode jump bar](/img/SB1.png)


> To be wriiten: 多个storyboard之间的页面如何共享