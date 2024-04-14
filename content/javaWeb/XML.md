---
external: false
title: XML
date: 2023-06-05
---

# 一、XML 简介

## 1. 什么是 xml？

> xml 是可扩展的标记性语言。                  

## 2. xml 的作用？

- xml 的主要作用有：

> 1. 用来保存数据，而且这些数据具有自我描述性                
> 2. 它还可以做为项目或者模块的配置文件                            
> 3. 还可以做为网络传输数据的格式（现在 JSON 为主）                                 

## 3. xml 语法                   

> 1. 文档声明                  
> 2. 元素（标签）                      
> 3. xml 属性                      
> 4. xml 注释                       
> 5. 文本区域（CDATA 区）                           

### 1. 文档声明

- (1) 创建一个 xml 文件

![创建xml文件](/assets/xml/创建xml文件.png)

`文件名：`

![xml文件名](/assets/xml/xml文件名.png)

```html
<?xml version="1.0" encoding="UTF-8"?> xml 声明。
<!-- xml 声明 version 是版本的意思 encoding 是编码 -->
而且这个<?xml要连在一起写，否则会有报错
```

`属性`

> version 是版本号                     
> encoding 是 xml 的文件编码                   
> standalone="yes/no" 表示这个 xml 文件是否是独立的 xml 文件                        

