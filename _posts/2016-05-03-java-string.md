---
layout: post
title:  "操作string"
date:   2016-05-03 14:09:00
categories: java
tags: java string pattern
author: eli
excerpt: java去除字符串中的空格、回车、换行符、制表符
---
* content
{:toc}

## 如何去除字符串中的空格，回车，换行符，制表符  

>`trim()`只能去除字符串收尾的空格，so 我们需要这样做  

```java
private String replaceBlank(String str)
	{
            String result = "";
		    if(StringUtils.isNotEmpty(str))
			{
				Pattern p = Pattern.compile("\\s*|\t|\r|\n");
				Matcher m = p.matcher(str);
				result = m.replaceAll("");
			}
		    return  result;
	}
```  

* `\n 回车(\u000a)`
* `\t 水平制表符(\u0009)`
* `\s 空格(\u0008)`
* `\r 换行(\u000d)`
