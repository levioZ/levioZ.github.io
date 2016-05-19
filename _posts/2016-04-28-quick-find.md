---
layout: post
title:  "Quickly Find"
date:   2016-04-28 18:20:00
categories:  QuicklyFind
tags: command keyboard shortcuts
---
* content
{:toc}  

## Intelllij Idea  

* 查找整个工程中使用地某一个类、方法或者变量的位置  `alt+F7`
* override/implement `ctrl+o`
* find method `ctrl+F12`

## jekyll  

* hot run server  `jekyll serve --watch`

## Atom

* copy and move  `ctrl+shift+d`


## Eclipse  

* copy and move `ctrl+alt+↓`  
* move `alt+↓/↑`

## Git  

* 查看远程分支  

```
  $ git branch -a  
  * defaultSpringSecurityconfiguration
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/defaultSpringSecurityconfiguration
  remotes/origin/master
```  

* 删除远程分支及tag

```
  $ git push origin --delete <branchName>
```  

```
  $ git push origin --delete tag <tagname>
```  

* 回退上次的commit  

```
$ git log -3
commit fa782074fad9422afc599d2901ef8fcd8c833bc1
Author: elili <eli@crownpartners.com>
Date:   Thu May 19 09:23:43 2016 +0800

    Revert "no message"

    This reverts commit adbaa34f14f9d8ade9c46708d9405007e7a19c9f.

commit adbaa34f14f9d8ade9c46708d9405007e7a19c9f
Author: elili <eli@crownpartners.com>
Date:   Thu May 19 09:03:53 2016 +0800

    no message

commit 53c6b72f25502fc00211ecce28438cd09e3ceda4
Author: elili <eli@crownpartners.com>
Date:   Wed May 18 14:44:30 2016 +0800

    init project

elili@EliLi MINGW64 /d/GitDepository/EliLee/github/gradle_springMVC_resful_mybatis (master)
$ git reset --hard 53c6b72f25502fc00211ecce28438cd09e3ceda4
HEAD is now at 53c6b72 init project  

```  


## Mercurial(hg)

## MySql

* **查看端口号**

```
mysql> show variables like 'port'
   -> ;
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port          | 3306  |
+---------------+-------+
1 row in set (0.00 sec)

``` 
