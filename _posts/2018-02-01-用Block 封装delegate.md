---
layout: post
title:  "用Block 封装delegate"
date:   2018-02-01 09:00:00 +0800
categories: iOS学习笔记
---

# 需求
最近遇到了这样的一个诡异需求，需要做一个All-in-One 的SDK，把公司的各个分散的内部SDK 封装成一个来用。那么这个里面就有一个非常棘手的情况，因为别人写的SDK，特别是有的SDK 的安卓和iOS版本是同一个安卓开发写的，那么接口就非常的安卓，到处都是delegate，但是为了调用者的使用方便，我们需要统一整理成一个方法，用block 的形式异步回调出去。

# 代码剖析
需要封装的类大致长这个样子：

```
@protocol ZeldaManagerDelegate <NSObject>

- (void)requestSuccess:()message;
- (void)requestFailed:()error;

@end

@interface ZeldaManager : NSObject

@property (nonatomic, weak) id<ZeldaManagerDelegate> delegate;

+ (instancetype)sharedManager;
- (void)requestSomething:(NSInteger)id;

@end
```

我希望封装完以后，一个接口就能调用完这个类，因此我希望他长的样子：

```
// ZeldaManager.h
- (void)requestSometing:(NSInteger)id success:(successBlock)success failed:(failedBlock)failed;
```

# 实现
那么现在需求是明确的，但是我在网上搜了一番之后没有太好的回答，就自己撸了一个wrapper 类来实现这个需求。

```
// ZeldaWrapper.h

typedef void (^ZeldaLoadSuccess)(void);
typedef void (^ZeldaLoadFailure)(void);

@interface ZeldaWrapper : NSObject

+ (ZeldaWrapper *)requestWithID:(NSInteger)id success:(ZeldaLoadSuccess)success failure:(ZeldaLoadFailure)failure;

@end
```


```
// ZeldaWrapper.m

@interface ZeldaWrapper () <ZeldaLoadDelegate>

@property (nonatomic, copy) ZeldaLoadSuccess success;
@property (nonatomic, copy) ZeldaLoadFailure failure;

@end

@implementation ZeldaWrapper

- (instancetype)initWithID:(NSInteger)id success:(ZeldaLoadSuccess)success failure:(ZeldaLoadFailure)failure {
    self = [super init];
    if (self != nil){
        self.success = success;
        self.failure = failure;
        
        // call the func you really wanna wrapper it
        // and set ZeldaWrapper itself as the delegate
    }
    return self;
}

+ (ZeldaWrapper *)requestWithID:(NSInteger)id success:(ZeldaLoadSuccess)success failure:(ZeldaLoadFailure)failure {
   return [[self alloc] initWithID:id success:success failure:failure];
}

#pragma mark - ZeldaLoadDelegate
- (void)onZeldaLoaded {
    self.success();
}

- (void)onZeldaFailed {
    self.failure();
}

@end
```
这样这个需求就算是实现了，那么调用起来也有要注意的地方，下面代码里的这个wrapper 必须要在调用的类中持有它，不然调用完被释放了后面的block 就会因为delegate 被释放而无法回调到。

```
// ZeldaManager.m
- (void)requestSometing:(NSInteger)id success:(successBlock)success failed:(failedBlock)failed {

	ZeldaWrapper *wrapper = [ZeldaWrapper requestWithID:id success:^{
        // do something
    } failure:^{
        // do something
    }];
    
    // You must keep wrapper in ZeldaManager.m or the block won't be called becase the delegate has been released
}
```

