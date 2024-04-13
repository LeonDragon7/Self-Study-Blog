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

