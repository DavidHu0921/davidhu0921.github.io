---
layout: post
title:  "利用Storyboard Reference拆分Storyboard"
date:   2017-05-03 09:00:00 +0800
categories: iOS学习笔记
---

自从nib和之后的storyboard 出现以来，iOS开发就一直有流派之争，时至今日，还有非常多的开发坚持纯代码的去写UI界面。但我认为，目前storyboard 已经变得非常强大，可以适用非常多的场景，使用纯代码去构建非常非常复杂的界面的使用场景已经不多了。

但是在这个争论过程中反复被提及的一点就是storyboard 在多人团队协作过程中，特别容易因为git merge 引发大量冲突惨案，那么接下来就简单说说最近做的一个新项目是如何利用Storyboard Reference 对项目的Storyboard 进行拆分的。

首先新建项目：

![Storyboard img 1](/img/SB1.png)

![Storyboard img 2](/img/SB2.png)

当然，如果是一个已有项目，应该看起来非常像下面这个样子。新项目的话，就拖动加上tabbar 加成下面的样子。

![Storyboard img 3](/img/SB3.png)

重点来了，选中一个tabbar 下面的所有页面，然后 Editor -> Embed in -> Refactor to Storyboard 这个时候原先main storyboard 里面这一大坨页面就会变成一个Storyboard Reference，这部分页面会变成一个全新的storyboard

![Storyboard img 4](/img/SB4.png)

这个时候main storyboard 看起来应该像这样。

![Storyboard img 6](/img/SB6.png)

每一个tabbar 的storyboard 看起来应该是这样。

![Storyboard img 7](/img/SB7.png)

> To be wriiten: 多个storyboard之间如何共享一个公用页面，比如登录注册页面