---
external: false
title: Jsp
date: 2023-06-10
---

# 一、为什么要学习 jsp 技术

## 1. 什么是 jsp，它有什么用?

> JSP(全称 Java Server Pages)是由 Sun 公司专门为了解决动态生成 HTML 文档的技术。    

*作用：*

> 1. jsp 的全换是 java server pages。Java 的服务器页面。                                            
> 2. jsp 的主要作用是代替 Servlet 程序回传 html 页面的数据。                                   
> 3. 因为 Servlet 程序回传 html 页面数据是一件非常繁锁的事情。开发成本和维护成本都极高。                                   

### 1. Servlet 回传 html 页面数据的代码：

```java
public class PringHtml extends HttpServlet {
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 通过响应的回传流回传 html 页面数据
resp.setContentType("text/html; charset=UTF-8");
PrintWriter writer = resp.getWriter();
writer.write("<!DOCTYPE html>\r\n");
writer.write(" <html lang=\"en\">\r\n");
writer.write(" <head>\r\n");
writer.write(" <meta charset=\"UTF-8\">\r\n");
writer.write(" <title>Title</title>\r\n");
writer.write(" </head>\r\n");
writer.write(" <body>\r\n");
writer.write(" 这是 html 页面数据 \r\n");
writer.write(" </body>\r\n");
writer.write("</html>\r\n");
writer.write("\r\n");
}
}
```

### 2. jsp 回传一个简单 html 页面的代码：

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
<title>Title</title>
</head>
<body>
这是 html 页面数据
</body>
</html>
```

*jsp 的小结：*

- 1、如何创建 jsp 的页面?

![创建jsp页面](/assets/jsp/创建jsp页面.png)

- 2、jsp 如何访问：

> jsp 页面和 html 页面一样，都是存放在 web 目录下。访问也跟访问 html 页面一样。                  

*比如：*

> 在 web 目录下有如下的文件：                    
> web 目录                            
> a.html 页面 访问地址是 =======>>>>>> http://ip:port/工程路径/a.html                               
> b.jsp 页面 访问地址是 =======>>>>>> http://ip:port/工程路径/b.jsp                           

# 二、jsp 的本质是什么

> jsp 页面本质上是一个 Servlet 程序。                  
> 当我们第一次访问 jsp 页面的时候。Tomcat 服务器会帮我们把 jsp 页面翻译成为一个 java 源文件。并且对它进行编译成为.class 字节码程序。我们打开 java 源文件不难发现其里面的内容是：                                  

![a_jsp](/assets/jsp/a_jsp.png)

> 我们跟踪原代码发现，HttpJspBase 类。它直接地继承了 HttpServlet 类。也就是说。jsp 翻译出来的 java 类，它间接了继承了 HttpServlet 类。也就是说，翻译出来的是一个 Servlet 程序                     

![HttpJspBase类](/assets/jsp/HttpJspBase类.png)

**总结：通过翻译的 java 源代码我们就可以得到结果：jsp 就是 Servlet 程序。**

- Servlet 程序的源代码,其底层实现，也是通过输出流。把 html 页面数据回传给客户端。

```java
public void _jspService(final javax.servlet.http.HttpServletRequest request, final
javax.servlet.http.HttpServletResponse response)
throws java.io.IOException, javax.servlet.ServletException {
final java.lang.String _jspx_method = request.getMethod();
if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method)
&& !javax.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) {
response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSPs only permit GET POST or
HEAD");
return;
}
final javax.servlet.jsp.PageContext pageContext;
javax.servlet.http.HttpSession session = null;
final javax.servlet.ServletContext application;
final javax.servlet.ServletConfig config;
javax.servlet.jsp.JspWriter out = null;
final java.lang.Object page = this;
javax.servlet.jsp.JspWriter _jspx_out = null;
javax.servlet.jsp.PageContext _jspx_page_context = null;
try {
response.setContentType("text/html;charset=UTF-8");
pageContext = _jspxFactory.getPageContext(this, request, response,
null, true, 8192, true);
_jspx_page_context = pageContext;
application = pageContext.getServletContext();
config = pageContext.getServletConfig();
session = pageContext.getSession();
out = pageContext.getOut();
_jspx_out = out;
out.write("\r\n");
out.write("\r\n");
out.write("<html>\r\n");
out.write("<head>\r\n");
out.write(" <title>Title</title>\r\n");
out.write("</head>\r\n");
out.write("<body>\r\n");
out.write(" a.jsp 页面\r\n");
out.write("</body>\r\n");
out.write("</html>\r\n");
} catch (java.lang.Throwable t) {
if (!(t instanceof javax.servlet.jsp.SkipPageException)){
out = _jspx_out;
if (out != null && out.getBufferSize() != 0)
try {
if (response.isCommitted()) {
out.flush();
} else {
out.clearBuffer();
}
} catch (java.io.IOException e) {}
if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
else throw new ServletException(t);
}
} finally {
_jspxFactory.releasePageContext(_jspx_page_context);
}
}
```

# 三、jsp 的三种语法

## 1. jsp 头部的 page 指令

- jsp 的 page 指令可以修改 jsp 页面中一些重要的属性，或者行为。

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```

