---
layout: single
title: "Centos 7 虚拟机网络配置"
date: "2016-12-13 15:12:49 +0800"
excerpt: "在virtualBox虚拟机安装CentOS 7后无法上网"
tags: "Linux"
---

# 感谢写在前面

今天帮同事弄CentOS 7系统才发现安装了很久的系统原来连不上网络，于是百度了解决方法，原文可以在[这里](http://simonhu.blog.51cto.com/196416/1588971)找到。

# 解决思路

## 1. 查看网络配置

首先想到的是查看当前的网络配置情况，执行`ifconfig`后居然提示没有这个命令，原来已经修改为`ip`了。在终端输入`ip addr`可以看到网卡配置的情况。

![figure-1]({{site.baseurl}}/assets/2016-12-13-centos-7-xu-ni-ji-wang-luo-pei-zhi-figure-1.png)

## 2. 修改配置文件

网络配置文件是存放在`/etc/sysconfig/network-scripts/`，找到`ifcfg*`的文件，使用`cat`查看里面内容，会发现一行

```bash
...
ONBOOT=no
...
```

将`ONBOOT`修改为`yes`后重启即可

