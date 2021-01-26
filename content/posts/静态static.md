---
title: "静态static"
date: 2020-08-15T17:12:17+08:00
draft: false
---

1. 静态域&实例域 

   **区别**：静态域是共享的，实例域是每个对象独有的。如果User有1000个实例，那么都会共享这一个nextId，每个user的实例都有自己的id。即使没有实例，也仍然存在nextId。

```java
public class User{    
    private static int nextId = 1; //静态域    
    private int id; //实例域
}
```

2. 静态常量

   使用静态常量之后可以直接调用System.out，不需要先得到一个System类型的对象，然后再调用out

   ```java
   public final class System {
   	...
   	public final static PrintStream out = null;
       ...
   }
   ```

3. 静态方法

   + 不能直接访问非静态属性、非静态方法，只能调用静态属性、方法。

   ```java
   public static int getNextId(){    
       return nextId; //只能访问静态变量，不能访问id
   }
   ```

   + 可以这样调用：

   法1：User.getNextId();

   法2：得到User的一个对象user，调用user.getNextId();

   + <u>什么时候使用static?</u>

   当一个类中没有属性，只有方法，可以将所有方法定义成静态方法，这样在调用方法的时候不需要实例化对象，可以直接调用。	

