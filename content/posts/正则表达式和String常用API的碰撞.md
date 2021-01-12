---
title: "正则表达式和String常用API的碰撞"
date: 2021-01-12T11:16:15+08:00
draft: false
---

最近工作上有遇到一个需要截取想要的字符串的情况，第一时间想到了正则表达式，后来用着用着，发现String的API真是太好用了，还比正则简单一些，记录一下心得。

当时的场景是需要截取全限定类名，大概格式是这样的：

AuthController可以认为是类名，login()是方法名

原结果    public java.lang.String org.XXX.XXX.web.xxx.AuthController.login()

所需结果  org.XXX.XXX.web.xxx.AuthController

也就是要从org开始取，取到类名结束

这个时候String的API就开始大显神通了，主要用到了split(char ch)、substring(startIndex , endIndex)、lastIndexOf(String str)

先用空格截取成三部分，最后一部分就是全限定类名加方法，通过左括号进行截取，再通过.进行截取，这样就得到最终结果了。

```java
String[] strArray = str.split(" ");
String methodName = strArray[strArray.length -1];
String bracketLeft = methodName.substring(0, methodName.lastIndexOf('(')); //此处为单引号！
String fullQualClassName = bracketLeft.substring(0, bracketLeft.lastIndexOf('.'));
```

<u>PS：split方法如果传参为“|”  “.”等特殊字符的时候，一定要记得//转义</u> 

<u>这个地方就有踩坑，可以跑一个main方法检验一下，节省时间，这样就不会发布之后才发现有问题</u>



常用的String API总结在这，有遗忘再翻阅

**字符数组相关：**

 ![](../img/StringArrayRelatedAPI.png) 

index从0开始

**字节数组相关：**

 ![](../img/ByteArrayRelatedAPI.png) 

**字符串比较：**

 ![](../img/StringCompareAPI.png) 

**字符串查找：**

 ![](../img/StringFindAPI.png) 

**字符串替换：**

 ![](../img/StringReplaceAPI.png) 

**字符串截取：**

 ![](../img/StringSubstringAPI.png) 

endIndex不包含该位，不可以是负数

**字符串拆分：**

 ![](../img/StringSplitAPI.png) 

如果用""(空字符串)拆分，则按照每个字符进行拆分

如果敏感字符拆不了，则用转义字符

**其他方法：**

 ![](../img/StringOtherAPI.png) 

用户进行数据输入时可能有无用的空格内容--trim

某些情况下要求用户输入的数据长度有限制，用此方式判断--length

<u>注：数组对象.length; String 对象.length(); 一个有括号，一个没有</u>

如果isEmpty()不方便，可以使用"".equals(str)

String类少了一个重要方法initcap()功能，首字母大写，其余字母小写