> 1.language 属性 表示 jsp 翻译后是什么语言文件。暂时只支持 java。                
> 2.contentType 属性 表示 jsp 返回的数据类型是什么。也是源码中 response.setContentType()参数值                       
> 3.pageEncoding 属性 表示当前 jsp 页面文件本身的字符集。                     
> 4.import 属性 跟 java 源代码中一样。用于导包，导类。                         
> ================两个属性是给 out 输出流使用================                        
> 5.autoFlush 属性 设置当 out 输出流缓冲区满了之后，是否自动刷新冲级区。默认值是 true。                      
> 6.buffer 属性 设置 out 缓冲区的大小。默认是 8kb                            
> 缓冲区溢出错误：                                      
![缓冲区溢出错误](/assets/jsp/缓冲区溢出错误.png)
> ================两个属性是给 out 输出流使用================                              
> 7.errorPage 属性 设置当 jsp 页面运行时出错，自动跳转去的错误页面路径。                              


```jsp
<!--
errorPage 表示错误后自动跳转去的路径 <br/>
这个路径一般都是以斜杠打头，它表示请求地址为 http://ip:port/工程路径/
映射到代码的 Web 目录
-->
viii. isErrorPage 属性 设置当前 jsp 页面是否是错误信息页面。默认是 false。如果是 true 可以
获取异常信息。
ix. session 属性 设置访问当前 jsp 页面，是否会创建 HttpSession 对象。默认是 true。
x. extends 属性 设置 jsp 翻译出来的 java 类默认继承谁。
```

## 2. jsp 中的常用脚本

### 1. 声明脚本(极少使用)

> 声明脚本的格式是： <%! 声明 java 代码 %>                          
> 作用：可以给 jsp 翻译出来的 java 类定义属性和方法甚至是静态代码块。内部类等。                        

`练习：`
> 1. 声明类属性                       
> 2. 声明 static 静态代码块                      
> 3. 声明类方法                         
> 4. 声明内部类                          

- 代码示例：

```java
<%--1、声明类属性--%>
<%!
private Integer id;
private String name;
private static Map<String,Object> map;
%>
<%--2、声明 static 静态代码块--%>
<%!
static {
map = new HashMap<String,Object>();
map.put("key1", "value1");
map.put("key2", "value2");
map.put("key3", "value3");
}
%>
<%--3、声明类方法--%>
<%!
public int abc(){
return 12;
}
%>
<%--4、声明内部类--%>
<%!
public static class A {
private Integer id = 12;
private String abc = "abc";
}
%>
```

- 声明脚本代码翻译对照：

![声明脚本代码翻译对照](/assets/jsp/声明脚本代码翻译对照.png)

## 2. 表达式脚本（常用）

> 表达式脚本的格式是：<%=表达式%>                                       
> 表达式脚本的作用是：的 jsp 页面上输出数据。                           

- 表达式脚本的特点：

> 1. 所有的表达式脚本都会被翻译到_jspService() 方法中                         
> 2. 表达式脚本都会被翻译成为 out.print()输出到页面上                                     
> 3. 由于表达式脚本翻译的内容都在_jspService() 方法中,所以_jspService()方法中的对象都可以直接使用。                                     
> 4. 表达式脚本中的表达式不能以分号结束。                        

`练习：`

> 1. 输出整型                     
> 2. 输出浮点型                            
> 3. 输出字符串                              
> 4. 输出对象                                      

- 示例代码：

```jsp
<%=12 %> <br>
<%=12.12 %> <br>
<%="我是字符串" %> <br>
<%=map%> <br>
<%=request.getParameter("username")%>
```

- 翻译对照：

![表达式脚本代码翻译对照](/assets/jsp/表达式脚本代码翻译对照.png)

