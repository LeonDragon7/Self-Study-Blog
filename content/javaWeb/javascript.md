---
external: false
title: javascript
date: 2023-06-02
---

# 一、JavaScript 介绍

> Javascript 语言诞生主要是完成页面的数据验证。因此它运行在客户端，需要运行浏览器来解析执行 JavaScript 代码。         
> JS 是 Netscape 网景公司的产品，最早取名为 LiveScript;为了吸引更多 java 程序员。更名为 JavaScript。            
> JS 是弱类型，Java 是强类型。            

**特点**

> 1. 交互性（它可以做的就是信息的动态交互）           
> 2. 安全性（不允许直接访问本地硬盘）                 
> 3. 跨平台性（只要是可以解释 JS 的浏览器都可以执行，和平台无关）             

# 二、JavaScript 和 html 代码的结合方式             

## 1. 第一种方式        

- 只需要在 head 标签中，或者在 body 标签中， 使用 script 标签 来书写 JavaScript 代码

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
    <script type="text/javascript">
    // alert 是 JavaScript 语言提供的一个警告框函数。
    // 它可以接收任意类型的参数，这个参数就是警告框的提示信息
    alert("hello javaScript!");
    </script>
</head>
<body>
</body>
</html>
```

## 2. 第二种方式

- 使用 script 标签引入 单独的 JavaScript 代码文件

**文件目录：**

![文件目录](/assets/javascript/文件目录.png)

**html 代码内容：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<!--现在需要使用 script 引入外部的 js 文件来执行
src 属性专门用来引入 js 文件路径（可以是相对路径，也可以是绝对路径）
script 标签可以用来定义 js 代码，也可以用来引入 js 文件
但是，两个功能二选一使用。不能同时使用两个功能
-->
<script type="text/javascript" src="1.js"></script>
<script type="text/javascript">
alert("国哥现在可以帅了");
</script>
</head>
<body>
</body>
</html>
```

# 三、变量

- 什么是变量？变量是可以存放某些值的内存的命名。

**JavaScript 的变量类型：**

> 数值类型：number                                           
> 字符串类型：string                      
> 对象类型：object                 
> 布尔类型：boolean                           
> 函数类型：function                            

**JavaScript 里特殊的值：**

> undefined 未定义，所有 js 变量未赋于初始值的时候，默认值都是 undefined               
> null 空值                          
> NaN 全称是：Not a Number。非数字。非数值。                            

**JS 中的定义变量格式：**

> var 变量名;                
> var 变量名 = 值;                 

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
var i;
// alert(i); // undefined
i = 12;
// typeof()是 JavaScript 语言提供的一个函数。
// alert( typeof(i) ); // number
i = "abc";
// 它可以取变量的数据类型返回
// alert( typeof(i) ); // String
var a = 12;
var b = "abc";
alert( a * b ); // NaN 是非数字，非数值。
</script>
</head>
<body>
</body>
</html>
```

# 四、关系（比较）运算  

> 等于： == 等于是简单的做字面值的比较              
> 全等于： === 除了做字面值的比较之外，还会比较两个变量的数据类型                   

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
    <script type="text/javascript">
    var a = "12";
    var b = 12;
    alert( a == b ); // true
    alert( a === b ); // false
    </script>
</head>
<body>
</body>
</html>
```

# 五、逻辑运算

> 且运算：&&              
> 或运算：||              
> 取反运算：!                  

- 在 JavaScript 语言中，所有的变量，都可以做为一个 boolean 类型的变量去使用。
**0 、null、 undefined、””(空串) 都认为是 false；**

```html
/*
&& 且运算。
有两种情况：
第一种：当表达式全为真的时候。返回最后一个表达式的值。
第二种：当表达式中，有一个为假的时候。返回第一个为假的表达式的值
|| 或运算
第一种情况：当表达式全为假时，返回最后一个表达式的值
第二种情况：只要有一个表达式为真。就会把回第一个为真的表达式的值
并且 && 与运算 和 ||或运算 有短路。
短路就是说，当这个&&或||运算有结果了之后 。后面的表达式不再执行
*/

var a = "abc";
var b = true;
var d = false;
var c = null;
```

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
/* 在 JavaScript 语言中，所有的变量，都可以做为一个 boolean 类型的变量去使用。
0 、null、 undefined、””(空串) 都认为是 false；*/
// var a = 0;
// if (a) {
// alert("零为真");
// } else {
// alert("零为假");
// }
// var b = null;
// if (b) {
// alert("null 为真");
// } else {
// alert("null 为假");
// }
// var c = undefined;
// if (c) {
// alert("undefined 为真");
// } else {
// alert("undefined 为假");
// }
// var d = "";
// if (d) {
// alert("空串为真");
// } else {
// alert("空串为假");
// }
/* && 且运算。
有两种情况：
第一种：当表达式全为真的时候。返回最后一个表达式的值。
第二种：当表达式中，有一个为假的时候。返回第一个为假的表达式的值*/
var a = "abc";
var b = true;
var d = false;
var c = null;
// alert( a && b );//true
// alert( b && a );//true
// alert( a && d ); // false
// alert( a && c ); // null
/* || 或运算
第一种情况：当表达式全为假时，返回最后一个表达式的值
第二种情况：只要有一个表达式为真。就会把回第一个为真的表达式的值*/
// alert( d || c ); // null
// alert( c|| d ); //false
// alert( a || c ); //abc
// alert( b || c ); //true
</script>
</head>
<body>
</body>
</html>
```

# 六、数组

## 1. 数组定义方式

- JS 中 数组的定义：
```html
格式：
var 数组名 = []; // 空数组
var 数组名 = [1 , ’abc’ , true]; // 定义数组同时赋值元素
```

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
var arr = [true,1]; // 定义一个空数组
// alert( arr.length ); // 0
arr[0] = 12;
// alert( arr[0] );//12
// alert( arr.length ); // 0
// javaScript 语言中的数组，只要我们通过数组下标赋值，那么最大的下标值，就会自动的给数组做扩容操作。
arr[2] = "abc";
alert(arr.length); //3
// alert(arr[1]);// undefined
// 数组的遍历
for (var i = 0; i < arr.length; i++){
alert(arr[i]);
}
</script>
</head>
<body>
</body>
</html>
```

