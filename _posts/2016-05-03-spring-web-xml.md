---
layout: post
title:  "web.xml 配置"
date:   2016-05-03 16:34:54
categories: spring
tags: spring Security
author: eli
excerpt: 一些常规的web配置
---
* content
{:toc}

### classpath 和 classpath* 区别：

`classpath：只会到你指定的class路径中查找找文件;`  
`classpath*：不仅包含class路径，还包括jar文件中(class路径)进行查找.`  

### 预加载配置文件 之后可通过${XXX}读取  

```xml
<bean id="propertyConfigurer"  
     class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">  
     <property name="locations">  
         <list>  
             <value>classpath:database.properties</value>  
         </list>  
     </property>  
 </bean>
```   

### JDBC Configuration  通过配置文件 配置直连 数据源  

```xml
<bean id="dataSource"  
     class="org.springframework.jdbc.datasource.DriverManagerDataSource">  
     <property name="driverClassName"  
         value="${hibernate.connection.driver_class}" />  
     <property name="url" value="${hibernate.connection.url}" />  
     <property name="username"  
         value="${hibernate.connection.username}" />  
     <property name="password"  
         value="${hibernate.connection.password}" />  
 </bean>  
```
