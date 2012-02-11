---
layout: post
styles: [syntax]
title: 认识UIKit的核心类和理解APP的工作流程
---

<h2>UIKit</h2>
UIKit是Cocoa框架的一部分。UIKit为所有的应用程序提供基本类，事件轮巡和基本交互。可以在自已的应用中通过子类化，委托和其它的技术来自定义UIKit中提供的默认处理。UIKit提供了很多的类，我将它们划分为五大类，分别是：控件类，控制类，协议类和事件处理类，还有一些杂交类。
而UIKit中的核心类有：UIApplication,UIApplicationDelegate,UIViewController,UIWindow,UIDocument(在应用中是可选)他们是创建一个App的基础对象。下面分别做些简单的介绍：

<b>UIApplication:管理应用程序对象，事件轮巡，高级行为。它将关联一个AppDelegate对象，从而使得我们可以在AppDelegate对象中定义应用的显示以及交互，而不需要考虑整个应用的创建，事件处理等一系列坑爹的问题，方便我们将精力集中在应用的业务逻辑交互处理上。</b>

<b>UIApplicationDelegate:</b>准确的说这是一个协议(也就是Java中的接口)类。在项目中需要我们自己定义一个实现UIApplicationDelegate协议的UIResponser的子类。我们可把这个类看成程序的入口，只需要在协议方法中加入我们的代码来控制应用的状态。

<b>UIViewController:用于管理一个简单的view和他的subviews在屏幕上的表现。对于view和subviews可以这样理解：view是一个容器；subviews就是容器是的一个东西的集合，可以使用addSubview添加Button,Label,UIView到这个集合中，最先添回的在最低层(相当于PS中的层的概念)。UIViewController类还是所有view controller的基础类，提供加载显示views，和屏幕旋转等默认功能。</b>

<b>UIWindow:</b>

<b>UIDocument:</b>

<h2>APP的工作流程</h2>
<img>
说明

<h2>UIApplicationDelegate常用方法介绍</h2>

<h2>示例</h2>在delegate类中

<h2>参考：</h2>