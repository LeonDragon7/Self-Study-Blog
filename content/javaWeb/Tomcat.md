---
external: false
title: Tomcat
date: 2023-06-06
---

# 一、JavaWeb 的概念

## 1. 什么是 JavaWeb

> JavaWeb 是指，所有通过 Java 语言编写可以通过浏览器访问的程序的总称，叫 JavaWeb。                           
> JavaWeb 是基于请求和响应来开发的。                          

## 2. 什么是请求

> 请求是指客户端给服务器发送数据，叫请求 Request。                      

## 3. 什么是响应

> 响应是指服务器给客户端回传数据，叫响应 Response。                             

## 4. 请求和响应的关系

> 请求和响应是成对出现的，有请求就有响应。                               

![请求和响应](/assets/tomcat/请求和响应.png)

# 二、Web 资源的分类

- web 资源按实现的技术和呈现的效果的不同，又分为静态资源和动态资源两种。

> 静态资源： html、css、js、txt、mp4 视频 , jpg 图片                             
> 动态资源： jsp 页面、Servlet 程序                                     

# 三、常用的 Web 服务器

> Tomcat：由 Apache 组织提供的一种 Web 服务器，提供对 jsp 和 Servlet 的支持。它是一种轻量级的 javaWeb 容器（服务
器），也是当前应用最广的 JavaWeb 服务器（免费）。                 
> Jboss：是一个遵从 JavaEE 规范的、开放源代码的、纯 Java 的 EJB 服务器，它支持所有的 JavaEE 规范（免费）。       
> GlassFish： 由 Oracle 公司开发的一款 JavaWeb 服务器，是一款强健的商业服务器，达到产品级质量（应用很少）。      
> Resin：是 CAUCHO 公司的产品，是一个非常流行的服务器，对 servlet 和 JSP 提供了良好的支持，性能也比较优良，resin 自身采用 JAVA 语言开发（收费，应用比较多）。                          
> WebLogic：是 Oracle 公司的产品，是目前应用最广泛的 Web 服务器，支持 JavaEE 规范，而且不断的完善以适应新的开发要求，适合大型项目（收费，用的不多，适合大公司）。                          

# 四、Tomcat 服务器和 Servlet 版本的对应关系

`当前企业常用的版本 7.*、8.*`

![Tomcat服务器和Servlet对应关系](/assets/tomcat/Tomcat服务器和Servlet对应关系.png)

> Servlet 程序从 2.5 版本是现在世面使用最多的版本（xml 配置）,到了 Servlet3.0 之后。就是注解版本的 Servlet 使用。
以 2.5 版本为主线讲解 Servlet 程序。                              

# 五、Tomcat 的使用

## 1. 安装

> 找到你需要用的 Tomcat 版本对应的 zip 压缩包，解压到需要安装的目录即可。                 

## 2. 目录介绍

![Tomcat目录介绍](/assets/tomcat/Tomcat目录介绍.png)

## 3. 如何启动 Tomcat 服务器

- 找到 Tomcat 目录下的 bin 目录下的 startup.bat 文件，双击，就可以启动 Tomcat 服务器。

> 如何测试 Tomcat 服务器启动成功？？？                                      
> 打开浏览器，在浏览器地址栏中输入以下地址测试：                                     
> 1. http://localhost:8080                          
> 2. http://127.0.0.1:8080                              
> 3. http://真实 ip:8080                            

**当出现如下界面，说明 Tomcat 服务器启动成功！！！**

![tomcat启动页面](/assets/tomcat/tomcat启动页面.png)

> 常见的启动失败的情况有，双击 startup.bat 文件，就会出现一个小黑窗口一闪而来。这个时候，失败的原因基本上都是因为没有配置好 JAVA_HOME 环境变量。                           

- 配置 JAVA_HOME 环境变量：

![tomcat配置环境变量](/assets/tomcat/tomcat配置环境变量.png)

- 常见的 JAVA_HOME 配置错误有以下几种情况：

> 一：JAVA_HOME 必须全大写。                             
> 二：JAVA_HOME 中间必须是下划线，不是减号-                                  
> 三：JAVA_HOME 配置的路径只需要配置到 jdk 的安装目录即可。不需要带上 bin 目录。                        

