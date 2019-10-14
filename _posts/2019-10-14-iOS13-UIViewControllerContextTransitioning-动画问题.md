---
layout: post
title:  "iOS13 UIViewControllerContextTransitioning 动画问题"
date:   2019-10-14 08:00:00 +0800
categories: iOS
---

自己的项目里用到了一个过场动画，主要是通过 `UIViewControllerContextTransitioning` 做一个VC 间的转场动画，结果到了iOS13 上就跪了，因为iOS13 中全局修改了默认的present 格式，默认变成了一个弹出式的卡片，这让我写的动画彻底失效，bug 极为诡异。因此搜了一下，大致[解决方案](https://stackoverflow.com/questions/57802743/uiviewcontroller-custom-transition-stuck-on-ios13)

贴一段代码：

```swift
func animateTransition(using transitionContext: UIViewControllerContextTransitioning) {
        let containerView = transitionContext.containerView
        guard let toView = transitionContext.viewController(forKey: .to)?.view, let fromView = transitionContext.viewController(forKey: .from)?.view else { return }
        
        let addWorkItemView = presenting ? toView : fromView
        
        let initialFrame = presenting ? originFrame : addWorkItemView.frame
        let finalFrame = presenting ? addWorkItemView.frame : originFrame
        
        let xScaleFactor = presenting ?
            initialFrame.width / finalFrame.width :
            finalFrame.width / initialFrame.width
        
        let yScaleFactor = presenting ?
            initialFrame.height / finalFrame.height :
            finalFrame.height / initialFrame.height
        
        let scaleTransform = CGAffineTransform(scaleX: xScaleFactor, y: yScaleFactor)
        
        if presenting {
            addWorkItemView.transform = scaleTransform
            addWorkItemView.center = CGPoint(
                x: initialFrame.midX,
                y: initialFrame.midY)
            addWorkItemView.clipsToBounds = true
        }
        
        containerView.addSubview(toView)
        containerView.bringSubviewToFront(addWorkItemView)
        
        UIView.animate(withDuration: duration,
                       delay:0.0,
                       usingSpringWithDamping: 1.0,
                       initialSpringVelocity: 0.0,
                       animations: {
                        addWorkItemView.transform = self.presenting ? CGAffineTransform.identity : scaleTransform
                        addWorkItemView.center = CGPoint(x: finalFrame.midX, y: finalFrame.midY)
        }, completion: { _ in
            if !self.presenting {
                self.dismissCompletion?()
            }
            transitionContext.completeTransition(true)
        })
    }
```

其中包含两个问题，都很恼人，一个是 `fromView = transitionContext.viewController(forKey: .from)` 默认变成了返回nil，这样导致动画运行的时候崩溃。需要用 `guard let` 防护一下。还有就是上面描述的弹出问题，主要是默认行为改了，非常非常蛋疼，确实原生app 风格统一了，三方app 只要用了默认的present 也是没有问题，但是自己写的动画的就非常的蛋疼。不过还好，解决方案也简单，在要弹出app 的地方加一行 `viewController.modalPresentationStyle = .fullScreen` 就解决问题了，这样弹出的方式还是跟iOS12 及之前的版本保持一致，不是弹出式的卡片，而是弹全屏，同时也解决了动画的问题。
