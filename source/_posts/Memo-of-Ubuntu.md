title: Ubuntu备忘
comment: true
date: 2015-01-28 18:44:46
categories: linux
tags: [Ubuntu,memo]
---
备忘...			
last updated: 2015.1.28
<!--more-->

###win8与ubuntu双系统时间错误
原因。简单地说，是因为win8和ubuntu对系统硬件时间的处理不一样，[详见这里](http://blog.csdn.net/flywindmouse/article/details/13025017)。		
<br>
解决方法。修改ubuntu或者win8的时间设定。修改ubuntu的方法为：将/etc/default/rcS文件中的"UTC=yes"改为"UTC=no"。