---
title:        "Runtime"
description:  "Runtime简称运行时。Object-C就是运行时机制，主要是消息机制。"
image:        "http://placehold.it/400x200"
author:       "GeekMeng"
---

一、综述
============

RunTime简称运行时。OC就是运行时机制，也就是在运行时候的一些机制，其中最主要的是消息机。

1、OC & C 比较
------------

对于C语言，函数的调用在编译的时候会决定调用哪个函数，编译完成之后直接顺序执行，没有任何二义性。

对于OC的函数调用称为消息发送，属于动态调用过程，在编译的时候并不能决定真正调用哪个函数，只有在真正运行的时候才会根据函数的名称找到对应的函数来调用。

在编译阶段，OC可以调用任何函数，即使这个函数并未实现，只要声明过就不会报错。
在编译阶段，C语言调用未实现的函数就会报错。

>二义性：指的是一个东西在一种环境下会出现两种以上（包含两种）含义，导致难以清楚到底何种意思。没有二义性，就是同名覆盖。）
>
>`Runtime`基本是用C和汇编写的。
>[苹果维护的开源代码](http://opensource.apple.com//source/objc4/)
>苹果和GNU各自维护一个开源的runtime版本，这两个版本之间都在努力的保持一致。
>

2、runtime 与OC交互
------------

Objective-C从三种不同的层级上与Runtime系统进行交互：

  * 通过Objective-C源代码；
  * 通过Foundation框架的NSObject类定义的方法；
  * 通过对runtime函数的直接调用。


3、runtime用途实现：
------------

  * 1) `Swizzie`黑魔法（拦截系统自带的方法，并替换系统的方法）
  * 2）将某些`OC`代码转为运行时代码
  * 3）实现分类也可以增加属性（通常情况`category`不能增加属性，`Extension`才可以）
  * 4）自动归档和自动解档（原理是通过遍历属性来实现）
  * 5）动态增加方法（动态的为某个类或对象增加一个方法）
  * 6）动态变量控制（动态对某个对象的变量的值进行替换）
  * 7）实现万能控制器跳转（推送过来的消息，要跳转到任意控制器。利用`runtime`动态生成对象、属性、方法这一特性）
  * 8）插件开发（通过头文件名猜测方法的作用，`swizzie`这些方法，插入自己的代码实现插件逻辑）
  * 9）`JSPath`热更新（在线修复bug，实现热更新）

☺

=======================================================


二、详述
============

1、消息机制
------------

  * 方法调用的本质，即为让对象发送消息
  * `objc_msgSend`，只有对象才能发送消息，因此以`obj`开头
  * 使用消息机制前提，必须导入`#import<objc/message.h>`

### 1.1 消息机制的简单使用 ###

~~~Objective-C
//1.对象方法
// 创建person对象
Person *p = [[Person alloc] init];
// 调用对象方法
[p eat];
// 本质：让对象发送消息
objc_msgSend(p, @selector(eat));

//2.类方法
// 调用类方法的方式：两种
// 第一种通过类名调用
[Person eat];
// 第二种通过类对象调用
[[Person class] eat];
// 用类名调用类方法，底层会自动把类名转换成类对象调用
// 本质：让类对象发送消息
objc_msgSend([Person class], @selector(eat));
~~~

### 1.2 消息机制的原理 ###
  * 对象根据方法编号`SEL`去映射表查找对应的方法实现

![runtime_msgSend_image](https://github.com/MengYP/MengYP.github.io/blob/master/resources/img/runtime_msgSend.png?raw=true "描述消息机制原理的图 ")


2、交换方法
------------
  * 开发使用场景：
        系统自带的方法功能不够，给系统自带的方法扩展一些功能，并且保持原有功能。
  * 解决方法：

        * 方式一：继承系统的类，重写方法。
        * 方式二：使用runtime，交换方法。

### 2.1 使用`runtime`交换方法 ###

~~~Objective-C
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    // 需求：给imageNamed方法提供功能，每次加载图片就判断下图片是否加载成功。

    // 步骤一：先搞个分类，定义一个能加载图片并且能打印的方法+ (instancetype)imageWithName:(NSString*)name;

    //步骤二：交换imageNamed和imageWithName的实现，就能调用imageWithName，间接调用imageWithName的实现。

    UIImage *image = [UIImage imageNamed:@"123"];
}
@end
~~~

~~~Objective-C
@implementation UIImage (Image)
// 加载分类到内存的时候调用
+ (void)load
{
    // 交换方法：
    // 获取imageWithName方法地址
    Method imageWithName = class_getClassMethod(self,@selector(imageWithName:));

    // 获取imageWithName方法地址
    Method imageName = class_getClassMethod(self, @selector(imageNamed:));

    // 交换方法地址，相当于交换实现方式
    method_exchangeImplementations(imageWithName, imageName);
}

// 不能在分类中重写系统方法imageNamed，因为会把系统的功能给覆盖掉，而且分类中不能调用super.

// 既能加载图片又能打印
+ (instancetype)imageWithName:(NSString *)name
{
    // 这里调用imageWithName，相当于调用imageName
    UIImage *image = [self imageWithName:name];
    if (image == nil) {
        NSLog(@"加载空的图片");
    }
    return image;
}
@end
~~~

### 2.2 使用`runtime`交换方法的原理 ###





### 未完待续 ###
