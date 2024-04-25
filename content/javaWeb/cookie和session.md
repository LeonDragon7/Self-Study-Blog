---
external: false
title: cookie和session
date: 2023-06-15
---

# 一、Cookie


## 1. 什么是 Cookie?

> 1. Cookie 翻译过来是饼干的意思。                                 
> 2. Cookie 是服务器通知客户端保存键值对的一种技术。                        
> 3. 客户端有了 Cookie 后，每次请求都发送给服务器。                             
> 4. 每个 Cookie 的大小不能超过 4kb                    

## 2. 如何创建 Cookie

![cookie创建](/assets/cookie和session/cookie创建.png)

- Servlet 程序中的代码：

```java
protected void createCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
//1 创建 Cookie 对象
Cookie cookie = new Cookie("key4", "value4");
//2 通知客户端保存 Cookie
resp.addCookie(cookie);
//1 创建 Cookie 对象
Cookie cookie1 = new Cookie("key5", "value5");
//2 通知客户端保存 Cookie
resp.addCookie(cookie1);
resp.getWriter().write("Cookie 创建成功");
}
```

## 3. 服务器如何获取 Cookie

- 服务器获取客户端的 Cookie 只需要一行代码：req.getCookies():Cookie[]

![服务器获取Cookie](/assets/cookie和session/服务器获取Cookie.png)

- Cookie 的工具类：

```java
public class CookieUtils {
/**
* 查找指定名称的 Cookie 对象
* @param name
* @param cookies
* @return
*/
public static Cookie findCookie(String name , Cookie[] cookies){
if (name == null || cookies == null || cookies.length == 0) {
return null;
}
for (Cookie cookie : cookies) {
if (name.equals(cookie.getName())) {
return cookie;
}
}
return null;
}
}
```

- Servlet 程序中的代码：

```java
protected void getCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
Cookie[] cookies = req.getCookies();
for (Cookie cookie : cookies) {
// getName 方法返回 Cookie 的 key（名）
// getValue 方法返回 Cookie 的 value 值
resp.getWriter().write("Cookie[" + cookie.getName() + "=" + cookie.getValue() + "] <br/>");
}
Cookie iWantCookie = CookieUtils.findCookie("key1", cookies);
// for (Cookie cookie : cookies) {
// if ("key2".equals(cookie.getName())) {
// iWantCookie = cookie;
// break;
// }
// }
// 如果不等于 null，说明赋过值，也就是找到了需要的 Cookie
if (iWantCookie != null) {
resp.getWriter().write("找到了需要的 Cookie");
}
}
```

## 4. Cookie 值的修改

*方案一：*

> 1. 先创建一个要修改的同名（指的就是 key）的 Cookie 对象                            
> 2. 在构造器，同时赋于新的 Cookie 值。                                              
> 3. 调用 response.addCookie( Cookie );                               

```java
// 方案一：
// 1、先创建一个要修改的同名的 Cookie 对象
// 2、在构造器，同时赋于新的 Cookie 值。
Cookie cookie = new Cookie("key1","newValue1");
// 3、调用 response.addCookie( Cookie ); 通知 客户端 保存修改
resp.addCookie(cookie);
```

*方案二：*

> 1. 先查找到需要修改的 Cookie 对象                                                                
> 2. 调用 setValue()方法赋于新的 Cookie 值。                                   
> 3. 调用 response.addCookie()通知客户端保存修改                                

```java
// 方案二：
// 1、先查找到需要修改的 Cookie 对象
Cookie cookie = CookieUtils.findCookie("key2", req.getCookies());
if (cookie != null) {
// 2、调用 setValue()方法赋于新的 Cookie 值。
cookie.setValue("newValue2");
// 3、调用 response.addCookie()通知客户端保存修改
resp.addCookie(cookie);
}
```

## 5. 浏览器查看 Cookie

### 1. 谷歌浏览器如何查看 Cookie

![谷歌查看cookie](/assets/cookie和session/谷歌查看cookie.png)

### 2. 火狐浏览器如何查看 Cookie

![火狐查看cookie](/assets/cookie和session/火狐查看cookie.png)

## 6. Cookie 生命控制

- Cookie 的生命控制指的是如何管理 Cookie 什么时候被销毁（删除）

*setMaxAge()*

> 正数，表示在指定的秒数后过期                           
> 负数，表示浏览器一关，Cookie 就会被删除（默认值是-1）                                     
> 零，表示马上删除 Cookie                               

```java
/**
* 设置存活 1 个小时的 Cooie
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void life3600(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
Cookie cookie = new Cookie("life3600", "life3600");
cookie.setMaxAge(60 * 60); // 设置 Cookie 一小时之后被删除。无效
resp.addCookie(cookie);
resp.getWriter().write("已经创建了一个存活一小时的 Cookie");
}
/**
* 马上删除一个 Cookie
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void deleteNow(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 先找到你要删除的 Cookie 对象
Cookie cookie = CookieUtils.findCookie("key4", req.getCookies());
if (cookie != null) {
// 调用 setMaxAge(0);
cookie.setMaxAge(0); // 表示马上删除，都不需要等待浏览器关闭
// 调用 response.addCookie(cookie);
resp.addCookie(cookie);
resp.getWriter().write("key4 的 Cookie 已经被删除");
}
}
/**
* 默认的会话级别的 Cookie
* @param req
* @param resp
* @throws ServletException
* @throws IOException
*/
protected void defaultLife(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
Cookie cookie = new Cookie("defalutLife","defaultLife");
cookie.setMaxAge(-1);//设置存活时间
resp.addCookie(cookie);
}
```

## 7. Cookie 有效路径 Path 的设置

> Cookie 的 path 属性可以有效的过滤哪些 Cookie 可以发送给服务器。哪些不发。                          
> path 属性是通过请求的地址来进行有效的过滤。                          


> CookieA path=/工程路径                                           
> CookieB path=/工程路径/abc                                           


- 请求地址如下:
> <http://ip:port/工程路径/a.html>                                
> CookieA 发送                                                
> CookieB 不发送                                         

> <http://ip:port/工程路径/abc/a.html>                                    
> CookieA 发送                                                                           
> CookieB 不发送                                   

```java
protected void testPath(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
Cookie cookie = new Cookie("path1", "path1");
// getContextPath() ===>>>> 得到工程路径
cookie.setPath( req.getContextPath() + "/abc" ); // ===>>>> /工程路径/abc
resp.addCookie(cookie);
resp.getWriter().write("创建了一个带有 Path 路径的 Cookie");
}
```

## 8. Cookie 练习---免输入用户名登录

![cookie免用户名登录](/assets/cookie和session/cookie免用户名登录.png)

- login.jsp 页面

```html
<form action="http://localhost:8080/13_cookie_session/loginServlet" method="get">
用户名：<input type="text" name="username" value="${cookie.username.value}"> <br>
密码：<input type="password" name="password"> <br>
<input type="submit" value="登录">
</form>
```

- LoginServlet 程序：

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
String username = req.getParameter("username");
String password = req.getParameter("password");
if ("wzg168".equals(username) && "123456".equals(password)) {
//登录 成功
Cookie cookie = new Cookie("username", username);
cookie.setMaxAge(60 * 60 * 24 * 7);//当前 Cookie 一周内有效
resp.addCookie(cookie);
System.out.println("登录 成功");
} else {
// 登录 失败
System.out.println("登录 失败");
}
}
```