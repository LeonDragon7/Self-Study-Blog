---
external: false
title: Servlet
date: 2023-06-08
---

# 一、Servlet 技术

## 1. 什么是 Servlet

> 1. Servlet 是 JavaEE 规范之一。规范就是接口                             
> 2. Servlet 就 JavaWeb 三大组件之一。三大组件分别是：Servlet 程序、Filter 过滤器、Listener 监听器             
> 3. Servlet 是运行在服务器上的一个 java 小程序，它可以接收客户端发送过来的请求，并响应数据给客户端            

## 2. 手动实现 Servlet 程序

> 1. 编写一个类去实现 Servlet 接口               
> 2. 实现 service 方法，处理请求，并响应数据                              
> 3. 到 web.xml 中去配置 servlet 程序的访问地址                    

- Servlet 程序的示例代码:

```java
public class HelloServlet implements Servlet {
/**
* service 方法是专门用来处理请求和响应的
* @param servletRequest
* @param servletResponse
* @throws ServletException
* @throws IOException
*/
@Override
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws
ServletException, IOException {
System.out.println("Hello Servlet 被访问了");
}
}
```

- web.xml 中的配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
version="4.0">
<!-- servlet 标签给 Tomcat 配置 Servlet 程序 -->
<servlet>
<!--servlet-name 标签 Servlet 程序起一个别名（一般是类名） -->
<servlet-name>HelloServlet</servlet-name>
<!--servlet-class 是 Servlet 程序的全类名-->
<servlet-class>com.atguigu.servlet.HelloServlet</servlet-class>
</servlet>
<!--servlet-mapping 标签给 servlet 程序配置访问地址-->
<servlet-mapping>
<!--servlet-name 标签的作用是告诉服务器，我当前配置的地址给哪个 Servlet 程序使用-->
<servlet-name>HelloServlet</servlet-name>
<!--url-pattern 标签配置访问地址 <br/>
/ 斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径 <br/>
/hello 表示地址为：http://ip:port/工程路径/hello <br/>
-->
<url-pattern>/hello</url-pattern>
</servlet-mapping>
</web-app>
```

**常见的错误 1：url-pattern 中配置的路径没有以斜杠打头。**

![常见错误1](/assets/servlet/常见错误1.png)

**常见错误 2：servlet-name 配置的值不存在：**

![常见错误2](/assets/servlet/常见错误2.png)

**常见错误 3：servlet-class 标签的全类名配置错误：**

![常见错误3](/assets/servlet/常见错误3.png)

## 3. url 地址到 Servlet 程序的访问

![url访问servlet](/assets/servlet/url访问servlet.png)

## 4. Servlet 的生命周期

> 1.执行 Servlet 构造器方法                      
> 2.执行 init 初始化方法                 
**第一、二步，是在第一次访问，的时候创建 Servlet 程序会调用。**
> 3.执行 service 方法
**第三步，每次访问都会调用。**
> 4.执行 destroy 销毁方法                         
**第四步，在 web 工程停止的时候调用。**

## 5. GET 和 POST 请求的分发处理

```java
public class HelloServlet implements Servlet {
/**
* service 方法是专门用来处理请求和响应的
* @param servletRequest
* @param servletResponse
* @throws ServletException
* @throws IOException
*/
@Override
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws
ServletException, IOException {
System.out.println("3 service === Hello Servlet 被访问了");
// 类型转换（因为它有 getMethod()方法）
HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
// 获取请求的方式
String method = httpServletRequest.getMethod();
if ("GET".equals(method)) {
doGet();
} else if ("POST".equals(method)) {
doPost();
}
}
/**
* 做 get 请求的操作
*/
public void doGet(){
System.out.println("get 请求");
System.out.println("get 请求");
}
/**
* 做 post 请求的操作
*/
public void doPost(){
System.out.println("post 请求");
System.out.println("post 请求");
}
}
```

## 6. 通过继承 HttpServlet 实现 Servlet 程序

- 一般在实际项目开发中，都是使用继承 HttpServlet 类的方式去实现 Servlet 程序。

> 1. 编写一个类去继承 HttpServlet 类                
> 2. 根据业务需要重写 doGet 或 doPost 方法                  
> 3. 到 web.xml 中的配置 Servlet 程序的访问地址                        

- Servlet 类的代码：

```java
public class HelloServlet2 extends HttpServlet {
/**
* doGet（）在 get 请求的时候调用
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
System.out.println("HelloServlet2 的 doGet 方法");
}
/**
* doPost（）在 post 请求的时候调用
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
System.out.println("HelloServlet2 的 doPost 方法");
}
}
```

- web.xml 中的配置：

```xml
<servlet>
<servlet-name>HelloServlet2</servlet-name>
<servlet-class>com.atguigu.servlet.HelloServlet2</servlet-class>
</servlet>
<servlet-mapping>
<servlet-name>HelloServlet2</servlet-name>
<url-pattern>/hello2</url-pattern>
</servlet-mapping>
```

## 7. 使用 IDEA 创建 Servlet 程序

### 1. 菜单：new ->Servlet 程序

![创建Servlet](/assets/servlet/创建Servlet.png)

### 2. 配置 Servlet 的信息：

![配置Servlet](/assets/servlet/配置Servlet.png)

### 3. Servlet 类的继承体系

![Servlet继承关系](/assets/servlet/Servlet继承关系.png)

# 二、ServletConfig 类

> ServletConfig 类从类名上来看，就知道是 Servlet 程序的配置信息类。                                     
> Servlet 程序和 ServletConfig 对象都是由 Tomcat 负责创建，我们负责使用。                    
> Servlet 程序默认是第一次访问的时候创建，ServletConfig 是每个 Servlet 程序创建时，就创建一个对应的ServletConfig对象                  

## 1. ServletConfig 类的三大作用

> 1. 可以获取 Servlet 程序的别名 servlet-name 的值                    
> 2. 获取初始化参数 init-param                         
> 3. 获取 ServletContext 对象                         

- web.xml 中的配置：

```xml
<!-- servlet 标签给 Tomcat 配置 Servlet 程序 -->
<servlet>
<!--servlet-name 标签 Servlet 程序起一个别名（一般是类名） -->
<servlet-name>HelloServlet</servlet-name>
<!--servlet-class 是 Servlet 程序的全类名-->
<servlet-class>com.atguigu.servlet.HelloServlet</servlet-class>
<!--init-param 是初始化参数-->
<init-param>
<!--是参数名-->
<param-name>username</param-name>
<!--是参数值-->
<param-value>root</param-value>
</init-param>
<!--init-param 是初始化参数-->
<init-param>
<!--是参数名-->
<param-name>url</param-name>
<!--是参数值-->
<param-value>jdbc:mysql://localhost:3306/test</param-value>
</init-param>
</servlet>
<!--servlet-mapping 标签给 servlet 程序配置访问地址-->
<servlet-mapping>
<!--servlet-name 标签的作用是告诉服务器，我当前配置的地址给哪个 Servlet 程序使用-->
<servlet-name>HelloServlet</servlet-name>
<!--
url-pattern 标签配置访问地址 <br/>
/ 斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径 <br/>
/hello 表示地址为：http://ip:port/工程路径/hello <br/>
-->
<url-pattern>/hello</url-pattern>
</servlet-mapping>
```

- Servlet 中的代码：

```java
@Override
public void init(ServletConfig servletConfig) throws ServletException {
System.out.println("2 init 初始化方法");
// 1、可以获取 Servlet 程序的别名 servlet-name 的值
System.out.println("HelloServlet 程序的别名是:" + servletConfig.getServletName());
// 2、获取初始化参数 init-param
System.out.println("初始化参数 username 的值是;" + servletConfig.getInitParameter("username"));
System.out.println("初始化参数 url 的值是;" + servletConfig.getInitParameter("url"));
// 3、获取 ServletContext 对象
System.out.println(servletConfig.getServletContext());
}
```

**注意点：**

![重写init](/assets/servlet/重写init.png)


# 三、ServletContext 类

## 1. 什么是 ServletContext?

> 1. ServletContext 是一个接口，它表示 Servlet 上下文对象                       
> 2. 一个 web 工程，只有一个 ServletContext 对象实例                              
> 3. ServletContext 对象是一个域对象                         
> 4. ServletContext 是在 web 工程部署启动的时候创建。在 web 工程停止的时候销毁                  

> 什么是域对象?                               
> 域对象，是可以像 Map 一样存取数据的对象，叫域对象。                                     
> 这里的域指的是存取数据的操作范围，整个 web 工程。                                      

![域对象](/assets/servlet/域对象.png)

## 2. ServletContext 类的四个作用

> 1. 获取 web.xml 中配置的上下文参数 context-param                
> 2. 获取当前的工程路径，格式: /工程路径                   
> 3. 获取工程部署后在服务器硬盘上的绝对路径                  
> 4. 像 Map 一样存取数据                      

- ServletContext 演示代码：

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws
ServletException, IOException {
// 1、获取 web.xml 中配置的上下文参数 context-param
ServletContext context = getServletConfig().getServletContext();
String username = context.getInitParameter("username");
System.out.println("context-param 参数 username 的值是:" + username);
System.out.println("context-param 参数 password 的值是:" +
context.getInitParameter("password"));
// 2、获取当前的工程路径，格式: /工程路径
System.out.println( "当前工程路径:" + context.getContextPath() );
// 3、获取工程部署后在服务器硬盘上的绝对路径
/**
* / 斜杠被服务器解析地址为:http://ip:port/工程名/ 映射到 IDEA 代码的 web 目录<br/>
*/
System.out.println("工程部署的路径是:" + context.getRealPath("/"));
System.out.println("工程下 css 目录的绝对路径是:" + context.getRealPath("/css"));
System.out.println("工程下 imgs 目录 1.jpg 的绝对路径是:" + context.getRealPath("/imgs/1.jpg"));
}
```

- web.xml 中的配置：

```xml
<!--context-param 是上下文参数(它属于整个 web 工程)-->
<context-param>
<param-name>username</param-name>
<param-value>context</param-value>
</context-param>
<!--context-param 是上下文参数(它属于整个 web 工程)-->
<context-param>
<param-name>password</param-name>
<param-value>root</param-value>
</context-param>
```

- ServletContext 像 Map 一样存取数据：
- ContextServlet1 代码：

```java
public class ContextServlet1 extends HttpServlet {
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws
ServletException, IOException {
// 获取 ServletContext 对象
ServletContext context = getServletContext();
System.out.println(context);
System.out.println("保存之前: Context1 获取 key1 的值是:"+ context.getAttribute("key1"));
context.setAttribute("key1", "value1");
System.out.println("Context1 中获取域数据 key1 的值是:"+ context.getAttribute("key1"));
}
}
```

- ContextServlet2 代码：

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException,
IOException {
ServletContext context = getServletContext();
System.out.println(context);
System.out.println("Context2 中获取域数据 key1 的值是:"+ context.getAttribute("key1"));
}
```

