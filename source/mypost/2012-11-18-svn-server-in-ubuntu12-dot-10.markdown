---
layout: post
title: "Ubuntu12.10 搭建 SVN服务器"
date: 2012-11-18 13:44
comments: true
categories: Linux
---

最近把实验室的一台Server升级到了12.10

因为实在受不了Arch的更新强度

经常滚死的Arch不适合做服务器了，So 还是回归Ubuntu吧

搭建起来。。。

``` bash
#Step 1 安装一些东西
sudo apt-get install subversion libapache2-svn apache2

#Step 2 建立SVN仓库目录
sudo mkdir /srv/svn

#Step 3 修改配置文件
sudo cp /etc/apache2/mods-enabled/dav_svn.conf /etc/apache2/mods-enabled/dav_svn.conf.orig
sudo nano /etc/apache2/mods-enabled/dav_svn.conf

<Location /svn>
DAV svn
SVNParentPath /srv/svn
AuthType Basic
AuthName "Subversion Repository"
AuthUserFile /etc/apache2/dav_svn.passwd
Require valid-user
</Location>

#Step4 生成用户以及密码
sudo htpasswd -cm /etc/apache2/dav_svn.passwd jasonllinux

#Last 建代码仓库啦
cd /srv/svn
sudo svnadmin create repo

```


###### Update
* Error: svn attempt to write a readonly database, commit failed

{%codeblock %}
chmod -R g+w /srv/svn
{%endcodeblock %}

### Q:  
{%codeblock %}
Error: svn attempt to write a readonly database, commit failed
#解决方法
chmod -R g+w /srv/svn
{%endcodeblock %}
