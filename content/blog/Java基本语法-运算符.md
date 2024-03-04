---
external: false
title: Java基本语法-运算符
date: 2022-12-10
---

# 一、运算符
运算符是一种特殊的符号，用以表示数据的运算、赋值和比较等。

 - 算术运算符
 - 赋值运算符
 - 比较运算符（关系运算符）
 - 逻辑运算符
 - **位运算符**
 - 三元运算符

# 二、算术运算符
![算术运算符](/assets/Java基本语法-运算符/8d092bb175974f95b07de3338891cebc.png)
**注：%:取余运算 结果的符号与被模数的符号相同**

练习:
- 随意给出一个整数，打印显示它的个位数，十位数，百位数的值。
例如：数字153的情况如下：
个位数：3
十位数：5
百位数：1

```java
		//整数被除10就去掉小数点后面的一位：例如：201除10 20.1 返回整型为20
		//取余10得出每位数从个位开始
		int num = 435;
        System.out.println("个位数：" + num % 10);
        System.out.println("十位数：" + num / 10 % 10);
        System.out.println("百位数：" + num / 10 / 10 % 10);
```
# 三、赋值运算符
- 符号：=
1.当“=”两侧数据类型不一致时，可以使用自动类型转换或使用强制类型转换原则进行处理。
2.**支持连续赋值。**
- 扩展赋值运算符：+=，-=，*=，/=，%=

```java
		int n1 = 10;
        n1 +=(n1++) + (++n1);
        System.out.println(n1);//32
```
# 四、比较运算符
![比较运算符](/assets/Java基本语法-运算符/f7e56ad3cc3a4d8b8a5366c4be68ad0a.png)
- 比较运算符的结果都是boolean型，也就是要么是true，要么是false。
- **比较运算符“==”不能误写成“=”。**

```java
		boolean b3 = false;
		
        if(b3 == true)
            System.out.println("结果为真");
        else
            System.out.println("结果为假");//输出为假

		if(b3 = true)
            System.out.println("结果为真");//输出为真
        else
            System.out.println("结果为假");
```
# 五、逻辑运算符
&-逻辑与       |-逻辑或       !-逻辑非
&&-短路与      ||-短路或       ^-逻辑异或
![逻辑运算符](/assets/Java基本语法-运算符/9c5547aeb99c42c9a90ce8d8d9b35b4a.png)

```java
		//区分& 与 &&
        /*
        相同点1：& 与 && 的运算结果相同
        相同点2：当符号左边是true时，二者都会执行符号右边的运算
        不同点：当符号左边是false时，&继续执行符号右边的运算，&&不再执行符号右边的运算
         */
        boolean b1 = true;
        b1 = false;
        int num1 = 10;
        if(b1 & (num1++ > 0))
            System.out.println("我现在在北京");
        else
            System.out.println("我现在在南京");
        System.out.println("num1 = " + num1);//11

        boolean b2 = true;
        b2 = false;
        int num2 = 10;
        if(b2 && (num2++ > 0))
            System.out.println("我现在在北京");
        else
            System.out.println("我现在在南京");
        System.out.println("num2 = " + num2);//10

        //区分& 与 &&
        /*
        相同点1：| 与 || 的运算结果相同
        相同点2：当符号左边是false时，二者都会执行符号右边的运算
        不同点：当符号左边是true时，|继续执行符号右边的运算，||									  不再执行符号右边的运算
         */
        boolean b3 = false;
        b3 = true;
        int num3 = 10;
        if(b3 | (num3++ > 0))
            System.out.println("我现在在北京");
        else
            System.out.println("我现在在南京");
        System.out.println("num3 = " + num3);//11

        boolean b4 = false;
        b4 = true;
        int num4 = 10;
        if(b4 || (num4++ > 0))
            System.out.println("我现在在北京");
        else
            System.out.println("我现在在南京");
        System.out.println("num4 = " + num4);//10
```
**说明：**
1.逻辑运算符操作的都是boolean类型的变量
2.开发中，推荐使用 && 和 ||
# 六、位运算符
![位运算符](/assets/Java基本语法-运算符/ac8e397aef474c9492e0bb8fe4278222.png)
![二进制](/assets/Java基本语法-运算符/60b50f6c81074a428e2f22a6f2840755.png)
![二进制](/assets/Java基本语法-运算符/98e09986f7ad40018c7f363980c90cf7.png)
![二进制](/assets/Java基本语法-运算符/85d4fe6a921549b2ae8433d867011f6e.png)

