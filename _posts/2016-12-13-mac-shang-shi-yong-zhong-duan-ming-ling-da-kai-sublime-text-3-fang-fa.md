---
layout: single
title: "Mac上使用终端命令打开Sublime Text 3 方法"
date: "2016-12-13 09:51:35 +0800"
excerpt: ""
tags: ""
---

`Sublime`本身提供了命令行打开的工具，只需要将它关联到`/path/bin`下，脚本如下

```shell
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
```
