---
external: false
title: Java学习之路-入门
date: 2022-10-26
---
# 第一章 初始Java


## 前言
Java语言是美国Sun公司（Stanford University Network），在1995年推出的高级的编程语言。所谓编程语言，是计算机的语言，人们可以使用编程语言对计算机下达命令，让计算机完成人们需要的功能。 

---


## 一、Java帝国的诞生？
>Java是一门面向对象的编程语言，不仅吸收了C++语言的各种优点，还摒弃了C++里难以理解的多继承、指针等概念，因此Java语言具有功能强大和简单易用两个特征。Java语言作为静态面向对象编程语言的代表，极好地实现了面向对象理论，允许程序员以优雅的思维方式进行复杂的编程。
### 1.Java初生
1995年的网页简单而粗糙，缺乏互动性。
图形界面的程序(Applet)

Java 2 标准版(J2SE)：去占领桌面
Java 2 移动版(J2ME)：去占领手机
Java 2 企业版(J2EE)：去占领服务器
### 2.Java发展
构造工具：Ant，Maven，Jekins
应用服务器：Tomcat，Jetty，Jboss，Websphere，weblogic
Web开发：Struts，Spring，Hibernate，myBatis
开发工具：Eclipse，Netbean，intellij idea，Jbuilder
......
> 三高：高可用、高性能、高并发
## 二、Java特性和优势
>简单性
>面向对象
>可移植性
>高性能
>分布式
>动态性(反射)
>多线程
>安全性
>健壮性

## 三、Java三大版本
Write Once、Run Anywhere

JavaSE：标准版（桌面程序，控制台开发......）
JavaME：嵌入式开发（手机，小家电......）[现今被淘汰]
JavaEE：E企业级开发（web前端，服务器开发）
## 四、JDK JRE JVM
JDK：Java Development Kit
JRE：Java Runtime Environment
JVM：JAVA Virtual Machine

![SANJ](/assets/Java学习之路-入门/7e411143eec6471684d357a2af332072.png)
## 五、搭建开发环境
### 1.JDK下载卸载和安装
1.1  卸载JDK
> 1. 删除java的安装路径
> 2. 删除Java_HOME
>3. 删除path下关于java的目录
>4. 验证：Win + R -> cmd -> java -version

1.2 安装JDK
> 1. 注册Oracle账号
> 2. 找到电脑对应的版本
> 3. 双击安装
> 4. 更改路径(**记住**)
>![iuimg](/assets/Java学习之路-入门/1b099a5972964dbab1a5d91c6fbe0b66.png) 

### 2.配置环境变量
> **有些版本不需配置环境变量**
 	1.我的电脑-->右键-->属性
 	2.环境变量-->系统变量-->新建
	![环境变量](/assets/Java学习之路-入门/4c621708d8554c0abbadc5697de6afca.png) 
	3.变量名：JAVA_HOME-->变量值:JDK安装地址
	![新建系统变量](/assets/Java学习之路-入门/61d38c81fd2e4e2e9885ded2fffd174d.png) 
	4.配置path变量(%%:表示应用)
	![编辑环境变量](/assets/Java学习之路-入门/1aa3bae71fbe4327a9f1139aec4150f4.png) 