- 位运算是直接对整数的二进制进行的运算

```java
		int i = 21;
        System.out.println("i << 2 :" + (i << 2));//84
        
        int m = 12;
        int n = 5;
        System.out.println("m & n :" + (m & n));//4
        System.out.println("m | n :" + (m | n));//13
        System.out.println("m ^ n :" + (m ^ n));//9

        int k = 6;
        System.out.println("~6 : " + ~6);//-7
```
![位运算符的细节](/assets/Java基本语法-运算符/473989b1277547fe9222aa2f88286df9.png)
**正解2图解：**
![二进制](/assets/Java基本语法-运算符/f40bc2e349b9479b89742d3b08961648.png)
```java
//练习：交换两个变量的值
        //自编1：
        int temp;
        int num1 = 10;
        int num2 = 20;
        //定义临时变量(推荐)
        temp = num1;
        num1 = num2;
        num2 = temp;
        System.out.println("num1 = " + num1);
        System.out.println("num2 = " + num2);

        //自编2：使用位运算符 - 与运算和或运算
        int num3 = 10;
        int num4 = 20;
        System.out.println("num3 = " + ((num3 | num4) & num4));
        System.out.println("num4 = " + ((num3 | num4) & num3));

        //正解1：
        /*
            好处：不用定义临时变量
            弊端：①相加操作可能超出存储范围。②有局限性：只能适用于数值类型。
         */
        int num5 = 10;
        int num6 = 20;
        num5 = num5 + num6;
        num6 = num5 - num6;
        num5 = num5 - num6;
        System.out.println("num5 = " + num5);
        System.out.println("num6 = " + num6);

        //正解2：使用位运算符 - 异或运算
        int num7 = 10;
        int num8 = 20;
        System.out.println("num7 = " + ((num7 ^ num8) ^ num7));
        System.out.println("num8 = " + ((num7 ^ num8) ^ num8));
```
# 七、三元运算符
- **格式：**
               
>  1. (条件表达式) ? 表达式1:表达式2;
>                 ① 当为true是，运算后的结果是表达式1;
>                 ② 当为false是，运算后的结果是表达式2;
> 2. 表达式1和表达式2定义前需**同种类型(统一类型)**
> 3. 三元运算符可以嵌套使用
> 4. **三元运算符与if-else的联系与区别**：
>                 ① 三元运算符可简化if-else
>                 ② 三元运算符要求必须返回一个结果
>                 ③ if后的代码块可有多个语句
>                 ④ 能用if-else，但是不一定能用三元运算符
>                 ⑤ 如果程序既可以使用三元运算符，又可以使用if-else			结构，那么优先选择三元运算符。原因：简洁、执行效率高。
```java
		int m = 12;
        int n = 5;

        double num = m > n ? 2 : 1.0;
        System.out.println(num);//2.0

        String maxStr = m > n ? "m大" : "n大";
        System.out.println(maxStr);//m大
        //优化
        String maxStr1 = m > n ? "m大" : m == n ? "m和n相等" : "n大";
        System.out.println(maxStr1);
```
# 八、运算符的优先级
- 运算符有不同的优先级，所谓优先级就是表达式运算中的运算顺序。
![运算符的优先级](/assets/Java基本语法-运算符/9995ad2ee7e7436f98dbc2cca82d50c3.png)
- 只有单目运算符、三元运算、赋值运算符是从右向左运算的。
