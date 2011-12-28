---
layout: post
styles: [syntax]
title: 使用Jekyll在Github上搭建博客
---

Jekyll是一个使用Ruby编写的静态文件转换工具。而Github为您的项目提供静态页面的服务，在Github上也提供了Jekyll服务，所以我们就可以使用Github提供的这些服务，来创建一个静态的站点。

在开始前，请确保你已经有了Github账号一枚和Git的正确配置。没有的朋友可以先移步[Github](https://github.com/plans)。

首先，创建你的 Blog 仓库 username(请确保跟你的账号名相同).github.com:
<pre class="terminal">
  <code>$ mkdir username.github.com</code>
  <code>$ cd username.github.com</code>
</pre>
新建一个 index.html 文件，像下面这样:

{% highlight html linenos %}
<!doctype html>
<html>
<head>
<title>Hello</title>
</head>

<body>
<h1>Hello!</h1>
</body>
</html>
{% endhighlight %}

初始化仓库、提交并push到Github:
<pre class="terminal">
  <code>$ git init</code>
  <code>$ git add .</code>
  <code>$ git commit -a -m 'init commit.'</code>
  <code>$ git remote add origin</code>
  <code>$ git push origin master</code>
</pre>
现在你打开 username.github.com 就可以看到刚才新建的页面了。你也可以绑定自己的域名。具体方法为在你的域名管理页面让域名指向207.97.227.245；并在username.github.com根目录中新建CNAME文件，文件内容为你的域名地址。详细介绍请移步Github的[Pages](http://pages.github.com)页面。

现在我们来认识下Jekyll的文件及目录配置，如下:
<pre class="terminal">
  |
  |- _layout         // 模版目录
  |- _include        // 存放引用文件目录
  |- _plugins        // 插件目录
  |- _post           // 文章目录
  |- _site           // Jekyll自动生成目录，存放转换后的所有文件
  |- _config.yml     // YMAL格式配置文件
</pre>
Note:
* 文章的文件的命名规则 y-m-d-title.(markdown|textile|html)
* 因为_site目录是Jekyll自动生成的，所以在提交的时候可以忽略掉，具体做法是新建.gitignore文件，文件内容可以设置任何你想让忽略的任何目录及文件

现在你可以在自己的仓库中配置好你自己的目录及文件，也可以clone我的仓库，然后修改。现在你就可以push你的代码到Github上，看到结果了。如果你想在本地测试的话，就需要在本地安装Jekyll，下面介绍下Jekyll的安装方法。

1. install ruby
2. install rubygem
3. install ruby devkit
4. install jekyll
5. install rdiscount
