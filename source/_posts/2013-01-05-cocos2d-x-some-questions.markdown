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


### __Q3__
Android工程中的src目录下缺少源文件  
A:  
修改`copy_files.sh`脚本
添加  
{%codeblock%} 
HELLO_WORLD_ROOT=$COCOS2DX_ROOT/samples/Cpp/HelloCpp
{%endcodeblock%}
在`copy_src_and_jni()`函数中加一行
{%codeblock%} 
cp -rf $COCOS2DX_ROOT/src/ $APP_DIR/proj.android
{%endcodeblock%}

