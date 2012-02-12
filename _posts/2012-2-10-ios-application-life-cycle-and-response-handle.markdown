---
layout: post
styles: [syntax]
title: ios app的生命周期及状态切换响应处理
---
<h2>APP的生命周期</h2>
自ios4.0以后的版本包含了多任务处理。也就是说我们的APP可以切换置后台，暂停或者继续在后台运行。当我们打开一个APP直到退出它，在这个过程中，可以将它们分成几个不同的状态，如：Not running,Inactive,Active,Background,Suspended五个状态。在

<h2>状态响应</h2>
当APP切换至不同状态时，会通知该我们自定义的delegate对象，在该对象中作响应处理。下面列出了delegate协议定义的各个响应处理的方法，和简单的介绍。

<h2>UIApplicationDelegate协议常用方法介绍</h2>
－ application:(UIApplication *) didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

- applicationWillResignActive

- applicationDidEnterBackground

- applicationWillEnterForeground

- applicationWillTerminate


<h2>参考：</h2>
－ <https://developer.apple.com/library/ios/#documentation/UIKit/Reference/UIApplicationDelegate_Protocol/Reference/Reference.html>