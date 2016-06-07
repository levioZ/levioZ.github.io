---
layout: post
title:  "new site没有数据，如何测试"
date:   2016-06-06 16:26:00
categories: hybris
author: eli
tags: env
excerpt: 多站点情况下，新站点没有数据，如何进行快速开发？
---
* content
{:toc}

>task来了，但是新站点木有数据，木法进行下一步操作，怎么解？ 造数据，耗时费力，如何能快速开发？

### 只需要修改三处地方就可以了

>这只是一个权宜之计，适用于同一个brand下的多站点情况

* 首先要进入hmc

![product](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/product.png)
![product1](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/product1.png)

* 这时需要同步下catalog

![product3](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/product3.png)

* 同步下solr，搞定
