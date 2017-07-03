---
layout: post
title:  "Swift 中的访问级别(Access Level)"
date:   2017-05-09 09:00:00 +0800
categories: iOS学习笔记
---

[原文链接](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/AccessControl.html)


## 访问级别(*Access Level*)

Swift为您的代码中的实体提供了五个不同的访问级别(*Access Level*)。这些访问级别与实体定义的源文件相关，并且与源文件所属的模块相关。

- Open access 和public access 使得实体可以在其定义模块中的任何源文件中使用，也可以在另一个导入定义模块的模块的源文件中使用。指定框架的公共接口时，通常使用open 或public access。它们直接的区别后面详细解释。
- Internal access 使实体可以在其定义模块中的任何源文件中使用，但不能在该模块之外的任何源文件中使用。在定义应用程序或框架的内部结构时，通常使用内部访问。
- File-private access 将实体的使用限制在其自己的定义源文件中。当在整个文件中使用这些细节时，使用文件专用访问来隐藏特定功能的实现细节。
- Private access 将实体的使用限制在封闭声明中。当这些细节仅在单个声明中使用时，使用私有访问来隐藏特定功能的实现细节。

Open access 是最高（最少限制）的访问级别， private access 是最低（最严格的）访问级别。

Open access 仅适用于类和类成员，它与public access 不同如下：

- 具有public access 权限或任何更多限制性访问级别的类可以仅在其定义的模块中进行子类化。
- 具有public access 或任何更多限制性访问级别的类成员可以仅在它们被定义的模块内的子类覆盖。
- 开放类可以在定义模块的子类中，并在任何导入模块定义的模块中进行子类化。
- 开放类成员可以被模块定义的子类覆盖，并且可以在任何导入模块定义的模块中覆盖。

将类标记为open，表示您已经考虑了使用该类作为超类的其他模块的代码的影响，并且相应地设计了类的代码。