---
title: "ArrayList扩容"
date: 2020-11-16T18:17:35+08:00
draft: false
---

**总结：**
ArrayList的底层是Object数组，默认容量为10，当往ArrayList里添加数据的时候，才会进行扩容。扩容主要由grow方法实现，扩容为之前的1.5倍左右，然后将之前的数据放到新数组里。

```java
private static final int DEFAULT_CAPACITY = 10;
private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
transient Object[] elementData; // non-private to simplify nested class access
```

**一、3种构造方法：**

1.无参构造

```java
public ArrayList() {    
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}
```

默认是一个空Object数组

2.集合作为参数的构造方法

```java
public ArrayList(Collection<? extends E> c) { 
    elementData = c.toArray();    
    if ((size = elementData.length) != 0) {        
        // c.toArray might (incorrectly) not return Object[] (see 6260652)        
        if (elementData.getClass() != Object[].class)            
            elementData = Arrays.copyOf(elementData, size, Object[].class);    
    } else {        
        // replace with empty array.        
        this.elementData = EMPTY_ELEMENTDATA;    
    }
}
```

当传入集合非空时，将该集合转换后赋值给elementData，否则elementData赋值成一个空Object[]

3.容量作为参数的构造方法

```java
public ArrayList(int initialCapacity) {    
    if (initialCapacity > 0) { 
        this.elementData = new Object[initialCapacity];    
    } else if (initialCapacity == 0) {    
        this.elementData = EMPTY_ELEMENTDATA; 
    } else {        
        throw new IllegalArgumentException("Illegal Capacity: "+  initialCapacity);    
    }
}
```

传入的初始容量大于0，则按照容量大小创建Object数组，如果为0，则直接是空数组，如果参数为负，则报异常

**二、ArrayList扩容机制**

无论以哪种方式创建ArrayList数组，都能发现**在创建过程中没有进行扩容，只有往数组内添加过多元素时，才会进行扩容**

1. 以add方法为例：

```java
//往本list末尾添加指定元素
public boolean add(E e) {...}
//往本list指定位置添加指定元素
public void add(int index, E element) {...}
//往本list末尾添加传参集合的所有元素
public boolean addAll(Collection<? extends E> c) {...}
//往本list指定位置添加传参集合的所有元素
public boolean addAll(int index, Collection<? extends E> c) {...}
```

这四种添加元素的方法都会走到ensureCapacityInternal()方法，前两个方法传参为 size+1，后两个方法传参为size + numNew，numNew是传参集合转成数组之后的length

2. ensureCapacityInternal() & calculateCapacity() & ensureExplicitCapacity

```java
private void ensureCapacityInternal(int minCapacity) {
  ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}

private static int calculateCapacity(Object[] elementData, int minCapacity) {
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
}

private void ensureExplicitCapacity(int minCapacity) {
        modCount++;

        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
}
```

假如刚开始是空的ArrayList，那么调用ensureCapacityInternal(size+1)之后，minCapacity取1和默认容量10的最大值--10，现在先不需要grow()

直到添加第11个元素时，minCapacity = 11,elementData.length = 10，此时进行grow方法的调用

3. grow()

```java
private void grow(int minCapacity) {    
    // overflow-conscious code    
    int oldCapacity = elementData.length; 
    int newCapacity = oldCapacity + (oldCapacity >> 1);    
    if (newCapacity - minCapacity < 0) 
        newCapacity = minCapacity;    
    if (newCapacity - MAX_ARRAY_SIZE > 0)  
        newCapacity = hugeCapacity(minCapacity);    
    // minCapacity is usually close to size, so this is a win:    
    elementData = Arrays.copyOf(elementData, newCapacity);
}
```

原始容量带符号右移一位，则相当于除以2，因此新容量是就容量的**1.5倍左右**。如果是偶数，就是1.5倍。如果是奇数，就舍去小数 例如 33+33/2=33+16=49

如果新容量大于MAX_ARRAY_SIZE，即Integer.MAX_VALUE - 8，就执行hugeCapacity(minCapacity)

最后将原数组内的元素拷贝到新数组里

4. hugeCapacity()

```java
private static int hugeCapacity(int minCapacity) {    
    if (minCapacity < 0) 
        // overflow        
        throw new OutOfMemoryError();    
        return (minCapacity > MAX_ARRAY_SIZE) ? Integer.MAX_VALUE : MAX_ARRAY_SIZE;
}
```

对minCapacity和MAX_ARRAY_SIZE进行比较

若minCapacity大，将Integer.MAX_VALUE作为新数组的大小

若MAX_ARRAY_SIZE大，将MAX_ARRAY_SIZE作为新数组的大小

MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8
