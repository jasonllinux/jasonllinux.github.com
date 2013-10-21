---
layout: post
title: "Linux下Eclipse中编译OpenCV相关工程问题"
date: 2012-10-27 21:53
comments: true
categories: OpenCV 
---
最近小研究了下使用OpenCV进行人脸检测

老早用Python实现过

最近回归C++

当然，还是用Eclipse了

刚开始只是惯性的设置了include路径，所以头文件什么的都没有问题

但是，最后Build的时候出现了N多 undefined reference to xxx

网上搜了一把，原来是要设置Lib路径

但是简单的把/usr/local/lib add进去也是没用

要一个一个add 注意去掉前面的 lib 以及后面的 .so

这样就OK了