# 七、函数

## 1. 函数的二种定义方式

### 第一种，可以使用 function 关键字来定义函数。

```html
使用的格式如下:
function 函数名(形参列表){
函数体
}
在 JavaScript 语言中，如何定义带有返回值的函数？
只需要在函数体内直接使用 return 语句返回值即可！
```

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
// 定义一个无参函数
function fun(){
alert("无参函数 fun()被调用了");
}
// 函数调用===才会执行
// fun();
function fun2(a ,b) {
alert("有参函数 fun2()被调用了 a=>" + a + ",b=>"+b);
}
// fun2(12,"abc");
// 定义带有返回值的函数
function sum(num1,num2) {
var result = num1 + num2;
return result;
}
alert( sum(100,50) );
</script>
</head>
<body>
</body>
</html>
```

### 函数的第二种定义方式，格式如下：

```html
使用格式如下：
var 函数名 = function(形参列表) { 函数体 }
```

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
var fun = function () {
alert("无参函数");
}
// fun();
var fun2 = function (a,b) {
alert("有参函数 a=" + a + ",b=" + b);
}
// fun2(1,2);
var fun3 = function (num1,num2) {
return num1 + num2;
}
alert( fun3(100,200) );
</script>
</head>
<body>
</body>
</html>
```

**注：在 Java 中函数允许重载。但是在 JS 中函数的重载会直接覆盖掉上一次的定义**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
function fun() {
alert("无参函数 fun()");
}
function fun(a,b) {
alert("有参函数 fun(a,b)");
}
fun();
</script>
</head>
<body>
</body>
</html>
```

## 2. 函数的 arguments 隐形参数（只在 function 函数内）

> 就是在 function 函数中不需要定义，但却可以直接用来获取所有参数的变量。我们管它叫隐形参数。隐形参数特别像 java 基础的可变长参数一样。public void fun( Object ... args );可变长参数其他是一个数组。                     

- 那么 js 中的隐形参数也跟 java 的可变长参数一样。操作类似数组。

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
function fun(a) {
alert( arguments.length );//可看参数个数
alert( arguments[0] );
alert( arguments[1] );
alert( arguments[2] );
alert("a = " + a);
for (var i = 0; i < arguments.length; i++){
alert( arguments[i] );
}
alert("无参函数 fun()");
}
// fun(1,"ad",true);
// 需求：要求 编写 一个函数。用于计算所有参数相加的和并返回
function sum(num1,num2) {
var result = 0;
for (var i = 0; i < arguments.length; i++) {
if (typeof(arguments[i]) == "number") {
result += arguments[i];
}
}
return result;
}
alert( sum(1,2,3,4,"abc",5,6,7,8,9) );
</script>
</head>
<body>
</body>
</html>
```

# 八、JS 中的自定义对象

## 1. Object 形式的自定义对象

- 对象的定义：

> var 变量名 = new Object(); // 对象实例（空对象）                 
> 变量名.属性名 = 值; // 定义一个属性                      
> 变量名.函数名 = function(){} // 定义一个函数                     

- 对象的访问：

> 变量名.属性 / 函数名();                   

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
// 对象的定义：
// var 变量名 = new Object(); // 对象实例（空对象）
// 变量名.属性名 = 值; // 定义一个属性
// 变量名.函数名 = function(){} // 定义一个函数
var obj = new Object();
obj.name = "华仔";
obj.age = 18;
obj.fun = function () {
alert("姓名：" + this.name + " , 年龄：" + this.age);
}
// 对象的访问：
// 变量名.属性 / 函数名();
// alert( obj.age );
obj.fun();
</script>
</head>
<body>
</body>
</html>
```

## 2. {}花括号形式的自定义对象

- 对象的定义：

```html
var 变量名 = { // 空对象
    属性名：值, // 定义一个属性
    属性名：值, // 定义一个属性
    函数名：function(){} // 定义一个函数
};
```

- 对象的访问：

> 变量名.属性 / 函数名();           

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<script type="text/javascript">
// 对象的定义：
// var 变量名 = { // 空对象
// 属性名：值, // 定义一个属性
// 属性名：值, // 定义一个属性
// 函数名：function(){} // 定义一个函数
// };
var obj = {
name:"国哥",
age:18,
fun : function () {
alert("姓名：" + this.name + " , 年龄：" + this.age);
}
};
// 对象的访问：
// 变量名.属性 / 函数名();
alert(obj.name);
obj.fun();
</script>
</head>
<body>
</body>
</html>
```



