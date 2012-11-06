---
layout: post
title: "Config Octopress"
date: 2012-11-04 12:58
comments: true
categories: Octopress
---

## 如何恢复
首先从github checkout两个分支
  
```bash
    git clone -b source git@github.com:username/username.github.com.git octopress
    cd octopress
    git clone git@github.com:username/username.github.com.git _deploy
```
    
安装依赖gems

```bash
    gem install bundler
    bundle install
    rake install # 可以省略？
```

pull最新的

```bash 
    cd xxx
    cd _deploy
    git pull origin master
    cd ..
    git pull origin source
```

## 添加robots.txt

## 添加404页面 

## More
excerpt_link: "Read on &rarr;"  # 在文章中使用<!-- more -->,列表页将不再显示全文，而是显示“Read on”的链接，指向全文  
    
