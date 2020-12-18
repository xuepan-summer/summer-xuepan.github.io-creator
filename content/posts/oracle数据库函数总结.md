---
title: "Oracle数据库函数总结"
date: 2020-12-18T10:30:14+08:00
draft: false
---

将平时SQL中遇到的oracle数据函数总结一下，便于遗忘时翻阅

1.lpad & rpad

lpad(string,n,[pad...string])  给定字符左侧添加指定字符至长度n.
rpad(string,n,[pad..string])  给定字符右侧添加指定字符至长度n.

2.substr

substr(string, int a, int b)  给定字符串从位置 a(a为0或1时表示从第一个字符开始截取)开始
截取b长度个字符
substr(string,int a)  从位置a开始，一直截取给定字符串到串尾

3.decode

decode(条件，值1，返回值1，值2，返回值2，..值 n，返回值n，缺省值)"
IF条件=值1 THEN RETURN 返回值1
ELSE IF条件=值2 THEN RETURN返回值2
...
ELSE IF条件=值n then RETURN返回值n
ELSE RETURN 缺省值

4.nvl

nvl(string1, replace_with)  如果string1为null，则返回replace_with，否则返回string1


