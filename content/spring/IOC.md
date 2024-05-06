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

# 五、IOC 操作 Bean 管理（xml 注入其他类型属性）

## 1. 字面量

### (1) null 值

```xml
<!--null 值-->
<property name="address">
    <null/>
</property>
```

### (2) 属性值包含特殊符号

```xml
<!--属性值包含特殊符号
 1 把<>进行转义 &lt; &gt;
 2 把带特殊符号内容写到 CDATA
-->
<property name="address">
    <value><![CDATA[<<南京>>]]></value>
</property>
```

## 2. 注入属性-外部 bean

> 1. 创建两个类 service 类和 dao 类                                          
> 2. 在 service 调用 dao 里面的方法                                             
> 3. 在 spring 配置文件中进行配置                                           

```java
public class UserService {
    //创建 UserDao 类型属性，生成 set 方法
    private UserDao userDao;
    public void setUserDao(UserDao userDao) {
    this.userDao = userDao;
    }
    public void add() {
    System.out.println("service add...............");
    userDao.update();
    }
}
```

```xml
<!--1 service 和 dao 对象创建-->
<bean id="userService" class="com.atguigu.spring5.service.UserService">
    <!--注入 userDao 对象
    name 属性：类里面属性名称
    ref 属性：创建 userDao 对象 bean 标签 id 值
    -->
    <property name="userDao" ref="userDaoImpl"></property>
    </bean>
<bean id="userDaoImpl" class="com.atguigu.spring5.dao.UserDaoImpl"></bean>
```

## 3. 注入属性-内部 bean
> 1.一对多关系：部门和员工                            
> 一个部门有多个员工，一个员工属于一个部门                                                      
> 部门是一，员工是多                                     
> 2.在实体类之间表示一对多关系，员工表示所属部门，使用对象类型属性进行表示                     

```java
//部门类
public class Dept {
    private String dname;
    public void setDname(String dname) {
    this.dname = dname;
    }
}
//员工类
public class Emp {
    private String ename;
    private String gender;
    //员工属于某一个部门，使用对象形式表示
    private Dept dept;
    public void setDept(Dept dept) {
    this.dept = dept;
    }
    public void setEname(String ename) {
    this.ename = ename;
    }
    public void setGender(String gender) {
    this.gender = gender;
    }
}
```

> 3.在 spring 配置文件中进行配置

```xml
<!--内部 bean-->
<bean id="emp" class="com.atguigu.spring5.bean.Emp">
    <!--设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--设置对象类型属性-->
    <property name="dept">
    <bean id="dept" class="com.atguigu.spring5.bean.Dept">
    <property name="dname" value="安保部"></property>
    </bean>
    </property>
</bean>
```

## 4. 注入属性-级联赋值

### (1) 第一种写法

```xml
<!--级联赋值-->
<bean id="emp" class="com.atguigu.spring5.bean.Emp">
    <!--设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--级联赋值-->
    <property name="dept" ref="dept"></property>
</bean>
<bean id="dept" class="com.atguigu.spring5.bean.Dept">
    <property name="dname" value="财务部"></property>
</bean>
```

### (2) 第二种写法

![级联赋值写法2](/assets/IOC/级联赋值写法2.png)

```xml
<!--级联赋值-->
<bean id="emp" class="com.atguigu.spring5.bean.Emp">
    <!--设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--级联赋值-->
    <property name="dept" ref="dept"></property>
    <property name="dept.dname" value="技术部"></property>
</bean>
<bean id="dept" class="com.atguigu.spring5.bean.Dept">
    <property name="dname" value="财务部"></property>
</bean>
```

# 六、IOC 操作 Bean 管理（xml 注入集合属性）

## 1. 注入数组类型属性
## 2. 注入 List 集合类型属性 
## 3. 注入 Map 集合类型属性

### (1) 创建类，定义数组、list、map、set 类型属性，生成对应 set 方法

