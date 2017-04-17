---
layout: post
title:  "Objective-C风格指南."
date:   2017-03-14 09:00:00 +0800
categories: iOS学习笔记
---


## 介绍

目前并没有非常好的，更贴近Apple 本身推荐的Objective-C 代码风格的文档，来规范代码，便于维护和阅读。原文太长了，机翻的+人工简单筛查了一下。

## Credits

来源: [GitHub](https://github.com/raywenderlich/objective-c-style-guide/blob/master/README.md) 各种版权声明信息和作者信息请在连接里查看。
但是我在看完之后发现了一些明显不符合苹果原生推荐的风格，因此作出一些改动，会跟英文原文不一样，不做特殊标注。

## 背景

这里有一些来自苹果的风格指南. 如果本文没有提及的部分, 可能在其中一个里有很详细的说明:

* [Objective-C编程语言](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa基础指南](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Cocoa的编码指南](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS应用程式设计指南](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)

## 目录

* [语言](#language)
* [代码组织](#code-organization)
* [缩进](#spacing)
* [评论](#comments)
* [命名](#naming)
	* [下划线](#underscores)
* [方法](#methods)
* [变量](#variables)
* [属性属性](#property-attributes)
* [点语法](#dot-notation-syntax)
* [字面值](#literal)
* [常数](#constants)
* [枚举类型](#enumerated-types)
* [Switch-Case](#case-statements)
* [私有属性](#private-properties)
* [Booleans](#booleans)
* [条件](#conditionals)
	* [三元操作](#ternary-operator)
* [Init Methods](#init-methods)
* [类构造方法](#class-constructor-methods)
* [CGRect函数](#cgrect-functions)
* [Golden path](#golden-path)
* [错误处理](#error-handling)
* [Singletons 单例](#singletons)
* [换行符](#line-breaks)
* [Xcode项目](#xcode-project)


## 语言

应使用美国英语. 

**首选:**

```objc
UIColor *myColor = [UIColor whiteColor];
```

**不推荐:**

```objc
UIColor *myColour = [UIColor whiteColor];
```


## 代码组织

使用`#pragma mark -`将方法和协议/委托按以下结构分类. 

```objc
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

## 缩进

* 使用默认的tabs 来锁紧。（原文是用两个空格，非常不认同） 
* 方法大括号和其他大括号(`if`/`else` /`switch` /`while`等)总是在与语句相同的行上打开, 但在新行上关闭. (else 前后记得加个空格)

**首选:**

```objc
if (user.isHappy) {
	//Do something
} else {
	//Do something else
}
```

**不推荐:**

```objc
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

* 在方法之间应该有一个空白行, 以帮助视觉清晰和组织. 方法中的空格应该按功能分离, 但通常应该是新的方法. 
* 推荐使用自动合成. 但是如果需要, `@ synthesize`和`@ dynamic`应该在实现中的新行上声明. 
* 应经常避免冒号对齐方法. 在一个方法里面有多于三个冒号的情况下, 冒号对齐使代码更易读. 但是 **千万不要** 在有block的时候用冒号对齐, 因为Xcode的缩进会使它难以辨认. 

**首选:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```


**不推荐:**

```objc
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

## 注释

当需要它们时, 注释应该用来解释一段特定的代码块 **为什么** 做了这些事情. 任何注释必须保持更新或删除. 

应该尽量避免大段注释, 因为代码最好配上间歇性的、少量的注释就能做到自注释。*例外* :这不适用于用于生成文档的那些注释. 

**头文件里推荐写成下面这个格式：**

```
/**
 * 将申请到的UID及校验字段设置给SDK
 * @param uid 用户id
 * @param verified 校验字段
 * @return 是否成功
 */
- (BOOL)setUserId:(NSString *)uid withVerified:(NSString *)verified;
```

## 命名

应尽可能遵守苹果命名约定, 特别是与[内存管理规则](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html)相关的命名规则  [NARC](http://stackoverflow.com/a/2865194/340508). 

长的、描述清晰的方法和变量名都很好. 


**首选:**

```objc
UIButton *settingsButton;
```

**不推荐:**

```objc
UIButton *setBut;
```

对于类名和常量, 应始终使用三字母前缀, 但对于CoreData实体名称可以省略. 对于任何官方raywenderlich.com图书, 入门套件或教程, 应使用前缀'RWT'. 

常量应该是驼峰式, 所有单词都大写, 前缀为相关的类名称. 

**首选:**


```objc
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

**不推荐:**

```objc
static NSTimeInterval const fadetime = 1.7;
```

属性应该是驼峰式, 前导词是小写. 使用自动合成属性而不是手动@synthesize语句, 除非你有很好的理由. 

**首选:**

```objc
@property (copy, nonatomic) NSString *descriptiveVariableName;
```

**不推荐:**

```objc
id varnm;
```

### 下划线

当使用属性时, 实例变量应该总是使用`self.`来访问和改变. 这意味着所有属性将在视觉上不同, 因为它们都将以self.开头. 

一个例外是:在初始化方法内部, 后台实例变量 (即 _variableName)应该直接使用, 以避免getter/setter的任何潜在的副作用. 

局部变量不应包含下划线. 

## 方法

在方法声明中, 在方法类型 (-/+符号)后面应该有一个空格. 方法段之间应该有一个空格 (匹配Apple的风格). 始终包括一个关键字, 并用描述该参数前面的单词描述他的作用. 

避免去使用“and”. 它不应该用于多个参数, 如下面的`initWithWidth:height:`示例所示. 

**首选:**

```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**不推荐:**

```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

## 变量

变量应尽可能描述性地命名. 除了在`for ()`循环中, 应该避免单字母变量名. 

指示指针的星号属于变量, 例如, `NSString *text` 不是 `NSString* text` 或 `NSString * text`, 除非是常量. 

应该尽可能使用[私有属性](#private-properties)来代替实例变量. 虽然使用实例变量是可行的, 但统一使用property 将使我们的代码更加一致. 

除了在初始化方法 (`init`, `initWithCoder:`等...), `dealloc`方法和自定义setter和getter中, 应该避免直接访问'back'属性的实例变量. 有关在初始化方法和dealloc中使用Accessor方法的更多信息, 请参见 [这里](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6). 

**首选:**

```objc
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**不推荐:**

```objc
@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
```

## 属性

属性应该被明确列出, 并且将帮助新程序员在阅读代码时. 属性的顺序应该是存储然后原子性, 这与从Interface Builder连接UI元素时自动生成的代码一致. 

**首选:**

```objc
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

**不推荐:**

```objc
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

可变对象 (例如NSString)的属性应该更喜欢`copy`而不是`strong`. 
为什么？即使你声明一个属性为NSString, 有人可能传入一个NSMutableString的实例, 然后改变它, 而不注意到. 

**首选:**


```objc
@property (copy, nonatomic) NSString *tutorialName;
```

**不推荐:**

```objc
@property (strong, nonatomic) NSString *tutorialName;
```

## 点符号语法

点语法纯粹是一个方便的包装器访问器方法调用. 当使用点语法时, 仍使用getter和setter方法访问或更改属性. 阅读更多[这里](https://developer.apple.com/library/ios/documentation/cocoa/conceptual/ProgrammingWithObjectiveC/EncapsulatingData/EncapsulatingData.html)

点标记应该**总是**用于访问和改变属性, 因为它使代码更简洁. 在所有其他情况下优选括号符号. 

**首选:**

```objc
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**不推荐:**

```objc
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## 字面值

当创建这些对象的不可变实例时, 应该使用'NSString', 'NSDictionary', 'NSArray'和'NSNumber'. 特别注意`nil`值不能传递到`NSArray`和`NSDictionary`字面量, 因为这将导致崩溃. 

**首选:**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**不推荐:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

## 常量

常数优于内联字符串字面值或数字, 因为它们允许容易地再现常用的变量并且可以快速改变而不需要查找和替换. 常量应该声明为`static`常量, 而不是`#define`s, 除非显式地用作宏. 

**首选:**

```objc
static NSString * const RWTAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const RWTImageThumbnailHeight = 50.0;
```

**不推荐:**

```objc
#define CompanyName @"RayWenderlich.com"

#define thumbnailHeight 2
```

## 枚举类型

当使用`enum`s时, 建议使用新的固定底层类型规范, 因为它具有更强的类型检查和代码完成.  SDK现在包括一个宏, 以便于和鼓励使用固定的底层类型:`NS_ENUM ()`

**例如:**

```objc
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {
  RWTLeftMenuTopItemMain,
  RWTLeftMenuTopItemShows,
  RWTLeftMenuTopItemSchedule
};
```

您还可以进行显式赋值 (显示较旧的k风格常量定义):

```objc
typedef NS_ENUM(NSInteger, RWTGlobalConstants) {
  RWTPinSizeMin = 1,
  RWTPinSizeMax = 5,
  RWTPinCountMin = 100,
  RWTPinCountMax = 500,
};
```

较旧的k风格常量定义应该是**避免**, 除非编写CoreFoundation C代码 (不太可能). 

**不推荐:**

```objc
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500,
};
```

## Switch-Case

大括号不需要case语句, 除非由编译器强制. 
当一个案例包含多行时, 应该添加大括号. 

```objc
switch (condition) {
  case 1:
    // ...
    break;
  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }
  case 3:
    // ...
    break;
  default: 
    // ...
    break;
}

```

有时候, 相同的代码可以用于多种情况, 应该使用下拉菜单. 下拉是删除case的'break'语句, 从而允许执行的流程传递到下一个case值. 为了编码的清晰, 应该评论一个下拉列表. 

```objc
switch (condition) {
  case 1:
    // ** fall-through! **
  case 2:
    // code executed for values 1 and 2
    break;
  default: 
    // ...
    break;
}

```

当为交换机使用枚举类型时, 不需要"default. 例如:

```objc
RWTLeftMenuTopItemType menuType = RWTLeftMenuTopItemMain;

switch (menuType) {
  case RWTLeftMenuTopItemMain:
    // ...
    break;
  case RWTLeftMenuTopItemShows:
    // ...
    break;
  case RWTLeftMenuTopItemSchedule:
    // ...
    break;
}
```

## 私有属性

私有属性应该在类的实现文件中的类扩展 (匿名类别)中声明. 除非扩展另一个类, 否则不应使用命名类别 (例如`RWTPrivate`或`private`). 匿名类可以共享/公开以使用<headerfile> + Private.h文件命名约定进行测试. 

**例如:**

```objc
@interface RWTDetailViewController ()

@property (strong, nonatomic) GADBannerView *googleAdView;
@property (strong, nonatomic) ADBannerView *iAdView;
@property (strong, nonatomic) UIWebView *adXWebView;

@end
```

## Boolean

Objective-C使用`YES`和`NO`. 因此, `true`和`false`只能用于CoreFoundation, C或C ++代码. 因为`nil`解析为`NO`, 所以不必在条件下比较. 永远不要直接与`YES'比较, 因为`YES`被定义为1, 一个`BOOL`可以高达8位. 

这允许跨文件的更一致性和更大的视觉清晰度. 

**首选:**

```objc
if (someObject) {}
if (![anotherObject boolValue]) {}
```

**不推荐:**

```objc
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
```

如果`BOOL`属性的名称表示为形容词, 该属性可以省略"is前缀, 但指定get访问器的常规名称, 例如:

```objc
@property (assign, getter=isEditable) BOOL editable;
```

来自[Cocoa命名指南](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284 -BAJGIIJE) 的文字和示例

## 条件

条件体应该总是使用大括号, 即使条件体可以没有大括号 (例如, 它只有一行), 以防止错误. 这些错误包括添加第二行并期望它是if语句的一部分. 另一个, [甚至更危险的缺陷](http://programmers.stackexchange.com/a/16530)可能发生在"内部行的if语句被注释掉, 而下一行不知不觉成为if-声明. 此外, 这种风格与所有其他条件更一致, 因此更容易扫描. 

**首选:**

```objc
if (!error) {
  return success;
}
```

**不推荐:**

```objc
if (!error)
  return success;
```

```objc
if (!error) return success;
```

### 三元运算符

三元运算符`？:`只应用于提高清晰度或代码整齐性. 单个条件通常都应该被评估. 评估多个条件通常更容易理解为一个"if语句, 或重构为实例变量. 一般来说, 三元运算符的最佳使用是在赋值变量并决定使用哪个值. 

非布尔变量应该与某事比较, 并且添加括号以提高可读性. 如果被比较的变量是布尔类型, 则不需要括号. 

**首选:**

```objc
NSInteger value = 5;
result = (value != 0) ? x : y;

BOOL isHorizontal = YES;
result = isHorizontal ? x : y;
```

**不推荐:**

```objc
result = a > b ? x = c > d ? c : d : y;
```

## 初始方法

Init方法应该遵循由Apple生成的代码模板提供的约定. 还应使用"instancetype的返回类型, 而不是"id. 

```objc
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```


参见[类构造器方法](#class-constructor-methods)链接到instancetype的文章. 

## 类构造器方法

在使用类构造函数方法时, 这些应该总是返回类型"instancetype和永不"id. 这确保编译器正确推断结果类型. 

```objc
@interface Airplane
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;
@end
```

有关instancetype的更多信息, 请参见[NSHipster.com](http://nshipster.com/instancetype/). 

## CGRect函数

当访问`CGRect`的`x`, `y`, `width`或`height`时, 总是使用[CGGeometry函数](http://developer.apple.com/library/ios/#文档/graphicsimaging/reference/CGGeometry/Reference/reference.html)而不是直接的struct成员访问. 从苹果的`CGGeometry`引用:

>本参考中描述的将CGRect数据结构作为输入的所有函数在计算结果之前隐式标准化这些矩形. 因此, 您的应用程序应避免直接读取和写入存储在CGRect数据结构中的数据. 相反, 使用此处描述的函数来处理矩形并检索其特征. 

**首选:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```
**不推荐:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```


## Golden Path

当使用条件编码时, 代码的左侧边距应该是"金色或"快乐路径. 也就是说, 不要嵌套`if`语句. 多个返回语句都可以. 

**首选:**

```objc
- (void)someMethod {
  if (![someOther boolValue]) {
	return;
  }

  //Do something important
}
```

**不推荐:**

```objc
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

## 错误处理

当方法通过引用返回错误参数时, 打开返回值, 而不是错误变量. 

**首选:**

```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
  // Handle Error
}
```

**不推荐:**

```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
  // Handle Error
}
```

一些Apple的API在成功的情况下将错误参数 (如果非NULL)写入垃圾值, 因此打开错误可能会导致错误的否定 (随后崩溃). 


## 单例

Singleton对象应该使用线程安全模式来创建它们的共享实例. 

```objc
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

这将防止[可能和有时多发的崩溃](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html). 


## 换行

换行符是一个重要的主题, 因为此样式指南专注于打印和在线可读性. 

例如:

```objc
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];
```

像这样的长长的代码应该被带到第二行, 遵循这个样式指南的间距部分 (两个空格). 

```objc
self.productsRequest = [[SKProductsRequest alloc] 
  initWithProductIdentifiers:productIdentifiers];
```


## Xcode项目

物理文件应该与Xcode项目文件保持同步, 以避免文件蔓延. 创建的任何Xcode组都应由文件系统中的文件夹反映. 代码不仅应按类型分组, 还应按特征分组, 以便更清楚. 

如果可能, 请始终在目标的构建设置中打开"将警告视为错误, 并尽可能启用尽可能多的[其他警告](http://boredzo.org/blog/archives/2009-11-07/warnings). 如果您需要忽略特定警告, 请使用[Clang's pragma feature](http://clang.llvm.org/docs/UsersManual.html#controlling-diagnostics-via-pragmas). 

# 其他Objective-C样式指南

如果我们不适合你的口味, 看看一些其他的风格指南:


* [Robots & Pencils](https://github.com/RobotsAndPencils/objective-c-style-guide)
* [New York Times](https://github.com/NYTimes/objective-c-style-guide)
* [Google](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
* [GitHub](https://github.com/github/objective-c-conventions)
* [Adium](https://trac.adium.im/wiki/CodingStyle)
* [Sam Soffes](https://gist.github.com/soffes/812796)
* [CocoaDevCentral](http://cocoadevcentral.com/articles/000082.php)
* [Luke Redpath](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
* [Marcus Zarra](http://www.cimgf.com/zds-code-style-guide/)

