---
layout: post
title:  "顽皮的Jalo"
date:   2016-05-03 17:21:00
categories: hybris
tags: hybris
author: eli
excerpt: Jalo是个淘气鬼，只有坏叔叔才能对付他，嘎嘎
---
* content
{:toc}

### jalo 是什么？

>在hybris的系统中，每一个type(ComposedType)都会有一个相应的jalo class，当你实例化一个对象的时候，它也被实例化了。它通常定义在items.xml中  
>Jalo虽然已经被hybris淘汰了，但是在实际开发中，你还是不得不和它打交道，也许你需要在里面写一些自己的逻辑，或者干错换掉它。(碰到这种问题一般是很棘手的，祝好运。)  

```xml
<itemtype code="Product" extends="LocalizableItem"
    jaloclass="de.hybris.platform.jalo.product.Product"
    ...
```

如果你想操作product对象的话，你通常会这么做：

```java
Product p = productmanager.findProductsByCode(...)  
```     
同时**de.hybris.platform.jalo.product.Product**被实例化了。  

这个时候如果你想用其他的class，你就得告诉hybris去替换它，你可以用这个方法**replaceCoreJaloClass()**   

### 如何替换Jalo?

有个例子：  

```java
class MyProduct extends Product
{
  @Override
  public String getCode( SessionContext ctx )
  {
     return super.getCode().toUpperCase();
  }
}

....
  JaloImplementationManager.replaceCoreJaloClass( Product.class, MyProduct.class );
....

To make sure you are replacing the class before some other thread is using the old class please do the actual registering inside your manager as follows:
public class MyProjectManager extends Manager
{
   ...
   static
   {
      new Registry.Init()
      {
         @Override
         protected void startup()
         {
             JaloImplementationManager.replaceCoreJaloClass( ..... );
         }
       };
    }
    ...
}

```  
但是有一点需要注意：

This can be used to create an EVENTING-like system where you can override methods - even of core jalo classes - where you do not have source code access and you do not want to do a complete subtyping (i.e. create type MyProduct via items.xml).

我的理解是，你应该在一个extension初始化时，就注册进去，否则可能会导致 某些地方还调用到old jalo，你应该这样做：

#### 首先给大家解释下 什么是Manager Beans?

每一个extension都有一个manager bean，比如 `print extension`,就会有一个默认的 `PrintManager.class`.  

当实例化一个 manager class的时候，hybris首先会在 **global ApplicationContext**中查找有没有一个 id 定义为 `<extension>.manager`的bean，如果没有找到，则会使用默认的实现。

```xml
<bean id="print.manager" class="myPackage.jalo.MyPrintManager" init-method="init" scope="tenant" />
```

另外 **core extension** 提供了很多的manager，比如 **UserManager**, **OrderManager** 和 **ProductManager**。这个时候 core.manager的规则就不适用了，需要加一个前缀 `core.${topic}Manager`  

```xml
<bean id="core.userManager" class="myPackage.jalo.MyUserManager" init-method="init" scope="tenant" />
```






##### 还有一种简单的方式，在spring配置文件中直接替换  

>这一种方式，也是我曾经使用的，亲测可用。  

```xml
<bean id="de.hybris.platform.jalo.product.Product" class="myPackage.jalo.MyProduct" scope="prototype" />    
```  
hybris wiki上的原文是这样解释的：  

`Here the bean id has to be the full qualified class name of the default Jalo class.`

`Be aware of that the bean is defined on scope prototype. It will be used only for instantiating an item, so do not inject it anywhere.`  