# 四、HTTP 协议

## 1. 什么是 HTTP 协议

> 什么是协议?                        
> 协议是指双方，或多方，相互约定好，大家都需要遵守的规则，叫协议。                        
> 所谓 HTTP 协议，就是指，客户端和服务器之间通信时，发送的数据，需要遵守的规则，叫 HTTP 协议。            
> HTTP 协议中的数据又叫报文。                          

## 2. 请求的 HTTP 协议格式

> 客户端给服务器发送数据叫请求。                             
> 服务器给客户端回传数据叫响应。                                    
> 请求又分为 GET 请求，和 POST 请求两种                                     

### 1. GET 请求

#### (1) 请求行
> 请求的方式 GET                     
> 请求的资源路径`[+?+请求参数]`                 
> 请求的协议的版本号 HTTP/1.1                            

#### (2) 请求头

> key : value 组成 不同的键值对，表示不同的含义。                        

![get请求](/assets/servlet/get请求.png)

### 2. POST 请求

#### (1) 请求行
> 请求的方式 POST                                     
> 请求的资源路径`[+?+请求参数]`                             
> 请求的协议的版本号 HTTP/1.1                     

#### (2) 请求头

> key : value 组成 不同的键值对，表示不同的含义。                        
> 空行                      

#### (3) 请求体 ===>>> 就是发送给服务器的数据              