```java
public class Stu {
    //1 数组类型属性
    private String[] courses;
    //2 list 集合类型属性
    private List<String> list;
    //3 map 集合类型属性
    private Map<String,String> maps;
    //4 set 集合类型属性
    private Set<String> sets;
    public void setSets(Set<String> sets) {
    this.sets = sets;
    }
    public void setCourses(String[] courses) {
    this.courses = courses;
    }
    public void setList(List<String> list) {
    this.list = list;
    }
    public void setMaps(Map<String, String> maps) {
    this.maps = maps;
    }
}
```

### (2) 在 spring 配置文件进行配置

```xml
<!--1 集合类型属性注入-->
<bean id="stu" class="com.atguigu.spring5.collectiontype.Stu">
    <!--数组类型属性注入-->
    <property name="courses">
        <array>
            <value>java 课程</value>
            <value>数据库课程</value>
        </array>
    </property>
 <!--list 类型属性注入-->
 <property name="list">
    <list>
        <value>张三</value>
        <value>小三</value>
    </list>
 </property>
 <!--map 类型属性注入-->
 <property name="maps">
    <map>
        <entry key="JAVA" value="java"></entry>
        <entry key="PHP" value="php"></entry>
    </map>
 </property>
 <!--set 类型属性注入-->
 <property name="sets">
    <set>
        <value>MySQL</value>
        <value>Redis</value>
    </set>
 </property>
</bean>
```

## 4. 在集合里面设置对象类型值

```xml
<bean id="course1" class="com.atguigu.spring5.collectiontype.Course">
    <property name="cname" value="Spring5 框架"></property>
</bean>
<bean id="course2" class="com.atguigu.spring5.collectiontype.Course">
    <property name="cname" value="MyBatis 框架"></property>
</bean>
<!--注入 list 集合类型，值是对象-->
<property name="courseList">
    <list>
        <ref bean="course1"></ref>
        <ref bean="course2"></ref>
    </list>
</property>
```

## 5. 把集合注入部分提取出来

### (1) 在 spring 配置文件中引入名称空间 util

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xmlns:p="http://www.springframework.org/schema/p"
 xmlns:util="http://www.springframework.org/schema/util"
 xsi:schemaLocation="http://www.springframework.org/schema/beans 
http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/util 
http://www.springframework.org/schema/util/spring-util.xsd">
```

### (2) 使用 util 标签完成 list 集合注入提取

<!--1 提取 list 集合类型属性注入-->
<util:list id="bookList">
    <value>易筋经</value>
    <value>九阴真经</value>
    <value>九阳神功</value>
</util:list>
<!--2 提取 list 集合类型属性注入使用-->
<bean id="book" class="com.atguigu.spring5.collectiontype.Book">
    <property name="list" ref="bookList"></property>
</bean>

# 七、IOC 操作 Bean 管理（FactoryBean）

## 1. Spring 有两种类型 bean，一种普通 bean，另外一种工厂 bean（FactoryBean）

## 2. 普通 bean：在配置文件中定义 bean 类型就是返回类型

## 3. 工厂 bean：在配置文件定义 bean 类型可以和返回类型不一样

> 1. 第一步 创建类，让这个类作为工厂 bean，实现接口 FactoryBean                 
> 2. 第二步 实现接口里面的方法，在实现的方法中定义返回的 bean 类型                      

```java
public class MyBean implements FactoryBean<Course> {
    //定义返回 bean
    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("abc");
        return course;
    }
    @Override
    public Class<?> getObjectType() {
        return null;
    }
    @Override
    public boolean isSingleton() {
        return false;
    }
}
```

```xml
<bean id="myBean" class="com.atguigu.spring5.factorybean.MyBean">
</bean>
```

```java
@Test
public void test3() {
    ApplicationContext context =
            new ClassPathXmlApplicationContext("bean3.xml");
    Course course = context.getBean("myBean", Course.class);
    System.out.println(course);
}
```

# 八、IOC 操作 Bean 管理（bean 作用域）

## 1. 在 Spring 里面，设置创建 bean 实例是单实例还是多实例

## 2. 在 Spring 里面，默认情况下，bean 是单实例对象

![默认Bean单例](/assets/IOC/默认Bean单例.png)

## 3. 如何设置单实例还是多实例

> (1) 在 spring 配置文件 bean 标签里面有属性（scope）用于设置单实例还是多实例

### (2) scope 属性值