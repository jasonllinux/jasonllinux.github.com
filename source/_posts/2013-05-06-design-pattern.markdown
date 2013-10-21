---
layout: post
title: "设计模式总结"
date: 2013-05-06 09:19
comments: true
categories: Algorithm

---

## 分类

* Creational Pattern (物件的建立)
* Structural Pattern （物件之间的静态结构）
* Behavioral Pattern  （物件之间的合作行为）


### [1]Creational Pattern  

#### Factory 工厂模式
           



#### Singleton 单例模式 
单例模式貌似是我接触的最早也是用的最多的设计模式  
说明： 仅在第一次需要该对象时实例化    
{% codeblock %} 
 
{% endcodeblock %}
#### Prototype 模式 

#### Builder 模式



#### 职责链模式  
将请求的发送者和请求的处理者解耦
处理者如果处理不了，转向它的successor对象去处理


#### 享元模式 Flywight 
运用共享技术有效支持大量细粒度对象的服用  
状态： 内部状态和外部状态
享元工场   
避免对象生产的浪费


#### Strategy 策略模式 
定义算法族  
由Client决定具体选择某种算法  


#### Mediator 中介者模式  
所谓中介者模式就是用一个中介对象来封装一系列的对象交互，中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。



#### Facade 外观模式
结构性  
为子系统中的一组接口提供一个一致的界面，Facade模式定义了一个高层接口，这个接口使得这一子系统更加容易使用  
介于Client和内部子系统之间,避免客户与子系统发生耦合    
为子系统创建一个统一的接口



####  Bridge 模式


#### Adapter 模式



