---
external: false
title: JDBC和数据库连接池
date: 2023-05-18
---

# 一、JDBC 概述

## 1. 基本介绍

> 1. JDBC为访问不同的数据库提供了统一的接口，为使用者屏蔽了细节问题。                       
> 2. Java程序员使用JDBC,可以连接任何提供了JDBC驱动程序的数据库系统，从而完成对数据库的各种操作。                   
> 3. JDBC的基本原理图[重要!]                    
![JDBC原理示意图](/assets/JDBC/JDBC原理示意图.png)

## 2. 模拟JDBC

```java
package com.hspedu.jdbc.myjdbc;

/**
 * 我们规定的jdbc接口(方法)
 */
public interface JdbcInterface {

    //连接
    public Object getConnection() ;
    //crud
    public void crud();
    //关闭连接
    public void close();
}
```

```java
package com.hspedu.jdbc.myjdbc;

/**
 * mysql 数据库实现了jdbc接口 [模拟] 【mysql厂商开发】
 */
public class MysqlJdbcImpl implements  JdbcInterface{
    @Override
    public Object getConnection() {
        System.out.println("得到 mysql 的连接");
        return null;
    }

    @Override
    public void crud() {
        System.out.println("完成 mysql 增删改查");
    }

    @Override
    public void close() {
        System.out.println("关闭 mysql 的连接");
    }
}
```

```java
package com.hspedu.jdbc.myjdbc;

/**
 * @author 韩顺平
 * @version 1.0
 * 模拟oracle数据库实现 jdbc
 */
public class OracleJdbcImpl implements  JdbcInterface {
    @Override
    public Object getConnection() {
        System.out.println("得到 oracle的连接 升级");
        return null;
    }

    @Override
    public void crud() {
        System.out.println("完成 对oracle的增删改查");
    }

    @Override
    public void close() {
        System.out.println("关闭 oracle的连接");
    }
}
```

```java
package com.hspedu.jdbc.myjdbc;

import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Properties;
import java.util.Scanner;
public class TestJDBC {
    public static void main(String[] args) throws Exception {
        //完成对mysql的操作
        JdbcInterface jdbcInterface = new MysqlJdbcImpl();
        jdbcInterface.getConnection(); //通过接口来调用实现类[动态绑定]
        jdbcInterface.crud();
        jdbcInterface.close();


        //完成对oracle的操作
        System.out.println("==============================");
        jdbcInterface = new OracleJdbcImpl();
        jdbcInterface.getConnection(); //通过接口来调用实现类[动态绑定]
        jdbcInterface.crud();
        jdbcInterface.close();
    }
}
```

## 3. JDBC 带来的好处

- 如果Java直接访问数据库(示意图)
![Java直接访问数据库](/assets/JDBC/Java直接访问数据库.png)

**JDBC带来的好处(示意图)**

- 说明：JDBC是Java提供一套用于数据库操作的接口APl, Java程序员只需要面向这套接口编程即可。不同的数据库厂商,需要针对这套接口,提供不同实现。

![JDBC带来的好处](/assets/JDBC/JDBC带来的好处.png)

> JDBC API是一系列的接口，它统一和规范了应用程序与数据库的连接、执行SQL语句，并到得到返回结果等各类操作,相关类和接口在java.sql与javax.sql包中          

![JDBCAPI1](/assets/JDBC/JDBCAPI1.png)

![JDBCAPI2](/assets/JDBC/JDBCAPI2.png)

# 二、JDBC 快速入门

## 1. JDBC 程序编写步骤

> 1. 注册驱动–加载Driver类                  
> 2. 获取连接–得到Connection（java程序和数据库之间的连接）                 
> 3. 执行增删改查–发送SQL给mysql执行              
> 4. 释放资源–关闭相关连接                     

## 2. JDBC 第一个程序

- 通过jdbc对表actor 进行添加，删除和修改操作