![post请求](/assets/servlet/post请求.png)

### 3. 常用请求头的说明

> 1. Accept: 表示客户端可以接收的数据类型                                    
> 2. Accpet-Languege: 表示客户端可以接收的语言类型                         
> 3. User-Agent: 表示客户端浏览器的信息                     
> 4. Host： 表示请求时的服务器 ip 和端口号                            

### 4. 哪些是 GET 请求，哪些是 POST 请求

- GET 请求有哪些：

> 1. form 标签 method=get                  
> 2. a 标签                
> 3. link 标签引入 css                     
> 4. Script 标签引入 js 文件                    
> 5. img 标签引入图片                    
> 6. iframe 引入 html 页面                             
> 7. 在浏览器地址栏中输入地址后敲回车                           

- POST 请求有哪些：
> 8. form 标签 method=pos

## 3. 响应的 HTTP 协议格式

## 1. 响应行

> (1) 响应的协议和版本号                  
> (2) 响应状态码                   
> (3) 响应状态描述符                      

## 2. 响应头
> (1) key : value 不同的响应头，有其不同含义                          
> (2) 空行                           
> (3) 响应体 ---->>> 就是回传给客户端的数据             

![响应http协议](/assets/servlet/响应http协议.png)

## 4. 常用的响应码说明

