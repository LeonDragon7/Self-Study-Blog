---
external: false
title: Java基础语法-流程控制
date: 2022-12-15
---

# 一、关于流程控制的说明
-  流程控制语句是用来控制程序中各语句执行顺序的语句，可以把语句组合成能完成一定功能的小逻辑块。
- 其流程控制方式采用结构化程序设计中规定的三种基本流程结构，即：
> 顺序结构：程序从上到下逐行地执行，中间没有任何判断和跳转。    
> 分支结构：  
① 根据循环条件，选择性地执行某段代码。  
② 有if...else和switch-case两种分支语句。  
> 循环结构：  
① 根据循环条件，重复性的执行某段代码。  
② 有while、do...while、for三种循环语句。  

- 注：JDK1.5提供了foreach循环，方便的遍历集合、数组元素。



# 二、分支结构
## 1. if-else结构
![分支结构](/assets/Java基本语法-流程控制/390b99238be04a4983b270ea1e550178.png)
![分支结构](/assets/Java基本语法-流程控制/7b70985e43484de8b5ab7d47f4802de9.png)

```java
		int heartBeats = 79;
        if(heartBeats < 60 || heartBeats > 100){
            System.out.println("需要做进一步检查");
        }
        System.out.println("检查结束");

        int age = 23;
        if(age < 18){
            System.out.println("你还可以看动画片");
        }else{
            System.out.println("你可以看成人电影了");
        }

        if(age < 0)
        {
            System.out.println("你输入的数据非法");
        }else if(age < 18){
            System.out.println("青少年时期");
        }else if(age < 35){
            System.out.println("青壮年时期");
        }else if(age < 60){
            System.out.println("中年时期");
        }else if(age < 120){
            System.out.println("老年时期");
        }else{
            System.out.println("你是要成仙啊~");
        }
```
## 2.switch-case结构
![switch-case结构](/assets/Java基本语法-流程控制/da0df77a6e9d4e27b53da3a32bc1dc09.png)
***说明：***
   ① 根据switch表达式的值，依次匹配各个case中的常量，一旦匹配成功，则进入相应case结构中，调用其执行语句。
   当调用完执行语句以后，则仍然继续向下执行其他case结构中的执行语句，直到遇到break关键字或default。
   ② break：可以使用在switch-case结构中，表示一旦执行到此关键字，就跳出switch-case结构（可选）
   ③ switch结构中的表达式，只能是如下的6种数据类型之一：byte、short、char、int、枚举类型（JDK5.0新增）、String类型（JDK7.0新增）
   ④ case之后只能声明常量或者常量表达式，不能声明变量。
   ⑤ default：相当于if-else结构中的else，位置灵活。（可选）
# 三 、Scanner类使用
- 具体实现步骤：

> 1、导包：import java.util.Scanner
>  2、Scanner的实例化
> 3、调用Scanner类的相关方法，来获取指定类型的变量



**注意：**
需要根据相应的方法，来输入指定类型的值，如果输入的数据类型与要求的类型不匹配时，会报异常：Exception in thread "main" java.util.InputMismatchException。

```java
 		//Scanner的实例化
        Scanner scanner = new Scanner(System.in);

        //调用Scanner类的相关方法
        System.out.println("请输入你的姓名:");
        String name = scanner.next();
        System.out.println(name);

        System.out.println("请输入你的芳龄:");
        int age = scanner.nextInt();
        System.out.println(age);

        System.out.println("请输入你的体重:");
        double weight = scanner.nextDouble();
        System.out.println(weight);

        System.out.println("你是否相中我了呢?(true/false)");
        boolean isLove = scanner.nextBoolean();
        System.out.println(isLove);

        //对于char型的获取，Scanner没有提供相关方法，只能获取一个字符串
        System.out.println("请输入你的性别:(男/女)");
        String gender = scanner.next();
        char genderChar = gender.charAt(0);//charAt(0):获取索引为0位置上的字符
        System.out.println(genderChar);
```

# 三、循环结构

## 1.for循环控制
- 基本语法：
>		for(循环变量初始化;循环条件;循环变量迭代){
>			循环操作(语句);
>		}

-	**说明：**
>	1.for关键字，表示循环控制
>	2.for有四元素：
>		① 循环变量初始化
>		② 循环条件
>		③ 循环操作
>		④ 循环变量迭代
>	3.循环操作，这里可以有多条语句，也就是我们要循环执行的代码
>	4.如果循环操作(语句)只有一条语句，可以省略{},建议不要省略

