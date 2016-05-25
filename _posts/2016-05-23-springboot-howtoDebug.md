---
layout: post
title:  "springBoot how to debug"
date:   2016-05-23 16:08:00
categories: springBoot
tags: springBoot debug remotes
excerpt: 三种方式可以remote debug springboot application
---
* content
{:toc}

###  有三种方式可以 remote debug

>第一种方式,在build.gradle文件中添加如下代码：

```xml
task debugRun(dependsOn:bootRun) {
    gradle.taskGraph.whenReady { graph ->
        if (graph.hasTask(debugRun)) {
            bootRun {
                debug = true
            }
        }
    }
}

```

>然后正常启动服务即可：

```xml

$gradlew bootRun

```

>第二种方式，直接在command line 启动  

```xml

$gradlew run --debug-jvm

```  

>第三种方式，在 build.gradle文件中添加：

```xml

applicationDefaultJvmArgs = [
        "-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5005"
]

mainClassName ="hello.Application"

```
**notice:** mainClassName 必须要指定。

>然后正常启动服务即可：

```xml

$gradlew bootRun

```  

>以上三种方式remote port 默认都是5005，只需要在 intellij idea 中配置一下即可：

![intellijConfiguration](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/intellijConfiguration.png)

>我有一个[Demo](https://github.com/levioZ/gradle_springMVC_resful_mybatis)在这里，感兴趣的话可以看看。
