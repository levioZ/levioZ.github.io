---
layout: post
title:  "springSecurity Oauth2"
date:   2016-04-27 15:30:54
categories: spring
tags: spring Security
---
* content
{:toc}

# Spring Security是什么？
>**简单来说，Spring Security就是利用filter对url进行拦截，以此来达到权限控制的目的。**  

## 有几种实现方式？  
+ 使用数据库
+ 使用配置文件
+ 使用filter拦截
+ 修改源码  
**第一种是实际应用中经常使用的，配置文件多适用于测试，至于用filter拦截和修改源码一般不推荐。**

## 核心流程  

>登陆验证拦截器**AuthenticationProcessingFilter**，管理登录验证。  
>资源管理拦截器**AbstractSecurityInterceptor**，管理访问资源。  
>**AuthenticationManager**，**accessDecisionManager**等组件是一些拦截器的具体实现。  
<br>
用户登陆，会被**AuthenticationProcessingFilter**拦截,调用**AuthenticationManager**的实现,而**AuthenticationManager**会调用**ProviderManager**来获取用户验证信息（不同的Provider调用的服务不同,因为这些信息可以是在数据库上，可以是在LDAP服务器上，
可以是xml配置文件上等)。如果验证通过后会将用户的权限信息封装一个**User**放到**spring**的全局缓存**SecurityContextHolder**中，以备后面访问资源时使用。
<br>
访问资源（即授权管理），访问**url**时，会通过**AbstractSecurityInterceptor**拦截器拦截，其中会调用**FilterInvocationSecurityMetadataSource**的方法来获取被拦截url所需的全部权限，在调用授权管理器**AccessDecisionManager**，这个授权管理器会通过spring的全局缓存**SecurityContextHolder*获取用户的权限信息，还会获取被拦截的url和被拦截url所需的全部权限，然后根据所配的策略（有：一票决定，一票否定，少数服从多数等），如果权限足够，则返回，权限不够则报错并调用权限不足页面。





# OAuth2是什么？  
    Oauth2是 Oauth协议的下一版本，但是并不向后兼容Oauth1.0.  OAuth2.0关注客户端开发者的建议性。要么通过组织在资源拥有者和HTTP服务商之间的被批准的交互动作代表用户，要么允许第三方应用代表用户获得访问的权限。同时为Web应用，桌面应用和手机，和起居室设备提供的专门的认证流程 ----------百度百科  


**简单的来说就是大话日常生活中的第三方登录，例如QQ，微信登录**  

## 名词解释  
+ **Third-party application**： 第三方应用程序，即clinet
+ **HTTP service**:  HTTP服务提供商, 即 服务提供商
+ **Resource Owner**： 资源所有者，即 user
+ **User Agent**： 用户代理
+ **Authorization server**：认证服务器，即服务提供商专门用来处理认证的服务器
+ **Resource server**：资源服务器，即服务提供商存放用户生成的资源的服务器。它与认证服务器，可以是同一台服务器，也可以是不同的服务器  

## OAuth的思路
>OAuth在"客户端"与"服务提供商"之间，设置了一个授权层（authorization layer）。"客户端"不能直接登录"服务提供商"，只能登录授权层，以此将用户与客户端区分开来。"客户端"登录授权层所用的令牌（token），与用户的密码不同。用户可以在登录的时候，指定授权层令牌的权限范围和有效期。
"客户端"登录授权层以后，"服务提供商"根据令牌的权限范围和有效期，向"客户端"开放用户储存的资料。  

## 运行流程  
* 用户打开客户端以后，客户端要求用户给予授权
* 用户同意给予客户端授权
* 客户端使用上一步获得的授权，向认证服务器申请令牌
* 认证服务器对客户端进行认证以后，确认无误，同意发放令牌
* 客户端使用令牌，向资源服务器申请获取资源
* 资源服务器确认令牌无误，同意向客户端开放资源  

## 客户端的授权模式
* 授权码模式（authorization code）
* 简化模式（implicit）
* 密码模式（resource owner password credentials）
* 客户端模式（client credentials）
