---
layout: post
styles: [syntax]
title: ios开发笔记－ios app的生命周期及状态切换响应处理
---
<h2>APP的生命周期</h2>
自ios4.0以后的版本包含了多任务处理，APP可以切换置后台，暂停或者继续在后台运行。当我们打开一个APP直到退出，在这个过程中，可以将它们分成几个不同的状态，如：

![iso app 状态变化](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/high_level_flow.jpg)

1.Not running:未启动
2.Inactive:刚打开，在接受事件处理的这一段时间
3.Active:准备完毕，随时可以进行交互
4.Background:后台运行
5.Suspended:后台暂停

以上介绍了APP整个生命周期的几种状态，下面来看看程序的运行周期和相关状态触发的时间。
![](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/app_life_cycle.png)

<h2>状态响应</h2>
当APP切换至不同状态时，会触发delegate对象中自定义的处理方式。下面列出了delegate协议定义的各个响应处理的方法，和简单的介绍。

－ application:(UIApplication *) didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

- applicationWillResignActive

- applicationDidEnterBackground

- applicationWillEnterForeground

- applicationWillTerminate


<h2>参考：</h2>
- <https://developer.apple.com/library/ios/#documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/ManagingYourApplicationsFlow/ManagingYourApplicationsFlow.html#//apple_ref/doc/uid/TP40007072-CH4-SW3>
－ <https://developer.apple.com/library/ios/#documentation/UIKit/Reference/UIApplicationDelegate_Protocol/Reference/Reference.html>