> 200 表示请求成功                             
> 302 表示请求重定向                          
> 404 表示请求服务器已经收到了，但是你要的数据不存在（请求地址错误）                        
> 500 表示服务器已经收到请求，但是服务器内部错误（代码错误）                          


## 5. MIME 类型说明

> MIME 是 HTTP 协议中数据类型。                        
> MIME 的英文全称是"Multipurpose Internet Mail Extensions" 多功能 Internet 邮件扩充服务。MIME 类型的格式是“大类型/小类型”，并与某一种文件的扩展名相对应。                               

- 常见的 MIME 类型：

![MIME类型1](/assets/servlet/MIME类型1.png)
![MIME类型2](/assets/servlet/MIME类型2.png)

- 谷歌浏览器如何查看 HTTP 协议：

![谷歌查看http协议](/assets/servlet/谷歌查看http协议.png)

- 火狐浏览器如何查看 HTTP 协议：

![火狐查看http协议](/assets/servlet/火狐查看http协议.png)


# 五、HttpServletRequest 类

## 1. HttpServletRequest 类有什么作用？

> 每次只要有请求进入 Tomcat 服务器，Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到 Request 对象中。然后传递到 service 方法（doGet 和 doPost）中给我们使用。我们可以通过 HttpServletRequest 对象，获取到所有请求的信息。                             

## 2. HttpServletRequest 类的常用方法

> 1. getRequestURI() 获取请求的资源路径                            
> 2. getRequestURL() 获取请求的统一资源定位符（绝对路径）                  
> 3. getRemoteHost() 获取客户端的 ip 地址                           
> 4. getHeader() 获取请求头                
> 5. getParameter() 获取请求的参数               
> 6. getParameterValues() 获取请求的参数（多个值的时候使用）                        
> 7. getMethod() 获取请求的方式 GET 或 POST                     
> 8. setAttribute(key, value); 设置域数据                      
> 9. getAttribute(key); 获取域数据                 
> 10. getRequestDispatcher() 获取请求转发对象                

- 常用 API 示例代码：

