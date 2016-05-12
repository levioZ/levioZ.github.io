---
layout: post
title:  "如何创建CronJob"
date:   2016-05-11 14:00:00
categories: hybris
tags: property configuration
excerpt: property优先级以及在hybris中如何读取property文件
---
* content
{:toc}


### CronJob 是什么？  

CronJob 是hybris定制的一种定时任务，包括Job 和 Trigger。

* `Job`: 定义一些具体的业务逻辑
* `Trigger`: 定义执行的时间

CronJob 就是把两者关联起来。

### 创建Job  

1、 要创建一个Job，即一个名为XX.java的类，需要继承 `AbstractJobPerformable.java`
2、 这个Job需要托管给spring管理，即要在spring配置文件中声明一下。

进行到这一步的时候，需要rebuild整个项目和进行update操作在HAC中(只需要勾选essential data)，然后你就可以用

```
select {code} from {servicelayerjob} where {code} = 'sendRankingJob'
```
查询到你刚才创建的Job了。

### 设置trigger

你可以在java code中直接写入，但我们通常的做法是通过**impex**文件来导入：

![cronjob](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/cronjob.png)  

#### 如何trigger的运行周期

>Relative 属性设置为false时，是周期性运行，默认为每天，需要增加属性 weekInterval(为空会报错，给个值)

**每周日的上午5点30分运行一次**
![trigger1](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/trgger1.png)

**每天的上午5点30分运行一次**
![trigger2](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/trigger2.png)

**每40分钟运行一次**
![trigger3](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/trigger3.png)

### 或者用 **cronExpression**  

**run 10:30, 11:30, every Wednesday and Friday**

```xml
INSERT_UPDATE Trigger; cronJob(code)[unique=true]; cronExpression
; myHelloWorldServicelayerCronJob; 0 30 10-11 ? * WED,FRI
```  

A cron expression is a string comprised of 6 or 7 fields separated by white space. Fields can contain any of the allowed values, along with various combinations of allowed special characters for that field.

![expression](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/expression.png)
