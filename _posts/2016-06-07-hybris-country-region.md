---
layout: post
title:  "create country and region via impex"
date:   2016-06-06 10:33:00
categories: hybris
author: eli
tags: impex region
excerpt: 如何在impex中配置 country 和 region
---
* content
{:toc}

### 让我们看看需要哪些文件

>这里定义了 country， region ，language ，currency，title, Warehouse ,Vendor的基础数据

![expression](https://raw.githubusercontent.com/levioZ/levioZ.github.io/master/images/essential.png)

### countries.impex

> 这里是OOTB定义的一些 country 和 region 信息,我截取了一部分。你也可以把它们定义在essential-data_xx.impex中


```xml
#
# Import Countries
# Full country list conforming to ISO 3166-1 alpha-2
#
INSERT_UPDATE Country;isocode[unique=true];name[lang=en];active[default=true]
;AD;"Andorra"
;AE;"United Arab Emirates"
;AF;"Afghanistan"
;AG;"Antigua and Barbuda"
;AI;"Anguilla"
;AL;"Albania"
;AM;"Armenia"
;AO;"Angola"
;AQ;"Antarctica"
;AR;"Argentina"
;AS;"American Samoa"
;AT;"Austria"
;AU;"Australia"
;AW;"Aruba"
;AX;"Aland Islands"
;AZ;"Azerbaijan"
;BA;"Bosnia and Herzegovina"
;BB;"Barbados"
;BD;"Bangladesh"
;BE;"Belgium"
;BF;"Burkina Faso"
;BG;"Bulgaria"
;BH;"Bahrain"
;BI;"Burundi"


#
# ISO 3166-2:US
#
INSERT_UPDATE Region;country(isocode);isocode[unique=true];isocodeShort;name[lang=en];active[default=true]
;US;US-AL;AL;"Alabama"
;US;US-AK;AK;"Alaska"
;US;US-AZ;AZ;"Arizona"
;US;US-AR;AR;"Arkansas"
;US;US-CA;CA;"California"
;US;US-CO;CO;"Colorado"
;US;US-CT;CT;"Connecticut"
;US;US-DE;DE;"Delaware"
;US;US-FL;FL;"Florida"
;US;US-GA;GA;"Georgia"
;US;US-HI;HI;"Hawaii"
;US;US-ID;ID;"Idaho"
;US;US-IL;IL;"Illinois"
;US;US-IN;IN;"Indiana"
;US;US-IA;IA;"Iowa"
;US;US-KS;KS;"Kansas"
;US;US-KY;KY;"Kentucky"
;US;US-LA;LA;"Louisiana"
;US;US-ME;ME;"Maine"
;US;US-MD;MD;"Maryland"
;US;US-MA;MA;"Massachusetts"
;US;US-MI;MI;"Michigan"
;US;US-MN;MN;"Minnesota"
;US;US-MS;MS;"Mississippi"
;US;US-MO;MO;"Missouri"
;US;US-MT;MT;"Montana"
;US;US-NE;NE;"Nebraska"
;US;US-NV;NV;"Nevada"
;US;US-NH;NH;"New Hampshire"
;US;US-NJ;NJ;"New Jersey"
;US;US-NM;NM;"New Mexico"
;US;US-NY;NY;"New York"
;US;US-NC;NC;"North Carolina"
;US;US-ND;ND;"North Dakota"
;US;US-OH;OH;"Ohio"
;US;US-OK;OK;"Oklahoma"
;US;US-OR;OR;"Oregon"
;US;US-PA;PA;"Pennsylvania"
;US;US-RI;RI;"Rhode Island"
;US;US-SC;SC;"South Carolina"
;US;US-SD;SD;"South Dakota"
;US;US-TN;TN;"Tennessee"
;US;US-TX;TX;"Texas"
;US;US-UT;UT;"Utah"
;US;US-VT;VT;"Vermont"
;US;US-VA;VA;"Virginia"
;US;US-WA;WA;"Washington"
;US;US-WV;WV;"West Virginia"
;US;US-WI;WI;"Wisconsin"
````

```xml
# Languages
INSERT_UPDATE Language;isocode[unique=true];fallbackLanguages(isocode);active[default=true]
;en;;;
;de;en;;
;ja;en;;
;zh;en;;

# Currencies
INSERT_UPDATE Currency;isocode[unique=true];conversion;digits;symbol
;GBP;1;2;��
;EUR;1;2;���
;USD;1,4;2;$
;JPY;120;0;��

```
