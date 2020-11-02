---
title: "Collection体系的常用类及其背后的数据结构"
date: 2020-06-28T16:20:17+08:00
draft: false
---
![](../img/collection.png)

集合有两个基本接口：Collection和Map

List是一个有序集合，Set里不包含重复元素，Queue是队列，遵循FIFO原则（First In First Out）

**List**

常用方法：

add()：增加元素

retainAll()：保留参数里的所有元素

containsAll()：是否包含参数这个集合里的所有元素

toArray()：转换成数组

1.ArrayList

2.LinkedList

3.Vector&Stack

现已不使用



<u>ArrayList & LinkedList：</u>

1.实现方式：ArrayList 基于数组来实现，LinkedList基于双向链表来实现

2.内存占用：LinkedList比ArrayList 更占内存，因为还需要存储两个引用（指向前面的元素和后面的元素）

**3.随机访问速度：ArrayList 更快**



**Set**

1.EnumSet

该Set里的元素必须都是指定枚举类型的枚举值

2.HashSet

3.TreeSet

<u>HashSet & TreeSet</u>

HashSet是二叉树实现的，加入的元素**不一定**和加入的顺序保持一致，这一点就和ArrayList不一样

TreeSet是SortedSet接口的唯一实现，元素是有序的，可以采用默认的排序方法，也可以自定义排序方法



**Queue**

1.Deque

双端队列，两端均可增加可减少元素

2.PriorityQueue

有优先级的队列，按关键字进行排序，插入元素的时候会自动找到合适位置插入



**Map**

1.HashMap

HashMap的实现没有被同步，所以它是线程不安全的，ConcurrentHashMap是线程安全的

HashMap在resize扩容的时候会造成死循环

2.TreeMap

TreeMap是基于红黑树实现的
