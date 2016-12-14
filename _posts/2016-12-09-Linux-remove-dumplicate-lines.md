---
layout: single
title: 如何去除Linux下的重复行
excerpt: 这里是摘要
---


{% highlight bash %}
uniq [选项] 文件

说明：这个命令读取输入文件，并比较相邻的行。在正常情况下，第二个及以后更多个重复行将被删去，行比较是根据所用字符集的排序序列进行的。该命令加工后的结果写到输出文件中。输入文件和输出文件必须不同。如果输入文件用“- ”表示，则从标准输入读取。

该命令各选项含义如下：、

- c 显示输出中，在每行行首加上本行在文件中出现的次数。它可取代- u和- d选项。

- d 只显示重复行。

- u 只显示文件中不重复的各行。

- n 前n个字段与每个字段前的空白一起被忽略。一个字段是一个非空格、非制表符的字符串，彼此由制表符和空格隔开（字段从0开始编号）。

+n 前n个字符被忽略，之前的字符被跳过（字符从0开始编号）。

- f n 与- n相同，这里n是字段数。

- s n 与＋n相同，这里n是字符数。

{% endhighlight %}