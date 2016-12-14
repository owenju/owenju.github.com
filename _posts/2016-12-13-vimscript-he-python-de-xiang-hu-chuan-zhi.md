---
layout: single
title: "为vim-jekyll插件增加新建中文标题博客支持"
date: "2016-12-13 16:59:34 +0800"
excerpt: ""
tags: "Vimscript"
---

# 感谢

感谢别人的无私奉献，让我得到进步，

* [using python in vimscript how to export a value from a python script back to vi](http://stackoverflow.com/questions/17656320/using-python-in-vimscript-how-to-export-a-value-from-a-python-script-back-to-vi)
* [vim插件开发之helloworld插件](https://my.oschina.net/gschen/blog/135303)
* [vim插件开发之python-helloworld插件](https://my.oschina.net/gschen/blog/135919)
* [Python 编码转换与中文处理](http://www.jianshu.com/p/53bb448fe85b)
* [正则表达式 匹配中文，英文字母和数字及的写法！同时控制长度](http://blog.csdn.net/sefvang/article/details/8270553)


# 随便唠叨几句

最近使用`vim`来写`jekyll blog`，发现了一个`vim`插件包含了常用的`jekyll`写博客功能，安装后发现挺好用的，改了改模板然后测试。当输入的标题是英文时完全没问题（PS：很正常，别人本来就不用使用中文），但是中文就比较鸡肋了。阅读源码后发现，博客标题的生成规则中国将中文字符串也一并忽略了，导致同一天新建的全中文标题都是一样的，于是就考虑将中文转成拼音，一番折腾后终于弄好了。


# 涉及到的东西

## [pypinyin](https://github.com/mozillazg/python-pinyin)

这是在网上找到一个`python`模块，可以解决有中文转有标注拼音和无标注拼音问题。

## [vim-jekyll](https://github.com/parkr/vim-jekyll)

这是插件地址。基于这个插件新增了对中文标题的支持

# 大致思路

原插件已经实现了功能的整体框架，需要修改的只是某一个环节，即生成`post title`。通过阅读代码能够只是原本的处理流程，我们将它改成自己需要的功能即可。
接下来的问题是，

1. 如何创建`vim`方法，

2. 将`vim`方法接收到的参数传给`python`方法

3. 如何将`python`处理的结果返回给`vim`

当然还有`python`编码问题，`vim`方法和变量作用域等问题，通过一一解决这些问题，最终就能达到预期的效果。

# 知识点

## Vimscript

说实话，基础语法也不熟悉，不过是按需查找，另外还可以阅读别人源代码来学习如何使用


## python

相对语言，对`python`的语法要熟悉些，实现功能上更得心应手，下面是`python`

# 代码

对程序员来说，最好的表达就是方法就是展示代码，所以贴出代码：

```vimscript
function! s:rename_chinese_to_pinyin(name)
python << EOF
#coding=utf-8
import vim
from pypinyin import lazy_pinyin

args = vim.eval('a:name')

args = unicode(args, 'utf-8')
namearr = []
# for arg in args:
#    namearr.append(unicode(arg, 'utf-8'))
# print namearr
# namestr = ' '.join(namearr)
newnames=lazy_pinyin(args)

for i, component in enumerate(newnames):
    newnames[i] = component.lstrip().rstrip()

newnamestr="-".join(newnames)
newnamestr=newnamestr.replace(" ", "-")

vim.command("let result = '%s'"% newnamestr)
EOF
return result
endfunction
```
