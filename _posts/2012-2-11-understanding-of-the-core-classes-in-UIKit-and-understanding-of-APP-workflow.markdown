---
layout: post
styles: [syntax]
title: 认识UIKit的核心类和理解APP的工作流程
---

<h2>UIKit</h2>
UIKit是Cocoa框架的子框架。UIKit为所有的应用程序提供基本类，事件轮巡和基本交互。可以在自已的应用中通过子类化，委托和其它的技术来自定义UIKit中提供的默认处理。UIKit提供了很多的类，我将它们划分为五大类，分别是：控件类，控制类，协议类和事件处理类，还有一些杂交类。

而UIKit中的核心类有：UIApplication UIApplicationDelegate UIViewController UIWindow UIDocument 他们是创建一个App的基础对象。下面分别做些简单的介绍：

<b>UIApplication:</b>

<b>UIApplicationDelegate:</b>准确的说这是一个协议类，也就是Java中的接口。需要我们自己定义一个实现UIApplicationDelegate协议的UIResponser的子类。然面我们也可把这个类中当成我们的程序的入口，在几个接口中加入我们的代码

<b>UIViewController:</b>

<b>UIWindow:</b>

<b>UIDocument:</b>

<h2>APP的工作流程</h2>
<img>
说明

<h2>UIApplicationDelegate常用方法介绍</h2>

<h2>示例</h2>在delegate类中

<h2>总结</h2>