```java
package com.hspedu.jdbc;

import com.mysql.jdbc.Driver;

import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

/**
 * 这是第一个Jdbc 程序，完成简单的操作
 */
public class Jdbc01 {
    public static void main(String[] args) throws SQLException {

        //前置工作： 在项目下创建一个文件夹比如 libs
        // 将 mysql.jar 拷贝到该目录下，点击 add to project ..加入到项目中
        //1. 注册驱动
        Driver driver = new Driver(); //创建driver对象

        //2. 得到连接
        //(1) jdbc:mysql:// 规定好表示协议，通过jdbc的方式连接mysql
        //(2) localhost 主机，可以是ip地址
        //(3) 3306 表示mysql监听的端口
        //(4) hsp_db02 连接到mysql dbms 的哪个数据库
        //(5) mysql的连接本质就是前面学过的socket连接
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        //将 用户名和密码放入到Properties 对象
        Properties properties = new Properties();
        //说明 user 和 password 是规定好，后面的值根据实际情况写
        properties.setProperty("user", "root");// 用户
        properties.setProperty("password", "hsp"); //密码
        Connection connect = driver.connect(url, properties);

        //3. 执行sql
        //String sql = "insert into actor values(null, '刘德华', '男', '1970-11-11', '110')";
        //String sql = "update actor set name='周星驰' where id = 1";
        String sql = "delete from actor where id = 1";
        //statement 用于执行静态SQL语句并返回其生成的结果的对象
        Statement statement = connect.createStatement();
        int rows = statement.executeUpdate(sql); // 如果是 dml 语句，返回的就是影响行数

        System.out.println(rows > 0 ? "成功" : "失败");

        //4. 关闭连接资源
        statement.close();
        connect.close();
    }
}
```

# 三、获取数据库连接5种方式

## 1. 方式1

```java
    //方式1
    @Test
    public void connect01() throws SQLException {
        Driver driver = new Driver(); //创建driver对象
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        //将 用户名和密码放入到Properties 对象
        Properties properties = new Properties();
        //说明 user 和 password 是规定好，后面的值根据实际情况写
        properties.setProperty("user", "root");// 用户
        properties.setProperty("password", "hsp"); //密码
        Connection connect = driver.connect(url, properties);
        System.out.println(connect);
    }
```

## 2. 方式2

```java
    //方式2
    @Test
    public void connect02() throws ClassNotFoundException, IllegalAccessException, InstantiationException, SQLException {
        //使用反射加载Driver类 , 动态加载，更加的灵活，减少依赖性（把forName后的信息放在配置文件上更加方便）
        Class<?> aClass = Class.forName("com.mysql.jdbc.Driver");
        Driver driver = (Driver)aClass.newInstance();

        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        //将 用户名和密码放入到Properties 对象
        Properties properties = new Properties();
        //说明 user 和 password 是规定好，后面的值根据实际情况写
        properties.setProperty("user", "root");// 用户
        properties.setProperty("password", "hsp"); //密码

        Connection connect = driver.connect(url, properties);
        System.out.println("方式2=" + connect);
    }
```

## 3. 方式3

- 使用DriverManager 替代 driver 进行统一管理

![DriverManager](/assets/JDBC/DriverManager.png)

```java
//方式3 使用DriverManager 替代 driver 进行统一管理
@Test
public void connect03() throws IllegalAccessException, InstantiationException, ClassNotFoundException, SQLException {

    //使用反射加载Driver
    Class<?> aClass = Class.forName("com.mysql.jdbc.Driver");
    Driver driver = (Driver) aClass.newInstance();

    //创建url 和 user 和 password
    String url = "jdbc:mysql://localhost:3306/hsp_db02";
    String user = "root";
    String password = "hsp";

    DriverManager.registerDriver(driver);//注册Driver驱动

    Connection connection = DriverManager.getConnection(url, user, password);
    System.out.println("第三种方式=" + connection);
} 
```

## 4. 方式4

```java
//方式4: 使用Class.forName 自动完成注册驱动，简化代码
//这种方式获取连接是使用的最多，推荐使用
@Test
public void connect04() throws ClassNotFoundException, SQLException {
    //使用反射加载了 Driver类
    //在加载 Driver类时，完成注册
    /*
        源码: 1. 静态代码块，在类加载时，会执行一次.
        2. DriverManager.registerDriver(new Driver());
        3. 因此注册driver的工作已经完成
        static {
            try {
                DriverManager.registerDriver(new Driver());
            } catch (SQLException var1) {
                throw new RuntimeException("Can't register driver!");
            }
        }
     */
    Class.forName("com.mysql.jdbc.Driver");

    //创建url 和 user 和 password
    String url = "jdbc:mysql://localhost:3306/hsp_db02";
    String user = "root";
    String password = "hsp";
    Connection connection = DriverManager.getConnection(url, user, password);

    System.out.println("第4种方式~ " + connection);

}
```

> 1. mysqL驱动5.1.6 可以无需 CLass . forName("com.mysql.jdbc.Driver");             
> 2. 从jdk1.5以后使用了jdbc4,不再需要显示调用class.forName()注册驱动而是自动调用驱动jar包下META-INF\servicesViava.sql.Driver文本中的类名称去注册                
> 3. 建议还是写上 CLass . forName("com.mysql.jdbc.Driver"),更加明确             

## 5. 方式5

