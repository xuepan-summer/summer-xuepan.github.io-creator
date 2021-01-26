---
title: "TreeSet踩坑"
date: 2020-10-12T17:09:04+08:00
draft: false
---

**1.Set & TreeSet**

- Set：通过HashSet()及equals()达到无序去重的目的
- TreeSet：通过实现Comparable接口的CompareTo()方法达到有序去重的目的

**2.TreeSet可能遇到的问题**

eg:User有两个属性，id和name，

如果只针对于name进行判断，将User存到list中。那么ComapreTo()方法如果重名的User，<u>即使id不同，TreeSet也不会区分出来，仍然认为是同一个User</u>

**所以使用TreeSet的时候，必须把去重条件写清楚！！！**

```java
public class User implements Comparable<User> {   
/**     * 用户ID，数据库主键，全局唯一     */    
private final Integer id;    
/**     * 用户名     */    
private final String name;
public User(Integer id, String name) {
        this.id = id;
        this.name = name;
    }
public Integer getId() {
        return id;
    }

public String getName() {
        return name;
    }
    
	@Override
    public boolean equals(Object o) {
        if (this == o) {
            return true;
        }
        if (o == null || getClass() != o.getClass()) {
            return false;
        }

        User person = (User) o;

        return Objects.equals(id, person.id);
    }
    
	@Override
    public int hashCode() {
        return id != null ? id.hashCode() : 0;
    }
    @Override
    public int compareTo(User o) {
        if (name.compareTo(o.name) == 0) {
            if (this.id != null && !(this.id.equals(o.id))) {
                if (this.id > o.id) {
                    return 1;
                }
                return -1;
            }
        }
        return name.compareTo(o.name);
    }
```




