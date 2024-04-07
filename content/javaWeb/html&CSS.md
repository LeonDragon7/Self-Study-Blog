---
external: false
title: IO流
date: 2023-05-30
---

# 一、B/S 软件的结构

- JavaSE -> C/S -> Client Server
- B/S -> Browser -> Server

![BS软件结构](/assets/html和css/BS软件结构.png)

# 二、前端的开发流程

![前端开发流程](/assets/html和css/前端开发流程.png)

# 三、网页的组成部分

- 页面由三部分内容组成，分别是内容（结构）、表现、行为。

> 内容（结构），是我们在页面中可以看到的数据。我们称之为内容。一般内容 我们使用html 技术来展示                
> 表现，指的是这些内容在页面上的展示形式。比如说。布局，颜色，大小等等。一般使用CSS 技术实现                     
> 行为，指的是页面中元素与输入设备交互的响应。一般使用 javascript 技术实现                       

# 四、HTML 简介

- Hyper Text Markup Language （超文本标记语言），简写：HTML

> HTML 通过标签来标记要显示的网页中的各个部分。网页文件本身是一种文本文件，通过在文本文件中添加标记符，可以告诉浏览器如何显示其中的内容（如：文字如何处理，画面如何安排，图片如何显示等）                   


# 五、创建 HTML 文件

## 1. 创建一个 web 工程（静态的 web 工程）

![创建web工程1](/assets/html和css/创建web工程1.png)

![创建web工程2](/assets/html和css/创建web工程2.png)

![创建web工程3](/assets/html和css/创建web工程3.png)

## 2. 在工程下创建 html 页面

![创建html页面1](/assets/html和css/创建html页面1.png)

### 选择浏览器执行页面

![选择游览器](/assets/html和css/选择游览器.png)

- 第一个 html 示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>标题</title>
</head>
<body>
    hello
</body>
</html
```

**注：Java 文件是需要先编译，再由 java 虚拟机跑起来。但 HTML 文件它不需要编译，直接由浏览器进行解析执行**

# 六、HTML 文件的书写规范

> 1. `<html></html>`:表示整个 html 页面的开始                      
> 2. `<head></head>`:头信息              
> 3. `<title>标题</title>`:标题            
> 4. `<body>页面主体内容</body>`:body 是页面的主体内容              
> 5. Html 的代码注释 <!-- 这是 html 注释，可以在页面右键查看源代码中看到 -->                    

# 七、HTML 标签介绍

## 1. 标签的格式:
> `<标签名>封装的数据</标签名>`            

## 2. 标签名大小写不敏感        

## 3. 标签拥有自己的属性

> 1. 分为基本属性：bgcolor="red",可以修改简单的样式效果                 
> 2. 事件属性：onclick="alert('你好！');",可以直接设置事件响应后的代码                

## 4. 标签又分为，单标签和双标签

> 1. 单标签格式： <标签名 /> ,br 换行,hr 水平线                 
> 2. 双标签格式: <标签名> ...封装的数据...</ 标签名>       

![标签介绍](/assets/html和css/标签介绍.png)

### 标签的语法：

- <!-- ①标签不能交叉嵌套 -->

```html
正确：<div><span>早安，尚硅谷</span></div>
错误：<div><span>早安，尚硅谷</div></span>
<hr />
```

- <!-- ②标签必须正确关闭 -->

```html
<!-- i.有文本内容的标签： -->
正确：<div>早安，尚硅谷</div>
错误：<div>早安，尚硅谷
<hr />

<!-- ii.没有文本内容的标签： -->
正确：<br />
错误：<br>
<hr />
```

- <!-- ③属性必须有值，属性值必须加引号 -->

```html
正确：<font color="blue">早安，尚硅谷</font>
错误：<font color=blue>早安，尚硅谷</font>
错误：<font color>早安，尚硅谷</font>
<hr />
```

- <!-- ④注释不能嵌套 -->

```html
正确：<!-- 注释内容 --> <br/>
错误：<!-- 这是错误的 html 注释 -->
<hr />
```

**注意事项：html 代码不是很严谨。有时候标签不闭合，也不会报错**
