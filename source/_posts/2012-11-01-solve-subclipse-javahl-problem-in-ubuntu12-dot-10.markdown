---
layout: post
title: "Solve Subclipse Javahl Problem in Ubuntu12.10"
date: 2012-11-01 20:29
comments: true
categories: Linux 
---

eclipse中安装完subclipse插件之后往往会报如下错误：

>Failed to load JavaHL Library.
>These are the errors that were encountered:
>no libsvnjavahl-1 in java.library.path
>no svnjavahl-1 in java.library.path
>no svnjavahl in java.library.path
>java.library.path = /usr/java/packages/lib/amd64:/usr/lib/jni:/lib:/usr/lib

解决方法：

在eclipse安装目录中的文件eclipse.ini中设置

-Djava.library.path=/usr/lib/x86_64-linux-gnu/jni/
