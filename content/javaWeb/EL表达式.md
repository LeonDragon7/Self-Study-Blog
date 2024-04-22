---
external: false
title: EL表达式
date: 2023-06-12
---

# 一、EL 表达式

## 1. 什么是 EL 表达式，EL 表达式的作用?

> EL 表达式的全称是：Expression Language。是表达式语言。                             
> EL 表达式的什么作用：EL 表达式主要是代替 jsp 页面中的表达式脚本在 jsp 页面中进行数据的输出。            
> 因为 EL 表达式在输出数据的时候，要比 jsp 的表达式脚本要简洁很多。                        

```java
<body>
<%
request.setAttribute("key","值");
%>
表达式脚本输出 key 的值是：
<%=request.getAttribute("key1")==null?"":request.getAttribute("key1")%><br/>
EL 表达式输出 key 的值是：${key1}
</body>
```

> EL 表达式的格式是：${表达式}                              
> EL 表达式在输出 null 值的时候，输出的是空串。jsp 表达式脚本输出 null 值的时候，输出的是 null 字符串。        

## 2. EL 表达式搜索域数据的顺序

> EL 表达式主要是在 jsp 页面中输出数据。                        
> 主要是输出域对象中的数据。                               
> 当四个域中都有相同的 key 的数据的时候，EL 表达式会按照四个域的从小到大的顺序去进行搜索，找到就输出。         

```java
<body>
<%
//往四个域中都保存了相同的 key 的数据。
request.setAttribute("key", "request");
session.setAttribute("key", "session");
application.setAttribute("key", "application");
pageContext.setAttribute("key", "pageContext");
%>
${ key }
</body>
```

## 3. EL 表达式输出 Bean 的普通属性，数组属性。List 集合属性，map 集合属性

> 需求——输出 Person 类中普通属性，数组属性。list 集合属性和 map 集合属性。                    

`Person类`

```java
public class Person {
// i.需求——输出 Person 类中普通属性，数组属性。list 集合属性和 map 集合属性。
private String name;
private String[] phones;
private List<String> cities;
private Map<String,Object> map;
public int getAge() {
return 18;
}
}
```

- 输出的代码：

```java
<body>
<%
Person person = new Person();
person.setName("国哥好帅！");
person.setPhones(new String[]{"18610541354","18688886666","18699998888"});
List<String> cities = new ArrayList<String>();
cities.add("北京");
cities.add("上海");
cities.add("深圳");
person.setCities(cities);
Map<String,Object>map = new HashMap<>();
map.put("key1","value1");
map.put("key2","value2");
map.put("key3","value3");
person.setMap(map);
pageContext.setAttribute("p", person);
%>
输出 Person：${ p }<br/>
输出 Person 的 name 属性：${p.name} <br>
输出 Person 的 pnones 数组属性值：${p.phones[2]} <br>
输出 Person 的 cities 集合中的元素值：${p.cities} <br>
输出 Person 的 List 集合中个别元素值：${p.cities[2]} <br>
输出 Person 的 Map 集合: ${p.map} <br>
输出 Person 的 Map 集合中某个 key 的值: ${p.map.key3} <br>
输出 Person 的 age 属性：${p.age} <br>
</body>
```

## 4. EL 表达式——运算

> 语法：${ 运算表达式 } ， EL 表达式支持如下运算符：                  

### 1. 关系运算

![关系运算](/assets/el表达式/关系运算.png)

### 2. 逻辑运算

![逻辑运算](/assets/el表达式/逻辑运算.png)

### 3. 算数运算

![算术运算](/assets/el表达式/算术运算.png)

### 4. empty 运算

> empty 运算可以判断一个数据是否为空，如果为空，则输出 true,不为空输出 false。           

- 以下几种情况为空：

> 1. 值为 null 值的时候，为空                         
> 2. 值为空串的时候，为空                              
> 3. 值是 Object 类型数组，长度为零的时候                          
> 4. list 集合，元素个数为零                               
> 5. map 集合，元素个数为零                      

