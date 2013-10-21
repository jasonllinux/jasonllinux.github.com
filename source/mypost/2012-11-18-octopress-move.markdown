---
layout: post
title: "迁移Octopress（Ubuntu 和 Win7）"
date: 2012-11-18 15:19
comments: true
categories: Octopress
---
# Octopress to Ubuntu 
最近实在受不了Arch的种种问题

于是，痛定思痛，准备把开发平台陆续迁移到Ubuntu上来


### Step1 先checkout出Octopress的源码   
{%codeblock %}    
git clone -b source git@github.com:username/username.github.com.git octopress
cd octopress
git clone git@github.com:username/username.github.com.git _deploy  
{%endcodeblock %}  

### Step2然后安装一些插件吧  
{%codeblock %}   
sudo gem install bundler
{%endcodeblock %}  
### 出现Error

 
{%codeblock %}  
ERROR:  Error installing RedCloth:  
ERROR: Failed to build gem native extension.  
{%endcodeblock %}  

解决方案  
{%codeblock %}   
sudo apt-get install ruby1.9.1-dev  
sudo bundle install  
{%endcodeblock %}  



# Octopress to Win7

最近又在Win7下面折腾Octopress了  
总结下：

### 安装Ruby环境
* Ruby Installer
* DevKit
* 修改淘宝的源
* 更新

### Clone仓库
* 和在Ubuntu中类似


### 安装一些东西
* gem install bundler
* bundle install

### 问题
* 编码问题  
* chcp 65001
