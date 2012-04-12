---
layout: post
styles: [syntax]
title: ios开发笔记－获取ios设备UUID
---

最近在学习ios开发的过程中，需要取设备的唯一id(UUID:
Universally Unique Identifier，通常用于识别和对用户活动进行跟踪，用来做数据分析)，就google找了下相关的api，找到了答案就在xcode里写下了相关代码，xcode马上给我报了个"'uniqueIdentifier' is deprecated"，被抛弃了？所以马上又google了 uidevice uniqueIdentifier，去官网看了下，是在ios 5之后开始被抛弃了。之后在stakeoverflow上看到有人讨论过这个问题，下面是我整理的几个解决方案：

mac+md5: 缺点－mac地址可以被更改，不能直接上传用户的mac地址，因为汲及到用户的隐私，所以得直行hash。

CFUUID: 这是官方提供可以在应用内创建该应用的唯一id，每次创建的id都不一样，所以当用户卸载重新安装后的id是不一样的，无法满足我们的需求。

SFHFKeychainUtils: 这是一个

-<http://stackoverflow.com/questions/6993325/uidevice-uniqueidentifier-deprecated-what-to-do-now>
-<https://github.com/ldandersen/scifihifi-iphone/blob/master/security/SFHFKeychainUtils.m>
-<http://gorgando.com/blog/tag/sfhfkeychainutils>