---
layout: post
styles: [syntax]
title: 自定义Xcode4工程模板
---

当我们新建一个项目后，都会为这个项目做一些相同的事件，比如：引用一些第三方的库，组织目录结构，配置Target等等。这个时候我们都会想有没有什么办法可以把这些重复的活给干了？当然没问题，我们都知道在新建工程时Xcode为我们提供了好多的工程模板，其实我们也可以新建自己的工程模板。下面是关于创建自定义模板的一些整理，供大家参考下：

## 创建模板

其实一个工程模板就是一个目录，和一个.plist配置文件和自已添加的的附加文件，比如图标、声音、源代码和XIB等文件组合。但是工程模板目录名必须以`.xctemplate`结尾；而.plist配置文件名必须是`TemplateInfo`，下面是一个最简单的模板结构：

```
-- XXX.xctemplate
	- TemplateInfo.plist
```

我们都知道plist文件的本质中一个xml，现在主要的问题就是这个xml有哪些配置项、配置规则？

规则很简单，一个key对应一个值，这个值可以是：Array,Boolean,Dictionary,String，下面是一个不完整的key：

```
Ancestors:
Concrete
Definitions
Description
Identifier
InjectionTargets
Kind
MacOSXVersionMin
Nodes
Options
Platforms
Project
SortOrder
Targets
```

现在我们可以配置自己想要的模板了，我来建个示例模板吧，我们就叫它`Custom Application`：

第一步：

新建一个目录，并为目录命名：`Custom Application.xctemplate`；

第二步：

进入`Custom Application.xctemplate`目录，使用文件编辑器新建文件保存为`TemplateInfo.plist`，文件内容如下：

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	// config something
</dict>
</plist>
```

有了这个基础结构，我们就可以添砖加瓦了，只需要在`dict`下添加一对对应的key/value节点就可以了，打个比方：

```
// String
<key></key>
<string></string>

// Boolean
<key></key>
<true/> or <false/>

// Dictionary
<key></key>
<string></string>

// Array 
<key></key>
<string></string>
```

第三步：添加


## 安装模板

安装非常简单，只要将我们新建的模板目录拷到下面的目录即可(Xcode 4.2)：

```
/Developer/Plaforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/Project Templates/Application
```

这个时候我们启动Xcode -> File -> New -> New Project… 在Application类别中即可看见我们自定义的模板`Custom Application`，如下图：

![选择Custom Application for Application Group](/static/images/post/custom-application-template-2.png "自定义模板")


我们看到在Xcode中新建项目选择模板时会有个分组，在我们自定义的模板多了后我们也可以创建个分组。只要在`Project Templates`目录下新建个目录，目录名就是分组名，然后将我们的模板都放在这个目录下，Xcode中新建项目时就可以从在我们创建的分组中选择模板了，如下图：

![选择Custom Application for Custom Group](/static/images/post/custom-application-template-1.png "自定义模板")

## 参考

- <http://meandmark.com/blog/2011/12/creating-custom-xcode-4-project-templates/>
- <https://snipt.net/yonishin/about-xcode-4-project-template/>