---
title: "解决Maven包冲突问题"
date: 2020-06-26T17:52:27+08:00
draft: false
---


1.JVM（java虚拟机）的作用：

只执行class文件，也就是字节码文件，如果遇到了新类就会去相应类路径classPath里找。各个类的字节码文件一般都打包在jar包里。

2.传递性依赖：类依赖其他类

maven的包管理解决了传递性依赖和包冲突：

1）传递性依赖的解决：

maven会告诉jvm到底去哪找，根据groupId/artifactId/version去中央仓库可以找到自己想要的jar包，对应的jar包还有其pom文件，文件里会说明它又依赖了什么jar包，所以整棵依赖树都会被下载下来

2）包冲突的解决：

【1】包冲突是什么？版本号不同的包名同时出现在classPath里，则jvm不知道到底采用哪个包

【2】包冲突的表现：

**AbstractMethodError**

**NoClassDefFoundError**

**ClassNotFoundException**

**LinkageError**

**NoSuchMethodError**

【3】看包依赖的方法

法1：看右侧maven的dependencies

![](../img/way1_dependencies.png)

法2：命令行里执行mvn dependency:tree 看到的是maven解决冲突之后的结构

![](../img/way2.png)

【4】
解决冲突的原则：

选择距离项目最近的jar包

当距离项目一样近时，选前者

【5】实例：

![](../img/instance.png)

因为此时既依赖了0.1版本的C包，又依赖了0.2版本的C包，所以产生了包冲突

所以maven在解决包冲突的时候，选择了较近的0.1版本的C包，而舍弃了高版本

当高版本的jar包里有我们需要的方法时，此时就会报错，要想采用高版本的jar包，有以下几种方式：

① 直接依赖0.2版本的C包，修改pom.xml文件的dependencies

```xml
<dependency>    
    <groupId>com.github.hcsp</groupId>    
    <artifactId>test-library-c</artifactId>    
    <version>0.2</version>    
</dependency>
```

② 排除掉0.1版本的C包

```xml
<dependency>
    <groupId>com.github.hcsp</groupId>
    <artifactId>test-library-d</artifactId>
    <version>0.1</version>
    <exclusions>
        <exclusion>
            <groupId>com.github.hcsp</groupId>
            <artifactId>test-library-c</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

③ 采用IDEA的Maven Helper插件

打开pom，命令行上方有dependency Analyzer 点Reimport按钮，则显示了maven冲突的地方，**选中要排除的那个**,然后右键exclude