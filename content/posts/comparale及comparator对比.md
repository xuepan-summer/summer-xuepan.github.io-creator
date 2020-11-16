---
title: "Comparale及Comparator对比"
date: 2020-11-16T18:21:50+08:00
draft: false
---

**comparable接口:**

```java
public interface Comparable {    
    int compareTo(Object other);
}
```

```java
public interface Comparable<T> {    
    int compareTo(<T> other);
}
```

实现该接口的类必须要覆写compareTo方法

**comparator接口:**

```java
public interface Comparator<T>{
	int compare(T first,T second)
}
```

实现该接口的类必须要覆写compare方法

```java
if (user1.getAge() > user2.getAge()) {    
    return 1;
}
if (user1.getAge() < user2.getAge()) {    
    return -1;
}
return 0;
```

代码可以简化为：

```java
return Integer.compare(user1.getAge(), user2.getAge());
```



```java
Collections.sort(userList, new Comparator<User>() {    
    @Override    
    public int compare(User user1, User user2) {        
        return Integer.compare(user1.getAge(), user2.getAge());    
    }
});
//声明一个匿名内部类，覆写了Comparator接口的compare方法，里面定义了比较的标准
```

可以简化为：

```java
Collections.sort(userList, (user1, user2) -> Integer.compare(user1.getAge(), user2.getAge()));
```

lambda表达式
可以再简化为：Comparator.comparingInt

```java
Collections.sort(userList, Comparator.comparingInt(User::getAge));
```

可以userList.sort，因为Collections.sort方法其实也就是userList.sort()

```java
userList.sort(Comparator.comparingInt(User::getAge));
```

```java
public static <T> void sort(List<T> list, Comparator<? super T> c) {    
    list.sort(c);
}
```