```java
public class RequestAPIServlet extends HttpServlet {
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// i.getRequestURI() 获取请求的资源路径
System.out.println("URI => " + req.getRequestURI());
// ii.getRequestURL() 获取请求的统一资源定位符（绝对路径）
System.out.println("URL => " + req.getRequestURL());
// iii.getRemoteHost() 获取客户端的 ip 地址
/**
* 在 IDEA 中，使用 localhost 访问时，得到的客户端 ip 地址是 ===>>> 127.0.0.1<br/>
* 在 IDEA 中，使用 127.0.0.1 访问时，得到的客户端 ip 地址是 ===>>> 127.0.0.1<br/>
* 在 IDEA 中，使用 真实 ip 访问时，得到的客户端 ip 地址是 ===>>> 真实的客户端 ip 地址<br/>
*/
System.out.println("客户端 ip 地址 => " + req.getRemoteHost());
// iv.getHeader() 获取请求头
System.out.println("请求头 User-Agent ==>> " + req.getHeader("User-Agent"));
// vii.getMethod() 获取请求的方式 GET 或 POST
System.out.println( "请求的方式 ==>> " + req.getMethod() );
}
}
```

## 3. 如何获取请求参数

*表单：*

```html
<body>
<form action="http://localhost:8080/07_servlet/parameterServlet" method="get">
用户名：<input type="text" name="username"><br/>
密码：<input type="password" name="password"><br/>
兴趣爱好：<input type="checkbox" name="hobby" value="cpp">C++
<input type="checkbox" name="hobby" value="java">Java
<input type="checkbox" name="hobby" value="js">JavaScript<br/>
<input type="submit">
</form>
</body>
```

*Java 代码：*

```java
public class ParameterServlet extends HttpServlet {
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 获取请求参数
String username = req.getParameter("username");
String password = req.getParameter("password");
String[] hobby = req.getParameterValues("hobby");
System.out.println("用户名：" + username);
System.out.println("密码：" + password);
System.out.println("兴趣爱好：" + Arrays.asList(hobby));
}
}
```

## 4. doGet 请求的中文乱码解决

```java
// 获取请求参数
String username = req.getParameter("username");
//1 先以 iso8859-1 进行编码
//2 再以 utf-8 进行解码
username = new String(username.getBytes("iso-8859-1"), "UTF-8");
```

## 5. POST 请求的中文乱码解决

```java
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 设置请求体的字符集为 UTF-8，从而解决 post 请求的中文乱码问题
req.setCharacterEncoding("UTF-8");
System.out.println("-------------doPost------------");
// 获取请求参数
String username = req.getParameter("username");
String password = req.getParameter("password");
String[] hobby = req.getParameterValues("hobby");
System.out.println("用户名：" + username);
System.out.println("密码：" + password);
System.out.println("兴趣爱好：" + Arrays.asList(hobby));
}
```

## 6. 请求的转发

- 什么是请求的转发?

> 请求转发是指，服务器收到请求后，从一次资源跳转到另一个资源的操作叫请求转发。                         

![请求转发](/assets/servlet/请求转发.png)


- Servlet1 代码：

```java
public class Servlet1 extends HttpServlet {
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 获取请求的参数（办事的材料）查看
String username = req.getParameter("username");
System.out.println("在 Servlet1（柜台 1）中查看参数（材料）：" + username);
// 给材料 盖一个章，并传递到 Servlet2（柜台 2）去查看
req.setAttribute("key1","柜台 1 的章");
// 问路：Servlet2（柜台 2）怎么走
/**
* 请求转发必须要以斜杠打头，/ 斜杠表示地址为：http://ip:port/工程名/ , 映射到 IDEA 代码的 web 目录
<br/>
*
*/
RequestDispatcher requestDispatcher = req.getRequestDispatcher("/servlet2");
// RequestDispatcher requestDispatcher = req.getRequestDispatcher("http://www.baidu.com");
// 走向 Sevlet2（柜台 2）
requestDispatcher.forward(req,resp);
}
}
```

- Servlet2 代码：

```java
public class Servlet2 extends HttpServlet {
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 获取请求的参数（办事的材料）查看
String username = req.getParameter("username");
System.out.println("在 Servlet2（柜台 2）中查看参数（材料）：" + username);
// 查看 柜台 1 是否有盖章
Object key1 = req.getAttribute("key1");
System.out.println("柜台 1 是否有章：" + key1);
// 处理自己的业务
System.out.println("Servlet2 处理自己的业务 ");
}
}
```

