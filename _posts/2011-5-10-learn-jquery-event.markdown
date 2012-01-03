---
layout: post
styles: [syntax]
title: jQuery Event 源码学习
---

众所周知，jQuery 通过jQuery.event.add & jQuery.event.remove 方法对DOM元素(文本和注释节点除外)进行事件的绑定和解绑。这两个方法都提供了四个参数，前三个参数elem, types, handler 是必选的，最后一个为可选参数分别是data和pos。

<h2>绑定:</h2>
jQuery在对DOM元素进行绑定事件时，通过jQuery.data在jQuery.cache中存储绑定的事件类型、响应函数和可选参数data。该数据结构如下：

{% highlight javascript linenos %}
{ 
  events: { }, 
  handle: function(e){ } 
}
{% endhighlight %}
  
events是一个对象，events中的属性值存储的是事件类型；值是一个数组。当为DOM元素绑定事件时，首先会创建一个包含响应函数、事件类型、guid和一些附加信息的对象，如果events中不存在值为该事件类型的属性，则添加一个值为该事件类型的属性，和一个值为空的数组，然后将刚创建的新对象push到数组中；如果存在，直接push到相对应的数组中。看下面这个例子就一目了然了：

{% highlight javascript linenos %}
//给id元素绑定两个单击和一个鼠标离开事件 
$('#id').bind('click', function() { alert('once'); }); 
$('#id').bind('click', function() { alert('second'); }); 
$('#id').bind('mouseout', function(){ alert('mouseout'); });

//events对象的值 
{ 
  'click': [ 
    {// 此对象还有:data,guid,namespace属性 
      handler: function() { alert('once'); }, 
      type: 'click' 
    }, 
    { 
      handler: function() { alert('second'); }, 
      type: 'click' 
    } 
  ], 
  'mouseout': [ 
    { 
      handler: function(){ alert('mouseover'); }, 
      type: 'mouseout' 
    } 
  ] 
}
{% endhighlight %}

handle是一个函数。jQuery为每一个DOM元素绑定的任意类型事件的响应函数都是此函数，并不是直接将用户传入的函数绑定为响应函数。该函数会在执行时调用一个公共方法jQuery.event.handle，通过apply更改this的指向，此函数还有一个静态属性elem，也是指向DOM元素自己，下面是jQuery中的源码：

{% highlight javascript linenos %}
//引用自jQuery源码 
add: 
  function(elem, types, handler, data) { 
    var elemData = jQuery._data(elem).handle, // 从jQuery.cache中提取的数据 
      eventHandle = elemData.handle; // 创建elem对象的事件响应函数 
    
    if (!eventHandle) { 
      elemData.handle = eventHandle = function(e) { 
        return jQuery.event.handle.apply( eventHandle.elem, arguments ); // 改变对象的this指向 
      }; 
    } 
    
    // handle元素的静态属性elem     
    eventHandle.elem = elem; 
    
    while (type = types[i++]) { 
      var handlers = events[ type ]; // 查看type类型的事件是否存在 
      
      if (!handlers) { 
        handlers = events[ type ] = []; 
        // 绑定事件 
        elem.addEventListener(type, eventHandle, false); 
      } 
      
      handlers.push(handler); 
    } 
  }
{% endhighlight %}

当用户触发事件后，jQuery.event.handle首先会调用jQuery.event.fix对Event对象做兼容处理，之后根据Event.type从jQuery.cache中获取用户绑定时传入的响应函数，逐个运行。

<h2>解绑:</h2>
主要思路是匹配guid，然后从jQuery.cache中events里删除包含相应的响应函数的对象。最后检查该DOM元素还有没有绑定的事件了，如果没有才是真的removeEventListener掉handle处理函数关删除jQuery.cache中的数据。

<h2>思考:</h2>
通过以上的了解，我们可以看到jQuery再为DOM元素的一种类型事件绑定多个响应函数时只会addEventListener一次，而不需要重复addEventListner，并且该DOM元素的所有类型的事件响应都指向一个函数。这时我的脑子里便浮出了这些问题(这里不谈浏览器兼容上比如IE的内存泄漏之类的问题)：这样做的好处是啥？可以减少内存的使用？还是可以提高运行效率？或者说jQuery只是为了对内部事件模块的统一管理？这只是本人所想的到的一些问题，John Resig 这样设计肯定有他的考虑。

接下来，本人就自己所想到的问题进行了思考。我们看看，这样做的唯一一点就是减少了JavaScript引擎对各个DOM元素本身相同类型事件的listening数，用一个对象将DOM元素绑定的响应函数重新组织了下，并增加了一些附加信息。难道说减少listening数可以减少对内存的使用，提高运行效率吗？如果是这样，我们便可以用最老土的方法来进行一些测试，以下是本人的测试方法和数据，仅供参考。

<pre>
Chrome 11          内存使用/MB   解析时间/ms   处理响应时间/ms
jQuery.bind        17.5	         44.75         30.75
addEventListener   21.75         215.75        11.5
</pre>

以上数据是在window下的chrome 11.0.696.65环境中，绑定10 000个事件处理后，测试得到的平均值。当我绑定100 000个事件处理时，使用原生的addEventListener Chrome就提示无影响了，而用jQuery.bind是正常的。

根据上面的数据，jQuery这样做却实能减少内存的使用和提高JavaScript引擎的解析时间，可是在触发事件后的响应处理要慢一点。