```java
//方式5 , 在方式4的基础上改进，增加配置文件，让连接mysql更加灵活
@Test
public void connect05() throws IOException, ClassNotFoundException, SQLException {

    //通过Properties对象获取配置文件的信息
    Properties properties = new Properties();
    properties.load(new FileInputStream("src\\mysql.properties"));
    //获取相关的值
    String user = properties.getProperty("user");
    String password = properties.getProperty("password");
    String driver = properties.getProperty("driver");
    String url = properties.getProperty("url");

    Class.forName(driver);//建议写上

    Connection connection = DriverManager.getConnection(url, user, password);

    System.out.println("方式5 " + connection);
}
```

# 四、ResultSet[结果集]

## 1. 基本介绍

> 1. 表示数据库结果集的数据表,通常通过执行查询数据库的语句生成             
> 2. ResultSet对象保持一个光标指向其当前的数据行。最初，光标位于第一行之前              
> 3. next方法将光标移动到下一行，并且由于在ResultSet对象中没有更多行时返回false，因此可以在while循环中使用循环来遍历结果集            

## 2. 应用实例

```java
package com.hspedu.jdbc.resultset_;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.sql.*;
import java.util.Properties;

/**
 * 演示select 语句返回 ResultSet ,并取出结果
 */
@SuppressWarnings({"all"})
public class ResultSet_ {
    public static void main(String[] args) throws Exception {

        //通过Properties对象获取配置文件的信息


        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");

        //1. 注册驱动
        Class.forName(driver);//建议写上

        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);

        //3. 得到Statement
        Statement statement = connection.createStatement();
        //4. 组织SqL
        String sql = "select id, name , sex, borndate from actor";
        //执行给定的SQL语句，该语句返回单个 ResultSet对象
        /*
        +----+-----------+-----+---------------------+
        | id | name      | sex | borndate            |
        +----+-----------+-----+---------------------+-------+
        |  4 | 刘德华    | 男  | 1970-12-12 00:00:00 |
        |  5 | jack      | 男  | 1990-11-11 00:00:00 |
        +----+-----------+-----+---------------------+-------+
         */
        /*
            阅读debug 代码 resultSet 对象的结构


         */
        ResultSet resultSet = statement.executeQuery(sql);
        // 初始时类似与指向表头
        //5. 使用while取出数据
        while (resultSet.next()) { // 让光标向后移动，如果没有更多行，则返回false
            int id  = resultSet.getInt(1); //获取该行的第1列
            //int id1 = resultSet.getInt("id"); 通过列名来获取值, 推荐
            String name = resultSet.getString(2);//获取该行的第2列
            String sex = resultSet.getString(3);
            Date date = resultSet.getDate(4);

            System.out.println(id + "\t" + name + "\t" + sex + "\t" + date);
        }

        //6. 关闭连接
        resultSet.close();
        statement.close();
        connection.close();

    }
}
```

![ResultSet存储解析](/assets/JDBC/ResultSet存储解析.png)

# 五、Statement

## 1. 基本介绍

> 1.Statement对象用于执行静态SQL语句并返回其生成的结果的对象           
> 2.在连接建立后,需要对数据库进行访问，执行命名或是SQL语句，可以通过           
- Statement[存在SQL注入]             
- PreparedStatement[预处理]               
- CallableStatement[存储过程]
> 3.Statement对象执行SQL语句,存在SQL注入风险。                  

![SQL注入](/assets/JDBC/SQL注入.png)

> 4.SQL注入是利用某些系统没有对用户输入的数据进行充分的检查，而在用户输入数据中注入非法的SQL语句段或命令,恶意攻击数据库。             
> 5.要防范SQL注入，只要用 PreparedStatement(从Statement扩展而来)取代Statement就可以了。                   

