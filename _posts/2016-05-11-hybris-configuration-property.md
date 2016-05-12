---
layout: post
title:  "Configuring the Behavior of hybris Commerce Suite"
date:   2016-05-11 14:39:00
categories: hybris
tags: property configuration
excerpt: property优先级以及在hybris中如何读取property文件
---
* content
{:toc}

## hybris中是如何加载property文件的？  

众所周知，hybris是基于spring的，so 它也是利用spring来加载的。  

### 那么spring是怎么加载的呢？  

它可以这样做：  

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:context="http://www.springframework.org/schema/context"
   xsi:schemaLocation="
      http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans-4.2.xsd
      http://www.springframework.org/schema/context
      http://www.springframework.org/schema/context/spring-context-4.2.xsd">

      <context:property-placeholder location="classpath:foo.properties" />

</beans>  
```

也可以这样干：  

```xml
<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
  <property name="locations">
    <list>
      <value>classpath:foo.properties</value>
    </list>
  </property>
  <property name="ignoreUnresolvablePlaceholders" value="true"/>
</bean>  
```
或者这样也行：  

```java

@Configuration
@PropertySource("classpath:foo.properties")
public class PropertiesWithJavaConfig {

   @Bean
   public static PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
      return new PropertySourcesPlaceholderConfigurer();
   }
}

```  

### spring又是如何读取的呢？  

在xml中你可以这样做:  

```xml  

<bean id="dataSource">
  <property name="url" value="${jdbc.url}" />
</bean>  

```  

在javabean中你需要这样做：  

```java

@Value( "${jdbc.url}" )
private String jdbcUrl;
```

### hybris 又是如何做的？  

跟spring类似，你只需要这样：  

```xml
<bean class="Foo">
  <property name="bar" value="${key_of_property}"/>
</bean>

<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
  <property name="properties" ref="hybrisProperties"/>
</bean>

```
你也可以自定义它:  

```xml
bean id="testBean" class="org.training.TestBean">
    <property name="value" value="${custom.property}"/>
</bean>
<bean id="customPropertyPlaceholderConfigurer" class="org.training.CustomPropertyPlaceholderConfigurer">
    <property name="properties" ref="hybrisProperties"/>
    <property name="order" value="1000"/>
</bean>
```

**需要注意的是 order 的值必须小于 99999**

```java

package org.training;

import java.util.Properties;
import org.springframework.beans.factory.config.PropertyPlaceholderConfigurer;

public class CustomPropertyPlaceholderConfigurer extends PropertyPlaceholderConfigurer
{
    @Override
    protected String resolvePlaceholder(final String placeholder, final Properties props, final int systemPropertiesMode)
    {
        if("custom.property".equals(placeholder)){
            return "custom.value";
        }
        return null;
    }
}
```  

幸运的是hybris中有一个接口 **ConfigurationService**,通常情况下，我们可以直接使用它。它的默认实现是 **DefaultConfigurationService**.

你可以这样用：  

```java
//fetch the commons configuration instance
Configuration cfg = configurationService.getConfiguration();

//there are various convenience methods
String strgValue = cfg.getString("key");
boolean boolValue = cfg.getBoolean("key");
int intValue = cfg.getInt("key");
BigDecimal bd = cfg.getBigDecimal("key");

//optional default values can be passed as a second parameter
strgValue = cfg.getString("key", "defaultValue");

//listeners can be registered
final ConfigurationListener listener = new ConfigurationListener()
{
    public void configurationChanged(final ConfigurationEvent event)
    {
        //listener gets invoked before and after the value gets changed
        boolean isBefore = event.isBeforeUpdate();
        Object value = event.getPropertyValue();
        String key = event.getPropertyName();
    }
};
((HybrisConfiguration)cfg).addConfigurationListener(listener);
```  

###  hybris中有很多property文件，如local.property，project.property等等，那它们有优先级吗？  

>当然有  

--------------------------------

**place of definition**

local.properties file

**location**  

${HYBRIS_CONFIG_DIR}

**Priority**  

Highest

**Overrides**  

* extension-specific
  * project.properties files  
* project.properties files   
* application code defaults

**Overridden by**  

(N/A)

-------------------------------

**place of definition**

* extension-specific
  * project.properties file

**location**  

${EXTENSION_DIR}

**Priority**  

High

**Overrides**  

* project.properties file
* application code defaults

**Overridden by**  

local.properties file

-----------------------------------

**place of definition**

hybris Platform project.properties file

**location**

${HYBRIS_BIN_DIR}/platform

**Priority**

Medium

**Overrides**

application code defaults

**Overridden by**

* local.properties file
* extension-specific
  * project.properties files

------------------------------

**place of definition**

Application code

**location**

Application code
When a property is not configured, a default value from the application code is used.

**Priority**

Low

**Overrides**

(N/A)

**Overridden by**

* local.properties file
* extension-specific
  * project.properties files
* project.properties file   

-------------------------------------------
