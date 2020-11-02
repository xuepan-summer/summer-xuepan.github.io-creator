---
title: "Stream总结 & Collections.sort()应用"
date: 2020-11-02T17:43:39+08:00
draft: false
---

学习了Stream之后，打算把Stream如何使用总结一下，便于下次翻阅。

##### 一、Stream的创建操作、中间操作和终结操作

**创建操作产生Stream**

①某collection.stream()

②某stream.of()

③某string.chars()

④IntStream.range() 左闭右开

**中间操作仍返回Stream**

①filter() 过滤

②map() 映射 

eg:map(User::getName)【方法引用】

③sorted()

eg:sorted(Comparator.comparing(某字段).thenComparing(某字段))

**终结操作返回非Stream，包括void**

①forEach()

②count()/max()/min()

③findFirst()/findAny

④anyMatch()/noneMatch()

**collect()**※ 是最常用的

Collectors.toList/toSet/toCollection

eg:Collectors.toCollection(TreeSet::new)

Collectors.groupingBy() 分组

eg:Collectors.groupingBy(Employee::getDepartment)

Collectors.joining() 连接

eg:Collectors.joining(", ")

Collectors.summingInt() 累加求和

eg:Collectors.summingInt(Employee::getSalary)

##### 二、Collections.sort()应用

1.包含两种传参方法

Collections.sort(list)

Collections.sort(list,Comparator)

2.java8新特性结合Collections.sort()

根据User的name对users(User类型的List)进行排序

有以下三种方法：

1.Comparator可以写成匿名内部类，实现compare方法

```java
//1.
Collections.sort(users, new Comparator<User>() {    
    @Override    
    public int compare(User user1, User user2) 
    {        
        return user1.getName().compareTo(user2.getName());    
    }
});
```

2.Comparator可以写成lambda表达式，如果写return的话需要加分号！

2.1是加上了参数类型的，参数表的参数类型可以忽略，如2.2所示

```java
//2.1 复杂
Collections.sort(users, (User user1, User user2) -> {    
    return user1.getName().compareTo(user2.getName());
});
//2.2 简单
Collections.sort(users, (user1, user2) -> user1.getName().compareTo(user2.getName()));
```

3.Comparator可以写成方法引用

```java
//3.
Collections.sort(users, Comparator.comparing(User::getName));
```

##### 三、并发流parallelStream

在正确使用的前提下，可以获得近似线性的性能提升

**但是性能要通过并发度parallelism进行测试，否则不要轻易使用**

一般来说，通过System,currentTimeMillis()来查看时间是否大大减少

