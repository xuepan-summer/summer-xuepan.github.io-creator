---
title: "BlockingQueue"
date: 2021-01-26T16:12:22+08:00
draft: false
---

项目中遇到了使用阻塞队列，但是自己对API还不是很熟练，所以对照源码及注释，将API整理一下，方便翻阅。

BlockingQueue是继承了Queue的一个接口，其实现类有ArrayBlockingQueue 、LinkedBlockingQueue 、LinkedBlockingDeque等，也遵照队列的先进先出原则。

API大概分为以下四类：

1. 第一类

add(E e)    添加元素，超出长度则抛异常IllegalStateException

remove()  取出并移除队首元素，队列为空则抛异常NoSuchElementException

element()  返回队首元素，队列为空则抛异常NoSuchElementException

2. 第二类

**使用容量受限的队列时，更推荐使用offer()**

offer(E e)   添加元素，成功返回true，超出长度返回false，不插入，不报错

poll()    取出并移除队首元素，队列为空返回null

peek()  返回队首元素，队列为空返回null

3. 第三类

put(E e)  添加元素，队列满则阻塞，直到有空位插入为止

take()      取出并移除队首元素，队列空则阻塞，直到有元素

4. 第四类

offer(E e, long timeout, TimeUnit unit)  队列已满无法插入时，等待定义的单位时间数，如果还满则返回false

poll(long timeout, TimeUnit unit)  队列无元素时，等待定义的单位时间数，无可取元素则返回null