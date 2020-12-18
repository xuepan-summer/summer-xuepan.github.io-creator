---
title: "命令查看oracle事务隔离级别"
date: 2020-12-18T10:10:34+08:00
draft: false
---

出于好奇，想看一下目前项目里oracle使用事务隔离级别是否是默认的，所以用命令验证了一下：
 ![](../img/oracleTransCommand.png) 

注：创建完之后先别commit，直接select即可选出数据

运行结果说明项目里目前没有修改oracle的事务隔离级别，仍然是默认的READ COMMITED读已提交

 ![](../img/oracleTransaction.png) 