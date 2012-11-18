---
layout: post
title: "迁移Octopress"
date: 2012-11-18 15:19
comments: true
categories: Octopress
---

最近实在受不了Arch的种种问题

于是，痛定思痛，准备把开发平台陆续迁移到Ubuntu上来

``` bash
#Step1 先checkout出Octopress的源码
git clone -b source git@github.com:username/username.github.com.git octopress
cd octopress
git clone git@github.com:username/username.github.com.git _deploy

#Step2然后安装一些插件吧

sudo gem install bundler

#出现Error
ERROR:  Error installing RedCloth:
ERROR: Failed to build gem native extension.
#解决方案
sudo apt-get install ruby1.9.1-dev

sudo bundle install

```
