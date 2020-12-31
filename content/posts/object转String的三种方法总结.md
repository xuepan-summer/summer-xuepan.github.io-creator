---
title: "Object转String的三种方法总结"
date: 2020-12-31T16:32:00+08:00
draft: false
---

在项目里遇到了将Object数组里的内容分别转换成所需类型的问题，发现Object转String可没有想象的那么简单，还需要考虑到null的情况，所以好好总结了一下。

1. Object.toString()

Object类里的toString()方法是每个继承了Object的类都有的，可以覆写，使得每个类有自己的toString实现

如果对象为null，会抛出**NullPointerException**，因为null不能再去调用方法或者变量了

2. (String)Object

强制类型转换

这个object对象必须能够转换成String类型，否则会抛异常**ClassCastException**

3. String.valueOf(Object)

即使object为null，也不会有问题
```
public static String valueOf(Object obj) {

 return (obj == null) ? "null" : obj.toString();  

}
```
注意：如果真的是空对象，**会返回“null”而不是null**