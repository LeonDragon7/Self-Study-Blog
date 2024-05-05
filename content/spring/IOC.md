---
external: false
title: IOC
date: 2023-06-22
---

# 一、IOC概念和原理

## 1. 什么是 IOC

> 1. 控制反转，把对象创建和对象之间的调用过程，交给 Spring 进行管理                                                 
> 2. 使用 IOC 目的：为了耦合度降低                                      
> 3. 做入门案例就是 IOC 实现                                      


## 2. IOC 底层原理

> xml 解析、工厂模式、反射                                                                       

## 3. 画图讲解 IOC 底层原理

![IOC底层原理](/assets/IOC/IOC底层原理.png)

# 二、IOC（BeanFactory 接口）

## 1. IOC 思想基于 IOC 容器完成，IOC 容器底层就是对象工厂                     


## 2. Spring 提供 IOC 容器实现两种方式：（两个接口）

> 1.BeanFactory：IOC 容器基本实现，是 Spring 内部的使用接口，不提供开发人员进行使用                                                            
**加载配置文件时候不会创建对象，在获取对象（使用）才去创建对象**                
> 2.ApplicationContext：BeanFactory 接口的子接口，提供更多更强大的功能，一般由开发人员进行使用                                                
**加载配置文件时候就会把在配置文件对象进行创建**    

## 3. ApplicationContext 接口有实现类

![ApplicationContext接口实现类](/assets/IOC/ApplicationContext接口实现类.png)


# 三、IOC 操作 Bean 管理（概念）

## 1. 什么是 Bean 管理

> 1. Bean 管理指的是两个操作                                                       
> 2. Spring 创建对象                                              
> 3. Spirng 注入属性                                                  

## 2. Bean 管理操作有两种方式

> 1. 基于 xml 配置文件方式实现                                
> 2. 基于注解方式实现                                

# 四、IOC 操作 Bean 管理（基于 xml 方式）

## 1. 基于 xml 方式创建对象

![基于xml方式创建对象](/assets/IOC/基于xml方式创建对象.png)

> 1.在 spring 配置文件中，使用 bean 标签，标签里面添加对应属性，就可以实现对象创建                           
> 2.在 bean 标签有很多属性，介绍常用的属性                     

**id 属性：唯一标识**
**class 属性：类全路径（包类路径）**

> 3.创建对象时候，默认也是执行无参数构造方法完成对象创建                                

## 2. 基于 xml 方式注入属性

> DI：依赖注入，就是注入属性                      

## 3. 第一种注入方式：使用 set 方法进行注入

> 1.创建类，定义属性和对应的 set 方法                                 

```java
/**
* 演示使用 set 方法进行注入属性
*/
public class Book {
    //创建属性
    private String bname;
    private String bauthor;
    //创建属性对应的 set 方法
    public void setBname(String bname) {
    this.bname = bname;
    }
    public void setBauthor(String bauthor) {
    this.bauthor = bauthor;
    }
}
```
> 2.在 spring 配置文件配置对象创建，配置属性注入

```xml
<!--2 set 方法注入属性-->
    <bean id="book" class="com.atguigu.spring5.Book">
    <!--使用 property 完成属性注入
    name：类里面属性名称
    value：向属性注入的值
    -->
    <property name="bname" value="易筋经"></property>
    <property name="bauthor" value="达摩老祖"></property>
</bean>
```

## 4. 第二种注入方式：使用有参数构造进行注入

> 1.创建类，定义属性，创建属性对应有参数构造方法                                               

```java
/**
* 使用有参数构造注入
*/
public class Orders {
    //属性
    private String oname;
    private String address;
    //有参数构造
    public Orders(String oname,String address) {
    this.oname = oname;
    this.address = address;
    }
}
```

> 2.在 spring 配置文件中进行配置                                

```xml
<!--3 有参数构造注入属性-->
<bean id="orders" class="com.atguigu.spring5.Orders">
    <constructor-arg name="oname" value="电脑"></constructor-arg>
    <constructor-arg name="address" value="China"></constructor-arg>
</bean>
```

## 5. p 名称空间注入（了解）

### (1) 使用 p 名称空间注入，可以简化基于 xml 配置方式

> 1.第一步 添加 p 名称空间在配置文件中                                      

![p名称空间注入1](/assets/IOC/p名称空间注入1.png)

> 2.第二步 进行属性注入，在 bean 标签里面进行操作

```xml
<!--2 set 方法注入属性-->
<bean id="book" class="com.atguigu.spring5.Book" p:bname="九阳神功" 
p:bauthor="无名氏"></bean>
```
