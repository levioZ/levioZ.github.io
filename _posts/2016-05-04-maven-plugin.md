---
layout: post
title:  "maven tomcat plugin"
date:   2016-05-04 17:00:00
categories: maven
tags: maven tomcatPlugin
author: eli
excerpt: Maven Tomcat插件现在主要有两个版本，tomcat-maven-plugin和tomcat7-maven-plugin，使用方式基本相同
---
* content
{:toc}

Maven Tomcat插件现在主要有两个版本，tomcat-maven-plugin和tomcat7-maven-plugin，使用方式基本相同。

### pom里加入编译插件和tomcat插件，就不需要借助IDE来启动服务了  

```xml
<span style="font-size:18px;"><build>
    <finalName>spring-mvc</finalName>
    <plugins>
           <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>1.7</source>
          <target>1.7</target>
        </configuration>
      </plugin>
            <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.2</version>
      </plugin>
    </plugins>
```  
只需要运行`mvn clean tomcat7:run`，就可以了

### tomcat-maven-plugin  插件使用

#### 配置

在pom.xm 加入以下xml  

```xml
<plugin>
	 <groupId>org.codehaus.mojo</groupId>
	 <artifactId>tomcat-maven-plugin</artifactId>
	 <version>1.1</version>
	 <configuration>
		 <path>/wp</path>
		 <port>8080</port>
		 <uriEncoding>UTF-8</uriEncoding>
		 <url>http://localhost:8080/manager/html</url>
		 <server>tomcat6</server>
	 </configuration>
</plugin>
```  
* path  是访问应用的路径
* port 是tomcat 的端口号
* uriEncoding  URL按UTF-8进行编码，这样就解决了中文参数乱码。
* Server 指定tomcat名称。  

#### run

>如果Eclipse 安装了Maven插件，选 择pom.xml文件，击右键——>选择 Run As——> Maven build 。
>
>如果是第一次运行，会弹出下面对话框。在Goals框加加入以下命令: tomcat:run  

![tomcatRun](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/tomcat_run.png)  

这样Tomcat 插件就可以运行。

下面介绍几个常用的Goal  

* `tomcat:deploy`  部署一个web war包
* `tomcat:reload`  重新加载web war包
* `tomcat:start`   启动tomcat
* `tomcat:stop`    停止tomcat
* `tomcat:undeploy` 停止一个war包
* `tomcat:run`     启动嵌入式tomcat ，并运行当前项目

## tomcat7-maven-plugin 使用  

两个插件使用方法基本一样，同样需要在pom.xml引用该插件，需要增加以下配置   

```xml
<plugin>
	 <groupId>org.apache.tomcat.maven</groupId>
	 <artifactId>tomcat7-maven-plugin</artifactId>
	 <version>2.1</version>
	 <configuration>
			 <port>9090</port>
			 <path>/mgr</path>
			 <uriEncoding>UTF-8</uriEncoding>
			 <finalName>mgr</finalName>
			 <server>tomcat7</server>
	 </configuration>
</plugin>
```   

`在这里要注意一下，该插件命名方式有些不同，比如启动tomcat ，对应的目标命令是: tomcat7:run ,同样，其它命令也是这样，需要更改为：tomcat7：<插件执行点>`  

[tomcat-maven-plugin 插件官网](http://mojo.codehaus.org/tomcat-maven-plugin/plugin-info.html)    
[tomcat7-maven-plugin](tomcat7-maven-plugin)
