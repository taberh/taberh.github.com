---
layout: post
styles: [syntax]
title: 自定义Xcode4工程模板
---

当我们新建一个项目后，都会为这个项目做一些相同的事件，比如：引用一些第三方的库，组织目录结构，配置Target等等。这个时候我们都会想有没有什么办法可以把这些重复的活给干了？当然没问题，我们都知道在新建工程时Xcode为我们提供了好多的工程模板，其实我们也可以新建自己的工程模板。下面是关于创建自定义模板的一些整理，供大家参考下：

## 创建模板

## 安装模板

安装非常简单，只要将我们新建的模板目录拷到下面的目录即可(Xcode 4.2)：

```
/Developer/Plaforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/Project Templates/Application
```

这个时候我们启动Xcode -> File -> New -> New Project… 在Application类别中即可看见我们自定义的模板`Custom Application`，如下图：

![选择Custom Application for Application Group](/static/images/post/custom-application-template-2.png "自定义模板")


我们还可以在`Project Templates`目录下创建一个分组，这样在Xcode中新建项目时可以从我们自己的分组中选择模板，如下图：

![选择Custom Application for Custom Group](/static/images/post/custom-application-template-1.png "自定义模板")

## 参考

- <http://meandmark.com/blog/2011/12/creating-custom-xcode-4-project-templates/>