---
layout: post
title:  "创建extension"
date:   2016-05-31 16:00:00
categories: hybris
author: eli
tags: extension extgen modulegen
excerpt: 创建定制化的extension
---
* content
{:toc}

### 如何创建extension?

> **hybris** 提供了两个task，专门来做这件事。

```
1、 extgen:    它可以帮助你创建一个 独立的 extension。

2、 modulegen: modulegen其实是包装了extgen,来生成一系列的extension，以此来快速的开始一个新的application。

```

**notice**: 一些extension必须彼此依赖才能起作用，比如 大部分的 Accelerator extensions。so 这种情况就应该用modulegen来创建。

### 定制化extension,需要配置两个文件

1、**platform/extgen/project.properties**

![project.properties](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/project_properties.png)

2、 **extgen.properties**

![extgen.properties](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/extgen_properties.png)

当你运行 **ant modulegen** 后，你需要输入下面的一下值：

* 使用哪个template: 默认取 **project.properties** 中的 **modulegen.module.default** 字段.
*  extension的名字: 默认取 **project.properties** 中的 **extgen.extension.name** 字段.
*    package的名字: 默认取 **project.properties** 中的 **extgen.extension.package** 字段.

```xml

modulegen:
    [input]
    [input] Please choose a template for generation.
    [input] Press [Enter] to use the default value ([accelerator], b2baccelerator, telcoaccelerator, commercewebservices)
accelerator
    [input]
    [input] Please choose the name of your module extension. It has to start with a letter followed by letters and/or numbers.
    [input] Press [Enter] to use the default value [training]
megastore
    [input]
    [input] Please choose the base package name of your extensions. It has to fulfill java package name convention. Each extension in the module will add its name to this package.
    [input] Press [Enter] to use the default value [org.training]
org.megastore

```
