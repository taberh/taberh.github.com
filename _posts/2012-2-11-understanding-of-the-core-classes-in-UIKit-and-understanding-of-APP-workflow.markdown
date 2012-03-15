---
layout: post
styles: [syntax]
title: 认识UIKit的核心类
---

<h2>UIKit</h2>
UIKit是Cocoa框架的一部分。UIKit为所有的应用程序提供基本类，事件轮巡和基本交互。可以在自已的应用中通过子类化，委托和其它的技术来自定义UIKit中提供的默认处理。UIKit提供了很多的类，我将它们划分为五大类，分别是：控件类，控制类，协议类和事件处理类，还有一些杂交类。

而UIKit中的核心类有：UIApplication,UIApplicationDelegate,UIViewController,UIWindow,UIDocument(在应用中是可选)他们是创建一个App的基础对象。下面分别做些简单的介绍：

<b>UIApplication:</b>管理应用程序对象，事件轮巡，高级行为。它将关联一个AppDelegate对象，从而使得我们可以在AppDelegate对象中定义应用的显示以及交互，而不需要考虑整个应用的创建，事件处理等一系列坑爹的问题，方便我们将精力集中在应用的业务逻辑交互处理上。

<b>UIApplicationDelegate:</b>准确的说这是一个协议(也就是Java中的接口)类。在项目中需要我们自己定义一个实现UIApplicationDelegate协议的UIResponser的子类。我们可把这个类看成程序的入口，只需要在协议方法中加入我们的代码来控制应用的状态。

<b>UIViewController:</b>用于管理一个简单的view和他的subviews在屏幕上的表现。对于view和subviews可以这样理解：view是一个容器；subviews就是容器是的一个东西的集合，可以使用addSubview添加Button,Label,UIView到这个集合中，最先添回的在最低层，而上层的对象如果跟下层的重叠的话，便会遮住下层的对象，看不到了。UIViewController类还是所有view controller的基础类，提供加载显示views，和屏幕旋转等默认功能。

<b>UIWindow:应该说是应用显示对象中的根对象，和javascript中的window类似。UIWindow对象只负责负责提供一个主容器，不负责显示内容，所有的显示内容都归views管理。在window上设置一个或者多个views用来显示具体内容。和view controller一样，它有一个subviews属性,还有一个rootViewController属性，可以设置一个根view controller。通常所有的APP只有一个window对象，因为可以使用view controller或subviews的位置，便可切换一同的views。当然也可以为连接到设置的外部显示器新建一个新的window，显示不同的内容。</b>

<b>UIDocument:是用于管理数据和文档的一个抽象类。可以使用这个类获得以下几个好处：在后台队队中异步读写数据；集成iCloud服务；支持文件版本冲突检查；安全的存取操作。</b>

<h2>参考：</h2>
- <https://developer.apple.com/library/ios/#documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/AppArchitecture/AppArchitecture.html#//apple_ref/doc/uid/TP40007072-CH3-SW1>