## 7. base 标签的作用

![base标签的作用](/assets/servlet/base标签的作用.png)

```html
<!DOCTYPE html>
<html lang="zh_CN">
<head>
<meta charset="UTF-8">
<title>Title</title>
<!--base 标签设置页面相对路径工作时参照的地址
href 属性就是参数的地址值
-->
<base href="http://localhost:8080/07_servlet/a/b/">
</head>
<body>
这是 a 下的 b 下的 c.html 页面<br/>
<a href="../../index.html">跳回首页</a><br/>
</body>
</html>
```

## 8. Web 中的相对路径和绝对路径

- 在 javaWeb 中，路径分为相对路径和绝对路径两种：

```java
/*
相对路径是：
. 表示当前目录
.. 表示上一级目录
资源名 表示当前目录/资源名
绝对路径：
http://ip:port/工程路径/资源路径
在实际开发中，路径都使用绝对路径，而不简单的使用相对路径。
1、绝对路径
2、base+相对
*/
```

## 9. web 中 / 斜杠的不同意义

```html
在 web 中 / 斜杠 是一种绝对路径。

/ 斜杠 如果被浏览器解析，得到的地址是：http://ip:port/
<a href="/">斜杠</a>

/ 斜杠 如果被服务器解析，得到的地址是：http://ip:port/工程路径
1. <url-pattern>/servlet1</url-pattern> 
2. servletContext.getRealPath("/");
3. request.getRequestDispatcher("/");

特殊情况： response.sendRediect("/"); 把斜杠发送给浏览器解析。得到 http://ip:port/
```

# 六、HttpServletResponse 类

## 1. HttpServletResponse 类的作用

> HttpServletResponse 类和 HttpServletRequest 类一样。每次请求进来，Tomcat 服务器都会创建一个 Response 对象传递给 Servlet 程序去使用。HttpServletRequest 表示请求过来的信息，HttpServletResponse 表示所有响应的信息，我们如果需要设置返回给客户端的信息，都可以通过 HttpServletResponse 对象来进行设置                                      


## 2. 两个输出流的说明

> 1. 字节流 getOutputStream(); 常用于下载（传递二进制数据）
> 2. 字符流 getWriter(); 常用于回传字符串（常用）

**两个流同时只能使用一个。使用了字节流，就不能再使用字符流，反之亦然，否则就会报错。**

![流报错](/assets/servlet/流报错.png)

## 3. 如何往客户端回传数据

*要求 ： 往客户端回传 字符串 数据。*

```java
public class ResponseIOServlet extends HttpServlet {
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 要求 ： 往客户端回传 字符串 数据。
PrintWriter writer = resp.getWriter();
writer.write("response's content!!!");
}
}
```

## 4. 响应的乱码解决

- 解决响应中文乱码方案一（不推荐使用）：

```java
// 设置服务器字符集为 UTF-8
resp.setCharacterEncoding("UTF-8");
// 通过响应头，设置浏览器也使用 UTF-8 字符集
resp.setHeader("Content-Type", "text/html; charset=UTF-8");
```

- 解决响应中文乱码方案二（推荐）：

```java
// 它会同时设置服务器和客户端都使用 UTF-8 字符集，还设置了响应头
// 此方法一定要在获取流对象之前调用才有效
resp.setContentType("text/html; charset=UTF-8");
```

## 5. 请求重定向

> 请求重定向，是指客户端给服务器发请求，然后服务器告诉客户端说。我给你一些地址。你去新地址访问。叫请求重定向（因为之前的地址可能已经被废弃）。                      

![请求重定向](/assets/servlet/请求重定向.png)

### 1. 请求重定向的第一种方案：
```java
// 设置响应状态码 302 ，表示重定向，（已搬迁）
resp.setStatus(302);
// 设置响应头，说明 新的地址在哪里
resp.setHeader("Location", "http://localhost:8080");
```

### 2. 请求重定向的第二种方案（推荐使用）：
```java
resp.sendRedirect("http://localhost:8080");
```