- **注意事项和细节说明**
>			1）循环条件是返回一个布尔值表达式
>			2）for(;循环判断条件;)中的初始化和变量迭代可以写到其他地方，但是两边的分
>			号不能省略。
>			3）循环初始化可以有多条初始化语句，但要求类型一样，并且中间用逗号隔开，
>			循环变量迭代也可以有多条变量迭代语句，中间用逗号隔开。
>			4）for(;;){}:表示一个无限循环，死循环，结合*break;*使用
 
 ## 2.while循环控制

 - 基本语法：
 > 循环变量初始化;
 > while(循环条件){
 >     循环体(语句);
 >     循环变量迭代;
 > }

 -	**说明：**
 > 1）while循环也有四要素
 > 2）只是四元素放的位置和for不一样

 - **注意事项和细节说明**
 > 1.循环条件是返回一个布尔值的表达式
 > 2.while循环是先判断在执行语句

  ## 3.do...while循环控制

  - 基本语法：
  > do{
  >	循环体(语句);
  >		循环变量迭代;
  >	}while(循环条件);

  -	**说明：**
  > 1.do...while是关键字
  > 2.也有循环四要素，只是位置不一样
  > 3.先执行，再判断，也就是说，一定会至少执行一次
  > 4.最后有一个分号;

   - **注意事项和细节说明**
   > 1）循环条件是返回一个布尔值的表达式
   > 2）do...while循环是先执行，在判断，因此它至少执行一次

   ## 4.跳转控制语句-break

   - 基本介绍：
   > break语句用于终止某个语句块的执行，一般使用在switch或者循环中

   - 基本语法：
   > {
   >   ...
   >   break;
   >   ...
   >   }
   
   - **注意事项和细节说明**
   > 1.break语句出现在多层嵌套的语句块中時，可以通过标签指明要终止的是哪一层语句块  
    > 2.标签的基本使用:  
    > label1:{  ...  
    > label2:        { ...  
    >    label3:                       {           ...  
    >                                              break label2;  
    >                                              ...  
    >                                   }  
    >                   }  
    >             }  
    **说明：**  
    > (1) break语句可以指定退出哪层。  
    > (2) label1是标签，由程序员指定。  
    > (3) break 后指定到哪个label就退出到哪里。  
    > (4) 在实际的开发中，尽量不要使用标签。  
    > (5) 如果没有指定 break，默认推出最近的循环体。  

   > 实现登录验证，有3 次机会，如果用户名为"丁真" ,密码"666"提示登录成功，否则提示还有几次机会，请使用for+break

```java
		import java.util.Scanner;
        public class BreakExercise02 { 
            public static void main(String[] args) {
                //实现登录验证，有3次机会，如果用户名为"丁真" ,密码"666"提示登录成功，
                //否则提示还有几次机会，请使用for+break完成
                //
                // 思路分析
                // 1. 创建Scanner对象接收用户输入  
                // 2. 定义 String name ; String passwd; 保存用户名和密码
                // 3. 最多循环3次[登录3次]，如果 满足条件就提前退出
                // 4. 定义一般变量 int chance 记录还有几次登录机会
                // 
                // 代码实现            
                Scanner myScanner  = new Scanner(System.in);
                String name = "";
                String passwd = "";
                int chance = 3; //登录一次 ，就减少一次
                for( int i = 1; i <= 3; i++) {//3次登录机会
                    System.out.println("请输入名字");
                    name = myScanner.next();
                    System.out.println("请输入密码");
                    passwd = myScanner.next();
                    //比较输入的名字和密码是否正确
                    //补充说明字符串 的内容 比较 使用的 方法 equals
                    // 字符串比较推荐这种写法，可以有效避免空指针。相比于（"name".equals(丁真)）
                    if("丁真".equals(name) && "666".equals(passwd)) {
                        System.out.println("恭喜你，登录成功~");
                        break;
                    }
                    //登录的机会就减少一次
                    chance--;
                    System.out.println("你还有" + chance + "次登录机会");
                }
            }
        }
```

   ## 5.跳转控制语句-break

   - 基本介绍：
   > 1) continue语句用于结束本次循环，继续执行下一次循环。
   > 2) continue语句出现在多层嵌套的循环语句体中时，可以通过标签指明要跳过的是哪一层循环，这个和前面的标签的使用的规则一样。    

   - 基本语法：  
   > {    
   >         ...  
   >         continue;  
   >         ...  
   >     }  

   ## 6.跳转控制语句-return
   - 介绍
   > return使用在方法，表示跳出所在方法。  
   **注意：如果return写在main方法，退出程序**