## 4. 另一种启动 tomcat 服务器的方式

> 1.打开命令行                
> 2.cd 到 你的 Tomcat 的 bin 目录下                      

![命令行启动tomcat](/assets/tomcat/命令行启动tomcat.png)

> 3.敲入启动命令： catalina run                        

## 5. Tomcat 的停止  

> 1. 点击 tomcat 服务器窗口的 x 关闭按钮                           
> 2. 把 Tomcat 服务器窗口置为当前窗口，然后按快捷键 Ctrl+C                   
> 3. 找到 Tomcat 的 bin 目录下的 shutdown.bat 双击，就可以停止 Tomcat 服务器                  

## 6. 如何修改 Tomcat 的端口号               

> Mysql 默认的端口号是：3306                               
> Tomcat 默认的端口号是：8080                             

- 找到 Tomcat 目录下的 conf 目录，找到 server.xml 配置文件。                 

![serverxml文件](/assets/tomcat/serverxml文件.png)

> 平时上百度：<http://www.baidu.com:80>                                 
> HTTP 协议默认的端口号是：80                                

## 7. 如何部暑 web 工程到 Tomcat 中

- 第一种部署方法：只需要把 web 工程的目录拷贝到 Tomcat 的 webapps 目录下即可

### 1. 在 webapps 目录下创建一个 book 工程

![创建book工程](/assets/tomcat/创建book工程.png)

### 2. 如何访问 Tomcat 下的 web 工程

> 只需要在浏览器中输入访问地址格式如下：<http://ip:port/工程名/目录下/文件名>

- 第二种部署方法：

> 找到 Tomcat 下的 conf 目录\Catalina\localhost\ 下,创建如下的配置文件：           

![conf配置文件](/assets/tomcat/conf配置文件.png)

- abc.xml 配置文件内容如下：

```xml
<!-- Context 表示一个工程上下文
path 表示工程的访问路径:/abc
docBase 表示你的工程目录在哪里
-->
<Context path="/abc" docBase="E:\book" />
<!-- 访问这个工程的路径如下:http://ip:port/abc/ 就表示访问 E:\book 目录 -->
```

## 8. 手托 html 页面到浏览器和在浏览器中输入 http://ip:端口号/工程名/访问的区别               

- 手托 html 页面的原理：

![手托html页面](/assets/tomcat/手托html页面.png)

- 输入访问地址的原因：

![访问流程](/assets/tomcat/访问流程.png)

## 9. ROOT 的工程的访问，以及 默认 index.html 页面的访问

- 当我们在浏览器地址栏中输入访问地址如下：
> <http://ip:port/> ====>>>> 没有工程名的时候，默认访问的是 ROOT 工程。                  

- 当我们在浏览器地址栏中输入的访问地址如下：
> <http://ip:port/工程名/> ====>>>> 没有资源名，默认访问 index.html 页面                    

# 六、IDEA 整合 Tomcat 服务器

- 操作的菜单如下：File | Settings | Build, Execution, Deployment | Application Servers

![IDEA整合Tomcat项目](/assets/tomcat/IDEA整合Tomcat项目.png)

- 配置你的 Tomcat 安装目录：

![配置Tomcat安装目录](/assets/tomcat/配置Tomcat安装目录.png)

**就可以通过创建一个 Model 查看是不是配置成功！！！**

![Tomcat整合成功](/assets/tomcat/Tomcat整合成功.png)

# 七、IDEA 中动态 web 工程的操作

## 1. IDEA 中如何创建动态 web 工程          

### (1) 创建一个新模块：

![创建模块](/assets/tomcat/创建模块.png)

### (2) 选择你要创建什么类型的模块：

![选择类型模块](/assets/tomcat/选择类型模块.png)

### (3) 输入你的模块名，点击【Finish】完成创建。

![输入模块名](/assets/tomcat/输入模块名.png)

### (4) 创建成功如下图：

![创建动态web工程](/assets/tomcat/创建动态web工程.png)