- (2) 图书有 id 属性 表示唯一 标识，书名，有作者，价格的信息       

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- xml 声明 version 是版本的意思 encoding 是编码 -->
<books> <!-- 这是 xml 注释 -->
<book id="SN123123413241"> <!-- book 标签描述一本图书 id 属性描述 的是图书 的编号 -->
<name>java 编程思想</name> <!-- name 标签描述 的是图书 的信息 -->
<author>华仔</author> <!-- author 单词是作者的意思 ，描述图书作者 -->
<price>9.9</price> <!-- price 单词是价格，描述的是图书 的价格 -->
</book>
<book id="SN12341235123"> <!-- book 标签描述一本图书 id 属性描述 的是图书 的编号 -->
<name>葵花宝典</name> <!-- name 标签描述 的是图书 的信息 -->
<author>班长</author> <!-- author 单词是作者的意思 ，描述图书作者 -->
<price>5.5</price><!-- price 单词是价格，描述的是图书 的价格 -->
</book>
</books>
```

`在浏览器中可以查看到文档`

![浏览网页文档](/assets/xml/浏览网页文档.png)

### 2. xml 注释

> html 和 XML 注释 一样 : <!-- html 注释 -->                 

### 3. 元素（标签）

- html 标签：

> 格式：`<标签名>封装的数据</标签名>`                                       
> 单标签: `<标签名 /> <br /> 换行 <hr />水平线`                                       
> 双标签 `<标签名>封装的数据</标签名>`                                    
> 标签名大小写不敏感                                
> 标签有属性，有基本属性和事件属性                                
> 标签要闭合（不闭合 ，html 中不报错。但我们要养成良好的书写习惯。闭合）                                      

- (1) 什么是 xml 元素

![xml元素](/assets/xml/xml元素.png)

**元素是指从开始标签到结束标签的内容。**
`例如：<title>java 编程思想</title>`

> 元素 我们可以简单的理解为是 标签。                                

- (2) XML 命名规则

**XML 元素必须遵循以下命名规则：**

> 1.名称可以含字母、数字以及其他的字符             

*例如:*

```xml
<book id="SN213412341"> <!-- 描述一本书 -->
<author>班导</author> <!-- 描述书的作者信息 -->
<name>java 编程思想</name> <!-- 书名 -->
<price>9.9</price> <!-- 价格 -->
</book>
```

> 2.名称不能以数字或者标点符号开始

![不能以数字打头](/assets/xml/不能以数字打头.png)

![不能以标点符号打头](/assets/xml/不能以字符打头.png)

> 3.名称不能包含空格

![不能包含空格](/assets/xml/不能包含空格.png)

- (3) xml 中的元素（标签）也 分成 单标签和双标签

*单标签*
> 格式： `<标签名 属性=”值” 属性=”值” ...... />`                              

*双标签*
> 格式：`< 标签名 属性=”值” 属性=”值” ......>文本数据或子标签</标签名>`

![xml标签](/assets/xml/xml标签.png)

### 4. xml 属性

- xml 的标签属性和 html 的标签属性是非常类似的，属性可以提供元素的额外信息

> 在标签上可以书写属性：                       
> 一个标签上可以书写多个属性。每个属性的值必须使用 引号 引起来。规则和标签的书写规则一致。                           

![xml属性](/assets/xml/xml属性.png)

- (1) 属性必须使用引号引起来，不引会报错示例代码

![xml属性必须用引号](/assets/xml/xml属性必须用引号.png)

### 5. 语法规则

#### 1. 所有 XML 元素都须有关闭标签（也就是闭合）

![xml关闭标签](/assets/xml/xml关闭标签.png)

#### 2. XML 标签对大小写敏感

![xml标签大小写敏感](/assets/xml/xml标签大小写敏感.png)

#### 3. XML 必须正确地嵌套

![xml嵌套](/assets/xml/xml嵌套.png)

#### 4. XML 文档必须有根元素

> 根元素就是顶级元素，没有父标签的元素，叫顶级元素。                           
> 根元素是没有父标签的顶级元素，而且是唯一一个才行。                               

![xml文档根元素](/assets/xml/xml文档根元素.png)

#### 5. XML 的属性值须加引号

![xml属性加引号](/assets/xml/xml属性加引号.png)

####  6. XML 中的特殊字符

![xml特殊字符](/assets/xml/xml特殊字符.png)

#### 7. 文本区域（CDATA 区）

- CDATA 语法可以告诉 xml 解析器，我 CDATA 里的文本内容，只是纯文本，不需要 xml 语法解析

**CDATA 格式：**

`<![CDATA[ 这里可以把你输入的字符原样显示，不会解析 xml ]]>`

![CDATA格式](/assets/xml/CDATA格式.png)

# 二、xml 解析技术介绍

> xml 可扩展的标记语言。不管是 html 文件还是 xml 文件它们都是标记型文档，都可以使用 w3c 组织制定的 dom 技术来解析。             

![xml解析技术介绍](/assets/xml/xml解析技术介绍.png)

**document 对象表示的是整个文档（可以是 html 文档，也可以是 xml 文档）**

- 早期 JDK 为我们提供了两种 xml 解析技术 DOM 和 Sax 简介（`已经过时，但我们需要知道这两种技术`）

> dom 解析技术是 W3C 组织制定的，而所有的编程语言都对这个解析技术使用了自己语言的特点进行实现。Java 对 dom 技术解析标记也做了实现。                           
> sun 公司在 JDK5 版本对 dom 解析技术进行升级：SAX（ Simple API for XML ）                                  
> SAX 解析，它跟 W3C 制定的解析不太一样。它是以类似事件机制通过回调告诉用户当前正在解析的内容。它是一行一行的读取 xml 文件进行解析的。不会创建大量的 dom 对象。所以它在解析 xml 的时候，在内存的使用上。和性能上。都优于 Dom 解析。                         


*第三方的解析：*

> jdom 在 dom 基础上进行了封装,                          
> dom4j 又对 jdom 进行了封装。                                   
> pull 主要用在 Android 手机开发，是在跟 sax 非常类似都是事件机制解析 xml 文件。                                         

**这个 Dom4j 它是第三方的解析技术。我们需要使用第三方给我们提供好的类库才可以解析 xml 文件。**

## 1. dom4j 解析技术

> 由于 dom4j 它不是 sun 公司的技术，而属于第三方公司的技术，我们需要使用 dom4j 就需要到 dom4j 官网下载 dom4j的 jar 包。                                

### 1.Dom4j 类库的使用

![Dom4j](/assets/xml/Dom4j.png)

`解压后：`

![Dom4j解压](/assets/xml/Dom4j解压.png)

### 2. dom4j 目录的介绍

#### (1) docs 是 文 档 目 录

![docs文档目录](/assets/xml/docs文档目录.png)

#### (2) 如何查 Dom4j 的文档

![查看Dom4j](/assets/xml/查看Dom4j.png)

#### (3) Dom4j 快速入门

![Dom4j快速入门](/assets/xml/Dom4j快速入门.png)

#### (4) lib 目录

![lib目录](/assets/xml/lib目录.png)

#### (5) src 目录是第三方类库的源码目录

![src源码目录](/assets/xml/src源码目录.png)

### 3. dom4j 编程步骤

> 第一步： 先加载 xml 文件创建 Document 对象                   
> 第二步：通过 Document 对象拿到根元素对象                                       
> 第三步：通过根元素.elelemts(标签名); 可以返回一个集合，这个集合里放着。所有你指定的标签名的元素对象                                
> 第四步：找到你想要修改、删除的子元素，进行相应在的操作                                      
> 第五步，保存到硬盘上                                     

### 4. 获取 document 对象

- 创建一个 lib 目录，并添加 dom4j 的 jar 包。并添加到类路径。

![获取document对象](/assets/xml/获取document对象.png)

- 需要解析的 books.xml 文件内容

```xml
<?xml version="1.0" encoding="UTF-8"?>
<books>
<book sn="SN12341232">
<name>辟邪剑谱</name>
<price>9.9</price>
<author>班主任</author>
</book>
<book sn="SN12341231">
<name>葵花宝典</name>
<price>99.99</price>
<author>班长</author>
</book>
</books>
```

> 解析获取 Document 对象的代码                             
> 第一步，先创建 SaxReader 对象。这个对象，用于读取 xml 文件，并创建 Document                   

```java
/*
* dom4j 获取 Documet 对象
*/
@Test
public void getDocument() throws DocumentException {
// 要创建一个 Document 对象，需要我们先创建一个 SAXReader 对象
SAXReader reader = new SAXReader();
// 这个对象用于读取 xml 文件，然后返回一个 Document。
Document document = reader.read("src/books.xml");
// 打印到控制台，看看是否创建成功
System.out.println(document);
}
```

### 5. 遍历 标签 获取所有标签中的内容

- 需要分四步操作:

> 第一步，通过创建 SAXReader 对象。来读取 xml 文件，获取 Document 对象                                   
> 第二步，通过 Document 对象。拿到 XML 的根元素对象                                 
> 第三步，通过根元素对象。获取所有的 book 标签对象                               
> 第四小，遍历每个 book 标签对象。然后获取到 book 标签对象内的每一个元素，再通过 getText() 方法拿到起始标签和结束标签之间的文本内容                               

```java
/*
* 读取 xml 文件中的内容
*/
@Test
public void readXML() throws DocumentException {
// 需要分四步操作:
// 第一步，通过创建 SAXReader 对象。来读取 xml 文件，获取 Document 对象
// 第二步，通过 Document 对象。拿到 XML 的根元素对象
// 第三步，通过根元素对象。获取所有的 book 标签对象
// 第四小，遍历每个 book 标签对象。然后获取到 book 标签对象内的每一个元素，再通过 getText() 方法拿到
起始标签和结束标签之间的文本内容
// 第一步，通过创建 SAXReader 对象。来读取 xml 文件，获取 Document 对象
SAXReader reader = new SAXReader();
Document document = reader.read("src/books.xml");
// 第二步，通过 Document 对象。拿到 XML 的根元素对象
Element root = document.getRootElement();
// 打印测试
// Element.asXML() 它将当前元素转换成为 String 对象
// System.out.println( root.asXML() );
// 第三步，通过根元素对象。获取所有的 book 标签对象
// Element.elements(标签名)它可以拿到当前元素下的指定的子元素的集合
List<Element> books = root.elements("book");
// 第四小，遍历每个 book 标签对象。然后获取到 book 标签对象内的每一个元素，
for (Element book : books) {
// 测试
// System.out.println(book.asXML());
// 拿到 book 下面的 name 元素对象
Element nameElement = book.element("name");
// 拿到 book 下面的 price 元素对象
Element priceElement = book.element("price");
// 拿到 book 下面的 author 元素对象
Element authorElement = book.element("author");
// 再通过 getText() 方法拿到起始标签和结束标签之间的文本内容
System.out.println("书名" + nameElement.getText() + " , 价格:"
+ priceElement.getText() + ", 作者：" + authorElement.getText());
}
}
```

*打印内容：*

![打印内容](/assets/xml/打印内容.png)