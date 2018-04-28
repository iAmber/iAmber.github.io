---
title: linux相关命令记录
tags: tags
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
### 文件与目录权限
- chgrp :改变文件所属群组
- chown :改变文件拥有者
- chmod :改变文件的权限, SUID, SGID, SBIT等等的特性
```
  chgrp [-R] dirname/filename ...
  chown [-R] 帐号名称 文件或目录
  chown [-R] 帐号名称:群组名称 文件或目录
```