```java
package com.hspedu.jdbc.statement_;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.sql.*;
import java.util.Properties;
import java.util.Scanner;

/**
 * 演示statement 的注入问题
 */
@SuppressWarnings({"all"})
public class Statement_ {
    public static void main(String[] args) throws Exception {

        Scanner scanner = new Scanner(System.in);

        //让用户输入管理员名和密码
        System.out.print("请输入管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); // 老师说明，如果希望看到SQL注入，这里需要用nextLine 直到回车才结束
        System.out.print("请输入管理员的密码: ");
        String admin_pwd = scanner.nextLine();

        //通过Properties对象获取配置文件的信息


        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");

        //1. 注册驱动
        Class.forName(driver);//建议写上

        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);

        //3. 得到Statement
        Statement statement = connection.createStatement();
        //4. 组织SqL
        String sql = "select name , pwd  from admin where name ='"
                + admin_name + "' and pwd = '" + admin_pwd + "'";
        ResultSet resultSet = statement.executeQuery(sql);
        if (resultSet.next()) { //如果查询到一条记录，则说明该管理存在
            System.out.println("恭喜， 登录成功");
        } else {
            System.out.println("对不起，登录失败");
        }

        //关闭连接
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

# 六、PreparedStatement

## 1. 基本介绍

![PreparedStatement类结构图](/assets/JDBC/PreparedStatement类结构图.png)

```java
String sql ="SELECT COUNT(*) FROM admin WHERE username =? AND PASSWORD=?";
```

> 1. PreparedStatement 执行的SQL语句中的参数用问号(?)来表示，调用 PreparedStatement对象的setXxx()方法来设置这些参数. setXxx()方法有两个参数，第一个参数是要设置的SQL语句中的参数的索引(从1开始)，第二个是设置的SQL语句中的参数的值               
> 2. 调用executeQuery()，返回ResultSet 对象                     
> 3. 调用executeUpdate():执行更新，包括增、删、修改                 

## 2. 预处理好处

> 1. 不再使用+拼接sql语句，减少语法错误               
> 2. 有效的解决了sql注入问题!              
> 3. 大大减少了编译次数,效率较高          

## 3. 应用案例

```java
package com.hspedu.jdbc.preparedstatement_;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.sql.*;
import java.util.Properties;
import java.util.Scanner;

/**
 * 演示PreparedStatement使用
 */
@SuppressWarnings({"all"})
public class PreparedStatement_ {
    public static void main(String[] args) throws Exception {

        //看 PreparedStatement类图

        Scanner scanner = new Scanner(System.in);

        //让用户输入管理员名和密码
        System.out.print("请输入管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); // 老师说明，如果希望看到SQL注入，这里需要用nextLine
        System.out.print("请输入管理员的密码: ");
        String admin_pwd = scanner.nextLine();

        //通过Properties对象获取配置文件的信息

        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");

        //1. 注册驱动
        Class.forName(driver);//建议写上

        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);

        //3. 得到PreparedStatement
        //3.1 组织SqL , Sql 语句的 ? 就相当于占位符
        String sql = "select name , pwd  from admin where name =? and pwd = ?";
        //3.2 preparedStatement 对象实现了 PreparedStatement 接口的实现类的对象
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        //3.3 给 ? 赋值
        preparedStatement.setString(1, admin_name);
        preparedStatement.setString(2, admin_pwd);

        //4. 执行 select 语句使用  executeQuery
        //   如果执行的是 dml(update, insert ,delete) executeUpdate()
        //   这里执行 executeQuery ,不要再写 sql

        ResultSet resultSet = preparedStatement.executeQuery(sql);
        if (resultSet.next()) { //如果查询到一条记录，则说明该管理存在
            System.out.println("恭喜， 登录成功");
        } else {
            System.out.println("对不起，登录失败");
        }

        //关闭连接
        resultSet.close();
        preparedStatement.close();
        connection.close();


    }
}
```

- 操作DML语句

```java
package com.hspedu.jdbc.preparedstatement_;

import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Properties;
import java.util.Scanner;

/**
 * 演示PreparedStatement使用 dml语句
 */
@SuppressWarnings({"all"})
public class PreparedStatementDML_ {
    public static void main(String[] args) throws Exception {

        //看 PreparedStatement类图

        Scanner scanner = new Scanner(System.in);

        //让用户输入管理员名和密码
        System.out.print("请输删除管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); // 老师说明，如果希望看到SQL注入，这里需要用nextLine
//        System.out.print("请输入管理员的新密码: ");
//        String admin_pwd = scanner.nextLine();

        //通过Properties对象获取配置文件的信息

        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");

        //1. 注册驱动
        Class.forName(driver);//建议写上

        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);

        //3. 得到PreparedStatement
        //3.1 组织SqL , Sql 语句的 ? 就相当于占位符
        //添加记录
        //String sql = "insert into admin values(?, ?)";
        //String sql = "update admin set pwd = ? where name = ?";
        String sql = "delete from  admin where name = ?";
        //3.2 preparedStatement 对象实现了 PreparedStatement 接口的实现类的对象
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        //3.3 给 ? 赋值
        preparedStatement.setString(1, admin_name);

        //preparedStatement.setString(2, admin_name);

        //4. 执行 dml 语句使用  executeUpdate
        int rows = preparedStatement.executeUpdate();
        System.out.println(rows > 0 ? "执行成功" : "执行失败");
        //关闭连接
        preparedStatement.close();
        connection.close();
    }
}
```

# 七、JDBC 的相关 API 小结

![JDBC_API](/assets/JDBC/JDBC_API.png)