```java
<body>
<%
// 1、值为 null 值的时候，为空
request.setAttribute("emptyNull", null);
// 2、值为空串的时候，为空
request.setAttribute("emptyStr", "");
// 3、值是 Object 类型数组，长度为零的时候
request.setAttribute("emptyArr", new Object[]{});
// 4、list 集合，元素个数为零
List<String> list = new ArrayList<>();
// list.add("abc");
request.setAttribute("emptyList", list);
// 5、map 集合，元素个数为零
Map<String,Object> map = new HashMap<String, Object>();
// map.put("key1", "value1");
request.setAttribute("emptyMap", map);
%>
${ empty emptyNull } <br/>
${ empty emptyStr } <br/>
${ empty emptyArr } <br/>
${ empty emptyList } <br/>
${ empty emptyMap } <br/>
</body>
```


### 5. 三元运算

> 表达式 1？表达式 2：表达式 3                           
> 如果表达式 1 的值为真，返回表达式 2 的值，如果表达式 1 的值为假，返回表达式 3 的值。                      

`实例：`

```java
${ 12 != 12 ? "国哥帅呆":"国哥又骗人啦" }
```

### 6. "."点运算 和 [] 中括号运算符

> .点运算，可以输出 Bean 对象中某个属性的值。                           
> []中括号运算，可以输出有序集合中某个元素的值。                     
> 并且[]中括号运算，还可以输出 map 集合中 key 里含有特殊字符的 key 的值。                          

```java
<body>
<%
Map<String,Object> map = new HashMap<String, Object>();
map.put("a.a.a", "aaaValue");
map.put("b+b+b", "bbbValue");
map.put("c-c-c", "cccValue");
request.setAttribute("map", map);
%>
${ map['a.a.a'] } <br>
${ map["b+b+b"] } <br>
${ map['c-c-c'] } <br>
</body>
```

## 5. EL 表达式的 11 个隐含对象

- EL 个达式中 11 个隐含对象，是 EL 表达式中自己定义的，可以直接使用。

```java
变量                        类型                            作用
pageContext           PageContextImpl             它可以获取 jsp 中的九大内置对象
pageScope             Map<String,Object>          它可以获取 pageContext 域中的数据
requestScope          Map<String,Object>          它可以获取 Request 域中的数据
sessionScope          Map<String,Object>          它可以获取 Session 域中的数据
applicationScope      Map<String,Object>          它可以获取 ServletContext 域中的数据
param                 Map<String,String>          它可以获取请求参数的值
paramValues           Map<String,String[]>        它也可以获取请求参数的值，获取多个值的时候使用。
header                Map<String,String>          它可以获取请求头的信息
headerValues          Map<String,String[]>        它可以获取请求头的信息，它可以获取多个值的情况
cookie                Map<String,Cookie>          它可以获取当前请求的 Cookie 信息
initParam             Map<String,String>          它可以获取在 web.xml 中配置的<context-param>上下文参数
```


### 1. EL 获取四个特定域中的属性

> pageScope ====== pageContext 域                       
> requestScope ====== Request 域                         
> sessionScope ====== Session 域                       
> applicationScope ====== ServletContext 域                              

```java
<body>
<%
pageContext.setAttribute("key1", "pageContext1");
pageContext.setAttribute("key2", "pageContext2");
request.setAttribute("key2", "request");
session.setAttribute("key2", "session");
application.setAttribute("key2", "application");
%>
${ applicationScope.key2 }
</body>
```

### 2. pageContext 对象的使用

> 1. 协议：                                      
> 2. 服务器 ip：                                 
> 3. 服务器端口：                               
> 4. 获取工程路径：                                 
> 5. 获取请求方法：                             
> 6. 获取客户端 ip 地址：                                 
> 7. 获取会话的 id 编号：                          

```java
<body>
<%--
request.getScheme() 它可以获取请求的协议
request.getServerName() 获取请求的服务器 ip 或域名
request.getServerPort() 获取请求的服务器端口号
getContextPath() 获取当前工程路径
request.getMethod() 获取请求的方式（GET 或 POST）
request.getRemoteHost() 获取客户端的 ip 地址
session.getId() 获取会话的唯一标识
--%>
<%
pageContext.setAttribute("req", request);
%>
<%=request.getScheme() %> <br>
1.协议： ${ req.scheme }<br>
2.服务器 ip：${ pageContext.request.serverName }<br>
3.服务器端口：${ pageContext.request.serverPort }<br>
4.获取工程路径：${ pageContext.request.contextPath }<br>
5.获取请求方法：${ pageContext.request.method }<br>
6.获取客户端 ip 地址：${ pageContext.request.remoteHost }<br>
7.获取会话的 id 编号：${ pageContext.session.id }<br>
</body>
```

