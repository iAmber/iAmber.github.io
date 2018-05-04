---
title: linux相关命令记录
tags: linux
date: 2018-04-28 19:02:54
---
### NetCat 
- transfer file
```
 ## sender:
 nc -l port < filename
 
 ## recevier
 nc [sender_ip] port > filename

```
### 压缩与解压
<!-- more -->

### 文件与目录权限
- chgrp :改变文件所属群组
- chown :改变文件拥有者
- chmod :改变文件的权限, SUID, SGID, SBIT等等的特性
```
  chgrp [-R] dirname/filename ...
  chown [-R] 帐号名称 文件或目录
  chown [-R] 帐号名称:群组名称 文件或目录
  chmod [-R] xyz 文件或目录
```
### 文件内容查阅
```
  cat 由第一行开始显示文件内容
  tac 从最后一行开始显示，可以看出 tac 是 cat 的倒着写!
  nl 显示的时候，顺道输出行号!
  more 一页一页的显示文件内容
  less 与 more 类似，但是比 more 更好的是，他可以往前翻页! head 只看头几行
  tail 只看尾巴几行
  od 以二进制的方式读取文件内容!
  
```
