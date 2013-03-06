---
layout: post
title: "Cocos2d-x 中的一些问题"
date: 2013-01-05 14:18
comments: true
categories: Cocos2d-x
---

#### __Q1__
Function 'sharedOpenGLView' could not be resolved  
A:
{% codeblock %}
#include "platform/android/CCEGLView.h"  
{% endcodeblock %}



#### __Q2__  
string之流无法解析  
A:  
在Providers标签中勾选 __CDT Builtin Compiler Settings__ 选项
{% img http://i.minus.com/ibcqMGoEk4m02A.png  %}
