---
layout: post
title:  "配置email服务以及更改数据库"
date:   2016-05-31 14:00:00
categories: hybris
author: eli
tags: email mysql
excerpt:
---
* content
{:toc}

>hybris 默认使用的数据库是 **HSQLDB** ,如果你想更换其他数据库的话,你只需要在 **{HYBRIS_DATA_DIR}/local.properties** 中指定即可。

例如这样：

```xml
#mysql settings
db.url=jdbc:mysql://localhost/table_name?useConfigs=maxPerformance&characterEncoding=utf8
db.driver=com.mysql.jdbc.Driver
db.username=root
db.password=password
db.tableprefix=
mysql.optional.tabledefs=CHARSET=utf8 COLLATE=utf8_bin
mysql.tabletype=InnoDB
```

邮箱可以这样配:

```xml
#configure email 163, mail.from 必须和 mail.replyto 一直，否则通不过163的安全校验
mail.from=username@163.com
mail.replyto=username@163.com
mail.smtp.server=smtp.163.com
mail.smtp.port=25
mail.smtp.user=username@163.com
mail.smtp.password=password
mail.smtp.starttls.enable=true
#end
```

[传送门](https://wiki.hybris.com/display/release5/Installation#Installation-SetUptheFunctionalRange)
