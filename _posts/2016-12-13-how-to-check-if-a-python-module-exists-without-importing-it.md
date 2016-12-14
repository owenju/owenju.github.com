---
layout: single
title: "How to check if a python module exists without importing it"
date: "2016-12-13 16:48:13 +0800"
excerpt: "如何检查python模块是否存在"
tags: "Python"
---

# 感谢

我只是搬运工，可以查看[原文地址](http://stackoverflow.com/questions/14050281/how-to-check-if-a-python-module-exists-without-importing-it)了解详细的内容，里面提供了`python 2`和`python 3`的解决方法

# 方法

如何检查`python`模块是否被存在

{% highlight python %}
import imp
try:
    imp.find_module('eggs')
    found = True
except ImportError:
    found = False
{% endhighlight %}
