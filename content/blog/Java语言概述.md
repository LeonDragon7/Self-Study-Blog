---
external: false
title: Java语言概述
date: 2022-11-10
---

# 一、单行注释、多行注释和文档注释

 - 用于注解说明解释性程序的文字就是注释。
 - **提高了代码的阅读性：调试程序的重要方法**。
 - 注释是一个程序员必须具有的良好编程习惯。
 - 将自己的思想通过注释先整理出来，再用代码去体现。
 
```java
/*
1.java规范的三种注释方式：
单行注释
多行注释
文档注释(java特有)

2.
单行注释和多行注释的作用:
    1、对所写的程序进行解释说明，增强可读性
    2、调试所写的代码

3.特点:单行注释和多行注释，注释的内容不参与编译。

4.文档注释的使用:
    注释内容可以被JDK提供的工具 javadoc 所解析，生成一套以网页文件形式体现的该程序的说明文档。
    操作方式:
        1、在该代码所在文件夹的命令行界面下-javadoc -d 文件名 -author -version 文件名称.java
        2、打开文件名->点击index.html
 
5.多行注释不可以嵌套使用
 */

/**
 * 文档注释
 * @author shkstart
 * @version v1.0
 * 这是我的第一个java程序!
 */

public class Annotation {
    //单行注释

    /*
    多行注释
    多行注释
     */

    /**
     * 文档注释
     */
}
     
```

# 二、Java API的文档

 - API(Application Programming Interface,应用程序编程接口)是java提供的基本编程接口。
 - Java语言提供了大量的基础类，因此Oracle也为这些基础类提供了相应的API文档，用于告诉开发者如何使用这些类，以及这些类里包含的方法。
 - 下载API
 [https://www.oracle.com/java/technologies/downloads/](https://www.oracle.com/java/technologies/downloads/)
![API文档](/assets/Java语言概述/ee22477961e34475b5b61a279e3f91f5.png)

---

# 总结
以上就是今天要讲的内容，本文仅仅简单介绍了Java语言概述。