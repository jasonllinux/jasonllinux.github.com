---
layout: post
title: "RoboCup机器人救援仿真自动化脚本个人总结"
date: 2013-10-07 11:47
comments: true
categories: RoboCup
---

> 为了平时测试的效率，小小研究了世界杯公布的服务器版本中的脚本，满足平时自动化测试的需要  

### 主要步骤  
{% codeblock [lang:bash] [Run scripts]%}

cd roborescue/scripts/remote-control/

./run.sh CLUSTER_NO MAP TEAM 

{% endcodeblock %}


该脚本中主要流程为：  

* 获取配置 config.sh 
在该脚本中配置  LOCAL_USER REMOTE_USER  本地和远程机器的用户名 一般默认都设置为 `rescue`
假设我们有一个集群cluster： c1-1 c1-2 c1-3 c1-4  
其中 c1-1 为kernel Node，其他均为client node  



* 检测Server Node上是不是已经在运行
判断Kernel Node上是否有正在运行的实例是通过检测boot目录中是否有rsl.lock 文件

* 如果没有，启动pre compute
主要针对有预计算需求的队伍在每个client node上进行预计算

* 启动Server
根据获得的的参数：地图，自动获取它相应的配置文件config 目录

* 启动evaluate脚本，记录快照和分数
evaluate脚本负责和kernel通讯，活的每周期的分数，以及每隔50周期，包括init和end时候的快照

* 启动client智能体  
ssh到各个client node，到code路径根据启动类型 pf at fb执行相应的启动脚本  

* 等待一个回合结束 
循环检测 kernel 目录中的是否还有lock，有则证明还有任务在running

* 若结束 cancle run
`./cancelRun.sh`

* 生成 eval html


### 杂项   

* 设置ssh别名	

* 获取host ip问题pre



### 修改后Server 仓库地址 
[https://github.com/jasonllinux/rcrss](https://github.com/jasonllinux/rcrss)  

* 除了脚本的修改之外，添加了对Mac的支持


### _未完，待补充_