**注：没有jre文件可不用配置**
	**扩展：Win + +：放大镜**
	5.测试JDK是否安装成功：Win+R-->cmd-->java -version
 JDK下载路径: [(https://www.oracle.com/java/technologies/downloads/#java8)](https://www.oracle.com/java/technologies/downloads/#java8)

### 3.JDK目录介绍
![JDK目录](/assets/Java学习之路-入门/8f14c68c8b0f41309a8023417aae817d.png) 
1、bin目录
>javac.exe（Java编译器）--- 将编写好的java文件（.java文件）编译成java[字节码](https://baike.baidu.com/item/%E5%AD%97%E8%8A%82%E7%A0%81/9953683?fr=aladdin)文件（.class文件）
>java.exe（Java运行工具）--- 启动java[虚拟机](https://baike.baidu.com/item/%E8%99%9A%E6%8B%9F%E6%9C%BA/104440?fr=aladdin)进程（JVM）,相当于一个操作系统，专门负责运行.class字节码文件
**重要掌握以下两个程序，其他的仅做了解**

2、db目录
>该目录是一个小型数据库，在Java中引入了一个开源的数据库管理系统——JavaDB。因此在学习JDBC时无需安装额外的数据库软件，直接使用JavaDB即可。

3、jre目录（Java Runtime Environment）**有些版本没有这个目录，包含在斌目录下**
>该目录为Java运行时的环境[根目录](https://baike.baidu.com/item/%E6%A0%B9%E7%9B%AE%E5%BD%95/6061330?fr=aladdin)，它包含Java虚拟机、运行时的类包、Java应用启动器和一个bin目录，但不包含开发环境中的开发工具。

4、include
>存放开放JDK所使用的c语言的头文件。

5、lib目录（library）
>Java类库或库文件，是开发工具使用的归档包文件。

6、src.zip文件与[javafx](https://baike.baidu.com/item/JavaFX/4231502?fr=aladdin)-src.zip文件
>存放JDK核心类源代码和JavaFX源代码，通过这两个文件可以查看Java基础类的源代码。
## 六、HelloWorld 及 简单语法规则
1、创建一个Java文件
![Hello.java](/assets/Java学习之路-入门/e7e77cf35d8144c0b54b782f77730c30.png)
2、编写代码

```java
public class Hello{
    public static void main(String[] args){
        System.out.print("Hello,World!");
    }
}
```
3、编译

 - 进入Hello.java文件的目录 --> 在所在文件的目录输入cmd
 - 编译.class文件 -->javac 文件名.java
 ![javac](/assets/Java学习之路-入门/34e4815b017142749bf881e440bb125f.png)
 ![.class](/assets/Java学习之路-入门/9cee09f286304825bc474959e95975de.png)
3.运行class文件
 ![run](/assets/Java学习之路-入门/cbd2e648f4c24006bed6af3e798e4d87.png)
**注：可能会遇到的情况**
 - 每个单词的大小写不能出现问题，Java大小写是敏感的
 - 尽量使用英文
 - 文件名 和 类名必须保证一致，并且首字母大写（方法名小写）
 - 符号不能使用中文 
 
## 七、Java 程序运行机制
 - 编译型
 运行编译型语言是相对于解释型语言存在的，编译型语的首先将源代码编译生成机器语言，再由机器运行机器（二进制）。像C/C++等都是编译型语言。
 编译型语言：程序在执行之前需要一个专门的编译过程，把程序编译成为机器语言的文件，运行时不需要重新翻译，直接使用编译的结果就行了。程序执行效率高，依赖编译器，跨平台性差些。如C、C++、Delphi等。
 - 解释型
解释型语言：程序不需要编译，程序在运行时才翻译成机器语言，每执行一次都要翻译一次。因此效率比较低。比如Basic语言，专门有一个解释器能够直接执行Basic程序，每个语句都是执行的时候才翻译。(在运行程序的时候才翻译，专门有一个解释器去进行翻译，每个语句都是执行的时候才翻译。效率比较低，依赖解释器，跨平台性好。)
**Java是同时具备上面两种特点**

Java程序运行机制
 ![Java运算机制](/assets/Java学习之路-入门/4f6096c383284fd39294c2ed08c35017.png)

## 八、IDEA安装和介绍
### 1.介绍
 1. 什么是IDE?
 1、编译器：用来编写代码，并且给代码着色，以方便阅读；
 2、调试器：观察程序的每一个运行步骤，发现程序的逻辑错误；
 3、项目管理工具：对程序涉及到的所有资源进行管理，包括源文件、图片、视频、第三方库等；
 4、漂亮的界面：各种按钮、面板、菜单、窗口等控件整齐排布，操作更方便。
 这些工具通常打包在一起，统一发布和安装，例如Visual Studio、Dev C++、Xcode、Visual C++ 6.0、C-Free、Code::Blocks 等，它们统称为集成开发环境（IDE，Integrated Development Environment）。
 
 **在实际开发中，我一般也是使用集成开发环境，而不是单独地使用编译器。**
 
 2. IDEA(IntelliJ IDEA)介绍
  IDEA是java编程语言的集成开发环境。IntelliJ在业界被公认为最好的Java开发工具，尤其在智能代码助手、代码自动提示、重构、JavaEE支持、各类版本工具(git、svn等)、JUnit、CVS整合、代码分析、 创新的GUI设计等方面的功能可以说是超常的。IDEA是JetBrains公司的产品，这家公司总部位于捷克共和国的首都布拉格，开发人员以严谨著称的东欧程序员为主。它的旗舰版（收费，限30天免费试用）还支持HTML，CSS，PHP，MySQL，Python等。社区版(免费)只支持Java,Kotlin等少数语言。

**IDEA下载地址： [https://www.jetbrains.com/](https://www.jetbrains.com/)**
### 2.安装

 1. 双击**idealC-2020.2.4.exe**安装文件
 ![安装](/assets/Java学习之路-入门/079489e77abe41689ea16786fbd10155.png)

 1. 点击下一步(Next >)
  ![next](/assets/Java学习之路-入门/c320ff0a64c147d489a2aa4250d23bd5.png)
 
 2. 选择文件目录，然后点击Next
 ![目录](/assets/Java学习之路-入门/6a063c58425f4b15b44206fabddf44bc.png)
 3. 选择配置
 ![配置](/assets/Java学习之路-入门/696b3662fb49471ca09fd25b9cef7f3c.png)

 **1、Create Desktop Shortcut**所指向的选项代表根据你的电脑选择对应的位数，这里我选择64位。  
 **2、Create Associations**所指向的选项代表关联文件，如果你打钩了，以后你双击电脑上的.java文件就会用它打开。  
 **3、Download and install 32-bit JetBrains Runtime**所指向的选项代表是否由JetBrain自动下载一个jre。  
 **其余的我们暂不选择**
 

 4. 安装成功
  ![succ](/assets/Java学习之路-入门/7d98cb1ce57f4ae98a52adabf3532aa1.png)

---

# 总结
以上就是今天要讲的内容，本文仅仅简单学习了Java的入门知识！