# java学习框架
![](..\img\java学习框架.jpg)

# 环境变量设置
- 右键我的电脑->属性->高级->环境变量->系统变量
    >注意：是下面的系统变量，不是上面的用户变量
- 新建变量名 JAVA_HOME，变量值 E:\JDK
    - 修改变量 Path ，在最前面加上 %JAVA_HOME%\bin;
        >注意："Path"是首字母大写，不要改成"PATH" bin后面要有分号;

        >注意：系统变量上面的用户变量里，不要有这两个，如果有应该去掉，以避免被干扰。

    ![1](..\img\264.png)
    ![1](..\img\6560.png)

# 验证配置
- 点WIN键->运行（或者使用win+r)
- 输入cmd命令
    - 输入java -version
- 如果出现版本信息，表明配置成功
![1](..\img\Snipaste_2019-08-06_10-06-54.png)



# 面向对象

https://zhidao.baidu.com/question/306745403487135764.html

首先要明白Java是面向对象的语言,
也就是把我们所用到的东西都看成对象来处理.
有句话叫万事万物皆对象,这个世界上任何的事物都可以看成是一个对象,
在Java的世界中也是如此.
举个例子说明,
你喝水用的杯子跟我喝水用的杯子也许是相同的,
更可能是同一个厂家生产的,
如果是这样,那么你的杯子是一个对象,
我的杯子也是一个对象,
而生产杯子的工厂是通过模板来生产出这一个个相同的杯子对象的,
在Java中模板就是所谓的类.
面向过程与面向对象的区别就在于面向过程注重如何去制造这样一个杯子,
也就是工厂要记住制造杯子的过程,然后重复这个过程来生产.
而面向对象则是把制造这个杯子需要的材料工艺等等看作是模板也就是杯子类,
然后需要杯子的时候只需要调用这个杯子模板即可.
那么你所问的这一句实际上就是在Java中最常见的一句通过一个模板来创建一个对象的过程.

```
    JFrame               f           =           new        JFrame();
这是规定你所需要的   这里给你通过  已经定义好了  创建对象的   调用构造方法来
对象是什么类型的,也  模板创建的那  模板与对象名  固定写法,这  进行赋值,也就
就是我们所说的模板   个对象起一个  那么接下来要  是一个关键   相当于是我们
                   对象名,比如   对它们实体化, 字,通过new   通过模板来进
                   你的杯子,我   也就是进行赋  来告诉Java   行实际的杯子
                   的杯子等      值操作       你要创建对象  生产
```

# Java程序基础

## JAVA程序的基本结构
### 类

java是面向对象的语言，一个程序的基本单位就是class，class是关键字。
```java
public class Hello { // 类名是Hello
    // ...
} // class定义结束
```

类名要求：
- 必须以英文字母开头，后面接字幕数字和下划线的组合
- 习惯以大写字母开头

public 是访问修饰符，表示该class是公开的。
>不写public也能编译，但是这个类将无法从命令执行。

### 方法(函数)

在class内部，可以定义若干个方法(method)。

```java
public class Hello {
    public static void main(String[] args) { // 方法名是main，返回值是void，表示没有返回值
        // 方法代码...
    } // 方法定义结束
}
```
方法定义了一组执行语句，方法内部的代码会被依次序执行

public除了修饰class外，也可以修饰方法。关键字static是静态方法的修饰符

java入口程序规定的方法必须是静态方法，方法名必须为main，括号内参数必须是String数组

方法命名规则和class一样，但首字母小写

方法内部的语句才是真正的执行代码，java每一行语句必须以分号结束

### 注释
在java程序中，注释是一种给人阅读的文本，编译器会自动忽略注释

java有三种注释，第一种是单行注释，以双斜线开头，直到行尾结束

```java
//这是注释
```

多行注释以`/*`开头。`*/`结束，可以有多行

```java
/*
这是注释
blablabla...
这也是注释
*/
```

还有一种特殊的多行注释，以`/**开头`，`*/`结尾，如果有多行，每行通常以星号开头

```java
/**
 * 可以用来自动创建文档的注释
 * 
 * @auther liaoxuefeng
 */
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```
这种特殊的多行注释需要写在类和方法的定义出，可以用于自动创建文档

## 变量和数据类型
java中，变量分两种：基本类型变量和引用类型变量

java中，变量必须先定义后使用，在定义变量时，可以给他一个初始值，比如：

```java
int x = 1;
```
不写初始值相当于指定默认值，默认值总是0

变量的一个重要特点是可以重新赋值，而且可以赋值给其他变量
```java
public class Main {
    public static void main(String[] args) {
        int n = 100; // 定义变量n，同时赋值为100
        System.out.println("n = " + n); // 打印n的值

        n = 200; // 变量n赋值为200
        System.out.println("n = " + n); // 打印n的值

        int x = n; // 变量x赋值为n（n的值为200，因此赋值后x的值也是200）
        System.out.println("x = " + x); // 打印x的值

        x = x + 100; // 变量x赋值为x+100（x的值为200，因此赋值后x的值是200+100=300）
        System.out.println("x = " + x); // 打印x的值
        System.out.println("n = " + n); // 再次打印n的值，n应该是200还是300？
   }
}
```

### 基本数据类型
基本数据类型是CPU可以直接进行运算的类型。java定义了以下几种基本数据类型
- 整数类型：byte，short，int，long
- 浮点数类型：float，double
- 字符类型：char
- 布尔类型：boolean

计算机内存的最小存储单元是字节(byte)，一个字节就是一个8位二进制是，即8个bit。它的二进制表示范围从00000000~11111111，换算成十进制是0~255，换算成十六进制是00~ff

内存单元从0开始编号，称为内存地址。每个内存单元可以看作一间房间，内存地址就是门牌号。
```
  0   1   2   3   4   5   6  ...
┌───┬───┬───┬───┬───┬───┬───┐
│   │   │   │   │   │   │   │...
└───┴───┴───┴───┴───┴───┴───┘
```

一个字节是 1byte ，1024 字节是 1K，1024K 是 1M，1024M 是 1G，1024G 是 1T。一个拥有 4T 内存的计算机的字节数量就是：
```
4T = 4 x 1024G
   = 4 x 1024 x 1024M
   = 4 x 1024 x 1024 x 1024K
   = 4 x 1024 x 1024 x 1024 x 1024
   = 4398046511104
```
不同的数据类型占用的字节数不一样。我们看一下 Java 基本数据类型占用的字节数：
```
       ┌───┐
  byte │   │
       └───┘
       ┌───┬───┐
 short │   │   │
       └───┴───┘
       ┌───┬───┬───┬───┐
   int │   │   │   │   │
       └───┴───┴───┴───┘
       ┌───┬───┬───┬───┬───┬───┬───┬───┐
  long │   │   │   │   │   │   │   │   │
       └───┴───┴───┴───┴───┴───┴───┴───┘
       ┌───┬───┬───┬───┐
 float │   │   │   │   │
       └───┴───┴───┴───┘
       ┌───┬───┬───┬───┬───┬───┬───┬───┐
double │   │   │   │   │   │   │   │   │
       └───┴───┴───┴───┴───┴───┴───┴───┘
       ┌───┬───┐
  char │   │   │
       └───┴───┘
```
byte 恰好就是一个字节，而 long 和 double 需要8个字节。

### 整型
对于整型类型，java 只定义了带符号的整型，因此，最高位的bit表示符号位(0表示正数，1表示负数)

各种整型能表示的最大范围如下
- byte：-128 ~ 127
- short: -32768 ~ 32767
- int: -2147483648 ~ 2147483647
- long: -9223372036854775808 ~ 9223372036854775807

定义例子
```java
public class Main {
    public static void main(String[] args) {
        int i = 2147483647;
        int i2 = -2147483648;
        int i3 = 2_000_000_000; // 加下划线更容易识别
        int i4 = 0xff0000; // 十六进制表示的16711680
        int i5 = 0b1000000000; // 二进制表示的512
        long l = 9000000000000000000L; // long型的结尾需要加L
    }
}
```
>特别注意：同一个数的不同进制的表示是完全相同的，例如 `15 = 0xf ＝ 0b1111`

### 浮点型
浮点型的数就是小数。因为小数用科学计数法表示的时候，小数点是可以‘浮动’的，如1234.5可以表示成12.345x10^3，所以称为浮点数

定义例子
```java
float f1 = 3.14f;
float f2 = 3.14e38f; // 科学计数法表示的3.14x10^38
double d = 1.79e308;
double d2 = -1.79e308;
double d3 = 4.9e-324; // 科学计数法表示的4.9x10^-324
```

对于 float 类型，需要加上 f 后缀

浮点数可以表示的范围非常大，float 类型可最大表示3.4x10^38，而 double 类型可最大表示1.79x10^308

### 布尔类型
布尔类型 boolean 只有 true 和 false 两个值，布尔类型总是关系运算的计算结果

定义例子
```java
boolean b1 = true;
boolean b2 = false;
boolean isGreater = 5 > 3; // 计算结果为true
int age = 12;
boolean isAdult = age >= 18; // 计算结果为false
```

java 对布尔类型的存储并没有做规定，因为理论上存储布尔类型只需要1bit，但通常JVM内部会把 boolean 表示为4字节整数

### 字符类型
字符类型 char 表示一个字符，java 的 char 类型除了可以表示标准的 ASKII 外，还可以表示一个 Unicode 字符

```java
public class Main {
    public static void main(String[] args) {
        char a = 'A';
        char zh = '中';
        System.out.println(a);
        System.out.println(zh);
    }
}
```

>char类型使用单引号 (`'`),而且仅有一个字符，要和双引号(`"`)的字符串类型区分开

### 常量
定义变量的时候，如果加上 final 修饰符，这个变量就变成了常量
```java
final double PI = 3.14; // PI是一个常量
double r = 5.0;
double area = PI * r * r;
PI = 300; // compile error!
```

常量在定义时进行初始化后就不可再次赋值，再次赋值会导致编译错误

常量的作用是用有意义的变量名来避免魔术数字(Magic number)，例如，不要在代码中到处写3.14，而是定义一个常量。如果将来需要提高计算精度，我们只需要在常量的定义处修改，例如，改成3.1416，而不必在所有地方替换3.14。

根据习惯，常量名通常全大写

### var关键字(java 10特性)
有些时候，类型的名字太长，写起来比较麻烦，例如
```java
StringBuilder sb = new StringBuilder();
```
这个时候，如果想省略变量类型，可以使用var关键字：
```
var sb = new StringBuilder();
```

编译器会根据赋值语句自动推断出变量sb的类型是StringBuilder。对编译器来说，语句：
```
var sb = new StringBuilder();
```

实际上会自动变成：
```
StringBuilder sb = new StringBuilder();
```

因此，使用var定义变量，仅仅是少写了变量类型而已。

### 变量的作用范围
在 java 中，多行语句用{}括起来，很多控制语句，例如条件判断和循环，都以{}作为他们自身的范围，例如
```java
if (...) { // if开始
    ...
    while (...) { while 开始
        ...
        if (...) { // if开始
            ...
        } // if结束
        ...
    } // while结束
    ...
} // if结束
```
正确嵌套编译器就能识别语句块的开始和结束，在语句块中定义的变量，他有一个作用域，就是从定义出开始，到语句块结束。超出了作用域引用这些变量，编译器会报错

定义变量时，要遵循作用域最小化原则，尽量将变量定义在尽可能小的作用域，并且，不要重复使用变量名。

## 整数运算
java 整数运算遵循四则运算规则，可以使用任意嵌套的小括号。
例如
```java
public class Main {
    public static void main(String[] args) {
        int i = (100 + 200) * (99 - 88); // 3300
        int n = 7 * (5 + (i - 9)); // 23072
        System.out.println(i);
        System.out.println(n);
    }
}
```

整数的数值表示不但是精确的，而且整数运算永远是精确的，即使是除法也是精确的，因为两个整数相除只能得到结果的整数部分
```java
int x = 12345 / 67; // 184
```
求余运算使用%：

```java
int y = 12345 % 67; // 12345÷67的余数是17
```
>特别注意：整数的除法对于除数为0时运行时将报错，但编译不会报错。

### 溢出
要特别注意，整数由于存在范围限制，如果计算结果超出了范围，就会产生溢出，而溢出`不会出错`,却会得到一个奇怪的结果

例如：
```java
public class Main {
    public static void main(String[] args) {
        int x = 2147483640;
        int y = 15;
        int sum = x + y;
        System.out.println(sum); // -2147483641
    }
}
```

解释上述结果：

把整数2147483640和15换成二进制做加法：
```
  0111 1111 1111 1111 1111 1111 1111 1000
+ 0000 0000 0000 0000 0000 0000 0000 1111
-----------------------------------------
  1000 0000 0000 0000 0000 0000 0000 0111
```
由于最高位计算结果为1，因此，加法的结果变成了一个负数

要解决上面的问题，可以把 int 型换成 long 型 ，由于 long 克表示的整型范围更大，所以结果不会溢出

```java
long x = 2147483640;
long y = 15;
long sum = x + y;
System.out.println(sum); // 2147483655
```

还有一种简写的运算符，即`+=`，`-=`，`*=`，`/=`，它们的使用方法如下：
```
n += 100; // 3409, 相当于 n = n + 100;
n -= 100; // 3309, 相当于 n = n - 100;
```

### 自增/自减
Java还提供了++运算和--运算，它们可以对一个整数进行加1和减1的操作：
```java
public class Main {
    public static void main(String[] args) {
        int n = 3300;
        n++; // 3301, 相当于 n = n + 1;
        n--; // 3300, 相当于 n = n - 1;
        int y = 100 + (++n); // 不要这么写
        System.out.println(y);
    }
}
```
注意++写在前面和后面计算结果是不同的，++n 表示先加1再引用n，n++ 表示先引用n再加1。不建议把++运算混入到常规运算中，容易自己把自己搞懵了。

### 移位计算
在计算机中，整数总是以二进制的形式表示，例如，int 类型的整数 7 使用 4 字节表示的二进制如下

```
00000000 0000000 0000000 00000111
```

可以对整数进行移位运算，对整数7左移1位得到整数14，左移两位得到整数28
```java
int n = 7;       // 00000000 00000000 00000000 00000111 = 7
int a = n << 1;  // 00000000 00000000 00000000 00001110 = 14
int b = n << 2;  // 00000000 00000000 00000000 00011100 = 28
int c = n << 28; // 01110000 00000000 00000000 00000000 = 1879048192
int d = n << 29; // 11100000 00000000 00000000 00000000 = -536870912
```

左移29位时，由于最高位变成1，因此结果变为负数
类似的，对整数28进行右移，结果如下：
```java
int n = 7;       // 00000000 00000000 00000000 00000111 = 7
int a = n >> 1;  // 00000000 00000000 00000000 00000011 = 3
int b = n >> 2;  // 00000000 00000000 00000000 00000001 = 1
int c = n >> 3;  // 00000000 00000000 00000000 00000000 = 0

```
如果对一个负数进行右移，最高位的1不动，结果仍然是一个负数：
```java
int n = -536870912;
int a = n >> 1;  // 11110000 00000000 00000000 00000000 = -268435456
int b = n >> 2;  // 10111000 00000000 00000000 00000000 = -134217728
int c = n >> 28; // 11111111 11111111 11111111 11111110 = -2
int d = n >> 29; // 11111111 11111111 11111111 11111111 = -1

```
还有一种不带符号的右移运算，使用>>>，它的特点是符号位跟着动，因此，对一个负数进行>>>右移，它会变成正数，原因是最高位的1变成了0：
```java
int n = -536870912;
int a = n >>> 1;  // 01110000 00000000 00000000 00000000 = 1879048192
int b = n >>> 2;  // 00111000 00000000 00000000 00000000 = 939524096
int c = n >>> 29; // 00000000 00000000 00000000 00000111 = 7
int d = n >>> 31; // 00000000 00000000 00000000 00000001 = 1

```
对byte和short类型进行移位时，会首先转换为int再进行位移

左移实际上就是不断地×2，右移实际上就是不断地÷2

### 位运算
位运算是按位进行与，或，非，和异或的运算

与运算的规则：必须两个数同时为1，结果才为1

```java
n = 0 & 0; // 0
n = 0 & 1; // 0
n = 1 & 0; // 0
n = 1 & 1; // 1
```

或运算的规则：只要任意一个为1，结果就为1

```java
n = 0 | 0; // 0
n = 0 | 1; // 1
n = 1 | 0; // 1
n = 1 | 1; // 1
```

非运算的规则：0和1互换

```java
n = ~0; // 1
n = ~1; // 0
```

异或运算的规则：如果两个数不同，结果为1，否则为0

```java
n = 0 ^ 0; // 0
n = 0 ^ 1; // 1
n = 1 ^ 0; // 1
n = 1 ^ 1; // 0
```

对着两个整数进行位运算，实际上就是按位对其，然后依次对每一位进行运算

例如
```java
public class Main {
    public static void main(String[] args) {
        int i = 167776589; // 00001010 00000000 00010001 01001101
        int n = 167776512; // 00001010 00000000 00010001 00000000
        System.out.println(i & n); // 167776512
    }
}
```
>上述按位与运算实际上可以看作两个整数表示的IP地址10.0.17.77和10.0.17.0，通过与运算，可以快速判断一个IP是否在给定的网段内。

### 运算优先级
在java 的计算表达式中，运算优先级从高到低依次是

- `()`
- `! ~ ++ --`
- `* / %`
- `+ -`
- `<< >> >>>`
- `&`
- `|`
- `+= -= *= /=`

>记不住也没关系，只需要加括号就可以保证运算的优先级正确。

### 类型自动提升与强制转型
运算过程中，如果参与运算的两个数类型不一致，那么计算结果为较大类型的整型。例如，short 和 int 计算，接过总是int ，原因是 short 首先自动被转型为 int 

例如
```java
public class Main {
    public static void main(String[] args) {
        short s = 1234;
        int i = 123456;
        int x = s + i; // s自动转型为int
        short y = s + i; // 编译错误!
    }
}
```

也可以将结果强制转型，即将大范围的整数转型为小范围的整数。强制转型使用 (类型) ，例如，将 int 强制转型为 short：

```java
int i = 12345;
short s = (short) i; // 12345
```

要注意，超出范围的强制转型会得到错误的结果，原因是转型时， int 的两个高位字节直接被扔掉了，仅保留了低位的两个字节：

```java
public class Main {
    public static void main(String[] args) {
        int i1 = 1234567;
        short s1 = (short) i1; // -10617
        System.out.println(s1);
        int i2 = 12345678;
        short s2 = (short) i2; // 24910
        System.out.println(s2);
    }
}
```

因此，强制转型的结果可能是错的

## 浮点数运算
浮点数运算和整数运算相比，只能进行加减乘除这些数值计算，不能做位运算和移位运算

在计算机中，浮点数虽然表示的范围大，但是，浮点数有个非常重要的特点，就是浮点数常常无法精确表示。

举个例子：

浮点数 0.1 在计算机中就无法精确表示，因为十进制的 0.1 换算成二进制是一个无限循环小数，无论使用 float 还是 double ，都只能存储一个 0.1 的近似值。但是 0.5 这个浮点数又可以精确的表示

因为浮点数常常无法精确表示，因浮点数运算会产生误差

```java
public class Main {
    public static void main(String[] args) {
        double x = 1.0 / 10;
        double y = 1 - 9.0 / 10;
        // 观察x和y是否相等:
        System.out.println(x);
        System.out.println(y);
    }
}
```

由于浮点数存在运算误差，所以比较两个浮点数是否相等常常会出现错误的结果。正确的比较方法是判断两个浮点数之差的绝对值是否小于一个很小的数：

```java
// 比较x和y是否相等，先计算其差的绝对值:
double r = Math.abs(x - y);
// 再判断绝对值是否足够小:
if (r < 0.00001) {
    // 可以认为相等
} else {
    // 不相等
}
```

浮点数在内存的表示方法和整数比更加复杂。Java的浮点数完全遵循IEEE-754标准，这也是绝大多数计算机平台都支持的浮点数标准表示方法。

>该标准的全称为IEEE二进制浮点数算术标准（ANSI/IEEE Std 754-1985），又称IEC 60559:1989，微处理器系统的二进制浮点数算术（本来的编号是IEC 559:1989）

>IEEE二进制浮点数算术标准（IEEE 754）是20世纪80年代以来最广泛使用的浮点数运算标准，为许多CPU与浮点运算器所采用。这个标准定义了表示浮点数的格式（包括负零-0）与反常值（denormal number）），一些特殊数值（无穷（Inf）与非数值（NaN）），以及这些数值的“浮点数运算符”；它也指明了四种数值舍入规则和五种例外状况（包括例外发生的时机与处理方式）。

### 类型提升
如果参与运算的两个数其中一个是整型，那么整型可以自动提升到浮点型

```java
public class Main {
    public static void main(String[] args) {
        int n = 5;
        double d = 1.2 + 24.0 / n; // 6.0
        System.out.println(d);
    }
}
```

需要特别注意，在一个复杂的四则运算中，两个整数的运算不会出现自动提升

例如：
```java
double d = 1.2 + 24 / 5; // 5.2
```

计算结果为 5.2 ，原因是编译器计算 24/5 这个子表达式时，按两个整数进行运算，结果仍为整数  4

### 溢出
整数运算在除数为 0 时会报错，而浮点数运算在除数为 0 时不会报错，但会返回几个特殊值：
- NaN表示Not a Number
- Infinity表示无穷大
- -Infinity表示负无穷大

例如：
```java
double d1 = 0.0 / 0; // NaN
double d2 = 1.0 / 0; // Infinity
double d3 = -1.0 / 0; // -Infinity
```

这三种特殊值在实际运算中很少碰到，我们只需要了解即可

### 强制转型
可以将浮点数强制转型为整数，在转型时，浮点数的小数部分会被丢掉。如果转型后超过了整型能表示的最大范围，将返回整型的最大值

例如：
```java
int n1 = (int) 12.3; // 12
int n2 = (int) 12.7; // 12
int n2 = (int) -12.7; // -12
int n3 = (int) (12.7 + 0.5); // 13
int n4 = (int) 1.2e20; // 2147483647
```

如果要进行四舍五入，可以对浮点数加上0.5再强制转型

```java
public class Main {
    public static void main(String[] args) {
        double d = 2.6;
        int n = (int) (d + 0.5);
        System.out.println(n);
    }
}
```

## 布尔运算
对于布尔类型 boolean 永远只有 true 和 false 两个值

布尔运算是一种关系运算，包括以下几类：
- 比较运算符：`>，>=，<，<=，==，!=`
- 与运算符：`&&`
- 或运算：`||`
- 非运算：`！`

下面是一些示例：
```java
boolean isGreater = 5 > 3; // true
int age = 12;
boolean isZero = age == 0; // false
boolean isNonZero = !isZero; // true
boolean isAdult = age >= 18; // false
boolean isTeenager = age >6 && age <18; // true
```
关系运算符的优先级从高到低依次是：

- `!`
- `>，>=，<，<=`
- `==，!=`
- `&&`
- `||`

### 短路运算
布尔运算的一个重要特点是短路运算。如果一个布尔运算的表达式能提前确定结果，则后续的计算不再执行，直接返回结果。

因为 flase && x 的结果总是 false ，无论 x 是 true 还是 false ，因此，与运算在确定第一个值为 false 后不再继续计算，直接返回值 false 。

例：
```java
public class Main {
    public static void main(String[] args) {
        boolean b = 5 < 3;
        boolean result = b && (5 / 0 > 0);
        System.out.println(result);
    }
}
```
如果没有短路运算，&&后面的表达式会由于除数为0而报错，但实际上该语句并未报错，原因在于与运算是短路运算符，提前计算出了结果false。

如果变量b的值为true，则表达式变为true && (5 / 0 > 0)。因为无法进行短路运算，该表达式必定会由于除数为0而报错

类似的，对于||运算，只要能确定第一个值为true ，后续计算也不再执行，直接返回true 

```java
boolean result = true || (5 / 0 > 0); // true
```

### 三元运算符
java 提供一个三元运算符 b ? x : y ,它更具第一个布尔表达式的结果，分别返回后续两个表达式之一的运算结果

例：
```java
public class Main {
    public static void main(String[] args) {
        int n = -100;
        int x = n >= 0 ? n : -n;
        System.out.println(x);
    }
}
```
上述语句的意思是，判断n >= 0是否成立，如果为true，则返回n，否则返回-n。这实际上是一个求绝对值的表达式。

注意到三元运算b ? x : y会首先计算b，如果b为true，则只计算x，否则，只计算y。此外，x和y的类型必须相同，因为返回值不是boolean，而是x和y之一。

## 字符和字符串
在java 中，字符和字符串是两个不同的类型

### 字符类型
字符类型 char 是基本数据类型，他是 character 的缩写。一个 char 保存一个 Unicode 字符

```java 
char c1 = 'A';
char c2 = '中';
```

因为 java 在内存中总是使用 Unidcode 字符，所以，一个英文字符和一个中文字符都用一个 char 类型表示，它们都占用两个字节，要显示一个字符的 Unicode 编码，只需将 char 类型直接赋值给 int 类型即可

```java
int n1 = 'A'; // 字母“A”的Unicodde编码是65
int n2 = '中'; // 汉字“中”的Unicode编码是20013
```

还可以直接用转义字符\u+Unicode编码来表示一个字符

```java
// 注意是十六进制:
char c3 = '\u0041'; // 'A'，因为十六进制0041 = 十进制65
char c4 = '\u4e2d'; // '中'，因为十六进制4e2d = 十进制20013
```

### 字符串类型
和 char 类型不同，字符串类型 String 是引用类型，我们用双引号"···"表示字符串。一个字符串可以储存0到任意个字符

```java
String s = ""; // 空字符串，包含0个字符
String s1 = "A"; // 包含一个字符
String s2 = "ABC"; // 包含3个字符
String s3 = "中文 ABC"; // 包含6个字符，其中有一个空格
```

因为字符串使用双引号"···"表示开始和结束，那如果字符串本身恰好包含一个 " 字符怎么表示？例如，"ABC"XYZ"，编译器就无法判断中间的引号究竟是字符串的一部分还是表示字符串的结束，这个时候需要借助转义字符 \ 

```java
String s = "abc\"xyz"; // 包含7个字符: a, b, c, ", x, y, z
```

因为\是转义字符，所以两个`\\`表示一个\字符

```java
String s = "abc\\xyz"; // 包含7个字符: a, b, c, \, x, y, z
```

常见转义字符包括:
- \" 表示字符"
- \' 表示字符'
- `\\` 表示字符\
- \n 表示换行符
- \r 表示回车符
- \t 表示Tab
- \u##### 表示一个Unicode编码的字符

例：
```java
String s = "ABC\n\u4e2d\u6587"; // 包含6个字符: A, B, C, 换行符, 中, 文
```

### 字符串连接
Java 的编译器对字符串做了特殊照顾。可以使用 + 连接任意字符串和其他数据类型。这样极大地方便了字符串的处理。

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "Hello";
        String s2 = "world";
        String s = s1 + " " + s2 + "!";
        System.out.println(s);
    }
}
```

如果用 + 字符串和其他的数据类型，会将其他数据类型先自动转型为字符串，再连接
```java
public class Main {
    public static void main(String[] args) {
        int age = 25;
        String s = "age is " + age;
        System.out.println(s);
    }
}
```

### 多行字符串
如果我们要表示多行字符串，使用 + 号连接会非常不方便
```java
String s = "first line \n"
         + "second line \n"
         + "end";
```

从java 13 开始，字符串可以使用"""..."""表示多行字符串(Text Blocks)了

例:
```java
public class Main {
    public static void main(String[] args) {
        String s = """
                   SELECT * FROM
                     users
                   WHERE id > 100
                   ORDER BY name DESC
                   """;
        System.out.println(s);
    }
}
```

上述多行字符串实际上是5行，在最后一个DESC后面还有一个\n。如果我们不想在字符串末尾加一个\n，就需要这么写：

```java
String s = """ 
           SELECT * FROM
             users
           WHERE id > 100
           ORDER BY name DESC""";
```     

还需要注意到，多行字符串前面共同的空格会被去掉，即：

```java
String s = """
...........SELECT * FROM
...........  users
...........WHERE id > 100
...........ORDER BY name DESC
...........""";
```

>用`.`标注的空格都会被去掉。

如果多行字符串的排版不规则，那么，去掉的空格就会变成这样：

```java
String s = """
.........  SELECT * FROM
.........    users
.........WHERE id > 100
.........  ORDER BY name DESC
.........  """;
```

即总是以最短的行首空格为基准。

最后，由于多行字符串是作为Java 13的预览特性（Preview Language Features）实现的，编译的时候，我们还需要给编译器加上参数：
```java
javac --source 13 --enable-preview Main.java
```

### 不可变特性
java的字符串除了是一个引用类型外，还有个重要的特点，就是字符串不可变。考察一下代码
```java
public class Main {
    public static void main(String[] args) {
        String s = "hello";
        System.out.println(s); // 显示 hello
        s = "world";
        System.out.println(s); // 显示 world
    }
}//最终显示为hello
```

观察执行结果，难道字符串s变了吗？其实变得不是字符串，而是变量s的指向。

### 空值null
引用类型的变量可以指向一个空值null，他表示不存在，即该变量不指向任何对象

例：
```java
String s1 = null; // s1是null
String s2; // 没有赋初值值，s2也是null
String s3 = s1; // s3也是null
String s4 = ""; // s4指向空字符串，不是null
```

注意区分空值null和空字符串""，空字符串是一个有效的字符串对象，它不等于null

## 数组类型
如果有一组类型相同的变量，例如，五位同学的成绩，可以这么写
```java
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int n1 = 68;
        int n2 = 79;
        int n3 = 91;
        int n4 = 85;
        int n5 = 62;
    }
}
```

但其实没必要定义5个 int 变量。可以用数组来表示"一组" int 类型。

```java
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int[] ns = new int[5];
        ns[0] = 68;
        ns[1] = 79;
        ns[2] = 91;
        ns[3] = 85;
        ns[4] = 62;
    }
}
```

定义一个数组类型的变量，使用数组类型 "类型 []" 例如，int []。和单个基本类型变量不同，数组变量初始化必须使用 new int [5]表示创建一个可以容纳5个 int 元素的数组

java数组有几个特点：
- 数组所有元素初始化为默认值，整型都是0，浮点型是0.0，布尔型是false
- 数组一但创建后，大小就不可改变

要访问数组中的某一个元素，需要使用索引。数组索引从0 开始，例如，5个元素的数组，索引范围是0~4

可以修改数组中的某一元素，使用赋值语句，例如，ns[1] = 79；

可以用 数组变量.length 获取数组大小

```java
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int[] ns = new int[5];
        System.out.println(ns.length); // 5
    }
}
```

数组是引用类型，在是用索引访问数组元素时，如果索引超出范围，运行将会报错
```java
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int[] ns = new int[5];
        int n = 5;
        System.out.println(ns[n]); // 索引n不能超出范围
    }
}
```

也可以在定义数组时直接指定初始化的元素，这样就不必写出数组的大小，而是由编译器自动推算数组大小。

例如
```java
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int[] ns = new int[] { 68, 79, 91, 85, 62 };
        System.out.println(ns.length); // 编译器自动推算数组大小为5
    }
}
```

还可以进一步的简写为
```java
int[] ns = { 68, 79, 91, 85, 62 };
```

注意数组是引用类型，并且数组大小不可变，

```java
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int[] ns;
        ns = new int[] { 68, 79, 91, 85, 62 };
        System.out.println(ns.length); // 5
        ns = new int[] { 1, 2, 3 };
        System.out.println(ns.length); // 3
    }
}
```
数组大小变了吗？看上去好像是变了，但其实根本没变。

对于数组ns来说，执行ns = new int[] { 68, 79, 91, 85, 62 };时，它指向一个5个元素的数组：
```
     ns
      │
      ▼
┌───┬───┬───┬───┬───┬───┬───┐
│   │68 │79 │91 │85 │62 │   │
└───┴───┴───┴───┴───┴───┴───┘
```
执行ns = new int[] { 1, 2, 3 };时，它指向一个新的3个元素的数组：
```
     ns ──────────────────────┐
                              │
                              ▼
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│   │68 │79 │91 │85 │62 │   │ 1 │ 2 │ 3 │   │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
```
但是，原有的5个元素的数组并没有改变，只是无法通过变量ns引用到它们而已。

### 字符串数组
如果数组元素不是基本类型，而是一个引用类型，那么，修改数组元素会有哪些不同？

字符串是引用类型，因此我们先定义一个字符串数组

```java
String[] names = {
    "ABC", "XYZ", "zoo"
};
```

对于 String[] 类型的数组变量 names ，他实际上包含3个元素，但每个元素都指向某个字符串对象
```
          ┌─────────────────────────┐
    names │   ┌─────────────────────┼───────────┐
      │   │   │                     │           │
      ▼   │   │                     ▼           ▼
┌───┬───┬─┴─┬─┴─┬───┬───────┬───┬───────┬───┬───────┬───┐
│   │░░░│░░░│░░░│   │ "ABC" │   │ "XYZ" │   │ "zoo" │   │
└───┴─┬─┴───┴───┴───┴───────┴───┴───────┴───┴───────┴───┘
      │                 ▲
      └─────────────────┘
```

对names[1]进行赋值，例如names[1] = "cat";，效果如下：
```
          ┌─────────────────────────────────────────────────┐
    names │   ┌─────────────────────────────────┐           │
      │   │   │                                 │           │
      ▼   │   │                                 ▼           ▼
┌───┬───┬─┴─┬─┴─┬───┬───────┬───┬───────┬───┬───────┬───┬───────┬───┐
│   │░░░│░░░│░░░│   │ "ABC" │   │ "XYZ" │   │ "zoo" │   │ "cat" │   │
└───┴─┬─┴───┴───┴───┴───────┴───┴───────┴───┴───────┴───┴───────┴───┘
      │                 ▲
      └─────────────────┘
```

这里注意到原来names[1]指向的字符串"XYZ"并没有改变，仅仅是将names[1]的引用从指向"XYZ"改成了指向"cat"，其结果是字符串"XYZ"再也无法通过names[1]访问到了。

# 流程控制

## 输入和输出

### 输出
在前面的代码中，我们总是使用 System.out.println() 来向屏幕输出一些内容。

println 是 print line 的缩写，表示输出并换行。因此，如果输出后不想换行，可以用 print():

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("A,");
        System.out.print("B,");
        System.out.print("C.");
        System.out.println();
        System.out.println("END");
    }
}
```

注意观察上述代码的执行效果

### 格式化输出
Java 还提供了格式化输出的功能。因为计算机表示的数据不一定适合人来阅读：

```java
public class Main {
    public static void main(String[] args) {
        double d = 12900000;
        System.out.println(d); // 1.29E7
    }
}
```

如果要把数据显示成我们期望的格式，就需要使用格式化输出的功能，格式化输出使用 System.out.printf() 通过使用占位符 %? ， printf() 可以把后面的参数格式换成指定的格式

```java
public class Main {
    public static void main(String[] args) {
        double d = 3.1415926;
        System.out.printf("%.2f\n", d); // 显示两位小数3.14
        System.out.printf("%.4f\n", d); // 显示4位小数3.1416
    }
}
```

Java 的格式化更能提供了多种占位符，可以把各种数据类型"格式化"成指定字符串

占位符	| 说明
-      | -
%d	   | 格式化输出整数
%x	   | 格式化输出十六进制整数
%f	   | 格式化输出浮点数
%e	   | 格式化输出科学计数法表示的浮点数
%s     | 格式化字符串

>由于%表示占位符，因此，连续两个%%表示一个%字符本身

占位符本身还可以有更详细的格式化参数，下面的例子把一个整数格式化成十六进制，并用0补足8位

```java
public class Main {
    public static void main(String[] args) {
        int n = 12345000;
        System.out.printf("n=%d, hex=%08x", n, n); // 注意，两个%占位符必须传入两个数
    }
}
```

格式化参数的jdk文档 [https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Formatter.html#syntax]()

### 输入
和输出相比，java的输入就要复杂得多

从控制台读取一个字符串和一个整数的例子：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // 创建Scanner对象
        System.out.print("Input your name: "); // 打印提示
        String name = scanner.nextLine(); // 读取一行输入并获取字符串
        System.out.print("Input your age: "); // 打印提示
        int age = scanner.nextInt(); // 读取一行输入并获取整数
        System.out.printf("Hi, %s, you are %d\n", name, age); // 格式化输出
    }
}
```
首先，我们通过 import 语句导入 java.util.Scanner ， import 是导入某个类的语句，必须放到 Java 源代码的开头。

然后，创建 Scanner 对象并传入 System.in 。 System.out 代表标准输出流，而 System.in 代表标准输入流。直接使用 System.in 读取用户输入虽然是可以的，但需要更复杂的代码，而通过 Scanner 就可以简化后续的代码。

有 Scanner 对象后，要读取用户输入的字符串，使用 scanner.nextline() ，要读取用户输入的整数，使用 Scanner.nextInt() 。Scanner 会自动转换数据类型，因此不必手动转换。

## if判断
在Java 程序中，如果要更具条件来决定是够执行某一段代码，就需要 if 语句。

if 语句的基本语法是：
```java
if (条件) {
    // 条件满足时执行
}
```

根据 if 的计算结果(true 还是 false)，JVM决定是否执行 if 语句块(即花括号{}包含的所有语句)

例：
```java
public class Main {
    public static void main(String[] args) {
        int n = 70;
        if (n >= 60) {
            System.out.println("及格了");
        }
        System.out.println("END");
    }
}
```

当天件 n>=60计算结果为 true 时，if 语句块被执行，将打印"及格了"，否则，if 语句块江北跳过。修改 n 的值可以看到执行结果

注意 if 语句包含的快可以包含多条语句

```java
public class Main {
    public static void main(String[] args) {
        int n = 70;
        if (n >= 60) {
            System.out.println("及格了");
            System.out.println("恭喜你");
        }
        System.out.println("END");
    }
}
```

当 if 语句块只有一行语句时，可以省略花括号{}

```java
public class Main {
    public static void main(String[] args) {
        int n = 70;
        if (n >= 60)
            System.out.println("及格了");
        System.out.println("END");
    }
}
```

但是，并不建议。因为假设某个时候，突然想给 if 语句块增加一条语句时

```java
public class Main {
    public static void main(String[] args) {
        int n = 50;
        if (n >= 60)
            System.out.println("及格了");
            System.out.println("恭喜你"); // 注意这条语句不是if语句块的一部分
        System.out.println("END");
    }
}
```

由于使用缩进格式，很容易吧两行语句都看成 if 语句的执行块，但实际上只有第一行语句是 if 的执行块。在使用git 这些版本控制系统自动合并时更容易出问题

else

if 语句还可以编写一个 else{ ··· } ，当条件判断为 false 时，将执行 else 语句块

```java
public class Main {
    public static void main(String[] args) {
        int n = 70;
        if (n >= 60) {
            System.out.println("及格了");
        } else {
            System.out.println("挂科了");
        }
        System.out.println("END");
    }
}
```

修改上述代码的 n 值，观察 if 条件为 true 或 false 时，程序执行的语句块

注意 ，else 不是必须的

还可以用多个 if···else if ··· 串联。

例：
```java
public class Main {
    public static void main(String[] args) {
        int n = 70;
        if (n >= 90) {
            System.out.println("优秀");
        } else if (n >= 60) {
            System.out.println("及格了");
        } else {
            System.out.println("挂科了");
        }
        System.out.println("END");
    }
}
```

串联的效果其实相当于

```java
if (n >= 90) {
    // n >= 90为true:
    System.out.println("优秀");
} else {
    // n >= 90为false:
    if (n >= 60) {
        // n >= 60为true:
        System.out.println("及格了");
    } else {
        // n >= 60为false:
        System.out.println("挂科了");
    }
}
```

串联使用多个 if 时，要特别注意判断顺序，观察以下代码

```java
public class Main {
    public static void main(String[] args) {
        int n = 100;
        if (n >= 60) {
            System.out.println("及格了");
        } else if (n >= 90) {
            System.out.println("优秀");
        } else {
            System.out.println("挂科了");
        }
    }
}
```

执行发现，n = 100时，满足条件n >= 90，但输出的不是"优秀"，而是"及格了"，原因是if语句从上到下执行时，先判断n >= 60成功后，后续else不再执行，因此，if (n >= 90)没有机会执行了。

正确的方式是按照判断范围从大到小依次判断：
```java
if (n >= 90) {
    // ...
} else if (n >= 60) {
    // ...
} else {
    // ...
}
```

或者改写成从小到大依次判断：
```java
if (n < 60) {
    // ...
} else if (n < 90) {
    // ...
} else {
    // ...
}
```

使用 if 时，还要特别注意边界条件。

例：
```java
public class Main {
    public static void main(String[] args) {
        int n = 90;
        if (n > 90) {
            System.out.println("优秀");
        } else if (n >= 60) {
            System.out.println("及格了");
        } else {
            System.out.println("挂科了");
        }
    }
}
```

假设我们期望90分或更高为“优秀”，上述代码输出的却是“及格”，原因是>和>=效果是不同的。

前面有写过浮点数在计算机中常常无法精确表示，并且计算可能出现误差，因此，判断浮点数相等用==判断不靠谱

```java
public class Main {
    public static void main(String[] args) {
        double x = 1 - 9.0 / 10;
        if (x == 0.1) {
            System.out.println("x is 0.1");
        } else {
            System.out.println("x is NOT 0.1");
        }
    }
}
```

正确方法是利用差值小于某个临界值来判断

```java
public class Main {
    public static void main(String[] args) {
        double x = 1 - 9.0 / 10;
        if (Math.abs(x - 0.1) < 0.00001) {
            System.out.println("x is 0.1");
        } else {
            System.out.println("x is NOT 0.1");
        }
    }
}
```

### 判断引用类型相等
在java 中，判断值类型的变量是否相等，可以使用==运算符，但是，判断引用类型的变量是否相等== 表示"引用是否相等"，或者说，是否指向同一个对象，例，下面两个String类型，他们的内容是相同的，但是，分别指向不同的对象，用== 判断，结果为false 

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "HELLO".toLowerCase();
        System.out.println(s1);
        System.out.println(s2);
        if (s1 == s2) {
            System.out.println("s1 == s2");
        } else {
            System.out.println("s1 != s2");
        }
    }
}
```

要判断引用类型的变量是否相等，必须使用equals()方法

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "HELLO".toLowerCase();
        System.out.println(s1);
        System.out.println(s2);
        if (s1.equals(s2)) {
            System.out.println("s1 equals s2");
        } else {
            System.out.println("s1 not equals s2");
        }
    }
}
```

注意，执行语句 s1.equals(s2) 时，如果变量 s1 为`null`，会报`NullPointerException`

```java
public class Main {
    public static void main(String[] args) {
        String s1 = null;
        if (s1.equals("hello")) {
            System.out.println("hello");
        }
    }
}
```

要避免`NullPointerException`错误，可以利用短路运算符 &&：

```java
public class Main {
    public static void main(String[] args) {
        String s1 = null;
        if (s1 != null && s1.equals("hello")) {
            System.out.println("hello");
        }
    }
}
```

还可以把一定不是 null 的对象 "hello" 放到前面：例如 if(”hello“.equals(s){...})

## Switch多重选择

除了 if 外还有一种条件判断，是更具某个表达式的结果，分别去执行不同的分支

例如，在游戏中让用户选择选项
1. 单人
2. 多人
3. 退出

这时，switch 语句就派上用场了。

switch 语句根据 swtich(表达式) 计算的结果，跳转到匹配的 case 结果，然后继续执行后续语句，知道遇到 break 结束执行

例
```java
public class Main {
    public static void main(String[] args) {
        int option = 1;
        switch (option) {
        case 1:
            System.out.println("Selected 1");
            break;
        case 2:
            System.out.println("Selected 2");
            break;
        case 3:
            System.out.println("Selected 3");
            break;
        }
    }
}
```

修改 option 的值分别为 1,2,3 观察执行结果

如果 option 的值没有匹配到任何 case ，例如 option = 99 那么，switch 语句不会执行任何语句。这时，可以给 switch 语句加一个 default ，当没有匹配到任何 case 时，执行default 

```java
public class Main {
    public static void main(String[] args) {
        int option = 99;
        switch (option) {
        case 1:
            System.out.println("Selected 1");
            break;
        case 2:
            System.out.println("Selected 2");
            break;
        case 3:
            System.out.println("Selected 3");
            break;
        default:
            System.out.println("Not selected");
            break;
        }
    }
}
```

如果把 switch 语句翻译成 if 语句，那么上述代码相当于

```java
if (option == 1) {
    System.out.println("Selected 1");
} else if (option == 2) {
    System.out.println("Selected 2");
} else if (option == 3) {
    System.out.println("Selected 3");
} else {
    System.out.println("Not selected");
}
```

对于多个 == 判断的情况，使用 switch 结构更加清晰

同时注意，上述"翻译"只有在 switch 语句中对每个 case 正确编写了 break 语句才能对应上

使用 switch 时，注意 case 语句斌没有花括号{}，而且 case 语句具有"穿透性"，漏写 break 将导致意想不到的结果

```java
public class Main {
    public static void main(String[] args) {
        int option = 2;
        switch (option) {
        case 1:
            System.out.println("Selected 1");
        case 2:
            System.out.println("Selected 2");
        case 3:
            System.out.println("Selected 3");
        default:
            System.out.println("Not selected");
        }
    }
}
```

当 option = 2 时，将依次输出 "Selected 2"、"Selected 3"、"Not selected" ，原因是从匹配到 case 2 开始，后续语句全部执行，直到遇到 break 语句，因此，任何时候都不要忘记 break 

如果有几个 case 语句执行的是同一组语句块，可以这么写：

```java
public class Main {
    public static void main(String[] args) {
        int option = 2;
        switch (option) {
        case 1:
            System.out.println("Selected 1");
            break;
        case 2:
        case 3:
            System.out.println("Selected 2, 3");
            break;
        default:
            System.out.println("Not selected");
            break;
        }
    }
}
```

使用 switch 语句时，只要保证有 break ，case 的顺序不影响程序逻辑

```java
switch (option) {
case 3:
    ...
    break;
case 2:
    ...
    break;
case 1:
    ...
    break;
}
```

但是任然建议按照自然顺序排列，便于阅读

switch 语句还可以匹配字符串，字符串匹配时，是比较"内容相等"。

例：
```java
public class Main {
    public static void main(String[] args) {
        String fruit = "apple";
        switch (fruit) {
        case "apple":
            System.out.println("Selected apple");
            break;
        case "pear":
            System.out.println("Selected pear");
            break;
        case "mango":
            System.out.println("Selected mango");
            break;
        default:
            System.out.println("No fruit selected");
            break;
        }
    }
}
```
对了，switch 语句还可以使用枚举类型。

### 编译检查
使用IDE时，可以自动检查是否漏写了break语句和default语句，方法是打开IDE的编译检查。

在`Eclipse`中，选择`Preferences - Java - Compiler - Errors/Warnings - Potential programming problems`，将以下检查标记为`Warning`：

```
'switch' is missing 'default' case
'switch' case fall-through
```
在`Idea`中，选择P`references - Editor - Inspections - Java - Control flow issues`，将以下检查标记为`Warning`：

```
Fallthrough in 'switch' statement
'switch' statement without 'default' branch
```
当switch语句存在问题时，即可在IDE中获得警告提示。

### switch表达式
使用switch时，如果遗漏了break，就会造成严重的逻辑错误，而且不易在源代码中发现错误。从Java 12开始，switch语句升级为更简洁的表达式语法，使用类似模式匹配（Pattern Matching）的方法，保证只有一种路径会被执行，并且不需要break语句：

```java
public class Main {
    public static void main(String[] args) {
        String fruit = "apple";
        switch (fruit) {
        case "apple" -> System.out.println("Selected apple");
        case "pear" -> System.out.println("Selected pear");
        case "mango" -> {
            System.out.println("Selected mango");
            System.out.println("Good choice!");
        }
        default -> System.out.println("No fruit selected");
        }
    }
}
```
注意新语法使用->，如果有多条语句，需要用{}括起来。不要写break语句，因为新语法只会执行匹配的语句，没有穿透效应。

很多时候，我们还可能用switch语句给某个变量赋值。例如：

```java
int opt;
switch (fruit) {
case "apple":
    opt = 1;
    break;
case "pear":
case "mango":
    opt = 2;
    break;
default:
    opt = 0;
    break;
}
```

使用新的switch语法，不但不需要break，还可以直接返回值。把上面的代码改写如下：

```java
public class Main {
    public static void main(String[] args) {
        String fruit = "apple";
        int opt = switch (fruit) {
            case "apple" -> 1;
            case "pear", "mango" -> 2;
            default -> 0;
        }; // 注意赋值语句要以;结束
        System.out.println("opt = " + opt);
    }
}
```

这样可以获得更简洁的代码。

### yield
大多数时候，在switch表达式内部，我们会返回简单的值。

但是，如果需要复杂的语句，我们也可以写很多语句，放到{...}里，然后，用yield返回一个值作为switch语句的返回值：
```java
public class Main {
    public static void main(String[] args) {
        String fruit = "orange";
        int opt = switch (fruit) {
            case "apple" -> 1;
            case "pear", "mango" -> 2;
            default -> {
                int code = fruit.hashCode();
                yield code; // switch语句返回值
            }
        };
        System.out.println("opt = " + opt);
    }
}
```

由于switch表达式是作为Java 13的预览特性（Preview Language Features）实现的，编译的时候，我们还需要给编译器加上参数：

```
javac --source 13 --enable-preview Main.java
```

这样才能正常编译。

## while循环
循环语句就是让计算机根据条件做循环计算，在条件满足时继续循环，条件不满足时退出循环

例如，计算1到100的和：
```
1 + 2 + 3 + 4 + … + 100 = ?
```

除了使用数列公式外，完全可以让计算机做100次循环累加。因为计算机的特点是计算速度非常快，我们让计算机循环一亿次也用不到1秒，所以很多计算的任务，人去算是算不了的，但是计算机算，使用循环这种简单粗暴的放大就可以快速得到结果

java提供的 wile 条件循环，基本用法是：
```java
while (条件表达式) {
    循环语句
}
// 继续执行后续代码
```
while 循环在每次循环开始前，首先判断条件是否成立，如果计算结果为 true ，就把煦暖体内的语句执行一遍，如果计算结果为 false ，那就直接跳到 while 循环的末尾，继续往下执行

用 while 循环来累加 1 - 100 可以这么写

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0; // 累加的和，初始化为0
        int n = 1;
        while (n <= 100) { // 循环条件是n <= 100
            sum = sum + n; // 把n累加到sum中
            n ++; // n自身加1
        }
        System.out.println(sum); // 5050
    }
}
```

注意到 while 循环事先判断循环条件，再循环，因此，有可能一次循环都不做。

对于循环条件判断，以及自增变量的处理，要特别注意边界条件

例：
```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        int n = 0;
        while (n <= 100) {
            n ++;//先自加了在执行赋值
            sum = sum + n;
        }
        System.out.println(sum);
    }
}
```

如果循环条件永远满足，那么这个循环就变成了死循环，死循环将导致100%的CPU占用，用户会感觉电脑运行缓慢，所以要避免编写死循环代码

如果循环条件的逻辑写的有问题，也会造成意料之外的结果
```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        int n = 1;
        while (n > 0) {
            sum = sum + n;
            n ++;
        }
        System.out.println(n); // -2147483648
        System.out.println(sum);
    }
}
```

表面上看，上面的while循环是一个死循环，但是，Java的int类型有最大值，达到最大值后，再加1会变成负数，结果，意外退出了while循环。

## do while循环
在java中，while 循环是先判断循环条件，在执行循环。而另一种do while 循环则是先执行循环再判断条件，条件满足时继续循环，条件不满足时退出

用法：
```java
do {
    执行循环语句
} while (条件表达式);
```

可见，do while循环会至少循环一次。

把对1到100 的求和用 do while 循环改写一下

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        int n = 1;
        do {
            sum = sum + n;
            n ++;
        } while (n <= 100);
        System.out.println(sum);
    }
}
```

使用do while 循环时，同样也要注意循环条件的判断

## for循环
除了 while 和 do while 循环，java 使用最广泛的是 for 循环

for 循环的功能非常强大，它使用计数器实现循环。for 循环会先初始化计数器，然后，在每次循环前检测循环条件，在每次循环后更新计数器，计数器变量名通常为 i

把1到100用 for 循环改写一下

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        for (int i=1; i<=100; i++) {
            sum = sum + i;
        }
        System.out.println(sum);
    }
}
```

在 for 循环执行前，会先执行初始化语句 int i=1，它定义了计数器变量 i 并赋初始值为 1，然后，循环前先检查循环条件 i<=100 ，循环后自动执行 i++，因此，和 while 循环相比，for 循环 把更新计数器的代码统一放到了一起。在 for 循环的循环体内部，不需要去更新变量 i

因此，for 循环的用法是
```java
for (初始条件; 循环检测条件; 循环后更新计数器) {
    // 执行语句
}
```

如果我们要对一个整型数组的所有元素求和，可以用 for 循环实现：
```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        int sum = 0;
        for (int i=0; i<ns.length; i++) {
            System.out.println("i = " + i + ", ns[i] = " + ns[i]);
            sum = sum + ns[i];
        }
        System.out.println("sum = " + sum);
    }
}
```

上面代码的循环条件是 `i<ns.length` 因为 ns 数组长度是5 ，因此，当循环 5次后，i 的值被更新为 5，就不满足循环条件，因此for 循环结束。

>如果把循环条件改为i<=ns.length，会出现什么问题？

注意 for 循环的初始化计数器总是会被执行，并且 for 循环也可能循环 0 次

使用 for 循环时，千万不要在循环体内修改计数器！在循环体中修改计数器常常导致莫名其妙的逻辑错误，对于下面的代码

```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int i=0; i<ns.length; i++) {
            System.out.println(ns[i]);
            i = i + 1;
        }
    }
}

```

虽然不会报错，但是，数组元素只打印了一般，原因是循环内部的 i = i + 1 导致了计数器变量每次循环实际上加了 2(因为 for 循环还会自动执行i++)。因此，在 for 循环中，不要修改计数器的值。计数器的初始化，判断条件，每次循环后的更新条件统一放到 for()语句中可以一目了然。

如果希望只访问索引为奇数的数组元素，应该把 for 循环改写为

```java
int[] ns = { 1, 4, 9, 16, 25 };
for (int i=0; i<ns.length; i=i+2) {
    System.out.println(ns[i]);
}
```

通过更新计数器的i = i + 2 就达到了这个效果，从而避免了在循环体内去修改变量 i

使用 for 循环时，计数器变量 i 要尽量定义在 for 循环中

```java
int[] ns = { 1, 4, 9, 16, 25 };
for (int i=0; i<ns.length; i++) {
    System.out.println(ns[i]);
}
// 无法访问i
int n = i; // compile error!
```

如果变量 i 定义在 for 循环外

```java
int[] ns = { 1, 4, 9, 16, 25 };
int i;
for (i=0; i<ns.length; i++) {
    System.out.println(ns[i]);
}
// 仍然可以使用i
int n = i;
```

那么，退出 for 循环后，变量 i 仍然课易被访问，这就破坏了变量应该吧访问范围缩到最小的原则

### 灵活使用for循环
for 循环还可以缺少初始化语句，循环条件和每次循环更新语句

例：
```java
// 不设置结束条件:
for (int i=0; ; i++) {
    ...
}
```
```java
// 不设置结束条件和更新语句:
for (int i=0; ;) {
    ...
}
```
```java
// 什么都不设置:
for (;;) {
    ...
}
```

通常不推荐这么写，但是，某些情况下，是可以省略 for 循环的某些语句的

### for each 循环
for 循环进场用了遍历数组，因为通过计数器可以根据索引来访问数组的每个元素：

```java
int[] ns = { 1, 4, 9, 16, 25 };
for (int i=0; i<ns.length; i++) {
    System.out.println(ns[i]);
}
```

但是，很多时候，我们实际上真正想要访问的是数组每个单元的值，java还提供了另一种 for each循环，它可以更简单的遍历数组

```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int n : ns) {
            System.out.println(n);
        }
    }
}
```

和 for 循环相比，for each 循环的变量 n 不再是计数器，而是直接对应到数组的每个元素。for each 循环的写法也更简洁，但是，for each 循环能够遍历所有“可迭代”的数据类型包括 List,map 等

## Break 和 Continue
无论是 while 循环还是 for 煦暖，有两个特别的语句可以使用，就是 break 语句和 continue 语句

### break
再循环过程中，可以使用 break 语句跳出当前循环。

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        for (int i=1; ; i++) {
            sum = sum + i;
            if (i == 100) {
                break;
            }
        }
        System.out.println(sum);
    }
}
```

使用 for 循环计算从 1 到 100 时，我们并没有在 for() 循环中设置循环退出的检测条件，但是，在循环内部，我们用 if 判断，如果 i == 100 ，就通过 break 退出循环

因此，break 语句通常都是配合 if 语句使用。要特别注意，break 语句总是跳出自己所在的那一层循环。

```java
public class Main {
    public static void main(String[] args) {
        for (int i=1; i<=10; i++) {
            System.out.println("i = " + i);
            for (int j=1; j<=10; j++) {
                System.out.println("j = " + j);
                if (j >= i) {
                    break;
                }
            }
            // break跳到这里
            System.out.println("breaked");
        }
    }
}
```

上面的代码是两个 for 循环嵌套。因为 break 语句唯一内层的 for 循环，因此，他会跳出内层 for 循环，但不会跳出外层 for 循环

### continue
break 会跳出当前循环，也就是整个循环都不会执行了，而 continue 则是提前结束本次循环，直接继续执行下次循环

例：
```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        for (int i=1; i<=10; i++) {
            System.out.println("begin i = " + i);
            if (i % 2 == 0) {
                continue; // continue语句会结束本次循环
            }
            sum = sum + i;
            System.out.println("end i = " + i);
        }
        System.out.println(sum); // 25
    }
}
```

当 i 为奇数时，完整的执行了整个循环，因此，会打印 begin i = 1和 end i = 1，在i为偶数时，continue语句会提前结束本次循环，因此，会打印begin i=2但不会打印end i = 2。

在多层嵌套的循环中，continue 语句同样是结束本次自己所在的循环

# 数组操作

## 遍历数组
java 程序基础中介绍过数组这种数据类型，有了数组，我们还需要来操作它。而数组最常见的一个操作就是遍历

通过 for 循环就可以遍历数组。因为数组的每个元素都可以通过索引来访问，因此，使用标准的 for 循环可以完成一个数组的遍历

```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int i=0; i<ns.length; i++) {
            int n = ns[i];
            System.out.println(n);
        }
    }
}
```

为了实现 for 循环遍历，初始条件为 i = 0，因为索引总是从 0 开始，继续循环的条件为`i<ns.length`,因为`i=ns.length`时，1 已经超出了索引范围（索引范围是0 ~ ns.length-1），每次循环后，i++

第二种方式使用for each 循环，直接迭代数组的每个元素

```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int n : ns) {
            System.out.println(n);
        }
    }
}
```

>在 for (int n : ns)循环中，变量 n 直接拿到 ns 数组的元素，而不是索引

显然 for each 循环更加简洁，但是，for each 循环无法拿到数组的索引，因此，到底用哪一种 for 循环，取决于我们的需要

### 打印数组的内容
直接打印数组变量，得到的是数组在JVM 中的引用地址：
```java
int[] ns = { 1, 1, 2, 3, 5, 8 };
System.out.println(ns); // 类似 [I@7852e922
```

这并没有什么意义，因为我们希望打印的数组的元素内容。因此，使用for each 循环来打印它
```java
int[] ns = { 1, 1, 2, 3, 5, 8 };
for (int n : ns) {
    System.out.print(n + ", ");
}
```
使用 for each 循环打印也很麻烦，幸好java 标准库提供了 Arrays.toString()，可以快速打印数组内容：

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 1, 2, 3, 5, 8 };
        System.out.println(Arrays.toString(ns));
    }
}
```

## 数组排序
对数组进行排序是程序中非常基本的需求，常用的排序算法有冒泡排序。插入排序和快速排序

冒泡排序吧一个整数从小到大进行排序
```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
        // 排序前:
        System.out.println(Arrays.toString(ns));
        for (int i = 0; i < ns.length - 1; i++) {
            for (int j = 0; j < ns.length - i - 1; j++) {
                if (ns[j] > ns[j+1]) {
                    // 交换ns[j]和ns[j+1]:
                    int tmp = ns[j];
                    ns[j] = ns[j+1];
                    ns[j+1] = tmp;
                }
            }
        }
        // 排序后:
        System.out.println(Arrays.toString(ns));
    }
}
```

冒泡排序的特点是，每一轮循环后，最大的一个数被交换到末尾，因此，下一轮循环就可以"刨除"最后的数，每一轮循环都比上一轮循环的结束位置靠前一位

另外，注意到交换两个变量的值必须借助一个临时变量，像这么写是错误的
```java
int x = 1;
int y = 2;

x = y; // x现在是2
y = x; // y现在还是2
```

正确的写法是
```java
int x = 1;
int y = 2;

int t = x; // 把x的值保存在临时变量t中, t现在是1
x = y; // x现在是2
y = t; // y现在是t的值1
```
实际上，java 的标准库已经内置了排序功能，我们只需要用JDK提供的Arrays.sort()就可以排序

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
        Arrays.sort(ns);
        System.out.println(Arrays.toString(ns));
    }
}
```

必须注意，对数组的排序实际上修改了数组本身，例如，排序前的数组是：
```
int[] ns = { 9, 3, 6, 5 };

```

在内存中，这个整型数组表示如下：

```
      ┌───┬───┬───┬───┐
ns───>│ 9 │ 3 │ 6 │ 5 │
      └───┴───┴───┴───┘
```

当我们调用Arrays.sort(ns);后，这个整型数组在内存中变为：

```
      ┌───┬───┬───┬───┐
ns───>│ 3 │ 5 │ 6 │ 9 │
      └───┴───┴───┴───┘
```

即变量ns指向的数组内容已经被改变了。

如果对一个字符串数组进行排序

例：
```java
String[] ns = { "banana", "apple", "pear" };
```
排序前，这个数组在内存中表示如下：

```
                   ┌──────────────────────────────────┐
               ┌───┼──────────────────────┐           │
               │   │                      ▼           ▼
         ┌───┬─┴─┬─┴─┬───┬────────┬───┬───────┬───┬──────┬───┐
ns ─────>│░░░│░░░│░░░│   │"banana"│   │"apple"│   │"pear"│   │
         └─┬─┴───┴───┴───┴────────┴───┴───────┴───┴──────┴───┘
           │                 ▲
           └─────────────────┘

```

调用Arrays.sort(ns);排序后，这个数组在内存中表示如下：

```
                   ┌──────────────────────────────────┐
               ┌───┼──────────┐                       │
               │   │          ▼                       ▼
         ┌───┬─┴─┬─┴─┬───┬────────┬───┬───────┬───┬──────┬───┐
ns ─────>│░░░│░░░│░░░│   │"banana"│   │"apple"│   │"pear"│   │
         └─┬─┴───┴───┴───┴────────┴───┴───────┴───┴──────┴───┘
           │                              ▲
           └──────────────────────────────┘

```

原来的3个字符串在内存中均没有任何变化，但是ns数组的每个元素指向变化了。

## 多维数组
### 二维数组
二维数组就是数组的数组，定义一个二维数组如下

```java
public class Main {
    public static void main(String[] args) {
        int[][] ns = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 }
        };
        System.out.println(ns.length); // 3
    }
}
```

因为 ns 包含3个数组，因此 ns.length 为 3。实际上 ns 在内存中的结构如下：
```
                    ┌───┬───┬───┬───┐
         ┌───┐  ┌──>│ 1 │ 2 │ 3 │ 4 │
ns ─────>│░░░│──┘   └───┴───┴───┴───┘
         ├───┤      ┌───┬───┬───┬───┐
         │░░░│─────>│ 5 │ 6 │ 7 │ 8 │
         ├───┤      └───┴───┴───┴───┘
         │░░░│──┐   ┌───┬───┬───┬───┐
         └───┘  └──>│ 9 │10 │11 │12 │
                    └───┴───┴───┴───┘
```

如果我们定一个普通数组 arr0 ，然后把 ns[0] 赋值给它

```java
public class Main {
    public static void main(String[] args) {
        int[][] ns = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 }
        };
        int[] arr0 = ns[0];
        System.out.println(arr0.length); // 4
    }
}
```

实际上 arr0 就获取了 ns 数组的第 0个元素，因为 ns 数组的每个元素也是一个数组，因此，arr0 指向的数组就是 {1,2,3,4}，在内存中，结构如下：
```
            arr0 ─────┐
                      ▼
                    ┌───┬───┬───┬───┐
         ┌───┐  ┌──>│ 1 │ 2 │ 3 │ 4 │
ns ─────>│░░░│──┘   └───┴───┴───┴───┘
         ├───┤      ┌───┬───┬───┬───┐
         │░░░│─────>│ 5 │ 6 │ 7 │ 8 │
         ├───┤      └───┴───┴───┴───┘
         │░░░│──┐   ┌───┬───┬───┬───┐
         └───┘  └──>│ 9 │10 │11 │12 │
                    └───┴───┴───┴───┘
```

访问二维数组的某个元素需要使用 array[row][col]

例：
```java
System.out.println(ns[1][2]); // 7
```

二位数组的每个数组元素的长度并不要求相同，例如，可以这么定义 ns 数组

```java
int[][] ns = {
    { 1, 2, 3, 4 },
    { 5, 6 },
    { 7, 8, 9 }
};
```
这个二维数组在内存中的结构如下

```
                    ┌───┬───┬───┬───┐
         ┌───┐  ┌──>│ 1 │ 2 │ 3 │ 4 │
ns ─────>│░░░│──┘   └───┴───┴───┴───┘
         ├───┤      ┌───┬───┐
         │░░░│─────>│ 5 │ 6 │
         ├───┤      └───┴───┘
         │░░░│──┐   ┌───┬───┬───┐
         └───┘  └──>│ 7 │ 8 │ 9 │
                    └───┴───┴───┘
```

要打印一个二维数组，可以使用两层嵌套的for 循环

```java
for (int[] arr : ns) {
    for (int n : arr) {
        System.out.print(n);
        System.out.print(', ');
    }
    System.out.println();
}
```

或者使用java 标准库的Arrays.deepToString();

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[][] ns = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 }
        };
        System.out.println(Arrays.deepToString(ns));
    }
}
```

### 三维数组
三维数组就是二维数组的数组，可以这么定一个三维数组

```java
int[][][] ns = {
    {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    },
    {
        {10, 11},
        {12, 13}
    },
    {
        {14, 15, 16},
        {17, 18}
    }
};
```

它在内存中的结构如下：

```
                              ┌───┬───┬───┐
                   ┌───┐  ┌──>│ 1 │ 2 │ 3 │
               ┌──>│░░░│──┘   └───┴───┴───┘
               │   ├───┤      ┌───┬───┬───┐
               │   │░░░│─────>│ 4 │ 5 │ 6 │
               │   ├───┤      └───┴───┴───┘
               │   │░░░│──┐   ┌───┬───┬───┐
        ┌───┐  │   └───┘  └──>│ 7 │ 8 │ 9 │
ns ────>│░░░│──┘              └───┴───┴───┘
        ├───┤      ┌───┐      ┌───┬───┐
        │░░░│─────>│░░░│─────>│10 │11 │
        ├───┤      ├───┤      └───┴───┘
        │░░░│──┐   │░░░│──┐   ┌───┬───┐
        └───┘  │   └───┘  └──>│12 │13 │
               │              └───┴───┘
               │   ┌───┐      ┌───┬───┬───┐
               └──>│░░░│─────>│14 │15 │16 │
                   ├───┤      └───┴───┴───┘
                   │░░░│──┐   ┌───┬───┐
                   └───┘  └──>│17 │18 │
                              └───┴───┘
```
如果我们要访问三维数组的某个元素，例如，ns[2][0][1],只需要伸着定位找到对应的最终元素 15 即可。

理论上，我们可以定义任意的N维数组。但在实际应用中，除了二维数组在某些时候还能用得上，更高维度的数组很少使用


## 命令行参数
java 程序的入口是main 方法。而main 方法可以接受一个命令行参数，他是一个 String[]数组

这个命令行参数由 JVM 接收用户输入并传给main 方法

```java
public class Main {
    public static void main(String[] args) {
        for (String arg : args) {
            System.out.println(arg);
        }
    }
}
```

我们可以利用接收到的命令行参数，根据不同的参数执行不同的代码，例如，实现一个 -version 参数，打印程序版本号

```java
public class Main {
    public static void main(String[] args) {
        for (String arg : args) {
            if ("-version".equals(arg)) {
                System.out.println("v 1.0");
                break;
            }
        }
    }
}
```

上面的这个程序必须在命令行执行，先编译

```
$ javac Main.java
```

然后，执行的时候，给它穿第一个 -version 参数

```
$ java Main -version
v 1.0
```

这样，程序就可以根据传入的命令行参数，做出不同的响应。

# 面向对象编程
Java 是一种面向对象的编程语言。面向对象编程，英文是Object-Oriented Programming，简称OOP

那什么面向对象的编程

和面向对象编程不同的，是面向过程编程。面向过程编程，死吧模型分解成一步一步的过程。比如，老板告诉你，你要编写一个TODO惹怒我，必须按照以下步骤一步一步来：

1. 读取文件；
2. 编写TODO；
3. 保存文件；

而面对对象编程，顾名思义，首先得有个对象

有了对象后，就可以和对象进行互动

```java
GirlFriend gf = new GirlFriend();
gf.name = "Alice";
gf.send("flowers");
```

面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一种编程方法。

# 面对对象基础
面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一种编程方法。

现实世界中，我们定义了“人”这种抽象概念，而具体的人则是“小明”、“小红”、“小军”等一个个具体的人。所以，“人”可以定义为一个“类”(class)，而具体的人则是实例(instance)

现实世界	|    计算机模型	  |   Java代码
   -       |        -      |         -          
人	       |   类 / class	|    class Person { }
小明	    |   实例 / ming	 |    Person ming = new Person()
小红	    |   实例 / hong	 |    Person hong = new Person()
小军	    |   实例 / jun	 |    Person jun = new Person()

同样的，“书”也是一种抽象的概念，所以它是类，而《Java核心技术》、《Java编程思想》、《Java学习笔记》则是实例：


现实世界	 |  计算机模型	   |  Java代码
 -          |      -        |     -                
书	        |  类 / class	 | class Book { }
Java核心技术 |	实例 / book1  |	Book book1 = new Book()
Java编程思想 |	实例 / book2  |	Book book2 = new Book()
Java学习笔记 |	实例 / book3  |	Book book3 = new Book()

**class 和 instance**
只要理解了class 和 instance 的概念，基本上就明白了什么是面向对象编程。

class 是一种对象模板，它定义了如何创建实例，因此，class本身就是一张数据类型

而 instance 是对象实例，instance 是根据 class 创建的实例，可以创建多个 instance ，每个 instance 类型相同，但各自属性可能并不相同

**定义 class**

在java 中，创建一个类，例如，给这个类命名为 person 就是定义一个class

```java
class Person {
    public String name;
    public int age;
}
```

一个 calss 可以包含多个字段 (field) ，字段用来描述一个类的特征，上面的 Person 类，我们定义了两个字段，一个是 String 类型的字段，命名为 name 一个是 int 类型的字段，命名为 age。因此，通过 class 把一数组数据汇集到一个对象上，实现了数据封装。

public 是用来修饰字段的，它表示这个字段可以被外部访问

在看另一个 Book 类的定义

```java
class Book {
    public String name;
    public String author;
    public String isbn;
    public double price;
}
```

字段 name
字段 author
字段 isbn
字段 price

**创建实例**
定义了 class ，只是定义了对象模板，而要根据对象模板创建出真正的对象实例，必须用 new 操作符

new 操作符可以创建一个实例，然后，我们需要定义一个引用类型的变量来指向这个实例

```java
Person ming = new Person();
```

上述代码创建了一个 Person ming 是定义 Person 类型的变量 ming ，而 new Person() 是创建 person 实例

有了指向这个实例的变量，我们就可以通过这个变量来操作实例，访问实例变量可以用 变量.字段 例如:
```java
ming.name = "Xiao Ming"; // 对字段name赋值
ming.age = 12; // 对字段age赋值
System.out.println(ming.name); // 访问字段name

Person hong = new Person();
hong.name = "Xiao Hong";
hong.age = 15;
```

上述两个变量分别指向两个不同的实例，他们在内存中的结构如下：

```
            ┌──────────────────┐
ming ──────>│Person instance   │
            ├──────────────────┤
            │name = "Xiao Ming"│
            │age = 12          │
            └──────────────────┘
            ┌──────────────────┐
hong ──────>│Person instance   │
            ├──────────────────┤
            │name = "Xiao Hong"│
            │age = 15          │
            └──────────────────┘
```

两个 instance 拥有 class 定义的 name 和 age 字段，且各自都有一份独立的数据，互不干扰。

## 方法
一个 class 可以包含多个 field ，例如，Person 类就定义了两个 field

```java
class Person {
    public String name;
    public int age;
}
```

但是，直接把 field 用 public 暴露给外部可能会破坏封装性。比如，代码可以这样写

>封装就是把普通的对象进行封装，对象的属性设为私有的，对外提供get和set方法，其他类只能通过get和set对对象属性值进行操作。

>继承是发生在两个类之间，一个类继承另一个类是说这个类属于另一个类，具有另一个类的所有属性和方法，同时它还可以有另一个类不具备的方法和属性。

>多态是建立在继承的基础上的，一个父类对象可以产生多个不同的子类对象，根据这些子类对象的不同可以具备不同的方法，也就是说表现出了不同的形态即多态

```java
Person ming = new Person();
ming.name = "Xiao Ming";
ming.age = -99; // age设置为负数 
```

显然，直接操作 field，容易造成逻辑混乱。为了避免外部代码直接去访问 field ，我们可以用 private 修饰 field ，拒绝外部访问。

```java
class Person {
    private String name;
    private int age;
}
```

把 field 从 public 改成 private ，外部代码不能访问这些 field ，那我们定义这些 field 有什么用？ 怎么才能给它赋值？怎么才能读取它的的值？

需要用到方法(method)来让外部代码可以简介修改field

```java
public class Main {
    public static void main(String[] args) {
        Person ming = new Person();
        ming.setName("Xiao Ming"); // 设置name
        ming.setAge(12); // 设置age
        System.out.println(ming.getName() + ", " + ming.getAge());
    }
}

class Person {
    private String name;
    private int age;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return this.age;
    }

    public void setAge(int age) {
        if (age < 0 || age > 100) {
            throw new IllegalArgumentException("invalid age value");
        }
        this.age = age;
    }
}
```

虽然外部代码不能直接修改 private 字段，但是，外部代码可以调用方法 setName() 和 setAge() 来间接修改 private 字段。在方法内部，我们就有机会检查参数对不对。比如，setAge() 就会检查传入的参数，参数超出了范围，直接报错。这样，外部代码就没有任何机会把 age 设置成不合理的值。

对 setName() 方法同样可以做检查，例如，不允许传入 null 和 空字符串 ：

```java
public void setName(String name) {
    if (name == null || name.isBlank()) {
        throw new IllegalArgumentException("invalid name");
    }
    this.name = name.strip(); // 去掉首尾空格
}
```

同样外部代码不能直接读取 private 字段，但可以通过 getName() 和 getAge() 间接获取 priavate 字段的值。

所以，一个类通过定义方法，就可以给外部代码暴露一些操作的接口，同时，内部自己保证逻辑一致性。

调用方法的语句时 实例变量.方法名(参数)； 一个方法调用即使一个语句，所以不要忘了在末尾加 ; 。例如： ming.setName("ming");。

### 定义方法
从上面的代码可以看出，定义方法的语句是：

```
修饰符 方法返回类型 方法名(方法参数列表) {
    若干方法语句;
    return 方法返回值;
}
```

方法返回值通过 return 语句实现，如果没有返回值，返回类型设置为 void 可以省略 return。

### private 方法
有 public 方法，自然就有 private 方法。和 private 字段一样，private 方法不允许外部调用，那我们定义 private 方法有什么用呢

定义 private 方法的理由是内部方法是可以调用 private 方法的

例：
```java
public class Main {
    public static void main(String[] args) {
        Person ming = new Person();
        ming.setBirth(2008);
        System.out.println(ming.getAge());
    }
}

class Person {
    private String name;
    private int birth;

    public void setBirth(int birth) {
        this.birth = birth;
    }

    public int getAge() {
        return calcAge(2019); // 调用private方法
    }

    // private方法:
    private int calcAge(int currentYear) {
        return currentYear - this.birth;
    }
}
```

观察上述代码，calcAge() 是一个 private 方法，外部代码无法调用，但是内部方法 getAge() 可以调用它。

此外，我们还注意到，这个 Person 类只定义了 birth 字段，没有定义 age 字段，获取 age 时，通过方法 getAge() 返回值是一个实时计算的值，并非存储在某个字段的值。这说明方法可以封装一个类的对外接口，调用方不需要知道也不关心 Person 实例在内部到底有没有 age 字段。

### this 变量
在方法内部，可以使用一个隐含的变量 this ，他始终指向当前实例。因此，通过 this.field 就可以访问当前实例字段。

如果没有命名冲突，可以省略 this 例如：

```java
class Person {
    private String name;

    public String getName() {
        return name; // 相当于this.name
    }
}
```

但是，如果有局部变量和字段重名，那么局部变量优先级更高，就必须加上 this：

```java
class Person {
    private String name;

    public void setName(String name) {
        this.name = name; // 前面的this不可少，少了就变成局部变量name了
    }
}
```

### 方法参数
方法可以包含0个或任意个参数。方法参数用于接收传递给方法的变量值。调用方法时，必须严格按照参数的定义一一传递。

例如：
```java
class Person {
    ...
    public void setNameAndAge(String name, int age) {
        ...
    }
}
```

调用这个 setNameAndAge() 方法时，必须有两个参数，且第一个参数必须为 String ，第二个参数必须为 int ：

```java
Person ming = new Person();
ming.setNameAndAge("Xiao Ming"); // 编译错误：参数个数不对
ming.setNameAndAge(12, "Xiao Ming"); // 编译错误：参数类型不对
```

### 可变参数
可变参数用 类型... 定义，可变参数相当于数组类型

```java
class Group {
    private String[] names;

    public void setNames(String... names) {
        this.names = names;
    }
}
```

上面的 setNames() 就定义了一个可变参数，调用时可以这么写

```java
Group g = new Group();
g.setNames("Xiao Ming", "Xiao Hong", "Xiao Jun"); // 传入3个String
g.setNames("Xiao Ming", "Xiao Hong"); // 传入2个String
g.setNames("Xiao Ming"); // 传入1个String
g.setNames(); // 传入0个String
```

完全可以吧可变参数改写为 String[] 类型

```java
class Group {
    private String[] names;

    public void setNames(String[] names) {
        this.names = names;
    }
}
```

但是，调用方需要自己先构造 String[] ，比较麻烦，例如

```java
Group g = new Group();
g.setNames(new String[] {"Xiao Ming", "Xiao Hong", "Xiao Jun"}); // 传入1个String[]
```

另一个问题是，调用方法可以传入 null ：

```java
Group g = new Group();
g.setNames(null);
```

而可变参数可以保证无法传入 null，因为传入 0 个参数时，接受到的实际值是个空数组而不是 null。

### 参数绑定
调用方法把参数传递给实例方法时，调用时传递的值会按参数未知一一绑定。

什么是参数绑定

基本类型的参数传递例子：
```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        int n = 15; // n的值为15
        p.setAge(n); // 传入n的值
        System.out.println(p.getAge()); // 15
        n = 20; // n的值改为20
        System.out.println(p.getAge()); // 15还是20?
    }
}

class Person {
    private int age;

    public int getAge() {
        return this.age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

运行代码，从结果可知，修改外部的局部变量 n ，不影响实例 p 的 age 字段，原因是 setAge() 方法获得的参数，复制了 n 的值，因此，p.age 和局部变量 n 互不影响

接了：基本类型参数的传递，是调用方值的复制。双方各自的后续修改，互不影响

传递引用参数的例子：
```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        String[] fullname = new String[] { "Homer", "Simpson" };
        p.setName(fullname); // 传入fullname数组
        System.out.println(p.getName()); // "Homer Simpson"
        fullname[0] = "Bart"; // fullname数组的第一个元素修改为"Bart"
        System.out.println(p.getName()); // "Homer Simpson"还是"Bart Simpson"?
    }
}

class Person {
    private String[] name;

    public String getName() {
        return this.name[0] + " " + this.name[1];
    }

    public void setName(String[] name) {
        this.name = name;
    }
}
```

注意到 setNmae() 的参数现在是一个数组。一开始，吧 fullname 数组穿进去，然后，修改 fullname 数组的内容，结果发现，实例 p 的字段 p.name 也被修改了

结论：引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的同一个对象。双方任意一方对这个对象的修改，都会影响对方(因为指向同一个对象)。

再来一个例子：
```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        String bob = "Bob";
        p.setName(bob); // 传入bob变量
        System.out.println(p.getName()); // "Bob"
        bob = "Alice"; // bob改名为Alice
        System.out.println(p.getName()); // "Bob"还是"Alice"?
    }
}

class Person {
    private String name;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

因为String 的赋值方法是开辟一块新的内存去存储 "Alice" 并且将 "Alice"的地址赋值给bob，原先的 "Bob" 还存在，而此时 name 的指向也还是 "Bob" 所以不会变。而之前数组改变的原因是内存中的数组本身就被改变了。

## 构造方法
创建实例的时，我们经常需要同时初始化这个实例的字段，例如：

```java
Person ming = new Person();
ming.setName("小明");
ming.setAge(12);
```

初始化对象实例需要三行代码，而且，如果忘了调用 setNmae() 或者 setAge()，这个实例内部的状态就是不正确的。

可以在创建对象实例时就把内部字段全部初始化为合适的值

这时，我们需要构造方法

创建实例的时候，实际上是通过构造方法来初始化实例的，我们先定义一个构造方法，能在创建 Person实例的时候，一次性传入 name 和 age ，完成初始化

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person("Xiao Ming", 15);
        System.out.println(p.getName());
        System.out.println(p.getAge());
    }
}

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}

```

由于构造方法是如此特殊，所以构造方法的名称就是类名。构造方法的参数没有限制，在方法内部，也可以编写任意语句。但是，和普通方法相比，构造方法没有返回值(也没有void)，调用构造方法，必须用 new 操作符。

### 默认构造方法
任何 class 都有构造方法

前面我们并没有为 Person 类编写构造方法，但可以调用 new Person()的原因是

如果一个类没有定义构造方法，编译器会自动为我们生成一个默认的构造方法，它没有参数，也没有执行语句，类似这样：
```java
class Person {
    public Person() {
    }
}
```

要特别注意的是，如果我们定义了一个构造方法，那么，编译器就不再自动创建默认的构造方法：

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person(); // 编译错误:找不到这个构造方法
    }
}

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
```

如果既要能使用带参数的构造方法，又想保留不带参数的构造方法，那么只能吧两个构造方法都定义出来

```java
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Xiao Ming", 15); // 既可以调用带参数的构造方法
        Person p2 = new Person(); // 也可以调用无参数构造方法
    }
}

class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }
}
```

没有在构造方法中初始话字段时，引用类型的字段默认是 null ，数值类型的字段用默认值，int 类型默认值是 0 ，布尔类型默认值是 flase：

```java
class Person {
    private String name; // 默认初始化为null
    private int age; // 默认初始化为0

    public Person() {
    }
}
```

也可以对字段直接进行初始化

```java
class Person {
    private String name = "Unamed";
    private int age = 10;
}
```

那么问题来了：既对字段进行初始化，又在构造方法中对字段进行初始化

```java
class Person {
    private String name = "Unamed";
    private int age = 10;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

当我们创建对象的时候，new Person("Xiao Ming", 12)得到的对象实例，字段的初始值是什么

在Java中，创建对象实例的时候，按照如下顺序进行初始化：

1. 先初始化字段，例如，int age = 10;表示字段初始化为10，double salary;表示字段默认初始化为0，String name;表示引用类型字段默认初始化为null；

2. 执行构造方法的代码进行初始化。

因此，构造方法的代码由于后运行，所以，new Person("Xiao Ming", 12)的字段值最终由构造方法的代码确定。

### 多构造方法
可以定义多个构造方法，在通过 new 操作符调用的时候，编译器通过构造方法的参数数量，位置和类型自动区分：

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name) {
        this.name = name;
        this.age = 12;
    }

    public Person() {
    }
}
```

如果调用new Person("Xiao Ming", 20);，会自动匹配到构造方法public Person(String, int)。

如果调用new Person("Xiao Ming");，会自动匹配到构造方法public Person(String)。

如果调用new Person();，会自动匹配到构造方法public Person()。

一个构造方法可以调用其他构造方法，这样做的目的是便于代码复用。调用其他构造方法的语法是
this(...)

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name) {
        this(name, 18); // 调用另一个构造方法Person(String, int)
    }

    public Person() {
        this("Unnamed"); // 调用另一个构造方法Person(String)
    }
}
```

## 方法重载
在同一个类中，我们可以定义多个方法。如果有一系列方法，他们的功能都是类似的，只有参数不同，那么，可以把这一组方法名做成`同名`方法，例如，在 Hello 类中，定义多个 hello()方法

```java
class Hello {
    public void hello() {
        System.out.println("Hello, world!");
    }

    public void hello(String name) {
        System.out.println("Hello, " + name + "!");
    }

    public void hello(String name, int age) {
        if (age < 18) {
            System.out.println("Hi, " + name + "!");
        } else {
            System.out.println("Hello, " + name + "!");
        }
    }
}
```

这种方法名相同，但各自的参数不同，称为方法重载(Overload)

注意：方法重载的返回值类型通常是相同的

方法重载的目的是，功能类似的方式使用统一名字，更容易记住，因此，调用起来更简单

举个例子，String类提供了多个重载方法indexOf()，可以查找子串：

- int indexOf(int ch)：根据字符的Unicode码查找；
- int indexOf(String str)：根据字符串查找；
- int indexOf(int ch, int fromIndex)：根据字符查找，但指定起始位置；
- int indexOf(String str, int fromIndex)根据字符串查找，但指定起始位置。

## 继承
在前面的章节中，我么你已经定义了 Person 类：

```java
class Person {
    private String name;
    private int age;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
}
```

现在假设需要定义一个 Student 类，字段如下：

```java
class Student {
    private String name;
    private int age;
    private int score;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
    public int getScore() { … }
    public void setScore(int score) { … }
}
```

仔细观察发现，发现 Student 类包含了 Person 类已有的字段和方法，只是多出了一个 score 字段和相应的 getScore(),setScore() 方法

Java 使用 extends 关键字来实现继承：

```java
class Person {
    private String name;
    private int age;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
}

class Student extends Person {
    // 不要重复name和age字段/方法,
    // 只需要定义新增score字段/方法:
    private int score;

    public int getScore() { … }
    public void setScore(int score) { … }
}
```

可见通过继承，Student 只需要编写额外的功能，不再需要重复代码

在OOP的术语中，我们把 Person 称为超类(super class)，父类(parent class)，基类(base class)，把 Student 称为子类(sub class)，扩展类(extended class)

### 继承树
注意到我们在定义 Person 的时候，没有写 extends，在Java中，没有明确写 extebds 的类，编译器会自动加上 extends Object 所以，除了 Object ，都会继承自某个类。下图是 Person ， Student 的继承树。

```
┌───────────┐
│  Object   │
└───────────┘
      ▲
      │
┌───────────┐
│  Person   │
└───────────┘
      ▲
      │
┌───────────┐
│  Student  │
└───────────┘
```

Java 只允许一个 chass 继承自一个类，因此，一个类有且仅有一个父类。只有 Object 特殊，它没有父类

类似的，如果我们定义一个继承自 Person 的 Teacher ，它的继承树关系如下

```java
       ┌───────────┐
       │  Object   │
       └───────────┘
             ▲
             │
       ┌───────────┐
       │  Person   │
       └───────────┘
          ▲     ▲
          │     │
          │     │
┌───────────┐ ┌───────────┐
│  Student  │ │  Teacher  │
└───────────┘ └───────────┘
```

### protected
继承有个特点，就是子类无法访问父类的 private 字段或者 private 方法。例如，Student 类就无法访问 Person 类的 name 和 age 字段：

```java
class Person {
    private String name;
    private int age;
}

class Student extends Person {
    public String hello() {
        return "Hello, " + name; // 编译错误：无法访问name字段
    }
}
```

这使得继承的作用被削弱了。为了让子类可以访问父类的字段，我们需要把 private 改为 protected 用 protected 修是的字段可以被子类访问：

```java
class Person {
    protected String name;
    protected int age;
}

class Student extends Person {
    public String hello() {
        return "Hello, " + name; // OK!
    }
}
```

因此， protected 关键字可以把字段和方法的访问权限控制在继承树内部，一个 protected 字段和方法可以被其子类，以及子类的子类所访问

### super
super 关键字表示父类(超类)，子类引用父类的字段时，可以用 super.fieldName

例：
```java
class Student extends Person {
    public String hello() {
        return "Hello, " + super.name;
    }
}
```

实际上，这里使用 super.name，this.name，name效果都是一样的，编译器会自动定位到父类的name 字段

但是在某些时候，就必须使用 super 例

```java
public class Main {
    public static void main(String[] args) {
        Student s = new Student("Xiao Ming", 12, 89);
    }
}

class Person {
    protected String name;
    protected int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class Student extends Person {
    protected int score;

    public Student(String name, int age, int score) {
        this.score = score;
    }
}
```
运行上面的代码，会得到一个编译错误，大意是在 Student 的构造方法中，无法调用 person 的构造方法

这是因为在 java 中，任何class 的构造方法，第一行语句必是调用父类的构造方法，如果没有明确的调用父类的构造方法，编译器会帮我们自动加一句 super(); 所以，Stundent 类的构造方法实际上是这样

```java
class Student extends Person {
    protected int score;

    public Student(String name, int age, int score) {
        super(); // 自动调用父类的构造方法
        this.score = score;
    }
}
```

但是，Person 类并没有无参数的构造方法，因此，编译失败。

解决方法是调用 Person 类存在的某个构造方法。

例：
```java
class Student extends Person {
    protected int score;

    public Student(String name, int age, int score) {
        super(name, age); // 调用父类的构造方法Person(String, int)
        this.score = score;
    }
}
```

这样就可以正常编译了

因此得出结论：如果父类没有默认的构造方法，子类就必须显示调用 super() 并给出参数以便让编译器定位到父类的一个合适的构造方法。

这里还顺带引出了另一个问题：即子类不会继承任何父类的构造方法。子类默认的构造方法是编译器自动生成的，不是继承的。

### 向上转型
如果一个引用变量的类型是 Student，那么它可以指向一个 Student 类型的实例：
```java
Student s = new Student();
```

如果一个引用类型的变量是Person，那么它可以指向一个Person类型的实例：
```java
Person p = new Person();
```

现在问题来了：如果Student是从Person继承下来的，那么，一个引用类型为Person的变量，能否指向Student类型的实例？
```java
Person p = new Student(); // ???
```

测试发现，这种指向是允许的

这是因为 Student 继承自 Person，因此，它拥有 Person 的全部功能，Person 类型的变量，如果指向 Student 类型的实例，对它进行操作，是没有问题的

这种把一个子类安全的变为父类类型的赋值，被称为向上转型(upcasting)

向上转型实际上是把一个子类型安全的变为更加抽象的父类型

```java
Student s = new Student();
Person p = s; // upcasting, ok
Object o1 = p; // upcasting, ok
Object o2 = s; // upcasting, ok
```

注意到继承树是 Student > Person > Object ，所以，可以吧 Student 类型转型为 Person，或者更高层次的 Object

### 向下转型
和向上转型相反，如果把一个父类型强制转型为子类类型，就是向下转型(downcasting)

例：
```java
Person p1 = new Student(); // upcasting, ok
Person p2 = new Person();
Student s1 = (Student) p1; // ok
Student s2 = (Student) p2; // runtime error! ClassCastException!
```

Person类型p1实际指向Student实例，Person类型变量p2实际指向Person实例。在向下转型的时候，把p1转型为Student会成功，因为p1确实指向Student实例，把p2转型为Student会失败，因为p2的实际类型是Person，不能把父类变为子类，因为子类功能比父类多，多的功能无法凭空变出来。

因此，向下转型很可能会失败，失败的时候，JAVA虚拟机会报 ClassCastException

为了避免向下转型出错，java 提供了 insyanceof 操作符，可以判断一个实例究竟是不是某种类型

```java
Person p = new Person();
System.out.println(p instanceof Person); // true
System.out.println(p instanceof Student); // false

Student s = new Student();
System.out.println(s instanceof Person); // true
System.out.println(s instanceof Student); // true

Student n = null;
System.out.println(n instanceof Student); // false
```

instanceof 实际上判断一个变量所指向的实例是否都是指定类型，或这个类型的子类，如果一个引用变量为 null 那么对任何 instanceof 的判断都为 false

利用 instanceof，在向下转型前可以先判断

```java
Person p = new Student();
if (p instanceof Student) {
    // 只有判断成功才会向下转型:
    Student s = (Student) p; // 一定会成功
}
```

### 区分继承和组合
在使用继承时，我们要注意逻辑一致性

考察下面的 Book 类

```java
class Book {
    protected String name;
    public String getName() {...}
    public void setName(String name) {...}
}
```

这个 Book 类也有 name 字段，name，我们能不能让 Student 继承自 Book 呢？

```java
class Student extends Book {
    protected int score;
}
```

显然，从逻辑上来讲，这是不合理的，Student 不应该从 Book 继承，而应该从 Person 继承

究其原因，是因为 Stundent 是 Person 的一种，它们是 is 关系，而 Student 并不是 Book 实际上 Student 和 Book 的关系是 has 关系

具有 has 关系不应该使用继承，而是使用组合，即 Student 可以持有一个 Book 实例

```java
class Student extends Person {
    protected Book book;
    protected int score;
}
```

因此，继承是 is 关系，组合是 has 关系

## 多态
在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为覆写(Override)

例如，在 Person 类中，我们定义了 run() 方法：

```java
class Person {
    public void run() {
        System.out.println("Person.run");
    }
}
```

在子类 Student 中，覆写这个 run() 方法：

```java
class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```

Override 和 Overload 不同的是，如果方法签名如果不同，就是 Overload，Overload方法是一个新方法；如果方法签名相同，并且返回值也相同，就是 Override

>注意：方法名相同，方法参数相同，但方法返回值不同，也是不同的方法。在Java程序中，出现这种情况，编译器会报错。

```java
class Person {
    public void run() { … }
}

class Student extends Person {
    // 不是Override，因为参数不同:
    public void run(String s) { … }
    // 不是Override，因为返回值不同:
    public int run() { … }
}
```

加上 `@Override` 可以让编译器帮助检查是否进行了正确的覆写，希望覆写，但是不小心写错了方法签名，编译器会报错

```java
public class Main {
    public static void main(String[] args) {
    }
}

class Person {
    public void run() {}
}

public class Student extends Person {
    @Override // Compile error!
    public void run(String s) {}
}
```

但是 `@Override` 不是必需的。

在上一节中，我们已经知道，引用变量的申明类型可能与其实际类型不符

例：

```java
Person p = new Student();
```

现在，考虑一种情况，如果子类覆写了父类的方法

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run(); // 应该打印Person.run还是Student.run?
    }
}

class Person {
    public void run() {
        System.out.println("Person.run");
    }
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```

那么，一个是实际类型为 Student ，引用类型为 Person 的变量，调用其 run() 方法，调用的是 Person 还是 Student 的 run() 方法？

运行了上面的代码就可以知道，实际上调用的方法是 Student 的 run() 方法。因此可以得出结论：

Java的实例方法调用的是基于运行时的实际类型的动态调用，而非变量的声明类型

这个非常重要的特性在面向对象编程中称之为多态。它的英文拼写非常复杂：Polymorphic

### 多态
多态是指，针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法，

例
```java
Person p = new Student();
p.run(); // 无法确定运行时究竟调用哪个run()方法
```

如果按照上面的代码来看，肯定调用的是 Student 的 run() 方法啊。

但是，假设我们编写这样一个方法：

```java
public void runTwice(Person p) {
    p.run();
    p.run();
}
```

它传入的参数类型是 Prtson，我们是无法知道传入的参数实际类型究竟是 Person，还是 Student，还是 Person 的其他子类，因此，也无法确定调用的是不是 Person 类定义的 run() 方法

所以，多态的特性就是，运行期才能动态决定调用的子类方法，对某个类型调用某个方法，执行的实际方法可能是某个子类的覆写方法，这种不确定性的方法调用，有什么用吗。

栗子：

假设定义一种收入，需要给他报税，那么先定义一个 Income 类：

```java
class Income {
    protected double income;
    public double getTax() {
        return income * 0.1; // 税率10%
    }
}
```

对于工资收入，可以减去一个技术，那么我们可以从 Income 派生出 SalaryIncome，并覆写 getTax()：

```java
class Salary extends Income {
    @Override
    public double getTax() {
        if (income <= 5000) {
            return 0;
        }
        return (income - 5000) * 0.2;
    }
}
```

如果你享受国务院的特殊津贴，那么按照规定，可以全部免税：

```java
class StateCouncilSpecialAllowance extends Income {
    @Override
    public double getTax() {
        return 0;
    }
}
```

现在，编写一个报税的财务软件，对于一个人的所有收入进行报税，可以这么写：

```java
public double totalTax(Income... incomes) {
    double total = 0;
    for (Income income: incomes) {
        total = total + income.getTax();
    }
    return total;
}
```

完整示例：

```java
public class Main {
    public static void main(String[] args) {
        // 给一个有普通收入、工资收入和享受国务院特殊津贴的小伙伴算税:
        Income[] incomes = new Income[] {
            new Income(3000),
            new Salary(7500),
            new StateCouncilSpecialAllowance(15000)
        };
        System.out.println(totalTax(incomes));
    }

    public static double totalTax(Income... incomes) {
        double total = 0;
        for (Income income: incomes) {
            total = total + income.getTax();
        }
        return total;
    }
}

class Income {
    protected double income;

    public Income(double income) {
        this.income = income;
    }

    public double getTax() {
        return income * 0.1; // 税率10%
    }
}

class Salary extends Income {
    public Salary(double income) {
        super(income);
    }

    @Override
    public double getTax() {
        if (income <= 5000) {
            return 0;
        }
        return (income - 5000) * 0.2;
    }
}

class StateCouncilSpecialAllowance extends Income {
    public StateCouncilSpecialAllowance(double income) {
        super(income);
    }

    @Override
    public double getTax() {
        return 0;
    }
}
```

观察 totalTax()方法：利用多台，totalTax() 方法只需要和 Income 打交道，他完全不需要知道 Salary 和 StateCouncilSpecialAllowance 的存在，就可以正确计算出总的税。如果我们要新增一种稿费收入，只需要从 Income 派生，然后正确覆写 getTax() 方法就可以。把新的类型传入 totalTax()，不需要修改任何代码。

可见，多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码。

### 覆写 Object方法
因为所有的 class 最终都继承自 Object，而Object 定义了几个重要的方法：

- toString()：把 instance 输出为 String
- equals()：判断两个 instance 是否逻辑相等
- hashCode()：计算一个 instance 的哈希值

在必要的情况下，我们可以覆写 Object 的这几个方法。例如

```java
class Person {
    ...
    // 显示更有意义的字符串:
    @Override
    public String toString() {
        return "Person:name=" + name;
    }

    // 比较是否相等:
    @Override
    public boolean equals(Object o) {
        // 当且仅当o为Person类型:
        if (o instanceof Person) {
            Person p = (Person) o;
            // 并且name字段相同时，返回true:
            return this.name.equals(p.name);
        }
        return false;
    }

    // 计算hash:
    @Override
    public int hashCode() {
        return this.name.hashCode();
    }
}
```

### 调用 super
在子类的覆写方法中，如果要调用父类的被覆写的方法，可以通过 super 来调用

例：
```java
class Person {
    protected String name;
    public String hello() {
        return "Hello, " + name;
    }
}

Student extends Person {
    @Override
    public String hello() {
        // 调用父类的hello()方法:
        return super.hello() + "!";
    }
}
```

### final
继承可以允许子类覆写父类的方法，如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为 final。用 final 修饰的方法不能被 Override；

```java
class Person {
    protected String name;
    public final String hello() {
        return "Hello, " + name;
    }
}

Student extends Person {
    // compile error: 不允许覆写
    @Override
    public String hello() {
    }
}
```

如果一个类不希望任何其他的类继承自它，那么可以把这个类本身标记为 final ，用 final 修饰的类不能被继承：

```java
final class Person {
    protected String name;
}

// compile error: 不允许继承自Person
Student extends Person {
}
```

对于一个类的实例字段，同样可以用 final 修饰，用 final 修饰的字段初始化后不能被修改。

```java
class Person {
    public final String name = "Unamed";
}
```

对 final 字段重新赋值会报错

```java
Person p = new Person();
p.name = "New Name"; // compile error!
```

可以在构造方法中初始化 final 字段：

```java
class Person {
    public final String name;
    public Person(String name) {
        this.name = name;
    }
}
```

这种方法更为常用，因为可以保证实例一旦创建，其 final 字段就不可修改

## 抽象类
由于多态的存在，每个子类都可以覆写父类的方法

```java
class Person {
    public void run() { … }
}

class Student extends Person {
    @Override
    public void run() { … }
}

class Teacher extends Person {
    @Override
    public void run() { … }
}
```

从 Person 类派生的 Student 和 Teacher 都可以覆写 run() 方法

如果父类 Person 的 run() 方法没有实际意义，能否去掉方法的执行语句？

```java
class Person {
    public void run(); // Compile Error!
}
```

是不行的，会导致编译错误，因为定义方法的时候，必须实现方法的语句。

能不能去掉父类的 run() 方法

答案还是不行，因为去掉父类的 run() 方法，就失去了多态的特效，例如， runTwice() 就无法编译

```java
public void runTwice(Person p) {
    p.run(); // Person没有run()方法，会导致编译错误
    p.run();
}
```

如果父类的方法本身不需要实现仍和功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以吧父类的方法声明为抽象方法：

```java
class Person {
    public abstract void run();
}
```

把一个方法声明为 abstract，表示它是一个抽象方法，本身没有实现任何方法语句，因为这个抽象方法本身是无法执行的，所以，Person 类也无法被实例化。编译器会告诉我们，无法编译 Person 类，因为它包含抽象方法。

必须把 Person 类本身也声明为 abstract，才能正确编译它

```java
abstract class Person {
    public abstract void run();
}
```

### 抽象类
如果一个 class 定义了方法，但没有具体执行代码，这个方法就是抽象方法，抽象方法用 abstract 修饰

因为无法执行抽象方法，因此这个类也必须申明为抽象类(abstract class)

使用 abstract 修饰的类就是抽象类，我们无法实例化一个抽象类

```java
Person p = new Person(); // 编译错误
```

无法实例化的抽象类有什么用。

因为抽象类本身被设计成只能用于被继承，因此，抽象类可以强迫子类实现其定义的抽象方法，否则编译会报错，因此，抽象方法实际上相当于定义了"规范"

例如，Person 类定义了抽象方法 run()，那么，在实现子类 Student 的时候，就必须覆写 run() 方法

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student();
        p.run();
    }
}

abstract class Person {
    public abstract void run();
}

class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student.run");
    }
}
```

### 面对抽象编程
当我们定义了抽象类 Person，以及具体的 Student，Teacher子类的时候，我们可以通过抽象类 Person 类型去引用具体的子类的实例：

```java
Person s = new Student();
Person t = new Teacher();
```

这种引用抽象类的好处在于，我们对其进行方法调用，并不关心 Person 类型变量的具体子类型：

```java
// 不关心Person变量的具体子类型:
s.run();
t.run();
```

同样的代码，如果引用的是一个新的子类，我们仍然不关系具体类型：

```java
// 同样不关心新的子类是如何实现run()方法的：
Person e = new Employee();
e.run();
```

这种尽量引用高层类型，避免引用实际子类型的方式，称之为面向抽象编程。

面向抽象编程的本质就是：

- 上层代码只定义规范（例如：abstract class Person）；

- 不需要子类就可以实现业务逻辑（正常编译）；

- 具体的业务逻辑由不同的子类实现，调用者并不关心。

## 接口
在抽象类中，抽象方法本质上是定义接口规范：即规定高层类的接口，从而保证所有子类都有相同的接口实现，这样，多态就能发挥出威力

如果一个抽象类没有字段，所有方法全部都是抽象方法

```java
abstract class Person {
    public abstract void run();
    public abstract String getName();
}
```

就可以把该抽象类改写为接口：interface

在java 中，使用 interface 可以声明一个接口：

```java
interface Person {
    void run();
    String getName();
}
```

所谓 interface，就是比抽象类还抽象的纯抽象接口，因为他连字段都不能有。因为接口定义的所有方法默认都是 public abstract 的，所以这两个修饰符可以不写出来(写不写都一样)

当具体的 class 去实现一个 interface 时，需要使用 implements 关键字

例
```java
class Student implements Person {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        System.out.println(this.name + " run");
    }

    @Override
    public String getName() {
        return this.name;
    }
}
```

我们知道，在java 中，一个类只能继承自另一个类，不能从多个类继承，但是，一个类可以实现多个 interface 例如：

```java
class Student implements Person, Hello { // 实现了两个interface
    ...
}
```

### 术语
注意区分术语

java 接口特指 interface 的定义，表示一个接口类型和一组方法签名，而编程接口泛指接口规范，如方法签名，数据格式，网络协议等。

抽象类和接口的对比如下：

- |  abstract class	   |      interface
-      |       -               |        -
继承	    |只能extends一个class	 |可以implements多个interface
字段	    |可以定义实例字段	      |不能定义实例字段
抽象方法	 |可以定义抽象方法	       |可以定义抽象方法
非抽象方法	 |可以定义非抽象方法	    |可以定义default方法

### 接口继承
一个 interface 可以继承自另一个 interface 。interface 继承自 interface 使用 extends ，他相当于扩展了接口的方法。

例
```java
interface Hello {
    void hello();
}

interface Person extends Hello {
    void run();
    String getName();
}
```

此时，Person 接口继承自 Hello 接口，因此，Person 接口现在实际上有三个抽象方法签名，其中一个来自继承的 Hello 接口

### 继承关系
合理设计 interface 和 abstract class 的街城管希，可充分复用代码，一般来说，公共逻辑适合放在 abstract class 中，具体逻辑放到各个子类，而几口层次代表抽象程度，可以参考java 的集合类定义的一组接口，抽象类以及具体子类的继承关系。

```
┌───────────────┐
│   Iterable    │
└───────────────┘
        ▲                ┌───────────────────┐
        │                │      Object       │
┌───────────────┐        └───────────────────┘
│  Collection   │                  ▲
└───────────────┘                  │
        ▲     ▲          ┌───────────────────┐
        │     └──────────│AbstractCollection │
┌───────────────┐        └───────────────────┘
│     List      │                  ▲
└───────────────┘                  │
              ▲          ┌───────────────────┐
              └──────────│   AbstractList    │
                         └───────────────────┘
                                ▲     ▲
                                │     │
                                │     │
                     ┌────────────┐ ┌────────────┐
                     │ ArrayList  │ │ LinkedList │
                     └────────────┘ └────────────┘
```

在使用的时候，实例化的对象永远只能是某个具体的子类，但总是通过接口去引用它，因为接口比抽象类更抽象：

```java
List list = new ArrayList(); // 用List接口引用具体子类的实例
Collection coll = list; // 向上转型为Collection接口
Iterable it = coll; // 向上转型为Iterable接口
```

### default方法
在接口中，可以定义 default 方法。例如，把 Person 接口的 run() 方法改为 default 方法

```java
public class Main {
    public static void main(String[] args) {
        Person p = new Student("Xiao Ming");
        p.run();
    }
}

interface Person {
    String getName();
    default void run() {
        System.out.println(getName() + " run");
    }
}

class Student implements Person {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}
```

实现类可以不必覆写 default 方法。default 方法的目的是，当我们需要给接口新增一个方法时，会涉及到修改全部子类。如果新增的事 default 方法，那么子类就不必全部修改，只需要在需要覆写的地方去覆写新增方法。

default 方法和抽象类的普通方法是有所不同的，因为 interface 没有字段，default 方法无法访问字段，而抽象类的普通方法可以访问实例字段。

## 静态字段和静态方法
在一个 class 中定义的字段，我们称之为实例字段。实例字段的特点是，每个实例都有独立的字段，各个实例的同名字段互不影响

还有一种字段，是用 static 修饰的字段，称之为静态字段：static field

实例子弹在每个事例中都有自己的一个独立"空间"，但是静态字段只有一个共享的"空间"，所有的实例都会共享该字段

```java
class Person {
    public String name;
    public int age;
    // 定义静态字段number:
    public static int number;
}
```

```java
public class Main {
    public static void main(String[] args) {
        Person ming = new Person("Xiao Ming", 12);
        Person hong = new Person("Xiao Hong", 15);
        ming.number = 88;
        System.out.println(hong.number);
        hong.number = 99;
        System.out.println(ming.number);
    }
}

class Person {
    public String name;
    public int age;

    public static int number;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

对于静态字段，无论修改哪个实例的静态字段，效果都是一样的：所有实例的静态字段都被修改了，原因是静态字段并不属于实例：

```java
        ┌──────────────────┐
ming ──>│Person instance   │
        ├──────────────────┤
        │name = "Xiao Ming"│
        │age = 12          │
        │number ───────────┼──┐    ┌─────────────┐
        └──────────────────┘  │    │Person class │
                              │    ├─────────────┤
                              ├───>│number = 99  │
        ┌──────────────────┐  │    └─────────────┘
hong ──>│Person instance   │  │
        ├──────────────────┤  │
        │name = "Xiao Hong"│  │
        │age = 15          │  │
        │number ───────────┼──┘
        └──────────────────┘
```

虽然实例可以访问静态字段，但是它们指向的其实都是 Person class 的静态字段，所以，所有实例共享一个静态字段

因此，不推荐使用 `实例变量.静态变量` 去访问静态字段，因为在 java 程序中，实例对象并没有静态字段，实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为 `类名.静态字段`来访问静态对象

推荐用类名来访问静态子弹。可以吧静态字段理解为描述 class 本身的字段(非实例字段)，对于上面的代码，更好的写法是：

```java
Person.number = 99;
System.out.println(Person.number);
```

### 静态方法
有静态字段，就有静态方法，用 static 修饰的方法称之为静态方法

调用实例方法必须通过一个实例变量，而调用静态方法则不需要实例变量，通过类名就可以调用。静态方法类似其他编程语言的函数，例如：

```java
public class Main {
    public static void main(String[] args) {
        Person.setNumber(99);
        System.out.println(Person.number);
    }
}

class Person {
    public static int number;

    public static void setNumber(int value) {
        number = value;
    }
}
```

因为静态方法属于 class 而不属于实例，因此，静态方法内部，无法访问 this 变量，也无法访问实例字段，它只能访问静态字段

通过实例变量也可以调用静态方法，但这只是编译器自动帮我们把实例改写成类名而已

通常情况下，通过实例变量访问静态字段和静态方法，会得到一个编译警告

静态方法经常用于工具类。

例:
```java
Arrays.sort()

Math.random()
```

静态方法也经常用于辅助方法，注意到 java 程序的入口 main() 也是静态方法

### 接口的静态字段
因为 interface 是一个纯抽象类，所以它不能定义实例字段，但是，interface 是可以有静态字段的，并且静态字段必须为 final 类型：

```java
public interface Person {
    public static final int MALE = 1;
    public static final int FEMALE = 2;
}
```

实际上，因为 interface 的字段只能是 public statci final 类型，所以我们可以把这些修饰符都去掉，上代码可以简写为：

```java
public interface Person {
    // 编译器会自动加上public statc final:
    int MALE = 1;
    int FEMALE = 2;
}
```

编译器会自动把该字段变为public static final类型。

## 包
在前面的代码中，我们把类和接口命名为Person、Student、Hello等简单名字。

在现实中，如果小明写了一个Person类，小红也写了一个Person类，现在，小白既想用小明的Person，也想用小红的Person，怎么办？

如果小军写了一个Arrays类，恰好JDK也自带了一个Arrays类，如何解决类名冲突？

在Java中，我们`使用package来解决名字冲突`。

Java定义了一种名字空间，称之为包：package。一个类总是属于某个包，类名（比如Person）只是一个简写，真正的完整类名是包名.类名。

例如：

```
小明的Person类存放在包ming下面，因此，完整类名是ming.Person；

小红的Person类存放在包hong下面，因此，完整类名是hong.Person；

小军的Arrays类存放在包mr.jun下面，因此，完整类名是mr.jun.Arrays；

JDK的Arrays类存放在包java.util下面，因此，完整类名是java.util.Arrays。

```

在定义class的时候，我们需要在第一行声明这个class属于哪个包。

小明的Person.java文件：

```java
package ming; // 申明包名ming

public class Person {
}
```

小军的Arrays.java文件：

```java
package mr.jun; // 申明包名mr.jun

public class Arrays {
}
```

在Java虚拟机执行的时候，JVM只看完整类名，因此，只要包名不同，类就不同。

包可以是多层结构，用.隔开。例如：java.util。

>要特别注意：包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。

没有定义包名的 class ，它使用的是默认包，非常容易引起名字冲突，因此，不推荐不写包名的做法

还需要按照包结构把上面的 java 文件组织起来，假设以 packege_sample 作为根目录，src 作为源码目录，那么所有文件的结构就是：

```
package_sample
└─ src
    ├─ hong
    │  └─ Person.java
    │  ming
    │  └─ Person.java
    └─ mr
       └─ jun
          └─ Arrays.java
```

即所有 java文件对应的目录层次要和包的层次一致

变异后的 .class 文件也需要按照包结构存放。如果使用IDE ，八遍以后的 .class 文件放到 bin 目录下，那么，编译的文件结构就是：

```
package_sample
└─ bin
   ├─ hong
   │  └─ Person.class
   │  ming
   │  └─ Person.class
   └─ mr
      └─ jun
         └─ Arrays.class
```

编译的命令相对比较复杂，我们需要在 src 目录下执行 javac 命令

```
javac -d ../bin ming/Person.java hong/Person.java mr/jun/Arrays.java
```

在 IDE中，会自动根据包结构编译所有的java 源码所以不担心使用命令行编译的复杂命令

### 包作用域
位于同一个包的类，可以访问包作用域的字段和方法，不用 public protected private 修是的字段和方法就是包作用域，例如，Person 类型定义在 hello 包下面

```java
package hello;

public class Person {
    // 包作用域:
    void hello() {
        System.out.println("Hello!");
    }
}
```

Main 类也定义在hello 包下面：

```java
package hello;

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.hello(); // 可以调用，因为Main和Person在同一个包
    }
}
```

### import
在一个 calss 中，我们总会引用其他的 class。例如，小明的 ming.Person 类,如果要引用小军的 mr.jun.Arrays 类，他有三种写法

第一种，直接写出完整类名

```java
// Person.java
package ming;

public class Person {
    public void run() {
        mr.jun.Arrays arrays = new mr.jun.Arrays();
    }
}
```

很显然，每次写完整类名比较痛苦。

因此，第二种写法是用 import 语句，导入小军的 Arrays，然后写简单类名

```java
// Person.java
package ming;

// 导入完整类名:
import mr.jun.Arrays;

public class Person {
    public void run() {
        Arrays arrays = new Arrays();
    }
}
```

在写 import 的时候，可以使用 * ，表示把这个包下面所有的 class 都导入进来(但不包括子包的class)

```java
// Person.java
package ming;

// 导入mr.jun包的所有class:
import mr.jun.*;

public class Person {
    public void run() {
        Arrays arrays = new Arrays();
    }
}
```

我们一般不推荐这种写法，因为在导入了多个包后，很难看出Arrays类属于哪个包。

还有一种import static的语法，它可以导入可以导入一个类的静态字段和静态方法：

```java
package main;

// 导入System类的所有静态字段和静态方法:
import static java.lang.System.*;

public class Main {
    public static void main(String[] args) {
        // 相当于调用System.out.println(…)
        out.println("Hello, world!");
    }
}
```

import static 很少使用

Java 编译器最终编译出的 .class 文件只使用`完整类名`，因此，在代码中，当编译器遇到一个 class名称时

- 如果是完整类名，就直接根据完整类名查找这个class；

- 如果是简单类名，按下面的顺序依次查找：

    - 查找当前package是否存在这个class；

    - 查找import的包是否包含这个class；

    - 查找java.lang包是否包含这个class。

如果按照上面的规则还无法确定类名，则编译报错

例
```java
// Main.java
package test;

import java.text.Format;

public class Main {
    public static void main(String[] args) {
        java.util.List list; // ok，使用完整类名 -> java.util.List
        Format format = null; // ok，使用import的类 -> java.text.Format
        String s = "hi"; // ok，使用java.lang包的String -> java.lang.String
        System.out.println(s); // ok，使用java.lang包的System -> java.lang.System
        MessageFormat mf = null; // 编译错误：无法找到MessageFormat: MessageFormat cannot be resolved to a type
    }
}
```

因此，编写 class 的时候，编译器会自动帮我们做两个 import 动作

- 默认自动 import 当前 package 的其他 class
- 默认自动 import java.lang.*

>注意：自动导入的是java.lang包，但类似java.lang.reflect这些包仍需要手动导入。

### 最佳实践
为了避免名字冲突，我们需要确定唯一的包名。推荐的做法是使用倒置的域名来确保唯一性。例如：

- org.apache
- org.apache.commons.log
- com.liaoxuefeng.sample

子包就可以根据功能自行命名。

要注意不要和java.lang包的类重名，即自己的类不要使用这些名字：

- String
- System
- Runtime
- ...

要注意也不要和JDK常用类重名：

- java.util.List
- java.text.Format
- java.math.BigInteger
- ...

## 作用域
在java 中，我们经常看到public protected private这些修饰符，在java 中，这些修饰符可以用来限定访问作用域

### public 
定义为 public 的 class，interface 可以被其他任何类访问

```java
package abc;

public class Hello {
    public void hi() {
    }
}
```

上面的 Hello 是 public 因此，可以被其他的包的类访问

```java
package xyz;

class Main {
    void foo() {
        // Main可以访问Hello
        Hello h = new Hello();
    }
}
```

定义为 public 的 field，method 可以被其他类访问，前提是首先有访问 class 的权限

```java
package abc;

public class Hello {
    public void hi() {
    }
}
```

上面的hi()方法是public，可以被其他类调用，前提是首先要能访问Hello类：

```java
package xyz;

class Main {
    void foo() {
        Hello h = new Hello();
        h.hi();
    }
}
```

### private
定义为 private 的 field，method无法被其他类访问

```java
package abc;

public class Hello {
    // 不能被其他类调用:
    private void hi() {
    }

    public void hello() {
        this.hi();
    }
}
```

实际上，确切的说，private 访问权限被限定在 class 内部，而且与方法声明顺序`无关`推荐把 private 方法放到后面，因为 public 方法定义了类对外提供的功能，阅读代码的时候，应该先关注 public 方法:

```java
package abc;

public class Hello {
    public void hello() {
        this.hi();
    }

    private void hi() {
    }
}
```

由于java 支持嵌套类，如果一个类内部还定义了嵌套类，那么，嵌套类拥有访问 private 的权限

```java
public class Main {
    public static void main(String[] args) {
        Inner i = new Inner();
        i.hi();
    }

    // private方法:
    private static void hello() {
        System.out.println("private hello!");
    }

    // 静态内部类:
    static class Inner {
        public void hi() {
            Main.hello();
        }
    }
}
```

定义在一个class 内部的 class 称为嵌套类(nested class)，java 支持好几种嵌套类

### protected
protected 作用域继承关系。定义为 protected 的字段和方法可以为子类访问，以及子类的子类

```java
package abc;

public class Hello {
    // protected方法:
    protected void hi() {
    }
}
```

上面的 protected 方法可以被继承的类访问

```java
package xyz;

class Main extends Hello {
    void foo() {
        Hello h = new Hello();
        // 可以访问protected方法:
        h.hi();
    }
}
```

### package
最后，包的作用域是指一个类允许访问同一个 package 的没有 public private 修饰的 class ，以及没有 public protected private 修是的字段和方法

```java
package abc;
// package权限的类:
class Hello {
    // package权限的方法:
    void hi() {
    }
}
```

只要在同一个包，就可以访问 package 权限的class field 和 method

```java
package abc;

class Main {
    void foo() {
        // 可以访问package权限的类:
        Hello h = new Hello();
        // 可以调用package权限的方法:
        h.hi();
    }
}
```

注意，包名必须完全一致，包没有父子关系，com.apache 和 com.apache.abc 是不同的包。

### 局部变量
在方法内部定义的变量称为局部变量，局部变量作用域从变量声明处开始到对应的块结束，方法参数也是局部变量

```java
package abc;

public class Hello {
    void hi(String name) { // ①
        String s = name.toLowerCase(); // ②
        int len = s.length(); // ③
        if (len < 10) { // ④
            int p = 10 - len; // ⑤
            for (int i=0; i<10; i++) { // ⑥
                System.out.println(); // ⑦
            } // ⑧
        } // ⑨
    } // ⑩
}
```

我们观察上面的 hi() 方法代码

- 方法参数name是局部变量，它的作用域是整个方法，即①～⑩；

- 变量s的作用域是定义处到方法结束，即②～⑩；

- 变量len的作用域是定义处到方法结束，即③～⑩；

- 变量p的作用域是定义处到if块结束，即⑤～⑨；

- 变量i的作用域是for循环，即⑥～⑧。

使用局部变量时，应该尽可能把局部变量的作用域缩小，尽可能延后声明局部变量

### final
java 还提供了一个 final 修饰符，final 与访问权限不冲突，他有很多作用

用 final 修饰 class 可以阻止被继承

```java
package abc;

// 无法被继承:
public final class Hello {
    private int n = 0;
    protected void hi(int t) {
        long i = t;
    }
}
```

用final 修饰 method 可以阻止被子类覆写

```java
package abc;

public class Hello {
    // 无法被覆写:
    protected final void hi() {
    }
}
```

用 final 修饰 field 可以阻止被重新赋值

```java
package abc;

public class Hello {
    private final int n = 0;
    protected void hi() {
        this.n = 1; // error!
    }
}
```

用 final 修饰局部变量可以阻止被重新赋值

```java
package abc;

public class Hello {
    protected void hi(final int t) {
        t = 1; // error!
    }
}
```

### 最佳实践
如果不确定是否需要public，就不声明为public，即尽可能少地暴露对外的字段和方法。

把方法定义为package权限有助于测试，因为测试类和被测试类只要位于同一个package，测试代码就可以访问被测试类的package权限方法。

一个.java文件只能包含一个public类，但可以包含多个非public类。如果有public类，文件名必须和public类的名字相同。

## classpath 和 jar
在java 中，我们经常听到 classpath 这个东西，什么是 classpath

classpath 是 JVM 用到的一个环境变量，它用来指示 JVM 如何搜索 class

因为Java 是编译型语言，源码文件是.java ，而编译后的 .class 文件才是真正可以被JVM执行的字节码。因此，JVM需要知道，如果要加载一个 abc.xyz.Hello 的类，应该去哪搜索对应的Hello.class 文件。

所以，classpath就是一组目录的集合，它设置的搜索路径与操作系统相关。例如，在Windows系统上，用;分隔，带空格的目录用`""`括起来，可能长这样：

```
C:\work\project1\bin;C:\shared;"D:\My Documents\project1\bin"
```

在 linux 系统上，用 : 分隔，可能长这样

```
/usr/shared:/usr/local/bin:/home/liaoxuefeng/bin
```

现在我们假设 classpath 是.; C:\work\project1\bin;C:\shared ，当JVM在加载abc.xyz.Hello 这个类时，会依次查找：

- <当前目录>\abc\xyz\Hello.class

- C:\work\project1\bin\abc\xyz\Hello.class

- C:\shared\abc\xyz\Hello.class

注意到 . 代表当前目录，如果 JVM 在某个路径下找到了对应的 class 文件，就不在往后继续搜索。如果所有路径下都没有找到，就报错

classpath 的设定方法有两种

- 在系统环境变量中设置 classpath 环境变量，不推荐
- 在启动 JVM 时设置 classpath 变量，推荐

强烈不推荐在系统环境变量中设置 classpath ，那样会污染整个系统环境，在启动 JVM 时设置 classpath 才是推荐的做法，实际上就是给 java 命令传入 -classpath 或 -cp 参数

```
java -classpath .;C:\work\project1\bin;C:\shared abc.xyz.Hello
```

或者使用 -cp 简写

```
java -cp .;C:\work\project1\bin;C:\shared abc.xyz.Hello
```

没有设置系统环境变量，也没有传入 -cp 参数，那么 JVM 默认的 classpath 为 . ，即当前目录

```
java abc.xyz.Hello
```

上述命令告诉 JVM 只在当前目录搜索 Hello.class

IDE 中运行的 java 程序，IDE 自动传入的 -cp 参数是当前工程的 bin 目录和引入的 jar 包

通常，我们在自己编写的class中，会引用Java核心库的class，例如，String、ArrayList等。这些class应该上哪去找？

有很多“如何设置classpath”的文章会告诉你把JVM自带的rt.jar放入classpath，但事实上，根本不需要告诉JVM如何去Java核心库查找class，JVM怎么可能笨到连自己的核心库在哪都不知道？

>不要把任何Java核心库添加到classpath中！JVM根本不依赖classpath加载核心库！

更好的做法是，不要设置 classpath ！ 默认的当前目录 . 对于大多数情况都够用了

## jar 包

如果有很多.class文件，散落在各层目录中，肯定不便于管理。如果能把目录打一个包，变成一个文件，就方便多了。

jar包就是用来干这个事的，它可以把package组织的目录层级，以及各个目录下的所有文件（包括.class文件和其他文件）都打成一个jar文件，这样一来，无论是备份，还是发给客户，就简单多了。

jar包实际上就是一个zip格式的压缩文件，而jar包相当于目录。如果我们要执行一个jar包的class，就可以把jar包放到classpath中：

java -cp ./hello.jar abc.xyz.Hello
这样JVM会自动在hello.jar文件里去搜索某个类。

那么问题来了：如何创建jar包？

因为jar包就是zip包，所以，直接在资源管理器中，找到正确的目录，点击右键，在弹出的快捷菜单中选择“发送到”，“压缩(zipped)文件夹”，就制作了一个zip文件。然后，把后缀从.zip改为.jar，一个jar包就创建成功。

假设编译输出的目录结构是这样：
```
package_sample
└─ bin
   ├─ hong
   │  └─ Person.class
   │  ming
   │  └─ Person.class
   └─ mr
      └─ jun
         └─ Arrays.class
```

这里需要特别注意的是，jar包里的第一层目录，不能是bin，而应该是hong、ming、mr。如果在Windows的资源管理器中看，应该长这样：

![](\img\java学习_jar包1.jpg)

如果长这样：

![](\img\java学习_jar包2.jpg)

说明打包打得有问题，JVM仍然无法从jar包中查找正确的class，原因是hong.Person必须按hong/Person.class存放，而不是bin/hong/Person.class。

jar包还可以包含一个特殊的/META-INF/MANIFEST.MF文件，MANIFEST.MF是纯文本，可以指定Main-Class和其它信息。JVM会自动读取这个MANIFEST.MF文件，如果存在Main-Class，我们就不必在命令行指定启动的类名，而是用更方便的命令：

```java
java -jar hello.jar
```

jar包还可以包含其它jar包，这个时候，就需要在MANIFEST.MF文件里配置classpath了。

在大型项目中，不可能手动编写MANIFEST.MF文件，再手动创建zip包。Java社区提供了大量的开源构建工具，例如Maven，可以非常方便地创建jar包。

## 模块(java 9 开始才有)
从Java 9开始，JDK又引入了模块（Module）。

什么是模块？这要从Java 9之前的版本说起。

我们知道，.class文件是JVM看到的最小可执行文件，而一个大型程序需要编写很多Class，并生成一堆.class文件，很不便于管理，所以，jar文件就是class文件的容器。

在Java 9之前，一个大型Java程序会生成自己的jar文件，同时引用依赖的第三方jar文件，而JVM自带的Java标准库，实际上也是以jar文件形式存放的，这个文件叫rt.jar，一共有60多M。

如果是自己开发的程序，除了一个自己的app.jar以外，还需要一堆第三方的jar包，运行一个Java程序，一般来说，命令行写这样：

java -cp app.jar:a.jar:b.jar:c.jar com.liaoxuefeng.sample.Main
 注意：JVM自带的标准库rt.jar不要写到classpath中，写了反而会干扰JVM的正常运行。
如果漏写了某个运行时需要用到的jar，那么在运行期极有可能抛出ClassNotFoundException。

所以，jar只是用于存放class的容器，它并不关心class之间的依赖。

从Java 9开始引入的模块，主要是为了解决“依赖”这个问题。如果a.jar必须依赖另一个b.jar才能运行，那我们应该给a.jar加点说明啥的，让程序在编译和运行的时候能自动定位到b.jar，这种自带“依赖关系”的class容器就是模块。

为了表明Java模块化的决心，从Java 9开始，原有的Java标准库已经由一个单一巨大的rt.jar分拆成了几十个模块，这些模块以.jmod扩展名标识，可以在$JAVA_HOME/jmods目录下找到它们：

```java
java.base.jmod
java.compiler.jmod
java.datatransfer.jmod
java.desktop.jmod
...

```

这些.jmod文件每一个都是一个模块，模块名就是文件名。例如：模块java.base对应的文件就是java.base.jmod。模块之间的依赖关系已经被写入到模块内的module-info.class文件了。所有的模块都直接或间接地依赖java.base模块，只有java.base模块不依赖任何模块，它可以被看作是“根模块”，好比所有的类都是从Object直接或间接继承而来。

把一堆class封装为jar仅仅是一个打包的过程，而把一堆class封装为模块则不但需要打包，还需要写入依赖关系，并且还可以包含二进制代码（通常是JNI扩展）。此外，模块支持多版本，即在同一个模块中可以为不同的JVM提供不同的版本。

编写模块
那么，我们应该如何编写模块呢？还是以具体的例子来说。首先，创建模块和原有的创建Java项目是完全一样的，以oop-module工程为例，它的目录结构如下：

```
oop-module
├── bin
├── build.sh
└── src
    ├── com
    │   └── itranswarp
    │       └── sample
    │           ├── Greeting.java
    │           └── Main.java
    └── module-info.java
```    

其中，bin目录存放编译后的class文件，src目录存放源码，按包名的目录结构存放，仅仅在src目录下多了一个module-info.java这个文件，这就是模块的描述文件。在这个模块中，它长这样：

```java
module hello.world {
	requires java.base; // 可不写，任何模块都会自动引入java.base
	requires java.xml;
}
```

其中，module是关键字，后面的hello.world是模块的名称，它的命名规范与包一致。花括号的requires xxx;表示这个模块需要引用的其他模块名。除了java.base可以被自动引入外，这里我们引入了一个java.xml的模块。

当我们使用模块声明了依赖关系后，才能使用引入的模块。例如，Main.java代码如下：

```java
package com.itranswarp.sample;
```

// 必须引入java.xml模块后才能使用其中的类:

```java
import javax.xml.XMLConstants;

public class Main {
	public static void main(String[] args) {
		Greeting g = new Greeting();
		System.out.println(g.hello(XMLConstants.XML_NS_PREFIX));
	}
}
```

如果把requires java.xml;从module-info.java中去掉，编译将报错。可见，模块的重要作用就是声明依赖关系。

下面，我们用JDK提供的命令行工具来编译并创建模块。

首先，我们把工作目录切换到oop-module，在当前目录下编译所有的.java文件，并存放到bin目录下，命令如下：

```
$ javac -d bin src/module-info.java src/com/itranswarp/sample/*.java

```

如果编译成功，现在项目结构如下：

```
oop-module
├── bin
│   ├── com
│   │   └── itranswarp
│   │       └── sample
│   │           ├── Greeting.class
│   │           └── Main.class
│   └── module-info.class
└── src
    ├── com
    │   └── itranswarp
    │       └── sample
    │           ├── Greeting.java
    │           └── Main.java
    └── module-info.java
```    

注意到src目录下的module-info.java被编译到bin目录下的module-info.class。

下一步，我们需要把bin目录下的所有class文件先打包成jar，在打包的时候，注意传入--main-class参数，让这个jar包能自己定位main方法所在的类：

```
$ jar --create --file hello.jar --main-class com.itranswarp.sample.Main -C bin .
```

现在我们就在当前目录下得到了hello.jar这个jar包，它和普通jar包并无区别，可以直接使用命令java -jar hello.jar来运行它。但是我们的目标是创建模块，所以，继续使用JDK自带的jmod命令把一个jar包转换成模块：

```
$ jmod create --class-path hello.jar hello.jmod
```

于是，在当前目录下我们又得到了hello.jmod这个模块文件，这就是最后打包出来的传说中的模块！

### 运行模块
要运行一个jar，我们使用java -jar xxx.jar命令。要运行一个模块，我们只需要指定模块名。试试：

```
$ java --module-path hello.jmod --module hello.world
```

结果是一个错误：

```
Error occurred during initialization of boot layer
java.lang.module.FindException: JMOD format not supported at execution time: hello.jmod
```

原因是.jmod不能被放入--module-path中。换成.jar就没问题了：

```
$ java --module-path hello.jar --module hello.world
Hello, xml!
```

那我们辛辛苦苦创建的hello.jmod有什么用？答案是我们可以用它来打包JRE。

### 打包JRE
前面讲了，为了支持模块化，Java 9首先带头把自己的一个巨大无比的rt.jar拆成了几十个.jmod模块，原因就是，运行Java程序的时候，实际上我们用到的JDK模块，并没有那么多。不需要的模块，完全可以删除。

过去发布一个Java应用程序，要运行它，必须下载一个完整的JRE，再运行jar包。而完整的JRE块头很大，有100多M。怎么给JRE瘦身呢？

现在，JRE自身的标准库已经分拆成了模块，只需要带上程序用到的模块，其他的模块就可以被裁剪掉。怎么裁剪JRE呢？并不是说把系统安装的JRE给删掉部分模块，而是“复制”一份JRE，但只带上用到的模块。为此，JDK提供了jlink命令来干这件事。命令如下：

```
$ jlink --module-path hello.jmod --add-modules java.base,java.xml,hello.world --output jre/
```

我们在--module-path参数指定了我们自己的模块hello.jmod，然后，在--add-modules参数中指定了我们用到的3个模块java.base、java.xml和hello.world，用,分隔。最后，在--output参数指定输出目录。

现在，在当前目录下，我们可以找到jre目录，这是一个完整的并且带有我们自己hello.jmod模块的JRE。试试直接运行这个JRE：

```
$ jre/bin/java --module hello.world
Hello, xml!
```

要分发我们自己的Java应用程序，只需要把这个jre目录打个包给对方发过去，对方直接运行上述命令即可，既不用下载安装JDK，也不用知道如何配置我们自己的模块，极大地方便了分发和部署。

### 访问权限
前面我们讲过，Java的class访问权限分为public、protected、private和默认的包访问权限。引入模块后，这些访问权限的规则就要稍微做些调整。

确切地说，class的这些访问权限只在一个模块内有效，模块和模块之间，例如，a模块要访问b模块的某个class，必要条件是b模块明确地导出了可以访问的包。

举个例子：我们编写的模块hello.world用到了模块java.xml的一个类javax.xml.XMLConstants，我们之所以能直接使用这个类，是因为模块java.xml的module-info.java中声明了若干导出：

```java
module java.xml {
    exports java.xml;
    exports javax.xml.catalog;
    exports javax.xml.datatype;
    ...
}
```

只有它声明的导出的包，外部代码才被允许访问。换句话说，如果外部代码想要访问我们的hello.world模块中的com.itranswarp.sample.Greeting类，我们必须将其导出：

```java
module hello.world {
    exports com.itranswarp.sample;

    requires java.base;
	requires java.xml;
}
```

因此，模块进一步隔离了代码的访问权限。

# Java核心类(java.lang)

## String
在java 中，String是一个引用类型，它本身也是一个 class。但是，java 编译器对 String 有特殊处理，即可以直接用 "..."来表示一个字符串：

```java
String s1 = "Hello!";
```

实际上字符串在 String 内部提供一个 char[] 数组表示的，因此，按下面的写法也是可以的

```
String s2 = new String(new char[] {'H', 'e', 'l', 'l', 'o', '!'});
```

因为 String 太常用了，所以 java提供了 "..." 这种字符串字面量表示方法

Java 字符串的一个重要的特点就是字符串不可变，这种不可变特性是通过内部的 private final char[] 字段，以及没有任何修改的 char[] 的方法实现的

例
```java
public class Main {
    public static void main(String[] args) {
        String s = "Hello";
        System.out.println(s);
        s = s.toUpperCase();
        System.out.println(s);
    }
}
```

### 字符串比较
当我们想要比较两个字符串是否相同时，要特别注意，我们实际上是想比较字符串的内容是否相同，必须使用 equals() 方法而不能用 ==

例：
```java
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "hello";
        System.out.println(s1 == s2);
        System.out.println(s1.equals(s2));
    }
}
```

表面上看，两个字符串用 == 和 equals() 比较都为 true ，但实际上那只是 java 编译器在编译期，会自动把所有相同的字符串当做一个对象放入常量池，自然 s1 和 s2的引用就是相同的

所以，这种 == 比较返回 true 纯属巧合，换一种写法，== 比较就会失败

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "HELLO".toLowerCase();
        System.out.println(s1 == s2);
        System.out.println(s1.equals(s2));
    }
}
```

结论：两个字符串比较，必须总是使用 equals() 方法

要忽略大小写比较，使用 equalsIgnoreCase() 方法

String 类还提供了多种方法来搜索子串，提取子串。常用的方法有：

```java
// 是否包含子串:
"Hello".contains("ll"); // true
```

注意到 contains() 方法的参数是 CharSequence 而不是 String ，因为 CharSequence 是 String 的父类

搜索字串例：

```java
"Hello".indexOf("l"); // 2
"Hello".lastIndexOf("l"); // 3
"Hello".startsWith("He"); // true
"Hello".endsWith("lo"); // true
```

提取子串的例子

```java
"Hello".substring(2); // "llo"
"Hello".substring(2, 4); "ll"
```

>注意索引号是从 0 开始的

### 去除首尾空白字符
使用 trim() 方法可以移除字符串首尾空白字符，空白字符包括空格，\t,\r,\n：

```
"  \tHello\r\n ".trim(); // "Hello"
```

>注意：trim() 并没有改变字符串的内容，而是返回了一个新字符串

另一个 strip() 方法也可以移除字符首尾空白字符。它和 trim() 不同的是，类似中文的空格字符 \u3000 也会被移除

```java
"\u3000Hello\u3000".strip(); // "Hello"
" Hello ".stripLeading(); // "Hello "
" Hello ".stripTrailing(); // " Hello"
```

String 还提供了 isEmpty() 和 isBlank() 来判断字符串是否为空和空白字符串

```java
"".isEmpty(); // true，因为字符串长度为0
"  ".isEmpty(); // false，因为字符串长度不为0
"  \n".isBlank(); // true，因为只包含空白字符
" Hello ".isBlank(); // false，因为包含非空白字符
```

### 替换子串
要在字符串中替换子串，有两种方法，一种是根据字符或字符串替换

```java
String s = "hello";
s.replace('l', 'w'); // "hewwo"，所有字符'l'被替换为'w'
s.replace("ll", "~~"); // "he~~o"，所有子串"ll"被替换为"~~"
```

另一种是通过正则表达式替换

```java
String s = "A,,B;C ,D";
s.replaceAll("[\\,\\;\\s]+", ","); // "A,B,C,D"
```

上面的代码通过正则表达式，把匹配的子串统一替换为 "，"

### 分割字符串
要分割字符串，使用 split() 方法，并且传入的也是正则表达式

```java
String s = "A,B,C,D";
String[] ss = s.split("\\,"); // {"A", "B", "C", "D"}
```

### 拼接字符串
拼接字符串使用静态方法join()，它用指定的字符串连接字符串数组：

```java
String[] arr = {"A", "B", "C"};
String s = String.join("***", arr); // "A***B***C"
```

### 类型转换
要把任意基本类型或引用类型转换为字符串，可以使用静态方法 vlaeOf() 这是一个重载方法，编译器会根据参数自动选择合适的方法

```java
String.valueOf(123); // "123"
String.valueOf(45.67); // "45.67"
String.valueOf(true); // "true"
String.valueOf(new Object()); // 类似java.lang.Object@636be97c
```

要把字符串转换为其他类型，就需要根据情况，例如，把字符串转换为 int 类型

```java
int n1 = Integer.parseInt("123"); // 123
int n2 = Integer.parseInt("ff", 16); // 按十六进制转换，255
```

把字符串转换为 boolean 类型

```java
boolean b1 = Boolean.parseBoolean("true"); // true
boolean b2 = Boolean.parseBoolean("FALSE"); // false
```

要特别注意，Integer 有个 getInteger(String) 方法，它不是将字符串转换为 int，而是把该字符串对应的系统变量转换为 Integer

```java
Integer.getInteger("java.version"); // 版本号，11
```

### 转换为 char[]
String 和 char[] 类型可以互相转换，方法是：

```java
char[] cs = "Hello".toCharArray(); // String -> char[]
String s = new String(cs); // char[] -> String
```

如果修改了 char[] 数组，String 并不会改变

```java
public class Main {
    public static void main(String[] args) {
        char[] cs = "Hello".toCharArray();
        String s = new String(cs);
        System.out.println(s);
        cs[0] = 'X';
        System.out.println(s);
    }
}
```

这是因为通过 new Sting(char[]) 创建新的 String 实例时，它并不会直接引用传入的 char[] 数组，而是会复制一份，所以，修改外部的 char[] 数组不会影响 String 实例内部的 char[] 数组，因为这是两个不同的数组

从 String 的不变性设计可以看出，如果传入的对象有可能改变，我们需要复制而不是直接引用

例，下面代码设计了一个 Score 类保存一组学生的成绩

```java
public class Main {
    public static void main(String[] args) {
        int[] scores = new int[] { 88, 77, 51, 66 };
        Score s = new Score(scores);
        s.printScores();
        scores[2] = 99;
        s.printScores();
    }
}

class Score {
    private int[] scores;
    public Score(int[] scores) {
        this.scores = scores;
    }

    public void printScores() {
        System.out.println(Arrays.toString(scores));
    }
}
```

观察两次输出，由于 Score 内部直接引用了外部传入的 int[] 数组，者会造成外部代码对 int[] 数组的修改，影响到 Score 类的字段。如果外部代码不可信。这就会造成安全隐患

请修复 Score 的构造方法，使得外部代码对数组的修改不影响 Score 实例的 int[] 字段

### 字符编码
在早期的计算机系统中，为了给字符编码，美国国家标准学会（American National Standard Institute：ANSI）制定了一套英文字母、数字和常用符号的编码，它占用一个字节，编码范围从0到127，最高位始终为0，称为ASCII编码。例如，字符'A'的编码是0x41，字符'1'的编码是0x31。

如果要把汉字也纳入计算机编码，很显然一个字节是不够的。GB2312标准使用两个字节表示一个汉字，其中第一个字节的最高位始终为1，以便和ASCII编码区分开。例如，汉字'中'的GB2312编码是0xd6d0。

类似的，日文有Shift_JIS编码，韩文有EUC-KR编码，这些编码因为标准不统一，同时使用，就会产生冲突。

为了统一全球所有语言的编码，全球统一码联盟发布了Unicode编码，它把世界上主要语言都纳入同一个编码，这样，中文、日文、韩文和其他语言就不会冲突。

Unicode编码需要两个或者更多字节表示，我们可以比较中英文字符在ASCII、GB2312和Unicode的编码：

英文字符'A'的ASCII编码和Unicode编码：

```
         ┌────┐
ASCII:   │ 41 │
         └────┘
         ┌────┬────┐
Unicode: │ 00 │ 41 │
         └────┴────┘
```

英文字符的Unicode编码就是简单地在前面添加一个00字节。

中文字符'中'的GB2312编码和Unicode编码：

```
         ┌────┬────┐
GB2312:  │ d6 │ d0 │
         └────┴────┘
         ┌────┬────┐
Unicode: │ 4e │ 2d │
         └────┴────┘
```

那我们经常使用的UTF-8又是什么编码呢？因为英文字符的Unicode编码高字节总是00，包含大量英文的文本会浪费空间，所以，出现了UTF-8编码，它是一种变长编码，用来把固定长度的Unicode编码变成1～4字节的变长编码。通过UTF-8编码，英文字符'A'的UTF-8编码变为0x41，正好和ASCII码一致，而中文'中'的UTF-8编码为3字节0xe4b8ad。

UTF-8编码的另一个好处是容错能力强。如果传输过程中某些字符出错，不会影响后续字符，因为UTF-8编码依靠高字节位来确定一个字符究竟是几个字节，它经常用来作为传输编码。

在Java中，char类型实际上就是两个字节的Unicode编码。如果我们要手动把字符串转换成其他编码，可以这样做：

```java
byte[] b1 = "Hello".getBytes(); // 按ISO8859-1编码转换，不推荐
byte[] b2 = "Hello".getBytes("UTF-8"); // 按UTF-8编码转换
byte[] b2 = "Hello".getBytes("GBK"); // 按GBK编码转换
byte[] b3 = "Hello".getBytes(StandardCharsets.UTF_8); // 按UTF-8编码转换
```

>注意：转换编码后，就不再是char类型，而是byte类型表示的数组。

如果要把已知编码的byte[]转换为String，可以这样做：

```java
byte[] b = ...
String s1 = new String(b, "GBK"); // 按GBK转换
String s2 = new String(b, StandardCharsets.UTF_8); // 按UTF-8转换
```

始终牢记：Java的String和char在内存中总是以Unicode编码表示。

### 延伸阅读
对于不同版本的JDK，String类在内存中有不同的优化方式。具体来说，早期JDK版本的String总是以char[]存储，它的定义如下：

```java
public final class String {
    private final char[] value;
    private final int offset;
    private final int count;
}
```

而较新的JDK版本的String则以byte[]存储：如果String仅包含ASCII字符，则每个byte存储一个字符，否则，每两个byte存储一个字符，这样做的目的是为了节省内存，因为大量的长度较短的String通常仅包含ASCII字符：

```java
public final class String {
    private final byte[] value;
    private final byte coder; // 0 = LATIN1, 1 = UTF16
```   

对于使用者来说，String内部的优化不影响任何已有代码，因为它的public方法签名是不变的。

## StringBuilder
Java 编译器对 String 做了特殊处理，使得我们可以直接用 + 拼接字符串

考察下面的循环代码

```java
String s = "";
for (int i = 0; i < 1000; i++) {
    s = s + "," + i;
}
```

虽然可以直接拼接字符串，但是，在循环中，每次循环都会创建新的字符串对象，然后扔掉旧的字符串。这样，绝大部分字符串都是临时对象，不但浪费内存，还会影响GC效率

为了能高效凭借字符串，Java 标准库提供了 StringBuilder，它是一个可变对象，可以预分配缓冲区，这样，网 StringBulider 中新增字符时，不会创建新的临时对象

```java
StringBuilder sb = new StringBuilder(1024);
for (int i = 0; i < 1000; i++) {
    sb.append(',');
    sb.append(i);
}
String s = sb.toString();
```

StringBuilder 还可以进行链式操作

```java
public class Main {
    public static void main(String[] args) {
        var sb = new StringBuilder(1024);
        sb.append("Mr ")
          .append("Bob")
          .append("!")
          .insert(0, "Hello, ");
        System.out.println(sb.toString());
    }
}
```

如果我们查看 StringBulider 的源码，可以发现，进行链式操作的关键是，定义 append() 方法会返回 this，这样，就可以不断调用自身的其他方法

仿照 StringBuilder，我们也可以设计支持链式操作的类，例如，一个可以不断增加的计数器

```java
public class Main {
    public static void main(String[] args) {
        Adder adder = new Adder();
        adder.add(3)
             .add(5)
             .inc()
             .add(10);
        System.out.println(adder.value());
    }
}

class Adder {
    private int sum = 0;

    public Adder add(int n) {
        sum += n;
        return this;
    }

    public Adder inc() {
        sum ++;
        return this;
    }

    public int value() {
        return sum;
    }
}
```

>注意：对于普通的字符串 + 操作，并不需要我们将其改写为 StringBuilder ，因为 Java 编译器在编译时就自动把多个连续的 + 操作编码为 StringConcatFactory 的操作。在运行期，StringConcatFactory 会自动把字符串连接操作有华为数组赋值或者 StringBuilder 操作。

你可能还听说过 StringBuffer ，这是 Java 早期的一个 StringBuilder 的线程安全版本，他通过同步来保证多个线程操作 StringBuffer 也是安全的，但是同步会带来执行速度的下降

StringBuilder 和 StringBuffer 接口完全相同，现在完全没有必要使用 StringBuffer

## StringJoiner
要高效拼接字符串，应该使用 StringBulider

很多时候，我们拼接的字符串像这样：

```java
public class Main {
    public static void main(String[] args) {
        String[] names = {"Bob", "Alice", "Grace"};
        var sb = new StringBuilder();
        sb.append("Hello ");
        for (String name : names) {
            sb.append(name).append(", ");
        }
        // 注意去掉最后的", ":
        sb.delete(sb.length() - 2, sb.length());
        sb.append("!");
        System.out.println(sb.toString());
    }
}
```

类似用分隔符拼接数组的需求很常见，所以 Java 标准库还提供了一个 StringJoiner 来干这个事

```java
public class Main {
    public static void main(String[] args) {
        String[] names = {"Bob", "Alice", "Grace"};
        var sj = new StringJoiner(", ");
        for (String name : names) {
            sj.add(name);
        }
        System.out.println(sj.toString());
    }
}
```

用StringJoiner的结果少了前面的"Hello "和结尾的"!"！遇到这种情况，需要给StringJoiner指定“开头”和“结尾”：

```java
public class Main {
    public static void main(String[] args) {
        String[] names = {"Bob", "Alice", "Grace"};
        var sj = new StringJoiner(", ", "Hello ", "!");
        for (String name : names) {
            sj.add(name);
        }
        System.out.println(sj.toString());
    }
}
```

那么 StringJoiner 内部是如何拼接字符串的呢？，如果查看源码可以发现，StringJoiner 内部实际上就是使用了 StringBulider ，所以拼接效率和 StringBulider 几乎是一模一样的。

### String.join()
String 还提供了一个静态方法 join() ，这个方法在内部使用了 StringJoiner 来拼接字符串，在不需要指定"开头"和"结尾"的时候，用 String.join() 更方便：

```java
String[] names = {"Bob", "Alice", "Grace"};
var s = String.join(", ", names);
```

## 包装类型

我们已经知道，Java 的数据类型分两种

- 基本类型：byte，short，int，long，boolean，float，double，char
- 引用类型：所有 class 和 interface类型

引用类型可以赋值为 null ，表示空，但是基本类型不能赋值为 null

```java
String s = null;
int n = null; // compile error!
```

那么，如何把一个基本类型视为对象？(引用类型)

比如，想要把 int 基本类型变成一个引用类型，我们可以定义一个 Integer 类，他只包含一个实例字段 int ，这样，Integer 类就可以视为 int 的包装类 (Wrapper Class)

```java
public class Integer {
    private int value;

    public Integer(int value) {
        this.value = value;
    }

    public int intValue() {
        return this.value;
    }
}
```

定义好了 Interger 类，我们就可以把int 和 Integer 互相转换

```java
Integer n = null;
Integer n2 = new Integer(99);
int n3 = n2.intValue();
```

实际上，因为包装类型非常有用，Java 核心库为每种基本类型都提供了对应的包装类型


基本类型  |	对应的引用类型
---------|--------------
boolean	 |  java.lang.Boolean
byte	 |  java.lang.Byte
short	 |  java.lang.Short
int	     |  java.lang.Integer
long	 |  java.lang.Long
float	 |  java.lang.Float
double	 |  java.lang.Double
char	 |  java.lang.Character

我们可以直接使用，并不需要自己去定义

```java
public class Main {
    public static void main(String[] args) {
        int i = 100;
        // 通过new操作符创建Integer实例(不推荐使用,会有编译警告):
        Integer n1 = new Integer(i);
        // 通过静态方法valueOf(int)创建Integer实例:
        Integer n2 = Integer.valueOf(i);
        // 通过静态方法valueOf(String)创建Integer实例:
        Integer n3 = Integer.valueOf("100");
        System.out.println(n3.intValue());
    }
}
```
### Auto Boxing
因为 int 和 Integer 可以互相转换

```java
int i = 100;
Integer n = Integer.valueOf(i);
int x = n.intValue();
```

所以，Java 编译器可以帮助我们自动在 int 和 Integer 之间转型

```java
Integer n = 100; // 编译器自动使用Integer.valueOf(int)
int x = n; // 编译器自动使用Integer.intValue()
```

这种直接把 int 变为 Integer 的赋值写法，成为自动装箱(Auto Boxing)，反过来，把 Inreger 变为 int 的赋值写法，成为自动拆箱(Auto Unboxing)

注意：自动装箱和自从拆箱只发生在编译，目的是为了少些代码

装箱和拆箱会影响代码的执行效率，因为编译后的 class 代码是严格区分基本类型和引用类型的，并且，自动拆箱执行时可能会报 NullPointerException：

```java
public class Main {
    public static void main(String[] args) {
        Integer n = null;
        int i = n;
    }
}
```

### 不变类
所有的包装类都是不变类。我们查看Integer 的源码可知，它的核心代码如下：

```java
public final class Integer {
    private final int value;
}
```

因此，一旦创建了 Integer 对象，该对象就是不变的

对两个 Integer 实例进行比较要特别注意：绝对不能用 == 比较，因为 Integer 是引用类型，必须使用 equals() 比较

```java
public class Main {
    public static void main(String[] args) {
        Integer x = 127;
        Integer y = 127;
        Integer m = 99999;
        Integer n = 99999;
        System.out.println("x == y: " + (x==y)); // true
        System.out.println("m == n: " + (m==n)); // false
        System.out.println("x.equals(y): " + x.equals(y)); // true
        System.out.println("m.equals(n): " + m.equals(n)); // true
    }
}
```

仔细观察结果可以发现，== 比较，较小的两个相同的 Integer 返回 true，较大的两个相同的Integer 返回 false，这是因为 Integer 是不变类，编译器把 Integer x = 127;自动变为Integer x = Integer.valueOf(127); ，为了节省内存，Integer.valueOf() 对于较小的数，始终返回相同的实例，因此，== 比较“恰好”为 true ，但我们绝不能因为Java 标准库的Integer 内部有缓存优化就用 == 比较，必须用 equals() 方法比较两个 Integer 。

>按照语义编程，而不是针对特定的底层实现去"优化"

因为  Integer.valueof() 可能始终返回同一个 Integer 实例，因此，在我们自己创建 Integer 的时候，以下两种方法

- 方法1：Integer n = new Integer(100)；
- 方法2：Integer n = Integer.valueOf(100)；

方法2更好，因为方法1总是在创建新的 Integer 实例，方法2把内部优化留给 Integer 的实现者去做，即在当前版本没有优化，也有可能在下一个版本进行优化

我们把能创建"新对象的静态方法称为静态工厂方法。Integer.valueOf() 就是静态工厂方法，他尽可能地返回缓存的实例以节省内存

>创建新对象时，优先选用静态工厂方法而不是 new 操作符

如果我们考察Byte.valueOf()方法的源码，可以看到，标准库返回的Byte实例全部是缓存实例，但调用者并不关心静态工厂方法以何种方式创建新实例还是直接返回缓存的实例。

### 进制转换
Integer 类本身还提供了大量方法，例如，最常用的静态方法 parseInt() 可以把字符串解析成一个整数

```java
int x1 = Integer.parseInt("100"); // 100
int x2 = Integer.parseInt("100", 16); // 256,因为按16进制解析
```

Integer 还可以把整数格式化为指定进制的字符串

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Integer.toString(100)); // "100",表示为10进制
        System.out.println(Integer.toString(100, 36)); // "2s",表示为36进制
        System.out.println(Integer.toHexString(100)); // "64",表示为16进制
        System.out.println(Integer.toOctalString(100)); // "144",表示为8进制
        System.out.println(Integer.toBinaryString(100)); // "1100100",表示为2进制
    }
}
```

注意：上述方法的输出都是 String ，在计算机内存中，只用二进制表示，不存在十进制或十六进制的表示方法。int n = 100在内存中总是以4字节的二进制表示：

```
┌────────┬────────┬────────┬────────┐
│00000000│00000000│00000000│01100100│
└────────┴────────┴────────┴────────┘
```

我们经常使用的 System.out.println(n); 是依靠核心库自动把整数格式化为10进制输出并显示在屏幕上，使用 Integer.toHexString(n) 则通过核心库自动把整数格式化为16进制。

这里我们注意到程序设计的一个重要原则：数据的存储和显示要分离。

java 的包装类型还定义了一些有用的静态变量

```java
// boolean只有两个值true/false，其包装类型只需要引用Boolean提供的静态字段:
Boolean t = Boolean.TRUE;
Boolean f = Boolean.FALSE;
// int可表示的最大/最小值:
int max = Integer.MAX_VALUE; // 2147483647
int min = Integer.MIN_VALUE; // -2147483648
// long类型占用的bit和byte数量:
int sizeOfLong = Long.SIZE; // 64 (bits)
int bytesOfLong = Long.BYTES; // 8 (bytes)
```

最后，所有的整数和浮点数的包装类型都继承自 Number，因此，可以非常方便的直接通过包装类型获取各种基本类型

```java
// 向上转型为Number:
Number num = new Integer(999);
// 获取byte, int, long, float, double:
byte b = num.byteValue();
int n = num.intValue();
long ln = num.longValue();
float f = num.floatValue();
double d = num.doubleValue();
```

### 处理无符号整型
在Java 中，并没有无符号整型(Unsigned)的基本数据类型。byte，short，int和long都是带符号整型，最高位是符号位。而C语言则提供了CPU支持的全部数据类型，包括无符号类型。无符号整型和有符号整型的转换在 Java中就需要借助包装类型的静态方法完成。

例如，byte是有符号整型，范围是-128~+127，但如果把byte看作无符号整型，它的范围就是0~255。我们把一个负的byte按无符号整型转换为int：

```java
public class Main {
    public static void main(String[] args) {
        byte x = -1;
        byte y = 127;
        System.out.println(Byte.toUnsignedInt(x)); // 255
        System.out.println(Byte.toUnsignedInt(y)); // 127
    }
}
```
因为byte的-1的二进制表示是11111111，以无符号整型转换后的int就是255。

类似的，可以把一个short按unsigned转换为int，把一个int按unsigned转换为long。

## JavaBean
在Java 中，有很多 class 的定义都符合这样的规范：

- 若干 private 实例字段
- 通过 public 方法来读写实例字段

例
```java
public class Person {
    private String name;
    private int age;

    public String getName() { return this.name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return this.age; }
    public void setAge(int age) { this.age = age; }
}
```

如果读写方法符合以下这种命名规范：

```java
// 读方法:
public Type getXyz()
// 写方法:
public void setXyz(Type value)
```

那么这种 class 被称为 JavaBean

上面的字段是 xyz ，那么读写方法名分别以 get 和 set

boolean 字段比较特殊，它的读方法一般命名为 isXyz()：

```java
// 读方法:
public boolean isChild()
// 写方法:
public void setChild(boolean value)
```

我们通常吧一组对应的读方法(getter)和写方法(setter)称为属性(property)。例如，name 属性：

- 对应的读方法是 String getName()
- 对应的写方法是 setName(String)

只有 getter 的属性称为只读属性 (read-only)，例如，定义一个 age 的只读属性：

- 对应的读方法是 int getAge()
- 无对应的写方法 intAge(int)

类似的，只有 setter 的属性陈文革只写属性 (write-only)

很明显，只读属性很常见，只写属性不常见

属性只需要定义 getter 和 setter 方法，不一定需要对应的字段，例如，child 只读属性定义如下

```java
public class Person {
    private String name;
    private int age;

    public String getName() { return this.name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return this.age; }
    public void setAge(int age) { this.age = age; }

    public boolean isChild() {
        return age <= 6;
    }
}
```

可以看出，getter 和 setter 也是一种数据封装的方法

### javaBean的作用
javaBean 主要用来传递数据，即吧一组数据组合称一个 JavaBean 便于传输。此外，JavaBean可以方便地被 IDE 工具分析，生成读写属性的代码，主要用在图形界面的可视化设计中。

通过 IDE ，可以快速生成 getter 和 setter 。例如，在 Eclipse中，先输入以下代码。

```java
public class Person {
    private String name;
    private int age;
}
```

然后，点击右键，在弹出的菜单中选择"Source"，"Generate Getters and Setters"，在弹出的对话框中选中需要生成 getter 和 setter 方法的字段，点击确定即可由 IDE 自动完成所有方法代码。

### 枚举 JavaBean 属性
要枚举一个 JavaBean 的所有属性，可以直接使用 Java 核心库提供的 Introspector：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        BeanInfo info = Introspector.getBeanInfo(Person.class);
        for (PropertyDescriptor pd : info.getPropertyDescriptors()) {
            System.out.println(pd.getName());
            System.out.println("  " + pd.getReadMethod());
            System.out.println("  " + pd.getWriteMethod());
        }
    }
}

class Person {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

运行上述代码，可以列出所有的属性，以及对应的读写方法，注意 class 属性是从 Object 继承的 getClass() 方法带来的


## 枚举类
Java 中，我们可以通过 static final 来定义常量，例如，我们希望定义周一到周日这七个常量，可以用7个不同的 int 表示

```java
public class Weekday {
    public static final int SUN = 0;
    public static final int MON = 1;
    public static final int TUE = 2;
    public static final int WED = 3;
    public static final int THU = 4;
    public static final int FRI = 5;
    public static final int SAT = 6;
}
```

使用常量的时候，可以这么引用

```java
if (day == Weekday.SAT || day == Weekday.SUN) {
    // TODO: work at home
}
```

也可以把常量定义为字符串类型，例如，定义三种颜色的常量

```java
public class Color {
    public static final String RED = "r";
    public static final String GREEN = "g";
    public static final String BLUE = "b";
}
```

������������������，可以这么引用：

```java
String color = ...
if (Color.RED.equals(color)) {
    // TODO:
}
```

无论是 int 常量 还是 String 常量，使用这些常量来表示一组枚举值的时候，有一个严重的问题是，编译器无法检查每个值的合理性

```java
if (weekday == 6 || weekday == 7) {
    if (tasks == Weekday.MON) {
        // TODO:
    }
}
```

上述代码均不会报错，但存在两个问题

- 注意到 Weekday 定义的常量范围是 0-6 ，并不包括 7 ，编译器无法检查不在枚举中的 int 值
- 定义的常量仍可与其他变量比较，但其用途并非是枚举星期值

### enum
为了让编译器能自动检查某个值在枚举的集合内，并且，不同用途的枚举需要不同的类型来标记，不能混用，我们可以使用 enum 来定义枚举类

```java
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        if (day == Weekday.SAT || day == Weekday.SUN) {
            System.out.println("Work at home!");
        } else {
            System.out.println("Work at office!");
        }
    }
}

enum Weekday {
    SUN, MON, TUE, WED, THU, FRI, SAT;
}
```

注意到定义枚举类是通过关键字 enum 实现的，我们只需依次列出枚举的常量名

和 int 定义的常量相比，使用 enum 定义枚举有如下好处

首先，enum 常量本身带有类型信息，即 Weekday.SUM 类型是 Weekday ，编译器会自动检查出类型错误。例如，下面的语句不可能编译通过

```java
int day = 1;
if (day == Weekday.SUN) { // Compile error: bad operand types for binary operator '=='
}
```

其次，不可能引用到非枚举的值，因为无法通过编译

最后，不同类型的枚举不能互相比较或者赋值，因为类型不符，例如不能给一个 Weekday 枚举类型的变量赋值为 Color 枚举类型的值

```java
Weekday x = Weekday.SUN; // ok!
Weekday y = Color.RED; // Compile error: incompatible types
```

这就使得编译器可以再编译期自动检查出所有可能的潜在错误

### enum的比较
使用 enum 定义的枚举类是一种引用类型，引用类型的比较，要使用 equals() 方法，如果使用 == 比较，它比较的是两个引用类型的变量是否是同一个对象。引用类型的比较，要始终使用 equals() 方法，但 enum 类型可以例外

这是因为 enum 类型的每个常量在 JVM 中只有唯一的一个实例，所以可以直接用 == 比较：

```java
if (day == Weekday.FRI) { // ok!
}
if (day.equals(Weekday.SUN)) { // ok, but more code!
}
```

### enum类型
通过 enum 定义的枚举类，和其他的 class 有什么区别？

没有任何区别，enum 定义的类就是 class ，只不过它有以下几个特点

- 定义的enum类型总是继承自java.lang.Enum，且无法被继承；
- 只能定义出enum的实例，而无法通过new操作符创建enum的实例；
- 定义的每个实例都是引用类型的唯一实例；
- 可以将enum类型用于switch语句。

例如，我们定义的 Color 枚举类

```java
public enum Color {
    RED, GREEN, BLUE;
}
```

编译器编译出的 class 大概长这样

```java
public final class Color extends Enum { // 继承自Enum，标记为final class
    // 每个实例均为全局唯一:
    public static final Color RED = new Color();
    public static final Color GREEN = new Color();
    public static final Color BLUE = new Color();
    // private构造方法，确保外部无法调用new操作符:
    private Color() {}
}
```

所以，变异后的 enum 类和普通 class 并没有仍和区别，但是我们自己无法按定义普通class 那样来定义 enum，必须使用 enum 关键字，这是 Java 语法规定的

因为 enum 是一个 class，每个枚举的值都是 class 实例，因此，这些实例有一些方法：

- name()
    
    返回常量名，例如：
    ```java
    String s = Weekday.SUN.name(); // "SUN"
    ```

- ordinal()
    
    返回定义的常量的顺序，从 0 开始计数，例如
    ```java
    int n = Weekday.MON.ordinal(); // 1
    ```

改变枚举常量定义跌顺序就会导致 ordinal()返回值发生变化，

例如
```java
public enum Weekday {
    SUN, MON, TUE, WED, THU, FRI, SAT;
}
```
和
```java
public enum Weekday {
    MON, TUE, WED, THU, FRI, SAT, SUN;
}
```

的ordinal 就是不同的。如果在代码中编写了类似 if(x.ordinal()==1) 这样的语句，就要保证 enum 的枚举顺序不能变，新增的常量必须放在最后

Weekday 的枚举查那个量如果要和 int 转换，使用 ordinal() 不是非常方便？比如这样写:

```java
String task = Weekday.MON.ordinal() + "/ppt";
saveToFile(task);
```

但是，如果不小心修改了枚举的顺序，编译器是无法检查出这种逻辑错误的，要编写健壮的代码，就不要依靠 ordinal() 的返回值。因为 enum 本身是 class，所以我们可以定义 private 的构造方法，并且，给每个枚举常量添加字段：

```java
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        if (day.dayValue == 6 || day.dayValue == 0) {
            System.out.println("Work at home!");
        } else {
            System.out.println("Work at office!");
        }
    }
}

enum Weekday {
    MON(1), TUE(2), WED(3), THU(4), FRI(5), SAT(6), SUN(0);

    public final int dayValue;

    private Weekday(int dayValue) {
        this.dayValue = dayValue;
    }
}
```

这样就无需担心顺序的变换，新增枚举常量时，也需要指定一个 int 值

> 注意：枚举类的字段也可以是非final类型，即可以在运行期修改，但是不推荐这样做！

默认情况下，对枚举畅想调用 toString() 会返回和 name() 一样的字符串，但是，toString() 可以被覆写，而 name() 则不行，我们可以给 Weekday 添加 toString() 方法

```java
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        if (day.dayValue == 6 || day.dayValue == 0) {
            System.out.println("Today is " + day + ". Work at home!");
        } else {
            System.out.println("Today is " + day + ". Work at office!");
        }
    }
}

enum Weekday {
    MON(1, "星期一"), TUE(2, "星期二"), WED(3, "星期三"), THU(4, "星期四"), FRI(5, "星期五"), SAT(6, "星期六"), SUN(0, "星期日");

    public final int dayValue;
    private final String chinese;

    private Weekday(int dayValue, String chinese) {
        this.dayValue = dayValue;
        this.chinese = chinese;
    }

    @Override
    public String toString() {
        return this.chinese;
    }
}
```

覆写 toString() 的目的是在输出时更有可读性

> 注意：判断枚举常量的名字，要始终使用name()方法，绝不能调用toString()！

### Switch
最后，枚举类可以应用在 switch 语句中，因为枚举类天生具有信息类型和有限个枚举常量，所以比 int，String 类型更适合用在 switch 语句中

```java
public class Main {
    public static void main(String[] args) {
        Weekday day = Weekday.SUN;
        switch(day) {
        case MON:
        case TUE:
        case WED:
        case THU:
        case FRI:
            System.out.println("Today is " + day + ". Work at office!");
            break;
        case SAT:
        case SUN:
            System.out.println("Today is " + day + ". Work at home!");
            break;
        default:
            throw new RuntimeException("cannot process " + day);
        }
    }
}

enum Weekday {
    MON, TUE, WED, THU, FRI, SAT, SUN;
}
```

加上 default 语句，可以再漏写某个枚举常时自动报错，从而及时发现错误。


## BigInteger
在Java 中，由CPU原生提供的整型最大范围是64位long 整数。使用 long 型整数可以直接通过 CPU 指令进行计算，速度非常快

如果我们使用的整数范围超过了 long 型 怎么办，这个时候，就只能用软件来模拟一个大整数。java.math.BigInteger 就是用来表示任意大小的整数。BigInteger 内部用一个 int[] 数组来模拟一个非常大的整数

```java
BigInteger bi = new BigInteger("1234567890");
System.out.println(bi.pow(5)); // 2867971860299718107233761438093672048294900000
```

对 BigInteger 做运算的时候，只能用实例方法，例如，加法计算：

```java
BigInteger i1 = new BigInteger("1234567890");
BigInteger i2 = new BigInteger("12345678901234567890");
BigInteger sum = i1.add(i2); // 12345678902469135780
```

和 long 型整数运算比，BigInteger 不会有范围限制，但缺点是速度比较慢。

也可以把 BigInteger 转换成 long 型

```java
BigInteger i = new BigInteger("123456789000");
System.out.println(i.longValue()); // 123456789000
System.out.println(i.multiply(i).longValueExact()); // java.lang.ArithmeticException: BigInteger out of long range
```

使用 longValueExact() 方法时，如果超出了 long 型的范围，会抛出 ArithmeticException

BigInteger 和 Integer，long 一样，也是不可变类，并且也继承自 Number 类。因为 Number 定义了转换为基本类型的几个方法

- 转换为byte：byteValue()
- 转换为short：shortValue()
- 转换为int：intValue()
- 转换为long：longValue()
- 转换为float：floatValue()
- 转换为double：doubleValue()

因此，通过上述方法，可以把 BigInteger 转换成基本类型，如果 BigInteger 表示的范围超过了基本类型的范围，转换时将丢失高位信息，即结果不一定是准确的，如果需要准确的转换成基本类型，可以使用intValueExact()、longValueExact()等方法，将直接抛出 ArithmeticException 异常。

如果BigInteger的值甚至超过了float的最大范围（3.4x1038），那么返回的float是什么呢？

```java
public class Main {
    public static void main(String[] args) {
        BigInteger n = new BigInteger("999999").pow(99);
        float f = n.floatValue();
        System.out.println(f);
    }
}
```


## BigDecimal

和 BigInteger 类似，BigDecimal 可以表示一个任意大小且精度完全准确的浮点数

```java
BigDecimal bd = new BigDecimal("123.4567");
System.out.println(bd.multiply(bd)); // 15241.55677489
```

BigDecimal 用 scale() 表示小数位数，例如

```java
BigDecimal d1 = new BigDecimal("123.45");
BigDecimal d2 = new BigDecimal("123.4500");
BigDecimal d3 = new BigDecimal("1234500");
System.out.println(d1.scale()); // 2,两位小数
System.out.println(d2.scale()); // 4
System.out.println(d3.scale()); // 0
```

通过 BigDecimal 的 stripTrailingZeros() 方法，可以将一个 BigDecimal 格式化为一个相等的，但去掉了末尾0 的 BigDecimal

```java
BigDecimal d1 = new BigDecimal("123.4500");
BigDecimal d2 = d1.stripTrailingZeros();
System.out.println(d1.scale()); // 4
System.out.println(d2.scale()); // 2,因为去掉了00

BigDecimal d3 = new BigDecimal("1234500");
BigDecimal d4 = d3.stripTrailingZeros();
System.out.println(d3.scale()); // 0
System.out.println(d4.scale()); // -2
```

如果一个 BigDecimal的scale() 返回负数，例如，-2，表示这个数是个整数，并且末尾有2个0。

可以对一个BigDecimal设置它的scale，如果精度比原始值低，那么按照指定的方法进行四舍五入或者直接截断

```java
public class Main {
    public static void main(String[] args) {
        BigDecimal d1 = new BigDecimal("123.456789");
        BigDecimal d2 = d1.setScale(4, RoundingMode.HALF_UP); // 四舍五入，123.4568
        BigDecimal d3 = d1.setScale(4, RoundingMode.DOWN); // 直接截断，123.4567
        System.out.println(d2);
        System.out.println(d3);
    }
}
```

对 BigDecimal 做加，减，乘时，精度不会丢失，但是做除法时，存在无法除尽的情况，这是，就必须指定精度以及如何进行截断

```java
BigDecimal d1 = new BigDecimal("123.456");
BigDecimal d2 = new BigDecimal("23.456789");
BigDecimal d3 = d1.divide(d2, 10, RoundingMode.HALF_UP); // 保留10位小数并四舍五入
BigDecimal d4 = d1.divide(d2); // 报错：ArithmeticException，因为除不尽
```

还可以对 BigDecimal 做除法的同时求余数

```java
public class Main {
    public static void main(String[] args) {
        BigDecimal n = new BigDecimal("12.345");
        BigDecimal m = new BigDecimal("0.12");
        BigDecimal[] dr = n.divideAndRemainder(m);
        System.out.println(dr[0]); // 102
        System.out.println(dr[1]); // 0.105
    }
}
```

调用 divideAndRemainder() 方法时，返回的数组包含两个 BigDecimal，分别是商和余数，其中商总是整数，余数不会大于除数。我们可以利用这个方法判断两个 BigDecimal 是否是整数的倍数

```java
BigDecimal n = new BigDecimal("12.75");
BigDecimal m = new BigDecimal("0.15");
BigDecimal[] dr = n.divideAndRemainder(m);
if (dr[1].signum() == 0) {
    // n是m的整数倍
}
```

### 比较 BigDecimal
在比较两个BigDecimal的值是否相等时，要特别注意，使用equals()方法不但要求两个BigDecimal的值相等，还要求它们的scale()相等：

```java
BigDecimal d1 = new BigDecimal("123.456");
BigDecimal d2 = new BigDecimal("123.45600");
System.out.println(d1.equals(d2)); // false,因为scale不同
System.out.println(d1.equals(d2.stripTrailingZeros())); // true,因为d2去除尾部0后scale变为2
System.out.println(d1.compareTo(d2)); // 0
```

必须使用 compareTo() 方法来比较，它根据两个值的大小分别返回负数，正数和0，分别表示小于，大于和等于

>总是使用compareTo()比较两个BigDecimal的值，不要使用equals()！

如果查看BigDecimal的源码，可以发现，实际上一个BigDecimal是通过一个BigInteger和一个scale来表示的，即BigInteger表示一个完整的整数，而scale表示小数位数：

```java
public class BigDecimal extends Number implements Comparable<BigDecimal> {
    private final BigInteger intVal;
    private final int scale;
}
```

BigDecimal也是从Number继承的，也是不可变对象。

## 常用工具类
### Math

顾名思义，Math类就是用来进行数学计算的，它提供了大量的静态方法来便于我们实现数学计算：

求绝对值：

```java
Math.abs(-100); // 100
Math.abs(-7.8); // 7.8
```

取最大或最小值：

```java
Math.max(100, 99); // 100
Math.min(1.2, 2.3); // 1.2
```

计算xy次方：

```java
Math.pow(2, 10); // 2的10次方=1024
```

计算√x：

```java
Math.sqrt(2); // 1.414...
```

计算ex次方：

```java
Math.exp(2); // 7.389...
```

计算以e为底的对数：

```java
Math.log(4); // 1.386...
```

计算以10为底的对数：

```java
Math.log10(100); // 2
```

三角函数：

```java
Math.sin(3.14); // 0.00159...
Math.cos(3.14); // -0.9999...
Math.tan(3.14); // -0.0015...
Math.asin(1.0); // 1.57079...
Math.acos(1.0); // 0.0
```

Math还提供了几个数学常量：

```java
double pi = Math.PI; // 3.14159...
double e = Math.E; // 2.7182818...
Math.sin(Math.PI / 6); // sin(π/6) = 0.5
```

生成一个随机数x，x的范围是0 <= x < 1:

```java
Math.random(); // 0.53907... 每次都不一样
```

如果我们要生成一个区间在[MIN,MAX]的随机数，可以借助 Math.random() 实现，计算如下

```java
// 区间在[MIN, MAX)的随机数
public class Main {
    public static void main(String[] args) {
        double x = Math.random(); // x的范围是[0,1)
        double min = 10;
        double max = 50;
        double y = x * (max - min) + min; // y的范围是[10,50)
        long n = (long) y; // n的范围是[10,50)的整数
        System.out.println(y);
        System.out.println(n);
    }
}
```

Java标准库还提供了一个StrictMath，它提供了和Math几乎一模一样的方法。这两个类的区别在于，由于浮点数计算存在误差，不同的平台（例如x86和ARM）计算的结果可能不一致（指误差不同），因此，StrictMath保证所有平台计算结果都是完全相同的，而Math会尽量针对平台优化计算速度，所以，绝大多数情况下，使用Math就足够了。

### Random
Random 用来创建伪随机数，是指只要给定一个初始的种子，产生的随机数序列是完全一样的。

要生成一个随机数，可以使用 nextInt()、nextLong()、nextFloat()、nextDouble()：

```java
Random r = new Random();
r.nextInt(); // 2071575453,每次都不一样
r.nextInt(10); // 5,生成一个[0,10)之间的int
r.nextLong(); // 8811649292570369305,每次都不一样
r.nextFloat(); // 0.54335...生成一个[0,1)之间的float
r.nextDouble(); // 0.3716...生成一个[0,1)之间的double
```

每次运行程序，生成的随机数都是不同的，没看出伪随机数的特性来。

这是因为我们创建Random实例时，如果不给定种子，就使用系统当前时间戳作为种子，因此每次运行时，种子不同，得到的伪随机数序列就不同。

如果我们在创建Random实例时指定一个种子，就会得到完全确定的随机数序列：

```java
public class Main {
    public static void main(String[] args) {
        Random r = new Random(12345);
        for (int i = 0; i < 10; i++) {
            System.out.println(r.nextInt(100));
        }
        // 51, 80, 41, 28, 55...
    }
}
```

前面我们使用的 Math.random() 实际上内部调用了Random类，所以它也是伪随机数，只是我们无法指定种子。

### SecureRandom
有伪随机数，就有真随机数。实际上真正的真随机数只能通过量子力学原理来获取，而我们想要的是一个不可预测的安全的随机数，SecureRandom就是用来创建安全的随机数的：

```java
SecureRandom sr = new SecureRandom();
System.out.println(sr.nextInt(100));
```

SecureRandom无法指定种子，它使用RNG（random number generator）算法。JDK的SecureRandom实际上有多种不同的底层实现，有的使用安全随机种子加上伪随机数算法来产生安全的随机数，有的使用真正的随机数生成器。实际使用的时候，可以优先获取高强度的安全随机数生成器，如果没有提供，再使用普通等级的安全随机数生成器：

```java
public class Main {
    public static void main(String[] args) {
        SecureRandom sr = null;
        try {
            sr = SecureRandom.getInstanceStrong(); // 获取高强度安全随机数生成器
        } catch (NoSuchAlgorithmException e) {
            sr = new SecureRandom(); // 获取普通的安全随机数生成器
        }
        byte[] buffer = new byte[16];
        sr.nextBytes(buffer); // 用安全随机数填充buffer
        System.out.println(Arrays.toString(buffer));
    }
}
```

SecureRandom的安全性是通过操作系统提供的安全的随机种子来生成随机数。这个种子是通过CPU的热噪声、读写磁盘的字节、网络流量等各种随机事件产生的“熵”。

在密码学中，安全的随机数非常重要。如果使用不安全的伪随机数，所有加密体系都将被攻破。因此，时刻牢记必须使用SecureRandom来产生安全的随机数。

> 需要使用安全随机数的时候，必须使用SecureRandom，绝不能使用Random！

# 异常处理

## Java 的异常

在计算机程序运行的过程中，总是会出现各种各样的错误。

有一些错误是用户造成的，比如，希望用户输入一个int类型的年龄，但是用户的输入是abc：

```
// 假设用户输入了abc：
String s = "abc";
int n = Integer.parseInt(s); // NumberFormatException!
```

程序想要读写某个文件的内容，但是用户已经把它删除了：

```
// 用户删除了该文件：
String t = readFile("C:\\abc.txt"); // FileNotFoundException!
```

还有一些错误是随机出现，并且永远不可能避免的。比如：

- 网络突然断了，连接不到远程服务器；
- 内存耗尽，程序崩溃了；
- 用户点“打印”，但根本没有打印机；
- ……

所以，一个健壮的程序必须处理各种各样的错误。

所谓错误，就是程序调用某个函数的时候，如果失败了，就表示出错。

调用方如何获知调用失败的信息？有两种方法：

方法一：约定返回错误码。

例如，处理一个文件，如果返回0，表示成功，返回其他整数，表示约定的错误码：

```java
int code = processFile("C:\\test.txt");
if (code == 0) {
    // ok:
} else {
    // error:
    switch (code) {
    case 1:
        // file not found:
    case 2:
        // no read permission:
    default:
        // unknown error:
    }
}
```

因为使用int类型的错误码，想要处理就非常麻烦。这种方式常见于底层C函数。

方法二：在语言层面上提供一个异常处理机制。

Java内置了一套异常处理机制，总是使用异常来表示错误。

异常是一种class，因此它本身带有类型信息。异常可以在任何地方抛出，但只需要在上层捕获，这样就和方法调用分离了：

```java
try {
    String s = processFile(“C:\\test.txt”);
    // ok:
} catch (FileNotFoundException e) {
    // file not found:
} catch (SecurityException e) {
    // no read permission:
} catch (IOException e) {
    // io error:
} catch (Exception e) {
    // other error:
}
```

因为Java的异常是class，它的继承关系如下：

```
                     ┌───────────┐
                     │  Object   │
                     └───────────┘
                           ▲
                           │
                     ┌───────────┐
                     │ Throwable │
                     └───────────┘
                           ▲
                 ┌─────────┴─────────┐
                 │                   │
           ┌───────────┐       ┌───────────┐
           │   Error   │       │ Exception │
           └───────────┘       └───────────┘
                 ▲                   ▲
         ┌───────┘              ┌────┴──────────┐
         │                      │               │
┌─────────────────┐    ┌─────────────────┐┌───────────┐
│OutOfMemoryError │... │RuntimeException ││IOException│...
└─────────────────┘    └─────────────────┘└───────────┘
                                ▲
                    ┌───────────┴─────────────┐
                    │                         │
         ┌─────────────────────┐ ┌─────────────────────────┐
         │NullPointerException │ │IllegalArgumentException │...
         └─────────────────────┘ └─────────────────────────┘
```

从继承关系可知：Throwable是异常体系的根，它继承自Object。Throwable有两个体系：Error和Exception，Error表示严重的错误，程序对此一般无能为力，例如：

- OutOfMemoryError：内存耗尽
- NoClassDefFoundError：无法加载某个Class
- StackOverflowError：栈溢出

而Exception则是运行时的错误，它可以被捕获并处理。

某些异常是应用程序逻辑处理的一部分，应该捕获并处理。例如：

- NumberFormatException：数值类型的格式错误
- FileNotFoundException：未找到文件
- SocketException：读取网络失败

还有一些异常是程序逻辑编写不对造成的，应该修复程序本身。例如：

- NullPointerException：对某个null的对象调用方法或字段
- IndexOutOfBoundsException：数组索引越界

Exception又分为两大类：

- RuntimeException以及它的子类；
- 非RuntimeException（包括IOException、ReflectiveOperationException等等）

Java规定：

- 必须捕获的异常，包括Exception及其子类，但不包括RuntimeException及其子类，这种类型的异常称为Checked Exception。

- 不需要捕获的异常，包括Error及其子类，RuntimeException及其子类。

### 捕获异常
捕获异常使用try...catch语句，把可能发生异常的代码放到try {...}中，然后使用catch捕获对应的Exception及其子类：

```java
public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) {
        try {
            // 用指定编码转换String为byte[]:
            return s.getBytes("GBK");
        } catch (UnsupportedEncodingException e) {
            // 如果系统不支持GBK编码，会捕获到UnsupportedEncodingException:
            System.out.println(e); // 打印异常信息
            return s.getBytes(); // 尝试使用用默认编码
        }
    }
}
```

如果我们不捕获UnsupportedEncodingException，会出现编译失败的问题：

```java
public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) {
        return s.getBytes("GBK");
    }
}
```

编译器会报错，错误信息类似：unreported exception UnsupportedEncodingException; must be caught or declared to be thrown，并且准确地指出需要捕获的语句是 return s.getBytes("GBK");。意思是说，像 UnsupportedEncodingException 这样的 Checked Exception ，必须被捕获。

这是因为String.getBytes(String)方法定义是：

```java
public byte[] getBytes(String charsetName) throws UnsupportedEncodingException {
    ...
}
```

在方法定义的时候，使用throws Xxx表示该方法可能抛出的异常类型。调用方在调用的时候，必须强制捕获这些异常，否则编译器会报错。

在toGBK()方法中，因为调用了String.getBytes(String)方法，就必须捕获UnsupportedEncodingException。我们也可以不捕获它，而是在方法定义处用throws表示toGBK()方法可能会抛出UnsupportedEncodingException，就可以让toGBK()方法通过编译器检查：

```java
public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        return s.getBytes("GBK");
    }
}
```

上述代码仍然会得到编译错误，但这一次，编译器提示的不是调用return s.getBytes("GBK");的问题，而是byte[] bs = toGBK("中文");。因为在main()方法中，调用toGBK()，没有捕获它声明的可能抛出的UnsupportedEncodingException。

修复方法是在main()方法中捕获异常并处理：

```java
public class Main {
    public static void main(String[] args) {
        try {
            byte[] bs = toGBK("中文");
            System.out.println(Arrays.toString(bs));
        } catch (UnsupportedEncodingException e) {
            System.out.println(e);
        }
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        // 用指定编码转换String为byte[]:
        return s.getBytes("GBK");
    }
}
```

可见，只要是方法声明的Checked Exception，不在调用层捕获，也必须在更高的调用层捕获。所有未捕获的异常，最终也必须在main()方法中捕获，不会出现漏写try的情况。这是由编译器保证的。main()方法也是最后捕获Exception的机会。

如果是测试代码，上面的写法就略显麻烦。如果不想写任何try代码，可以直接把main()方法定义为throws Exception：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) throws UnsupportedEncodingException {
        // 用指定编码转换String为byte[]:
        return s.getBytes("GBK");
    }
}
```

因为main()方法声明了可能抛出Exception，也就声明了可能抛出所有的Exception，因此在内部就无需捕获了。代价就是一旦发生异常，程序会立刻退出。

还有一些人喜欢在toGBK()内部“消化”异常：

```java
static byte[] toGBK(String s) {
    try {
        return s.getBytes("GBK");
    } catch (UnsupportedEncodingException e) {
        // 什么也不干
    }
    return null;
```

这种捕获后不处理的方式是非常不好的，即使真的什么也做不了，也要先把异常记录下来：

```java
static byte[] toGBK(String s) {
    try {
        return s.getBytes("GBK");
    } catch (UnsupportedEncodingException e) {
        // 先记下来再说:
        e.printStackTrace();
    }
    return null;
```

所有异常都可以调用printStackTrace()方法打印异常栈，这是一个简单有用的快速打印异常的方法。

## 捕获异常
在Java中，凡是可能抛出异常的语句，都可以用try ... catch捕获。把可能发生异常的语句放在try { ... }中，然后使用catch捕获对应的Exception及其子类。

### 多catch语句
可以使用多个 catch 语句，每个 catch 分别捕获对应的 Exception 及其子类，JVM在捕获到异常后，会从上到下匹配catch语句，匹配到某个catch后，执行catch代码块，然后不再继续匹配。

简单地说就是：多个catch语句只有一个能被执行。例如：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (IOException e) {
        System.out.println(e);
    } catch (NumberFormatException e) {
        System.out.println(e);
    }
}
```

存在多个catch的时候，catch的顺序非常重要：子类必须写在前面。例如：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (IOException e) {
        System.out.println("IO error");
    } catch (UnsupportedEncodingException e) { // 永远捕获不到
        System.out.println("Bad encoding");
    }
}
```

对于上面的代码，UnsupportedEncodingException异常是永远捕获不到的，因为它是IOException的子类。当抛出UnsupportedEncodingException异常时，会被catch (IOException e) { ... }捕获并执行。

因此，正确的写法是把子类放到前面：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (UnsupportedEncodingException e) {
        System.out.println("Bad encoding");
    } catch (IOException e) {
        System.out.println("IO error");
    }
}
```

### finally语句

无论是否有异常发生，如果我们都希望执行一些语句，例如清理工作，怎么写？

可以把执行语句写若干遍：正常执行的放到try中，每个catch再写一遍。例如：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
        System.out.println("END");
    } catch (UnsupportedEncodingException e) {
        System.out.println("Bad encoding");
        System.out.println("END");
    } catch (IOException e) {
        System.out.println("IO error");
        System.out.println("END");
    }
}
```

上述代码无论是否发生异常，都会执行System.out.println("END");这条语句。

那么如何消除这些重复的代码？Java的try ... catch机制还提供了finally语句，finally语句块保证有无错误都会执行。上述代码可以改写如下：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (UnsupportedEncodingException e) {
        System.out.println("Bad encoding");
    } catch (IOException e) {
        System.out.println("IO error");
    } finally {
        System.out.println("END");
    }
}
```

注意finally有几个特点：

- finally语句不是必须的，可写可不写；
- finally总是最后执行。

如果没有发生异常，就正常执行try { ... }语句块，然后执行finally。如果发生了异常，就中断执行try { ... }语句块，然后跳转执行匹配的catch语句块，最后执行finally。

可见，finally是用来保证一些代码必须执行的。

某些情况下，可以没有catch，只使用try ... finally结构。例如：

```java
void process(String file) throws IOException {
    try {
        ...
    } finally {
        System.out.println("END");
    }
}
```

### 捕获多种异常
如果某些异常的处理逻辑相同，但是异常本身不存在继承关系，那么就得编写多条catch子句：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (IOException e) {
        System.out.println("Bad input");
    } catch (NumberFormatException e) {
        System.out.println("Bad input");
    } catch (Exception e) {
        System.out.println("Unknown error");
    }
}
```

因为处理IOException和NumberFormatException的代码是相同的，所以我们可以把它两用|合并到一起：

```java
public static void main(String[] args) {
    try {
        process1();
        process2();
        process3();
    } catch (IOException | NumberFormatException e) { // IOException或NumberFormatException
        System.out.println("Bad input");
    } catch (Exception e) {
        System.out.println("Unknown error");
    }
}
```

## 抛出异常
### 异常的传播
当某个方法抛出了异常时，如果当前方法没有捕获异常，异常就会被抛到上层调用方法，直到遇到某个try ... catch被捕获为止：

```java
public class Main {
    public static void main(String[] args) {
        try {
            process1();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static void process1() {
        process2();
    }

    static void process2() {
        Integer.parseInt(null); // 会抛出NumberFormatException
    }
}
```

通过printStackTrace()可以打印出方法的调用栈，类似：

```
java.lang.NumberFormatException: null
    at java.base/java.lang.Integer.parseInt(Integer.java:614)
    at java.base/java.lang.Integer.parseInt(Integer.java:770)
    at Main.process2(Main.java:16)
    at Main.process1(Main.java:12)
    at Main.main(Main.java:5)
```

printStackTrace()对于调试错误非常有用，上述信息表示：NumberFormatException是在java.lang.Integer.parseInt方法中被抛出的，调用层次从上到下依次是：

- main()调用process1()；
- process1()调用process2()；
- process2()调用Integer.parseInt(String)；
- Integer.parseInt(String)调用Integer.parseInt(String, int)。

查看Integer.java源码可知，抛出异常的方法代码如下：

```java
public static int parseInt(String s, int radix) throws NumberFormatException {
    if (s == null) {
        throw new NumberFormatException("null");
    }
    ...
}
```

并且，每层调用均给出了源代码的行号，可直接定位。

### 抛出异常
当发生错误时，例如，用户输入了非法的字符，我们就可以抛出异常。

如何抛出异常？参考Integer.parseInt()方法，抛出异常分两步：

- 创建某个Exception的实例；
- 用throw语句抛出。

下面是一个例子：

```java
void process2(String s) {
    if (s==null) {
        NullPointerException e = new NullPointerException();
        throw e;
    }
}
```

实际上，绝大部分抛出异常的代码都会合并写成一行：

```
void process2(String s) {
    if (s==null) {
        throw new NullPointerException();
    }
}
```

如果一个方法捕获了某个异常后，又在catch子句中抛出新的异常，就相当于把抛出的异常类型“转换”了：

```java
void process1(String s) {
    try {
        process2();
    } catch (NullPointerException e) {
        throw new IllegalArgumentException();
    }
}

void process2(String s) {
    if (s==null) {
        throw new NullPointerException();
    }
}
```

当process2()抛出NullPointerException后，被process1()捕获，然后抛出IllegalArgumentException()。

如果在main()中捕获IllegalArgumentException，我们看看打印的异常栈：

```java
public class Main {
    public static void main(String[] args) {
        try {
            process1();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static void process1() {
        try {
            process2();
        } catch (NullPointerException e) {
            throw new IllegalArgumentException();
        }
    }

    static void process2() {
        throw new NullPointerException();
    }
}
```

打印出的异常栈类似：

```java
java.lang.IllegalArgumentException
    at Main.process1(Main.java:15)
    at Main.main(Main.java:5)
```

这说明新的异常丢失了原始异常信息，我们已经看不到原始异常NullPointerException的信息了。

为了能追踪到完整的异常栈，在构造异常的时候，把原始的Exception实例传进去，新的Exception就可以持有原始Exception信息。对上述代码改进如下：

```java
public class Main {
    public static void main(String[] args) {
        try {
            process1();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static void process1() {
        try {
            process2();
        } catch (NullPointerException e) {
            throw new IllegalArgumentException(e);
        }
    }

    static void process2() {
        throw new NullPointerException();
    }
}
```

运行上述代码，打印出的异常栈类似：

```
java.lang.IllegalArgumentException: java.lang.NullPointerException
    at Main.process1(Main.java:15)
    at Main.main(Main.java:5)
Caused by: java.lang.NullPointerException
    at Main.process2(Main.java:20)
    at Main.process1(Main.java:13)

```

注意到Caused by: Xxx，说明捕获的IllegalArgumentException并不是造成问题的根源，根源在于NullPointerException，是在Main.process2()方法抛出的。

在代码中获取原始异常可以使用Throwable.getCause()方法。如果返回null，说明已经是“根异常”了。

有了完整的异常栈的信息，我们才能快速定位并修复代码的问题。

如果我们在try或者catch语句块中抛出异常，finally语句是否会执行？例如：

```java
public class Main {
    public static void main(String[] args) {
        try {
            Integer.parseInt("abc");
        } catch (Exception e) {
            System.out.println("catched");
            throw new RuntimeException(e);
        } finally {
            System.out.println("finally");
        }
    }
}
```

上述代码执行结果如下：

```
catched
finally
Exception in thread "main" java.lang.RuntimeException: java.lang.NumberFormatException: For input string: "abc"
    at Main.main(Main.java:8)
Caused by: java.lang.NumberFormatException: For input string: "abc"
    at ...
```

第一行打印了catched，说明进入了catch语句块。第二行打印了finally，说明执行了finally语句块。

因此，在catch中抛出异常，不会影响finally的执行。JVM会先执行finally，然后抛出异常。

### 异常屏蔽
如果在执行finally语句时抛出异常，那么，catch语句的异常还能否继续抛出？例如：

```java
public class Main {
    public static void main(String[] args) {
        try {
            Integer.parseInt("abc");
        } catch (Exception e) {
            System.out.println("catched");
            throw new RuntimeException(e);
        } finally {
            System.out.println("finally");
            throw new IllegalArgumentException();
        }
    }
}
```

执行上述代码，发现异常信息如下：

```
catched
finally
Exception in thread "main" java.lang.IllegalArgumentException
    at Main.main(Main.java:11)
```

这说明finally抛出异常后，原来在catch中准备抛出的异常就“消失”了，因为只能抛出一个异常。没有被抛出的异常称为“被屏蔽”的异常（Suppressed Exception）。

在极少数的情况下，我们需要获知所有的异常。如何保存所有的异常信息？方法是先用origin变量保存原始异常，然后调用Throwable.addSuppressed()，把原始异常添加进来，最后在finally抛出：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Exception origin = null;
        try {
            System.out.println(Integer.parseInt("abc"));
        } catch (Exception e) {
            origin = e;
            throw e;
        } finally {
            Exception e = new IllegalArgumentException();
            if (origin != null) {
                e.addSuppressed(origin);
            }
            throw e;
        }
    }
}
```

当catch和finally都抛出了异常时，虽然catch的异常被屏蔽了，但是，finally抛出的异常仍然包含了它：

```
Exception in thread "main" java.lang.IllegalArgumentException
    at Main.main(Main.java:11)
Suppressed: java.lang.NumberFormatException: For input string: "abc"
    at java.base/java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
    at java.base/java.lang.Integer.parseInt(Integer.java:652)
    at java.base/java.lang.Integer.parseInt(Integer.java:770)
    at Main.main(Main.java:6)
```

通过Throwable.getSuppressed()可以获取所有的Suppressed Exception。

绝大多数情况下，在finally中不要抛出异常。因此，我们通常不需要关心Suppressed Exception。

## 自定义异常

Java标准库定义的常用异常包括：

```
Exception
│
├─ RuntimeException
│  │
│  ├─ NullPointerException
│  │
│  ├─ IndexOutOfBoundsException
│  │
│  ├─ SecurityException
│  │
│  └─ IllegalArgumentException
│     │
│     └─ NumberFormatException
│
├─ IOException
│  │
│  ├─ UnsupportedCharsetException
│  │
│  ├─ FileNotFoundException
│  │
│  └─ SocketException
│
├─ ParseException
│
├─ GeneralSecurityException
│
├─ SQLException
│
└─ TimeoutException
```

当我们在代码中需要抛出异常时，尽量使用JDK已定义的异常类型。例如，参数检查不合法，应该抛出IllegalArgumentException：

```java
static void process1(int age) {
    if (age <= 0) {
        throw new IllegalArgumentException();
    }
}
```

在一个大型项目中，可以自定义新的异常类型，但是，保持一个合理的异常继承体系是非常重要的。

一个常见的做法是自定义一个BaseException作为“根异常”，然后，派生出各种业务类型的异常。

BaseException需要从一个适合的Exception派生，通常建议从RuntimeException派生：

```java
public class BaseException extends RuntimeException {
}
```

其他业务类型的异常就可以从BaseException派生：

```java
public class UserNotFoundException extends BaseException {
}

public class LoginFailedException extends BaseException {
}

...
```

自定义的BaseException应该提供多个构造方法：

```java
public class BaseException extends RuntimeException {
    public BaseException() {
        super();
    }

    public BaseException(String message, Throwable cause) {
        super(message, cause);
    }

    public BaseException(String message) {
        super(message);
    }

    public BaseException(Throwable cause) {
        super(cause);
    }
}
```

上述构造方法实际上都是原样照抄RuntimeException。这样，抛出异常的时候，就可以选择合适的构造方法。通过IDE可以根据父类快速生成子类的构造方法。

## 使用断言

断言（Assertion）是一种调试程序的方式。在Java中，使用assert关键字来实现断言。

我们先看一个例子：

```java
public static void main(String[] args) {
    double x = Math.abs(-123.45);
    assert x >= 0;
    System.out.println(x);
}
```

语句assert x >= 0;即为断言，断言条件x >= 0预期为true。如果计算结果为false，则断言失败，抛出AssertionError。

使用assert语句时，还可以添加一个可选的断言消息：

```java
assert x >= 0 : "x must >= 0";

```

这样，断言失败的时候，AssertionError会带上消息x must >= 0，更加便于调试。

Java断言的特点是：断言失败时会抛出AssertionError，导致程序结束退出。因此，断言不能用于可恢复的程序错误，只应该用于开发和测试阶段。

对于可恢复的程序错误，不应该使用断言。例如：

```java
void sort(int[] arr) {
    assert arr != null;
}
```

应该抛出异常并在上层捕获：

```java
void sort(int[] arr) {
    if (x == null) {
        throw new IllegalArgumentException("array cannot be null");
    }
}
```

当我们在程序中使用assert时，例如，一个简单的断言：

```java
// assert
public class Main {
    public static void main(String[] args) {
        int x = -1;
        assert x > 0;
        System.out.println(x);
    }
}
```

断言x必须大于0，实际上x为-1，断言肯定失败。执行上述代码，发现程序并未抛出AssertionError，而是正常打印了x的值。

这是怎么肥四？为什么assert语句不起作用？

这是因为JVM默认关闭断言指令，即遇到assert语句就自动忽略了，不执行。

要执行assert语句，必须给Java虚拟机传递-enableassertions（可简写为-ea）参数启用断言。所以，上述程序必须在命令行下运行才有效果：

```java
$ java -ea Main.java
Exception in thread "main" java.lang.AssertionError
	at Main.main(Main.java:5)
``` 

还可以有选择地对特定地类启用断言，命令行参数是：-ea:com.itranswarp.sample.Main，表示只对com.itranswarp.sample.Main这个类启用断言。

或者对特定地包启用断言，命令行参数是：-ea:com.itranswarp.sample...（注意结尾有3个.），表示对com.itranswarp.sample这个包启动断言。

## 使用 JDK Logging

在编写程序的过程中，发现程序运行结果与预期不符，怎么办？当然是用 System.out.println() 打印出执行过程中的某些变量，观察每一步的结果与代码逻辑是否符合，然后有针对性地修改代码。

代码改好了怎么办？当然是删除没有用的System.out.println()语句了。

如果改代码又改出问题怎么办？再加上System.out.println()。

反复这么搞几次，很快大家就发现使用System.out.println()非常麻烦。

怎么办？

解决方法是使用日志。

那什么是日志？日志就是Logging，它的目的是为了取代System.out.println()。

输出日志，而不是用System.out.println()，有以下几个好处：

- 可以设置输出样式，避免自己每次都写"ERROR: " + var；
- 可以设置输出级别，禁止某些级别输出。例如，只输出错误日志；
- 可以被重定向到文件，这样可以在程序运行结束后查看日志；
- 可以按包名控制日志级别，只输出某些包打的日志；
- 可以……

总之就是好处很多啦。

那如何使用日志？

因为Java标准库内置了日志包java.util.logging，我们可以直接用。先看一个简单的例子：

```java
public class Hello {
    public static void main(String[] args) {
        Logger logger = Logger.getGlobal();
        logger.info("start process...");
        logger.warning("memory is running out...");
        logger.fine("ignored.");
        logger.severe("process will be terminated...");
    }
}
```

运行上述代码，得到类似如下的输出：

```java
Mar 02, 2019 6:32:13 PM Hello main
INFO: start process...
Mar 02, 2019 6:32:13 PM Hello main
WARNING: memory is running out...
Mar 02, 2019 6:32:13 PM Hello main
SEVERE: process will be terminated...
```

对比可见，使用日志最大的好处是，它自动打印了时间、调用类、调用方法等很多有用的信息。

再仔细观察发现，4条日志，只打印了3条，logger.fine()没有打印。这是因为，日志的输出可以设定级别。JDK的Logging定义了7个日志级别，从严重到普通：

- SEVERE
- WARNING
- INFO
- CONFIG
- FINE
- FINER
- FINEST

因为默认级别是INFO，因此，INFO级别以下的日志，不会被打印出来。使用日志级别的好处在于，调整级别，就可以屏蔽掉很多调试相关的日志输出。

使用Java标准库内置的Logging有以下局限：

Logging系统在JVM启动时读取配置文件并完成初始化，一旦开始运行main()方法，就无法修改配置；

配置不太方便，需要在JVM启动时传递参数

-Djava.util.logging.config.file=<config-file-name>。

因此，Java标准库内置的Logging使用并不是非常广泛。

## 使用 Commons Logging

和Java标准库提供的日志不同，Commons Logging是一个第三方日志库，它是由Apache创建的日志模块。

Commons Logging的特色是，它可以挂接不同的日志系统，并通过配置文件指定挂接的日志系统。默认情况下，Commons Loggin自动搜索并使用Log4j（Log4j是另一个流行的日志系统），如果没有找到Log4j，再使用JDK Logging。

使用Commons Logging只需要和两个类打交道，并且只有两步：

第一步，通过LogFactory获取Log类的实例； 第二步，使用Log实例的方法打日志。

示例代码如下：

```java
public class Main {
    public static void main(String[] args) {
        Log log = LogFactory.getLog(Main.class);
        log.info("start...");
        log.warn("end.");
    }
}
```

运行上述代码，肯定会得到编译错误，类似error: package org.apache.commons.logging does not exist（找不到org.apache.commons.logging这个包）。因为Commons Logging是一个第三方提供的库，所以，必须先把它下载下来。下载后，解压，找到commons-logging-1.2.jar这个文件，再把Java源码Main.java放到一个目录下，例如work目录：

```
work
│
├─ commons-logging-1.2.jar
│
└─ Main.java
```

如果编译成功，那么当前目录下就会多出一个Main.class文件：

```
work
│
├─ commons-logging-1.2.jar
│
├─ Main.java
│
└─ Main.class
```

现在可以执行这个Main.class，使用java命令，也必须指定classpath，命令如下：

```
java -cp .;commons-logging-1.2.jar Main
```

注意到传入的classpath有两部分：一个是.，一个是commons-logging-1.2.jar，用;分割。.表示当前目录，如果没有这个.，JVM不会在当前目录搜索Main.class，就会报错。

如果在Linux或macOS下运行，注意classpath的分隔符不是;，而是:：

```
java -cp .:commons-logging-1.2.jar Main
```

运行结果如下：

```
Mar 02, 2019 7:15:31 PM Main main
INFO: start...
Mar 02, 2019 7:15:31 PM Main main
WARNING: end.
```

Commons Logging定义了6个日志级别：

- FATAL
- ERROR
- WARNING
- INFO
- DEBUG
- TRACE

默认级别是INFO。

使用Commons Logging时，如果在静态方法中引用Log，通常直接定义一个静态类型变量：

```java
// 在静态方法中引用Log:
public class Main {
    static final Log log = LogFactory.getLog(Main.class);

    static void foo() {
        log.info("foo");
    }
}
```

在实例方法中引用Log，通常定义一个实例变量：

```java
// 在实例方法中引用Log:
public class Person {
    protected final Log log = LogFactory.getLog(getClass());

    void foo() {
        log.info("foo");
    }
}
```

注意到实例变量log的获取方式是LogFactory.getLog(getClass())，虽然也可以用LogFactory.getLog(Person.class)，但是前一种方式有个非常大的好处，就是子类可以直接使用该log实例。例如：

```java
// 在子类中使用父类实例化的log:
public class Student extends Person {
    void bar() {
        log.info("bar");
    }
}
```

由于Java类的动态特性，子类获取的log字段实际上相当于LogFactory.getLog(Student.class)，但却是从父类继承而来，并且无需改动代码。

此外，Commons Logging的日志方法，例如info()，除了标准的info(String)外，还提供了一个非常有用的重载方法：info(String, Throwable)，这使得记录异常更加简单：

```java
try {
    ...
} catch (Exception e) {
    log.error("got exception!", e);
}
```

## 使用 Log4j
前面介绍了Commons Logging，可以作为“日志接口”来使用。而真正的“日志实现”可以使用Log4j。

Log4j是一种非常流行的日志框架，最新版本是2.x。

Log4j是一个组件化设计的日志系统，它的架构大致如下：

```
log.info("User signed in.");
 │
 │   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 ├──>│ Appender │───>│  Filter  │───>│  Layout  │───>│ Console  │
 │   └──────────┘    └──────────┘    └──────────┘    └──────────┘
 │
 │   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 ├──>│ Appender │───>│  Filter  │───>│  Layout  │───>│   File   │
 │   └──────────┘    └──────────┘    └──────────┘    └──────────┘
 │
 │   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 └──>│ Appender │───>│  Filter  │───>│  Layout  │───>│  Socket  │
     └──────────┘    └──────────┘    └──────────┘    └──────────┘
```

当我们使用Log4j输出一条日志时，Log4j自动通过不同的Appender把同一条日志输出到不同的目的地。例如：

- console：输出到屏幕；
- file：输出到文件；
- socket：通过网络输出到远程计算机；
- jdbc：输出到数据库

在输出日志的过程中，通过Filter来过滤哪些log需要被输出，哪些log不需要被输出。例如，仅输出ERROR级别的日志。

最后，通过Layout来格式化日志信息，例如，自动添加日期、时间、方法名称等信息。

上述结构虽然复杂，但我们在实际使用的时候，并不需要关心Log4j的API，而是通过配置文件来配置它。

以XML配置为例，使用Log4j的时候，我们把一个log4j2.xml的文件放到classpath下就可以让Log4j读取配置文件并按照我们的配置来输出日志。下面是一个配置文件的例子：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
	<Properties>
        <!-- 定义日志格式 -->
		<Property name="log.pattern">%d{MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36}%n%msg%n%n</Property>
        <!-- 定义文件名变量 -->
		<Property name="file.err.filename">log/err.log</Property>
		<Property name="file.err.pattern">log/err.%i.log.gz</Property>
	</Properties>
    <!-- 定义Appender，即目的地 -->
	<Appenders>
        <!-- 定义输出到屏幕 -->
		<Console name="console" target="SYSTEM_OUT">
            <!-- 日志格式引用上面定义的log.pattern -->
			<PatternLayout pattern="${log.pattern}" />
		</Console>
        <!-- 定义输出到文件,文件名引用上面定义的file.err.filename -->
		<RollingFile name="err" bufferedIO="true" fileName="${file.err.filename}" filePattern="${file.err.pattern}">
			<PatternLayout pattern="${log.pattern}" />
			<Policies>
                <!-- 根据文件大小自动切割日志 -->
				<SizeBasedTriggeringPolicy size="1 MB" />
			</Policies>
            <!-- 保留最近10份 -->
			<DefaultRolloverStrategy max="10" />
		</RollingFile>
	</Appenders>
	<Loggers>
		<Root level="info">
            <!-- 对info级别的日志，输出到console -->
			<AppenderRef ref="console" level="info" />
            <!-- 对error级别的日志，输出到err，即上面定义的RollingFile -->
			<AppenderRef ref="err" level="error" />
		</Root>
	</Loggers>
</Configuration>
```

虽然配置Log4j比较繁琐，但一旦配置完成，使用起来就非常方便。对上面的配置文件，凡是INFO级别的日志，会自动输出到屏幕，而ERROR级别的日志，不但会输出到屏幕，还会同时输出到文件。并且，一旦日志文件达到指定大小（1MB），Log4j就会自动切割新的日志文件，并最多保留10份。

有了配置文件还不够，因为Log4j也是一个第三方库，我们需要从这里[下载](https://logging.apache.org/log4j/2.x/download.html)Log4j，解压后，把以下3个jar包放到classpath中：

- log4j-api-2.x.jar
- log4j-core-2.x.jar
- log4j-jcl-2.x.jar

因为Commons Logging会自动发现并使用Log4j，所以，把上一节下载的commons-logging-1.2.jar也放到classpath中。

要打印日志，只需要按Commons Logging的写法写，不需要改动任何代码，就可以得到Log4j的日志输出，类似：

```
03-03 12:09:45.880 [main] INFO  com.itranswarp.learnjava.Main
Start process...
```

在开发阶段，始终使用Commons Logging接口来写入日志，并且开发阶段无需引入Log4j。如果需要把日志写入文件， 只需要把正确的配置文件和Log4j相关的jar包放入classpath，就可以自动把日志切换成使用Log4j写入，无需修改任何代码。

## 使用 SLF4J 和 Logback
前面介绍了Commons Logging和Log4j这一对好基友，它们一个负责充当日志API，一个负责实现日志底层，搭配使用非常便于开发。

有的童鞋可能还听说过SLF4J和Logback。这两个东东看上去也像日志，它们又是啥？

其实SLF4J类似于Commons Logging，也是一个日志接口，而Logback类似于Log4j，是一个日志的实现。

为什么有了Commons Logging和Log4j，又会蹦出来SLF4J和Logback？

这是因为Java有着非常悠久的开源历史，不但OpenJDK本身是开源的，而且我们用到的第三方库，几乎全部都是开源的。

开源生态丰富的一个特定就是，同一个功能，可以找到若干种互相竞争的开源库。

因为对Commons Logging的接口不满意，有人就搞了SLF4J。因为对Log4j的性能不满意，有人就搞了Logback。

我们先来看看SLF4J对Commons Logging的接口有何改进。

在Commons Logging中，我们要打印日志，有时候得这么写：

```java
int score = 99;
p.setScore(score);
log.info("Set score " + score + " for Person " + p.getName() + " ok.");
```

拼字符串是一个非常麻烦的事情，所以SLF4J的日志接口改进成这样了：

```java
int score = 99;
p.setScore(score);
logger.info("Set score {} for Person {} ok.", score, p.getName());
```

我们靠猜也能猜出来，SLF4J的日志接口传入的是一个带占位符的字符串，用后面的变量自动替换占位符，所以看起来更加自然。

如何使用SLF4J？它的接口实际上和Commons Logging几乎一模一样：

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

class Main {
    final Logger logger = LoggerFactory.getLogger(getClass());
}
```

对比一下Commons Logging和SLF4J的接口：

```
Commons Logging	                             SLF4J
org.apache.commons.logging.Log	             org.slf4j.Logger
org.apache.commons.logging.LogFactory	     org.slf4j.LoggerFactory
```

不同之处就是Log变成了Logger，LogFactory变成了LoggerFactory。

使用SLF4J和Logback和前面讲到的使用Commons Logging加Log4j是类似的，先分别下载[SLF4J](https://www.slf4j.org/download.html)和[Logback](https://logback.qos.ch/download.html)，然后把以下jar包放到classpath下：

- slf4j-api-1.7.x.jar
- logback-classic-1.2.x.jar
- logback-core-1.2.x.jar

然后使用SLF4J的Logger和LoggerFactory即可。和Log4j类似，我们仍然需要一个Logback的配置文件，把logback.xml放到classpath下，配置如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

	<appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
		<encoder>
			<pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
		</encoder>
	</appender>

	<appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
		<encoder>
			<pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
			<charset>utf-8</charset>
		</encoder>
		<file>log/output.log</file>
		<rollingPolicy class="ch.qos.logback.core.rolling.FixedWindowRollingPolicy">
			<fileNamePattern>log/output.log.%i</fileNamePattern>
		</rollingPolicy>
		<triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">
			<MaxFileSize>1MB</MaxFileSize>
		</triggeringPolicy>
	</appender>

	<root level="INFO">
		<appender-ref ref="CONSOLE" />
		<appender-ref ref="FILE" />
	</root>
</configuration>
```

运行即可获得类似如下的输出：

13:15:25.328 [main] INFO  com.itranswarp.learnjava.Main - Start process...
从目前的趋势来看，越来越多的开源项目从Commons Logging加Log4j转向了SLF4J加Logback。

# 反射

## Class 类
除了 int 等基本类型外，java 的其他类型全部都是 class(包括 interface)。例如

- String
- Object
- Runnable
- Exception
- ...

可以得出结论:class (包括interface) 的本质是数据类型 (Type) 无继承关系的数据类型无法赋值

```java
Number n = new Double(123.456); // OK
String s = new Double(123.456); // compile error!
```

而 class 是由 JVM 在执行过程中动态加载的。JVM 在第一次读到一种 class 类型时，将其加载进内存

每加载一种 class，JVM 就为其创建一个 class 类型的实例，并关联起来，注意：这里的 Class 类型是一个名叫 Class 的 class ，长这样

```java
public final class Class {
    private Class() {}
}
```

以 String 类为例，当 JVM加载 String 类时，他首先读取 String.class 文件到内存，然后，为 String 类创建一个 Class 实例并关联起来：

```java
Class cls = new Class(String);
```

这个 Class 实例是 JVM 内部创建的，如果我们查看 JDK源码，可以发现 Class类的构造方法是 private ，只有JVM 能创建 Class 实例，我们自己的 Java 程序是无法创建 Class 实例的

所以，JVM 持有的每个 Class 实例都指向一个数据类型(class 或 interface)

```
┌───────────────────────────┐
│      Class Instance       │──────> String
├───────────────────────────┤
│name = "java.lang.String"  │
└───────────────────────────┘
┌───────────────────────────┐
│      Class Instance       │──────> Random
├───────────────────────────┤
│name = "java.util.Random"  │
└───────────────────────────┘
┌───────────────────────────┐
│      Class Instance       │──────> Runnable
├───────────────────────────┤
│name = "java.lang.Runnable"│
└───────────────────────────┘
```

一个 Class 实例包含了该 class 的所有完整信息

```
┌───────────────────────────┐
│      Class Instance       │──────> String
├───────────────────────────┤
│name = "java.lang.String"  │
├───────────────────────────┤
│package = "java.lang"      │
├───────────────────────────┤
│super = "java.lang.Object" │
├───────────────────────────┤
│interface = CharSequence...│
├───────────────────────────┤
│field = value[],hash,...   │
├───────────────────────────┤
│method = indexOf()...      │
└───────────────────────────┘
```

由于 JVM 为每个加载的 class 创建了对应的 Class 实例，并在实例中保存了该 class 的所有信息，包括类名，包名，父类，实现的接口，所有方法，字段等，因此，如果获取了某个 Class 实例，我们就可以通过这个 Class 实例获取到该实例对应的 class 的所有信息

这种通过 Class 实例获取 class 信息的方法称为反射 (Reflection)

如何获取一个 class 的 Class 实例？

方法一：直接通过一个 class 的静态变量 class 获取：
```java
Class cls = String.class;
```

方法二：如果我们有一个实例变量，可以通过该实例变量提供的 getClass() 方法获取：
```java
String s = "Hello";
Class cls = s.getClass();
```

方法三：如果知道一个 class 的完整类名，可以通过静态方法 Class.forName()获取：
```java
Class cls = Class.forName("java.lang.String");
```

因为 Class 实例在 JVM 中是唯一的，所以，上述方法获取的 Class 实例是同一个实例。可以用 == 比较两个 Class实例：

```java
Class cls1 = String.class;

String s = "Hello";
Class cls2 = s.getClass();

boolean sameClass = cls1 == cls2; // true
```

注意 Class 实例比较和 instanceof 的差别

```java
Integer n = new Integer(123);

boolean b1 = n instanceof Integer; // true，因为n是Integer类型
boolean b2 = n instanceof Number; // true，因为n是Number类型的子类

boolean b3 = n.getClass() == Integer.class; // true，因为n.getClass()返回Integer.class
boolean b4 = n.getClass() == Number.class; // false，因为Integer.class!=Number.class
```

用 instanceof 补番匹配指定类型，还匹配指定类型的子类。而用 == 判断 class 实例可以精确地判断数据类型，但不能做子类比较

通常情况下，我们应该用 instanceof 判断数据类型，因为面向抽象编程的时候，我么不关心具体的子类型，只有在需要精确判断一个类型是不是某个 class 的时候，我们才使用 == 判断 class 实例

因为反射的目的是为了获得某个实例的信息。因此，当我们拿到某个 Object 实例时。我们可以通过反射该 Object 的 class 信息

```java
void printObjectInfo(Object obj) {
    Class cls = obj.getClass();
}
```

要从 Class 实例获取获取的基本信息，参考如下：

```java
public class Main {
    public static void main(String[] args) {
        printClassInfo("".getClass());
        printClassInfo(Runnable.class);
        printClassInfo(java.time.Month.class);
        printClassInfo(String[].class);
        printClassInfo(int.class);
    }

    static void printClassInfo(Class cls) {
        System.out.println("Class name: " + cls.getName());
        System.out.println("Simple name: " + cls.getSimpleName());
        if (cls.getPackage() != null) {
            System.out.println("Package name: " + cls.getPackage().getName());
        }
        System.out.println("is interface: " + cls.isInterface());
        System.out.println("is enum: " + cls.isEnum());
        System.out.println("is array: " + cls.isArray());
        System.out.println("is primitive: " + cls.isPrimitive());
    }
}
```

注意到数组（例如String[]）也是一种Class，而且不同于String.class，它的类名是[Ljava.lang.String。此外，JVM为每一种基本类型如int也创建了Class，通过int.class访问。

如果获取到了一个Class实例，我们就可以通过该Class实例来创建对应类型的实例：

```java
// 获取String的Class实例:
Class cls = String.class;
// 创建一个String实例:
String s = (String) cls.newInstance();
```

上述代码相当于 new String()。通过 Class.newInstance() 可以创建类实例，它的局限是：只能调用 public 的无参数构造方法。带参数的构造方法，或者非 public 的构造方法都无法通过Class.newInstance() 被调用。

### 动态加载
JVM在执行Java程序的时候，并不是一次性把所有用到的class全部加载到内存，而是第一次需要用到class时才加载。例如：

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        if (args.length > 0) {
            create(args[0]);
        }
    }

    static void create(String name) {
        Person p = new Person(name);
    }
}
```

当执行 Main.java 时，由于用到了 Main，因此，JVM 首先会把 Main.class 加载到内存。然而，并不会加载 Person.class，除非程序执行到 create() 方法，JVM发现需要加载 Person 类时，才会首次加载 Person.class。如果没有执行 create() 方法，那么 Person.class 根本就不会被加载。

这就是 JVM 动态加载 class 的特性。

动态加载 class 的特性对于 Java 程序非常重要。利用 JVM 动态加载 class 的特性，我们才能在运行期根据条件加载不同的实现类。例如，Commons Logging 总是优先使用 Log4j，只有当 Log4j不存在时，才使用 JDK 的 logging。利用 JVM 动态加载特性，大致的实现代码如下：

```java
// Commons Logging优先使用Log4j:
LogFactory factory = null;
if (isClassPresent("org.apache.logging.log4j.Logger")) {
    factory = createLog4j();
} else {
    factory = createJdkLog();
}

boolean isClassPresent(String name) {
    try {
        Class.forName(name);
        return true;
    } catch (Exception e) {
        return false;
    }
}
```

这就是为什么我们只需要把Log4j的jar包放到classpath中，Commons Logging就会自动使用Log4j的原因。

## 访问字段

对任意的一个 Object 实例，只要我们获取了它的 Class，就可以获取它的一切信息。

我们先看看如何通过 Class 实例获取字段信息。Class 类提供了以下几个方法来获取字段：

- Field getField(name)：根据字段名获取某个public的field（包括父类）
- Field getDeclaredField(name)：根据字段名获取当前类的某个field（不包括父类）
- Field[] getFields()：获取所有public的field（包括父类）
- Field[] getDeclaredFields()：获取当前类的所有field（不包括父类）

示例代码：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Class stdClass = Student.class;
        // 获取public字段"score":
        System.out.println(stdClass.getField("score"));
        // 获取继承的public字段"name":
        System.out.println(stdClass.getField("name"));
        // 获取private字段"grade":
        System.out.println(stdClass.getDeclaredField("grade"));
    }
}

class Student extends Person {
    public int score;
    private int grade;
}

class Person {
    public String name;
}
```

上述代码首先获取Student的Class实例，然后，分别获取public字段、继承的public字段以及private字段，打印出的Field类似：

```
public int Student.score
public java.lang.String Person.name
private int Student.grade
```

一个 Field 对象包含了一个字段所有信息：

- getName()：返回字段名称，例如，"name"；
- getType()：返回字段类型，也是一个Class实例，例如，String.class；
- getModifiers()：返回字段的修饰符，它是一个int，不同的bit表示不同的含义。

以 String 类的value 字段为例，它的定义是：

```java
public final class String {
    private final byte[] value;
}
```

用反射获取该字段的信息，代码如下：

```java
Field f = String.class.getDeclaredField("value");
f.getName(); // "value"
f.getType(); // class [B 表示byte[]类型
int m = f.getModifiers();
Modifier.isFinal(m); // true
Modifier.isPublic(m); // false
Modifier.isProtected(m); // false
Modifier.isPrivate(m); // true
Modifier.isStatic(m); // false
```

### 获取字段值

利用反射拿到字段的一个Field实例只是第一步，我们还可以拿到一个实例对应的该字段的值。

例如，对于一个Person实例，我们可以先拿到name字段对应的Field，再获取这个实例的name字段的值：

```java
public class Main {

    public static void main(String[] args) throws Exception {
        Object p = new Person("Xiao Ming");
        Class c = p.getClass();
        Field f = c.getDeclaredField("name");
        Object value = f.get(p);
        System.out.println(value); // "Xiao Ming"
    }
}

class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }
}
```

述代码先获取Class实例，再获取Field实例，然后，用Field.get(Object)获取指定实例的指定字段的值。

运行代码，如果不出意外，会得到一个IllegalAccessException，这是因为name被定义为一个private字段，正常情况下，Main类无法访问Person类的private字段。要修复错误，可以将private改为public，或者，在调用Object value = f.get(p);前，先写一句：

```java
f.setAccessible(true);
```

调用 Field.setAccessible(true) 的意思是，别管这个字段是不是 public，一律允许访问。

可以试着加上上述语句，再运行代码，就可以打印出 private 字段的值。

有童鞋会问：如果使用反射可以获取 private 字段的值，那么类的封装还有什么意义？

答案是正常情况下，我们总是通过 p.name 来访问 Person 的 name 字段，编译器会根据 public、protected 和 private 决定是否允许访问字段，这样就达到了数据封装的目的。

而反射是一种非常规的用法，使用反射，首先代码非常繁琐，其次，它更多地是给工具或者底层框架来使用，目的是在不知道目标实例任何信息的情况下，获取特定字段的值。

此外，setAccessible(true) 可能会失败。如果 JVM 运行期存在 SecurityManager，那么它会根据规则进行检查，有可能阻止 setAccessible(true)。例如，某个 SecurityManager 可能不允许对 java 和 javax 开头的 package 的类调用 setAccessible(true)，这样可以保证 JVM 核心库的安全。

### 设置字段值
通过 Field 实例既然可以获取到指定实例的字段值，自然也可以设置字段的值。

设置字段值是通过 Field.set(Object, Object) 实现的，其中第一个 Object 参数是指定的实例，第二个 Object 参数是待修改的值。示例代码如下：

```java
public class Main {

    public static void main(String[] args) throws Exception {
        Person p = new Person("Xiao Ming");
        System.out.println(p.getName()); // "Xiao Ming"
        Class c = p.getClass();
        Field f = c.getDeclaredField("name");
        f.setAccessible(true);
        f.set(p, "Xiao Hong");
        System.out.println(p.getName()); // "Xiao Hong"
    }
}

class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}
```

运行上述代码，打印的 name 字段从Xiao Ming变成了Xiao Hong，说明通过反射可以直接修改字段的值。

同样的，修改非 public 字段，需要首先调用setAccessible(true)。

### 小结

- Java的反射API提供的Field类封装了字段的所有信息：

- 通过Class实例的方法可以获取Field实例：getField()，getFields()，getDeclaredField()，getDeclaredFields()；

- 通过Field实例可以获取字段信息：getName()，getType()，getModifiers()；

- 通过Field实例可以读取或设置某个对象的字段，如果存在访问限制，要首先调用setAccessible(true)来访问非public字段。

- 通过反射读写字段是一种非常规方法，它会破坏对象的封装。

## 调用方法

我们已经能通过Class实例获取所有Field对象，同样的，可以通过Class实例获取所有Method信息。Class类提供了以下几个方法来获取Method：

- Method getMethod(name, Class...)：获取某个public的Method（包括父类）
- Method getDeclaredMethod(name, Class...)：获取当前类的某个Method（不包括父类）
- Method[] getMethods()：获取所有public的Method（包括父类）
- Method[] getDeclaredMethods()：获取当前类的所有Method（不包括父类）

我们来看一下示例代码：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Class stdClass = Student.class;
        // 获取public方法getScore，参数为String:
        System.out.println(stdClass.getMethod("getScore", String.class));
        // 获取继承的public方法getName，无参数:
        System.out.println(stdClass.getMethod("getName"));
        // 获取private方法getGrade，参数为int:
        System.out.println(stdClass.getDeclaredMethod("getGrade", int.class));
    }
}

class Student extends Person {
    public int getScore(String type) {
        return 99;
    }
    private int getGrade(int year) {
        return 1;
    }
}

class Person {
    public String getName() {
        return "Person";
    }
}
```

上述代码首先获取Student的Class实例，然后，分别获取public方法、继承的public方法以及private方法，打印出的Method类似：

```
public int Student.getScore(java.lang.String)
public java.lang.String Person.getName()
private int Student.getGrade(int)
```

一个Method对象包含一个方法的所有信息：

- getName()：返回方法名称，例如："getScore"；
- getReturnType()：返回方法返回值类型，也是一个Class实例，例如：String.class；
- getParameterTypes()：返回方法的参数类型，是一个Class数组，例如：{String.class, int.class}；
- getModifiers()：返回方法的修饰符，它是一个int，不同的bit表示不同的含义。

### 调用方法
当我们获取到一个 Method 对象时，就可以对它进行调用。我们以下面的代码为例：

```java
String s = "Hello world";
String r = s.substring(6); // "world"
```

如果用反射来调用substring方法，需要以下代码：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        // String对象:
        String s = "Hello world";
        // 获取String substring(int)方法，参数为int:
        Method m = String.class.getMethod("substring", int.class);
        // 在s对象上调用该方法并获取结果:
        String r = (String) m.invoke(s, 6);
        // 打印调用结果:
        System.out.println(r);
    }
}
```

注意到 substring() 有两个重载方法，我们获取的是 String substring(int) 这个方法。思考一下如何获取 String substring(int, int) 方法。

对 Method 实例调用 invoke 就相当于调用该方法，invoke 的第一个参数是对象实例，即在哪个实例上调用该方法，后面的可变参数要与方法参数一致，否则将报错。

### 调用静态方法
如果获取到的 Method 表示一个静态方法，调用静态方法时，由于无需指定实例对象，所以 invoke 方法传入的第一个参数永远为 null。我们以I nteger.parseInt(String) 为例：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        // 获取Integer.parseInt(String)方法，参数为String:
        Method m = Integer.class.getMethod("parseInt", String.class);
        // 调用该静态方法并获取结果:
        Integer n = (Integer) m.invoke(null, "12345");
        // 打印调用结果:
        System.out.println(n);
    }
}
```

### 调用非 public 方法
和 Field 类似，对于非 public 方法，我们虽然可以通过 Class.getDeclaredMethod() 获取该方法实例，但直接对其调用将得到一个 IllegalAccessException。为了调用非 public 方法，我们通过 Method.setAccessible(true) 允许其调用：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Person p = new Person();
        Method m = p.getClass().getDeclaredMethod("setName", String.class);
        m.setAccessible(true);
        m.invoke(p, "Bob");
        System.out.println(p.name);
    }
}

class Person {
    String name;
    private void setName(String name) {
        this.name = name;
    }
}
```

此外，setAccessible(true) 可能会失败。如果JVM运行期存在 SecurityManager，那么它会根据规则进行检查，有可能阻止 setAccessible(true)。例如，某个 SecurityManager 可能不允许对 java 和 javax 开头的 package 的类调用 setAccessible(true)，这样可以保证JVM核心库的安全。

### 多态

我们来考察这样一种情况：一个 Person 类定义了 hello() 方法，并且它的子类 Student 也覆写了 hello() 方法，那么，从 Person.class 获取的 Method，作用于 Student 实例时，调用的方法到底是哪个？

```java
public class Main {
    public static void main(String[] args) throws Exception {
        // 获取Person的hello方法:
        Method h = Person.class.getMethod("hello");
        // 对Student实例调用hello方法:
        h.invoke(new Student());
    }
}

class Person {
    public void hello() {
        System.out.println("Person:hello");
    }
}

class Student extends Person {
    public void hello() {
        System.out.println("Student:hello");
    }
}
```

运行上述代码，发现打印出的是 Student:hello，因此，使用反射调用方法时，仍然遵循多态原则：即总是调用实际类型的覆写方法（如果存在）。上述的反射代码：

```java
Method m = Person.class.getMethod("hello");
m.invoke(new Student());
```

实际上相当于：

```java
Person p = new Student();
p.hello();
```

### 小结
- Java的反射API提供的Method对象封装了方法的所有信息：

- 通过Class实例的方法可以获取Method实例：getMethod()，getMethods()，getDeclaredMethod()，getDeclaredMethods()；

- 通过Method实例可以获取方法信息：getName()，getReturnType()，getParameterTypes()，getModifiers()；

- 通过Method实例可以调用某个对象的方法：Object invoke(Object instance, Object... parameters)；

- 通过设置setAccessible(true)来访问非public方法；

- 通过反射调用方法时，仍然遵循多态原则。

## 调用构造方法

## 获取继承关系

## 动态代理

# 注解

## 使用注解

注解（Annotation）是放在Java源码的类、方法、字段、参数前的一种特殊“注释”：

```java
// this is a component:
@Resource("hello")
public class Hello {
    @Inject
    int n;

    @PostConstruct
    public void hello(@Param String name) {
        System.out.println(name);
    }

    @Override
    public String toString() {
        return "Hello";
    }
}
```

注释会被编译器直接忽略，注解则可以被编译器打包进入class文件，因此，注解是一种用作标注的“元数据”。

### 注解的作用

从JVM的角度看，注解本身对代码逻辑没有任何影响，如何使用注解完全由工具决定。

Java的注解可以分为三类：

第一类是由编译器使用的注解，例如：

- @Override：让编译器检查该方法是否正确地实现了覆写；
- @SuppressWarnings：告诉编译器忽略此处代码产生的警告。

这类注解不会被编译进入 .class 文件，它们在编译后就被编译器扔掉了。

第二类是由工具处理 .class 文件使用的注解，比如有些工具会在加载 class 的时候，对 class 做动态修改，实现一些特殊的功能，这类注解会被编译进入 .class 文件，但加载结束后并不会存在于内存中。这类注解只被一些底层库使用，一般我们不必自己处理

第三类是程序运行期能够读取的注释，他们在加载后一直存在于 JVM 中，这也是最常用给的注解。例如，一个配置了 @PostConstruct 的方法会在调用构造方法后自动被调用(这是Java代码读取该注解实现的功能，JVM并不会识别该注解)

定义一个注解时，还可以定义配置参数，配置参数可以包括：

- 所有基本类型
- String
- 枚举类型
- 基本类型，String以及枚举的数组

因为配置参数必须是常量，所以，上述限制保证了注解在定义时就已经确定了每个参数的值

注解的配置参数可以有默认值，缺少某个配置参数时将使用默认值

此外，大部分注解会有一个名为 value 的配置参数，对此参数赋值，可以只写常量，相当于省略了 vlaue 参数

如果只写注解，相当于全部使用默认值

```java
public class Hello {
    @Check(min=0, max=100, value=55)
    public int n;

    @Check(value=99)
    public int p;

    @Check(99) // @Check(value=99)
    public int x;

    @Check
    public int y;
}
```

@Check就是一个注解。第一个@Check(min=0, max=100, value=55)明确定义了三个参数，第二个@Check(value=99)只定义了一个value参数，它实际上和@Check(99)是完全一样的。最后一个@Check表示所有参数都使用默认值。

### 小结
- 注解（Annotation）是Java语言用于工具处理的标注：

- 注解可以配置参数，没有指定配置的参数使用默认值；

- 如果参数名称是value，且只有一个参数，那么可以省略参数名称。

## 定义注解

Java语言使用 @interface 语法来定义注解（Annotation），它的格式如下：

```java
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

注解的参数类似无参数方法，可以用default设定一个默认值（强烈推荐）。最常用的参数应当命名为value。

### 元注解
有一些注解可以修饰其他注解，这些注解就称为元注解（meta annotation）。Java标准库已经定义了一些元注解，我们只需要使用元注解，通常不需要自己去编写元注解。

#### @Target

最常用的元注解是@Target。使用@Target可以定义Annotation能够被应用于源码的哪些位置：

- 类或接口：ElementType.TYPE；
- 字段：ElementType.FIELD；
- 方法：ElementType.METHOD；
- 构造方法：ElementType.CONSTRUCTOR；
- 方法参数：ElementType.PARAMETER。

例如，定义注解@Report可用在方法上，我们必须添加一个@Target(ElementType.METHOD)：

```java
@Target(ElementType.METHOD)
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

定义注解@Report可用在方法或字段上，可以把@Target注解参数变为数组{ ElementType.METHOD, ElementType.FIELD }：

```java
@Target({
    ElementType.METHOD,
    ElementType.FIELD
})
public @interface Report {
    ...
}
```

实际上@Target定义的value是ElementType[]数组，只有一个元素时，可以省略数组的写法。

#### @Retention

另一个重要的元注解@Retention定义了Annotation的生命周期：

- 仅编译期：RetentionPolicy.SOURCE；
- 仅class文件：RetentionPolicy.CLASS；
- 运行期：RetentionPolicy.RUNTIME。

如果@Retention不存在，则该Annotation默认为CLASS。因为通常我们自定义的Annotation都是RUNTIME，所以，务必要加上@Retention(RetentionPolicy.RUNTIME)这个元注解：

```java
@Retention(RetentionPolicy.RUNTIME)
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

#### @Repeatable

使用@Repeatable这个元注解可以定义Annotation是否可重复。这个注解应用不是特别广泛。

```java
@Repeatable
@Target(ElementType.TYPE)
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

经过@Repeatable修饰后，在某个类型声明处，就可以添加多个@Report注解：

```java
@Report(type=1, level="debug")
@Report(type=2, level="warning")
public class Hello {
}
```

#### @Inherited

使用@Inherited定义子类是否可继承父类定义的Annotation。@Inherited仅针对@Target(ElementType.TYPE)类型的annotation有效，并且仅针对class的继承，对interface的继承无效：

```java
@Inherited
@Target(ElementType.TYPE)
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

在使用的时候，如果一个类用到了@Report：

```java
@Report(type=1)
public class Person {
}

```
则它的子类默认也定义了该注解：

```java
public class Student extends Person {
}
```

### 如何定义Annotation

我们总结一下定义Annotation的步骤：

第一步，用@interface定义注解：

```java
public @interface Report {
}
```

第二步，添加参数、默认值：

```java
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

把最常用的参数定义为value()，推荐所有参数都尽量设置默认值。

第三步，用元注解配置注解：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

其中，必须设置@Target和@Retention，@Retention一般设置为RUNTIME，因为我们自定义的注解通常要求在运行期读取。一般情况下，不必写@Inherited和@Repeatable。

## 处理注解
Java 的注解本身对代码的逻辑没有任何影响。根据@Retention的配置：

- SOURCE类型的注解在编译期就被丢掉了；
- CLASS类型的注解仅保存在class文件中，它们不会被加载进JVM；
- RUNTIME类型的注解会被加载进JVM，并且在运行期可以被程序读取。

如何使用注解完全由工具决定。SOURCE类型的注解主要由编译器使用，因此我们一般只使用，不编写。CLASS类型的注解主要由底层工具库使用，涉及到class的加载，一般我们很少用到。只有RUNTIME类型的注解不但要使用，还经常需要编写。

因此，我们只讨论如何读取RUNTIME类型的注解。

因为注解定义后也是一种class，所有的注解都继承自java.lang.annotation.Annotation，因此，读取注解，需要使用反射API。

Java提供的使用反射API读取Annotation的方法包括：

判断某个注解是否存在于Class、Field、Method或Constructor：

- Class.isAnnotationPresent(Class)
- Field.isAnnotationPresent(Class)
- Method.isAnnotationPresent(Class)
- Constructor.isAnnotationPresent(Class)

例如：
```java
// 判断@Report是否存在于Person类:
Person.class.isAnnotationPresent(Report.class);
```

使用反射API读取Annotation：

- Class.getAnnotation(Class)
- Field.getAnnotation(Class)
- Method.getAnnotation(Class)
- Constructor.getAnnotation(Class)

例如：

```java
// 获取Person定义的@Report注解:
Report report = Person.class.getAnnotation(Report.class);
int type = report.type();
String level = report.level();
```

使用反射API读取Annotation有两种方法。方法一是先判断Annotation是否存在，如果存在，就直接读取：

```java
Class cls = Person.class;
if (cls.isAnnotationPresent(Report.class)) {
    Report report = cls.getAnnotation(Report.class);
    ...
}
```

第二种方法是直接读取Annotation，如果Annotation不存在，将返回null：

```java
Class cls = Person.class;
Report report = cls.getAnnotation(Report.class);
if (report != null) {
   ...
}
```

读取方法、字段和构造方法的 Annotation 和 Class 类似。但要读取方法参数的 Annotation 就比较麻烦一点，因为方法参数本身可以看成一个数组，而每个参数又可以定义多个注解，所以，一次获取方法参数的所有注解就必须用一个二维数组来表示。例如，对于以下方法定义的注解：

```java
public void hello(@NotNull @Range(max=5) String name, @NotNull String prefix) {
}
```

要读取方法参数的注解，我们先用反射获取Method实例，然后读取方法参数的所有注解：

```java
// 获取Method实例:
Method m = ...
// 获取所有参数的Annotation:
Annotation[][] annos = m.getParameterAnnotations();
// 第一个参数（索引为0）的所有Annotation:
Annotation[] annosOfName = annos[0];
for (Annotation anno : annosOfName) {
    if (anno instanceof Range) { // @Range注解
        Range r = (Range) anno;
    }
    if (anno instanceof NotNull) { // @NotNull注解
        NotNull n = (NotNull) anno;
    }
}
```

### 使用注解
注解如何使用，完全由程序自己决定。例如，JUnit是一个测试框架，它会自动运行所有标记为@Test的方法。

我们来看一个@Range注解，我们希望用它来定义一个String字段的规则：字段长度满足@Range的参数定义：

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface Range {
    int min() default 0;
    int max() default 255;
}
```

在某个JavaBean 中，我们可以使用该注解

```java
public class Person {
    @Range(min=1, max=20)
    public String name;

    @Range(max=10)
    public String city;
}
```

但是，定义了注解，本身对程序逻辑没有任何影响。我们必须自己编写代码来使用注解。这里，我们编写一个Person实例的检查方法，它可以检查Person实例的String字段长度是否满足@Range的定义：

```java
void check(Person person) throws IllegalArgumentException, ReflectiveOperationException {
    // 遍历所有Field:
    for (Field field : person.getClass().getFields()) {
        // 获取Field定义的@Range:
        Range range = field.getAnnotation(Range.class);
        // 如果@Range存在:
        if (range != null) {
            // 获取Field的值:
            Object value = field.get(person);
            // 如果值是String:
            if (value instanceof String) {
                String s = (String) value;
                // 判断值是否满足@Range的min/max:
                if (s.length() < range.min() || s.length() > range.max()) {
                    throw new IllegalArgumentException("Invalid field: " + field.getName());
                }
            }
        }
    }
}
```

这样一来，我们通过@Range注解，配合check()方法，就可以完成Person实例的检查。注意检查逻辑完全是我们自己编写的，JVM不会自动给注解添加任何额外的逻辑。

# 泛型

## 什么是泛型

在讲解什么是泛型之前，先观察下 java 标准库提供的 ArrayList ，它可以看做"可变长度"的数组，因为用起来比数组方便

世界上 ArrayList 内不就是一个 Object[] 数组，配合存储一个当前分配的长度，就可以充当"可变数组"

```java
public class ArrayList {
    private Object[] array;
    private int size;
    public void add(Object e) {...}
    public void remove(int index) {...}
    public Object get(int index) {...}
}
```

如果用上述 ArrayList 存储 String 类型，总会有这么几个缺点

- 需要强制转型
- 不方便，易出错

例如，代码必须这么写

```java
ArrayList list = new ArrayList();
list.add("Hello");
// 获取到Object，必须强制转型为String:
String first = (String) list.get(0);
```

要解决上述问题，我们可以为 String 单独编写一种 ArrayList 

```java
public class StringArrayList {
    private String[] array;
    private int size;
    public void add(String e) {...}
    public void remove(int index) {...}
    public String get(int index) {...}
}
```

这样一来，存入的必须是 String 取出的也一定是 String 不需要强制转型，因为编译器会强制检查放入的类型

```java
StringArrayList list = new StringArrayList();
list.add("Hello");
String first = list.get(0);
// 编译错误: 不允许放入非String类型:
list.add(new Integer(123));
```

问题暂时解决

然而新的问题是，如果要存储 Integer，还需要为 Integer 单独编写一种 ArrayList

```java
public class IntegerArrayList {
    private Integer[] array;
    private int size;
    public void add(Integer e) {...}
    public void remove(int index) {...}
    public Integer get(int index) {...}
}
```

实际上还需要为其他所有class单独编写一种 ArrayList

- LongArrayList
- DoubleArrayList
- PersonArrayList
- ...

这是不可能的，JDK的class就有上千个，而且他还不知道其他人编写的class

为了解决新的问题，我们必须把 ArrayList 变成一种模板：`ArrayList<T>`，代码如下

```java
public class ArrayList<T> {
    private T[] array;
    private int size;
    public void add(T e) {...}
    public void remove(int index) {...}
    public T get(int index) {...}
}
```

T 可以是任何class，这样一来，我们就实现了：编写一次模板，可以创建任意类型的 ArrayList

```java
// 创建可以存储String的ArrayList:
ArrayList<String> strList = new ArrayList<String>();
// 创建可以存储Float的ArrayList:
ArrayList<Float> floatList = new ArrayList<Float>();
// 创建可以存储Person的ArrayList:
ArrayList<Person> personList = new ArrayList<Person>();
```

因此，泛型就是定义一种模板，例如 `ArrayList<T>` ，然后在代码中为用到的类创建对应的 ArrayList<类型>

```java
ArrayList<String> strList = new ArrayList<String>();
```

由编译器针对类型做检查

```java
strList.add("hello"); // OK
String s = strList.get(0); // OK
strList.add(new Integer(123)); // compile error!
Integer n = strList.get(0); // compile error!
```

这样一来，既实现了编写一次，万能匹配，又通过编译器保证了类型安全：这就是泛型。

### 向上转型

在 Java 标准库中的 `ArrayList<T>` 实现了 `List<T>` 接口，它可以向上转型为`List<T>`

```java
public class ArrayList<T> implements List<T> {
    ...
}

List<String> list = new ArrayList<String>();
```

即类型 `ArrayList<T>` 可以向上转型为 `List<T>`

要`特别注意`：不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`或`List<Number>`。

这是为什么呢？假设`ArrayList<Integer>`可以向上转型为`ArrayList<Number>`，观察一下代码：

```java
// 创建ArrayList<Integer>类型：
ArrayList<Integer> integerList = new ArrayList<Integer>();
// 添加一个Integer：
integerList.add(new Integer(123));
// “向上转型”为ArrayList<Number>：
ArrayList<Number> numberList = integerList;
// 添加一个Float，因为Float也是Number：
numberList.add(new Float(12.34));
// 从ArrayList<Integer>获取索引为1的元素（即添加的Float）：
Integer n = integerList.get(1); // ClassCastException!
```

我们把一个`ArrayList<Integer>`转型为`ArrayList<Number>`类型后，这个`ArrayList<Number>`就可以接受 Float 类型，因为 Float 是 Number 的子类。但是，`ArrayList<Number>`实际上和`ArrayList<Integer>`是同一个对象，也就是`ArrayList<Integer>`类型，它不可能接受 Float 类型， 所以在获取 Integer 的时候将产生ClassCastException。

实际上，编译器为了避免这种错误，根本就不允许把`ArrayList<Integer>`转型为`ArrayList<Number>`。

>ArrayList<Integer>和ArrayList<Number>两者完全没有继承关系。

### 小结
- 泛型就是编写模板代码来适应任意类型；

- 泛型的好处是使用时不必对类型进行强制转换，它通过编译器对类型进行检查；

- 注意泛型的继承关系：可以把`ArrayList<Integer>`向上转型为`List<Integer>`（T不能变！），但不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`（T不能变成父类）。

## 使用泛型

使用 ArrayList时，如果不定义泛型类型时，泛型类型实际上就是 Object

```java
// 编译器警告:
List list = new ArrayList();
list.add("Hello");
list.add("World");
String first = (String) list.get(0);
String second = (String) list.get(1);
```

此时，只能把`<T>`当做 Object使用，没有发挥泛型的优势

当我们定义泛型类型`<String>`后，list`<T>`的泛型接口变为强类型List`<String>`

```java 
// 无编译器警告:
List<String> list = new ArrayList<String>();
list.add("Hello");
list.add("World");
// 无强制转型:
String first = list.get(0);
String second = list.get(1);
```

当我们定义泛型类型`<Number>`后，List`<T>`的泛型接口变为强类型List`<Number>`

```java
List<Number> list = new ArrayList<Number>();
list.add(new Integer(123));
list.add(new Double(12.34));
Number first = list.get(0);
Number second = list.get(1);
```

编译器如果能自动推断出泛型类型，就可以生落后后面的泛型类型。
例：
```java
List<Number> list = new ArrayList<Number>();
```

编译器看到泛型类型 List`<Number>` 就可以自动推断出后面的 ArrayList`<T>`的泛型类型必须是ArrayList`<Number>` 因此，可以把代码简写为

```java
// 可以省略后面的Number，编译器可以自动推断泛型类型：
List<Number> list = new ArrayList<>();
```

### 泛型接口
除了ArrayList`<T>` 使用了泛型，还可以在接口中使用泛型，例如，Arrays.sort(Object[])可以对任意数组进行排序，但待排序的元素必须实现 Comparable`<T>` 这个泛型接口

```java
public interface Comparable<T> {
    /**
     * 返回-1: 当前实例比参数o小
     * 返回0: 当前实例与参数o相等
     * 返回1: 当前实例比参数o大
     */
    int compareTo(T o);
}
```

可以直接对 String 数组进行排序

```java
String[] ss = new String[] { "Orange", "Apple", "Pear" };
        Arrays.sort(ss);
        System.out.println(Arrays.toString(ss));

```



## 编写泛型

## 擦拭法

## extends 通配符

## super 通配符

## 泛型和反射

# 集合

## Java 集合简介

什么是集合(Collection) 集合就是 “由若干个确定的元素所构成的整体”。

例如，五只小兔构成的集合

```
┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐

│   (\_(\     (\_/)     (\_/)     (\_/)      (\(\   │
    ( -.-)    (•.•)     (>.<)     (^.^)     (='.')
│  C(")_(")  (")_(")   (")_(")   (")_(")   O(_")")  │

└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
```

在数学中，我们经常遇到集合的概念，例如

- 有限集合
    - 一个班所有的同学构成的集合；
    - 一个网站所有的商品构成的集合；
    - ...

- 无限集合：
    - 全体自然数集合：1,2,3....
    - 有理数集合；
    - 实数集合；
    - ...

为什么要在计算机中引入集合呢?,这是为了便于处理一组类似的数据，例如：

- 列举所有的同学的总成绩和平均成绩
- 列举所有的商品名称和价格
- ...

在 Java 中，如果一个 Java 对象可以再内部持有若干其他 Java 对象，并对外提供访问接口，我们把这种 Java 对象成为集合。很显然，Java 的数组可以看做是一种集合

```java
String[] ss = new String[10]; // 可以持有10个String对象
ss[0] = "Hello"; // 可以放入String对象
String first = ss[0]; // 可以获取String对象
```

既然 Java 提供了数组这种数据类型，可以充当集合，那么，我们为什么还需要其他集合类？这是因为数组有如下限制：

- 数组初始化后大小不可变
- 数组只能按索引顺序存取

因此，我们需要各种不同类型的集合类来处理不同的数据，例如：

- 可变大小的顺序链表；
- 保证无重复元素的集合；
- ...

### Collection

Java 标准库自带的 java.util包提供了集合类：Collection。他是除 Map 外所有其它集合类的根接口。Java 的java.util包主要提供了一下三种类型的集合：

- List：一种有序列表的集合，例如，按索引排列的 Student 的 List
- Set：一种保证没有重复元素的集合，例如，所有无重复名称的 Student 的 Set
- Map：一种通过键值(key-value)查找的映射表集合，例如，根据 Student 的 name 查找对应的 Student 的 Map

Java 集合的设计有几个特点：一是实现了接口和实现类相分离，例如，有序表的接口是 List，具体的实现类有 ArrayList，LinkedList 等，二是支持泛型，我们可以限制在一个集合中只能放入同一种数据类型的元素，例如：

```java
List<String> list = new ArrayList<>(); // 只能放入String类型
```

最后，Java 访问集合总是通过统一的方式--迭代器(Iterator)来实现，它最明显的好处在于无需知道合集内部元素是按什么方式存储的。

由于 Java 的集合设计非常久远，中间经历过大规模改进，我们要注意到有一小部分集合是遗留类，不应该继续使用

- Hashtable：一种线程安全的Map实现；
- Vector：一种线程安全的List实现；
- Stack：基于Vector实现的LIFO的栈。

还有一小部分接口是遗留接口，也不应该继续使用：

- Enumeration<E>：已被Iterator<E>取代。

### 小结

Java 的集合类定义在 java.util 包中，支持泛型，主要提供了3种集合类，包括 List，Set 和Map。Java集合使用统一的 Iterator 遍历，尽量不要使用遗留接口。

## 使用 list

在集合类中，List 是最基础的一种集合：它是一种有序链表。

List 的行为和数组几乎完全相同：List 内部按照放入元素的先后顺序存放，每个元素都可以通过索引确定自己的位置，List 的索引和数组一样，从0开始

数组和 List 类似，也是有序结构，如果我们使用数组，在添加和删除元素的时候，会非常不方便。例如，从一个已有的数组{'A','B','C','D','E'} 中删除索引为2 的元素：

```
┌───┬───┬───┬───┬───┬───┐
│ A │ B │ C │ D │ E │   │
└───┴───┴───┴───┴───┴───┘
              │   │
          ┌───┘   │
          │   ┌───┘
          │   │
          ▼   ▼
┌───┬───┬───┬───┬───┬───┐
│ A │ B │ D │ E │   │   │
└───┴───┴───┴───┴───┴───┘
```

这个"删除"操作实际上是把'C'后面的元素依次往前挪一个位置，而"添加"操作实际上是把指定位置以后的元素都依次向后挪一个位置，腾出来的位置给新加的元素。这两种操作，用数组实现非常麻烦

因此，在实际应用中，需要增删元素的有序列表，我们使用最多的是 ArrayList。 实际上，ArrayList 在内部使用了数组来存储所有的元素。例如，一个 ArrayList 拥有 5 个元素，实际数组大小为 6(即有一个空位)：

```
size=5
┌───┬───┬───┬───┬───┬───┐
│ A │ B │ C │ D │ E │   │
└───┴───┴───┴───┴───┴───┘
```

当添加一个元素并指定索引到 ArrayList 时，ArrayList 自动移动需要移动的元素：

```
size=5
┌───┬───┬───┬───┬───┬───┐
│ A │ B │   │ C │ D │ E │
└───┴───┴───┴───┴───┴───┘
```

然后，往内部指定索引的数组位置添加一个元素，然后把 size 加 1：

```
size=6
┌───┬───┬───┬───┬───┬───┐
│ A │ B │ F │ C │ D │ E │
└───┴───┴───┴───┴───┴───┘
```

继续添加元素，但是数组以满，没有空闲位置的时候，ArrayList 先创建一个更大的新数组，然后把旧数组的所有元素复制到新数组，紧接着用新数组取代旧数组:

```
size=6
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ A │ B │ F │ C │ D │ E │   │   │   │   │   │   │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
```

现在，新数组就有了空位可以继续添加一个元素到数组末尾，同时 size 加 1：

```
size=7
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ A │ B │ F │ C │ D │ E │ G │   │   │   │   │   │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
```

可见，ArrayList 把添加和删除的操作封装起来，让我们操作 List 类似于操作数组，却不用关心内部元素如何移动。

考察 List<E> 接口，可以看到几个主要的接口方法：

- 在末尾添加一个元素：void add(E e)
- 在指定索引添加一个元素：void add(int index, E e)
- 删除指定索引的元素：int remove(int index)
- 删除某个元素：int remove(Object e)
- 获取指定索引的元素：E get(int index)
- 获取链表大小（包含元素的个数）：int size()

但是，实现 List 接口并非只能通过数组(即 ArrayList的实现方式)来实现，另一种 LinkedList 通过"链表"也实现了 List 接口。在 LinkedList 中，它的内部每个元素都指向下一个元素：

```
        ┌───┬───┐   ┌───┬───┐   ┌───┬───┐   ┌───┬───┐
HEAD ──>│ A │ ●─┼──>│ B │ ●─┼──>│ C │ ●─┼──>│ D │   │
        └───┴───┘   └───┴───┘   └───┴───┘   └───┴───┘
```

比较一下 ArrayList 和 LinkedList


-      |        ArrayList	   |    LinkedList
-      |            -          |        -
获取指定元素	    |     速度很快	     | 需要从头开始查找元素
添加元素到末尾	    |      速度很快      |  	速度很快
在指定位置添加/删除  |	   需要移动元素    |   不需要移动元素
内存占用	       |       少	        |      较大

通常情况下，我们总是优先使用 ArrayList

### List 的特点
使用 List 时，我们要关注 List 接口的规范。List 接口允许我们添加重复的元素，即 List 内部的元素可以重复：

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("apple"); // size=1
        list.add("pear"); // size=2
        list.add("apple"); // 允许重复添加元素，size=3
        System.out.println(list.size());
    }
}
```

List 还允许添加 null

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("apple"); // size=1
        list.add(null); // size=2
        list.add("pear"); // size=3
        String second = list.get(1); // null
        System.out.println(second);
    }
}
```

### 创建List
除了使用 ArrayList 和 LinkedList ，还可以通过 List 接口提供的 of() 方法，根据给定元素快速创建 List：

```java
List<Integer> list = List.of(1, 2, 5);
```

但是 List.of() 方法不接受 null 值，如果传入 null ，会抛出 NullPointerException 异常

### 遍历List
和数组类型，我们要遍历一个List，完全可以用 for 循环根据索引配合 get(int) 方法遍历：

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        for (int i=0; i<list.size(); i++) {
            String s = list.get(i);
            System.out.println(s);
        }
    }
}
```

但这种方式并不推荐，一是代码复杂，二因为 get(int) 方法只有 ArrayList 的实现是高效的，换成 LinkedList 后，索引越大，访问速度越慢

所以我们要始终坚持使用迭代器 Iterator 来访问 List。Iterator 本身也是一个对象，但是它是由 List 的实例调用 iterator() 方法的时候创建的。Iterator 对象知道如何遍历一个 List，
并且不同的 List 类型，返回的 Iterator 对象实现也是不同的，但总是具有最高的访问效率

Iterator 对象有两个方法： boolean hasNext()判断是否有下一个元素，E next()返回下一个元素。因此，使用 Iterator 遍历 List 代码如下

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
            String s = it.next();
            System.out.println(s);
        }
    }
}
```

有人可能觉得使用 Iterator 访问 List 的代码比使用索引更复杂，但是，通过 Iterator 遍历 List 永远是最高效的方式，并且，由于 Iterator 遍历是如此常用，所以，Java 的 for each 循环本身就可以帮我们使用 Iterator 遍历，改写上面的代码：

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        for (String s : list) {
            System.out.println(s);
        }
    }
}
```

上面就是编写遍历 List 的常见代码

实际上，只要实现了 Iterable 接口的集合类都可以直接用for each循环来遍历，Java 编译器本身并不知道如何遍历集合对象，但他会自动把 for each 循环编程 Iterator 的调用，原因就在于 Iterable 接口定义了一个 Iterator<E> iterator() 方法，强迫集合类必须返回一个 Iterator 实例。

### List和Array转换
把 List 变为 Array 有三种方法，第一种是调用 toArray()方法直接返回一个 Object[] 数组

```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("apple", "pear", "banana");
        Object[] array = list.toArray();
        for (Object s : array) {
            System.out.println(s);
        }
    }
}
```

这种方法会丢失类型信息，所以实际应用很少

第二种方式是给 toArray(T[]) 传入一个类型相同的 Array，List 内部自动把元素复制到传入的 Array 中

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = List.of(12, 34, 56);
        Integer[] array = list.toArray(new Integer[3]);
        for (Integer n : array) {
            System.out.println(n);
        }
    }
}
```

注意到这个 toArray(T[]) 方法的泛型参数 <T> 并不是List接口定义的泛型参数 <E>，所以，我们实际上可以传入其他类型的数组，例如我们传入 Number 类型的数组，返回值仍然是 Number 类型

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = List.of(12, 34, 56);
        Number[] array = list.toArray(new Number[3]);
        for (Number n : array) {
            System.out.println(n);
        }
    }
}
```

但是，如果我们传入类型不匹配的数组，例如，String[] 类型的数组，由于 List 的元素是 Integer，所以无法放入 String 数组，这个方法会抛出 ArrayStoreException

如果我们传入的数组大小和 List 实际的元素个数不一致怎么办，根据 List接口 的文档，我们可以知道：

如果传入的数组不够大，那么 List 内部会创建一个新的刚好够大的数组，填充后返回；如果传入的数组比 List 元素还要多，那么填充完元素后，身下的数组元素一律填充 null

实际上，最常用的是传入一个"恰好"大小的数组：

```java
Integer[] array = list.toArray(new Integer[list.size()]);
```

最后一种更简洁的写法是通过 List 接口定义的 T[] toArray(IntFunction<T[]> generator)方法：

```java
Integer[] array = list.toArray(Integer[]::new);
```

这种函数式写法我们会在后续讲到。

反过来，把Array变为List就简单多了，通过List.of(T...)方法最简单：

```java
Integer[] array = { 1, 2, 3 };
List<Integer> list = List.of(array);
```

对于JDK 11之前的版本，可以使用Arrays.asList(T...)方法把数组转换成List。

要注意的是，返回的List不一定就是ArrayList或者LinkedList，因为List只是一个接口，如果我们调用List.of()，它返回的是一个只读List：

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = List.of(12, 34, 56);
        list.add(999); // UnsupportedOperationException
    }
}
```

对只读List调用add()、remove()方法会抛出UnsupportedOperationException。

### 小结

- List是按索引顺序访问的长度可变的有序表，优先使用ArrayList而不是LinkedList；  
- 可以直接使用for each遍历List；
- List可以和Array相互转换。

## 编写 equals 方法

我们知道 List是一种有序链表：List 内部按照放入元素的先后顺序存放，并且每个元素都可以通过索引确定自己的位置。

List 还提供了boolean contains(Object o) 方法来判断 List是否包含某个指定元素。此外，int indexOf(Object o) 方法可以返回某个元素的索引，如果元素不存在，就返回-1。

例子：
```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("A", "B", "C");
        System.out.println(list.contains("C")); // true
        System.out.println(list.contains("X")); // false
        System.out.println(list.indexOf("C")); // 2
        System.out.println(list.indexOf("X")); // -1
    }
}
```

注意一个问题，往 List中添加的"C" 和调用 contains("C") 传入的 "C" 是不是同一个实例

如果这两个 "C" 不是同一个实例，这段代码是否还能得到正确的结果

测试：
```java
public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("A", "B", "C");
        System.out.println(list.contains(new String("C"))); // true or false?
        System.out.println(list.indexOf(new String("C"))); // 2 or -1?
    }
}
```

因为传入的是 new String("C") ，所以一定是不同的实例，但结果仍然符合预期。

因为 List内部并不是通过 == 判断两个元素是否相等，而是使用 equals() 方法判断两个元素是否相等，例如 contains() 方法可以实现如下：

```java
public class ArrayList {
    Object[] elementData;
    public boolean contains(Object o) {
        for (int i = 0; i < size; i++) {
            if (o.equals(elementData[i])) {
                return true;
            }
        }
        return false;
    }
}
```

因此，要正确使用 List的 contains()、indexOf()这些方法，放入的实例必须正确覆写 equals()方法，否则，放进去的实例，查找不到。我们之所以能正常放入 String、Integer这些对象，是因为Java标准库定义的这些类已经正确实现了 equals()方法。

测试：
```java Jdk9
public class Main {
    public static void main(String[] args) {
        List<Person> list = List.of(
            new Person("Xiao Ming"),
            new Person("Xiao Hong"),
            new Person("Bob")
        );
        System.out.println(list.contains(new Person("Bob"))); // false
    }
}

class Person {
    String name;
    public Person(String name) {
        this.name = name;
    }
}
```

```java Jdk8
public static void main(String[] args) {
        List list = new ArrayList<Person>(){
            {
                add(new Person("asd"));
                add(new Person("acc"));
                add(new Person("Bob"));
            }
        };
        System.out.println(list.contains(new Person("Bob"))); // false
    }
```

不出意外，虽然放入了 new Person("Bob")，但是用另一个 new Person("Bob")查询不到，原因就是 Person类没有覆写 equals()方法。

### 编写 equals
如何正确编写equals()方法？equals()方法要求我们必须满足以下条件：

- 自反性（Reflexive）：对于非null的x来说，x.equals(x)必须返回true；
- 对称性（Symmetric）：对于非null的x和y来说，如果x.equals(y)为true，则y.equals(x)也必须为true；
- 传递性（Transitive）：对于非null的x、y和z来说，如果x.equals(y)为true，y.equals(z)也为true，那么x.equals(z)也必须为true；
- 一致性（Consistent）：对于非null的x和y来说，只要x和y状态不变，则x.equals(y)总是一致地返回true或者false；
对null的比较：即x.equals(null)永远返回false。

上述规则看上去似乎非常复杂，但其实代码实现equals()方法是很简单的，我们以Person类为例：

```java
public class Person {
    public String name;
    public int age;
}
```

首先，我们要定义“相等”的逻辑含义。对于 Person类，如果 name相等，并且 age相等，我们就认为两个 Person实例相等。

因此，编写 equals()方法如下

```java
public boolean equals(Object o) {
    if (o instanceof Person) {
        Person p = (Person) o;
        return this.name.equals(p.name) && this.age == p.age;
    }
    return false;
}
```

对于引用字段的比较，我们是用 equals() ，对于基本类型的比较我们使用 ==

如果 this.name 为 null，那么 equals() 方法会报错，因此，需要改写如下：

```java
public boolean equals(Object o) {
    if (o instanceof Person) {
        Person p = (Person) o;
        boolean nameEquals = false;
        if (this.name == null && p.name == null) {
            nameEquals = true;
        }
        if (this.name != null) {
            nameEquals = this.name.equals(p.name);
        }
        return nameEquals && this.age == p.age;
    }
    return false;
}
```

如果 Person有好几个引用类型的字段，上面的写法就太复杂了。要简化引用类型的比较，我们使用  Objects.equals()静态方法：

```java
public boolean equals(Object o) {
    if (o instanceof Person) {
        Person p = (Person) o;
        return Objects.equals(this.name, p.name) && this.age == p.age;
    }
    return false;
}
```

总结一下equals()方法的正确编写方法：

1. 先确定实例“相等”的逻辑，即哪些字段相等，就认为实例相等；
2. 用instanceof判断传入的待比较的Object是不是当前类型，如果是，继续比较，否则，返回false；
3. 对引用类型用Objects.equals()比较，对基本类型直接用==比较。

使用 Objects.equals()比较两个引用类型是否相等的目的是省去了判断null的麻烦。两个引用类型都是null时它们也是相等的。

如果不调用List的contains()、indexOf()这些方法，那么放入的元素就不需要实现equals()方法。

### 小结

在List中查找元素时，List的实现类通过元素的equals()方法比较两个元素是否相等，因此，放入的元素必须正确覆写equals()方法，Java标准库提供的String、Integer等已经覆写了equals()方法；

编写equals()方法可借助Objects.equals()判断。

如果不在List中查找元素，就不必覆写equals()方法。

## 使用 Map

List 是一种顺序列表，如果有一个存储学生 Student实例的List，要在 List中根据 name查找某个指定 Student的分数，该怎么办。

最简单的方法是遍历 List并判断 name是否相等，然后返回指定元素

```java
List<Student> list = ...
Student target = null;
for (Student s : list) {
    if ("Xiao Ming".equals(s.name)) {
        target = s;
        break;
    }
}
System.out.println(target.score);
```

这种需求其实很常见，即通过一个键去查询对应的值。使用 List来实现存在效率非常低的问题，因为平均需要扫描一半的元素才能确定，而 Map这种键值（key-value）映射表的数据结构，作用就是能高效通过key快速查找value（元素）

用 Map来实现根据 name查询某个 Student的代码如下：
```java
public class Main {
    public static void main(String[] args) {
        Student s = new Student("Xiao Ming", 99);
        Map<String, Student> map = new HashMap<>();
        map.put("Xiao Ming", s); // 将"Xiao Ming"和Student实例映射并关联
        Student target = map.get("Xiao Ming"); // 通过key查找并返回映射的Student实例
        System.out.println(target == s); // true，同一个实例
        System.out.println(target.score); // 99
        Student another = map.get("Bob"); // 通过另一个key查找
        System.out.println(another); // 未找到返回null
    }
}

class Student {
    public String name;
    public int score;
    public Student(String name, int score) {
        this.name = name;
        this.score = score;
    }
}
```

通过上述代可知：Map<K，V> 是一种键-值映射表，当我们调用put(K key,V value)方法时，就把 key和 value做了映射并放入 Map。当我们调用 V get(K key)时，就可以通过key获取到对应的 value。如果 key不存在，则返回 null。和 List类似，Map也是一个借口，最常用的实现类是 HashMap。

如果只是想查询某个 key是否存在，可以调动 boolean containsKey(K key)方法。

如果我们在存储 Map映射关系的时候，对同一个key调用两次 put()方法，分别放入不同的 value，会有什么问题呢

例：
```java
public class Main {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 123);
        map.put("pear", 456);
        System.out.println(map.get("apple")); // 123
        map.put("apple", 789); // 再次放入apple作为key，但value变为789
        System.out.println(map.get("apple")); // 789
    }
}
```

重复放入 key-value并不会有任何问题，但是一个 key只能关联一个 value。在上面的代码中，一开始我们把 key对象 "apple" 映射到 Integer对象 123��然后��次调用 put()方法把 "apple"映射到 789，这时，原来关联的 value对象 123就被“冲掉”了。实际上，put()方法的签名是 V put(K key, V value)，如果放入的 key已经存在，put()方法会返回被删除的旧的 value，否则，返回 null。

>始终牢记：Map中不存在重复的key，因为放入相同的key，只会把原有的key-value对应的value给替换掉。

此外，在一个Map中，虽然key不能重复，但value是可以重复的：

```java
Map<String, Integer> map = new HashMap<>();
map.put("apple", 123);
map.put("pear", 123); // ok
```
###  遍历Map
对 Map来说，要遍历 key可以使用for each循环遍历 Map实例的 keySet()方法返回的 Set集合，它包含不重复的 key的集合

```java
public class Main {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 123);
        map.put("pear", 456);
        map.put("banana", 789);
        for (String key : map.keySet()) {
            Integer value = map.get(key);
            System.out.println(key + " = " + value);
        }
    }
}
```

同时遍历 key和 value可以使用 for each循环遍历 Map对象的 entrySet()集合，它包含每一个key-value映射：

```java
public class Main {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 123);
        map.put("pear", 456);
        map.put("banana", 789);
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            String key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(key + " = " + value);
        }
    }
}
```

Map和 List不同的是，Map存储的是 key-value的映射关系，并且，它不保证顺序。在遍历的时候，遍历的顺序既不一定是 put()时放入的 key的顺序，也不一定是 key的排序顺序。使用 Map时，任何依赖顺序的逻辑都是不可靠的。以 HashMap为例，假设我们放入"A"，"B"，"C"这3个 key，遍历的时候，每个 key会保证被遍历一次且仅遍历一次，但顺序完全没有保证，甚至对于不同的 JDK版本，相同的代码遍历的输出顺序都是不同的！

> 遍历Map时，不可假设输出的key是有序的！

### 小结
Map是一种映射表，可以通过key快速查找value。

可以通过for each遍历keySet()，也可以通过for each遍历entrySet()，直接获取key-value。

最常用的一种Map实现是HashMap。

## 编写 equals 和 hashCode

Map是一种键-值（key-value）映射表，可以通过key快速查找对应的 value

以HashMap为例，观察下列代码

```java
Map<String, Person> map = new HashMap<>();
map.put("a", new Person("Xiao Ming"));
map.put("b", new Person("Xiao Hong"));
map.put("c", new Person("Xiao Jun"));

map.get("a"); // Person("Xiao Ming")
map.get("x"); // null
```

HashMap之所以能根据 key直接拿到 value，原因是它内部通过空间换时间的方法，用一个大数组存储所有 value，并根据 key直接计算出 value应该存储在哪个索引：

```java
  ┌───┐
0 │   │
  ├───┤
1 │ ●─┼───> Person("Xiao Ming")
  ├───┤
2 │   │
  ├───┤
3 │   │
  ├───┤
4 │   │
  ├───┤
5 │ ●─┼───> Person("Xiao Hong")
  ├───┤
6 │ ●─┼───> Person("Xiao Jun")
  ├───┤
7 │   │
  └───┘
```

如果 key的值为 "a"，计算得到的索引总是 1，因此返回 value为Person("Xiao Ming")，如果key的值为 "b"，计算得到的索引总是 5，因此返回 value为Person("Xiao Hong")，这样，就不必遍历整个数组，即可直接读取 key对应的 value。

我们经常使用 String作为 key，因为 String已经正确覆写了 equals()方法。但如果我们放入的key是一个自己写的类，就必须保证正确覆写了 equals()方法。

我们再思考一下 HashMap为什么能通过 key直接计算出 value存储的索引。相同的 key对象(使用equals()判断时返回true)必须要计算出相同的索引，否则，相同的 key每次取出的 value就不一定对。

通过 key计算索引的方式就是调用 key对象的 hashCode()方法，它返回一个 int整数。HashMap正是通过这个方法直接定位 key对应的 value的索引，继而直接返回 value。

因此，正确使用Map必须保证：

1. 作为key的对象必须正确覆写equals()方法，相等的两个key实例调用equals()必须返回true；

2. 作为key的对象还必须正确覆写hashCode()方法，且hashCode()方法要严格遵循以下规范：

- 如果两个对象相等，则两个对象的hashCode()必须相等；
- 如果两个对象不相等，则两个对象的hashCode()尽量不要相等。

即对应两个实例a和b：

- 如果a和b相等，那么 a.equals(b)一定为true，则 a.hashCode()必须等于 b.hashCode()；
- 如果a和b不相等，那么 a.equals(b)一定为false，则 a.hashCode()和 b.hashCode()尽量不要相等。

上述第一条规范是正确性，必须保证实现，否则HashMap不能正常工作。

而第二条如果尽量满足，则可以保证查询效率，因为不同的对象，如果返回相同的hashCode()，会造成Map内部存储冲突，使存取的效率下降。

正确编写equals()的方法我们已经在编写equals方法一节中讲过了，以Person类为例：

```java
public class Person {
    String firstName;
    String lastName;
    int age;
}
```

把需要比较的字段找出来：

- firstName
- lastName
- age

然后，引用类型使用 Objects.equals()比较，基本类型使用 == 比较。

在正确实现 equals()的基础上，我们还需要正确实现 hashCode()，即上述3个字段分别相同的实例， hashCode()返回的 int必须相同：

```java
public class Person {
    String firstName;
    String lastName;
    int age;

    @Override
    int hashCode() {
        int h = 0;
        h = 31 * h + firstName.hashCode();
        h = 31 * h + lastName.hashCode();
        h = 31 * h + age;
        return h;
    }
}
```

所以，编写 equals()和 hashCode()遵循的原则是：

- equals()用到的用于比较的每一个字段，都必须在 hashCode()中用于计算；equals()中没有使用到的字段，绝不可放在 hashCode()中计算。

另外注意，对于放入HashMap的value对象，没有任何要求。

### 延伸阅读

既然HashMap内部使用了数组，通过计算key的hashCode()直接定位value所在的索引，那么第一个问题来了：hashCode()返回的int范围高达±21亿，先不考虑负数，HashMap内部使用的数组得有多大？

实际上HashMap初始化时默认的数组大小只有16，任何key，无论它的hashCode()有多大，都可以简单地通过：

```java
int index = key.hashCode() & 0xf; // 0xf = 15
```

把索引确定在0～15，即永远不会超出数组范围，上述算法只是一种最简单的实现。

第二个问题：如果添加超过16个key-value到HashMap，数组不够用了怎么办？

添加超过一定数量的key-value时，HashMap会在内部自动扩容，每次扩容一倍，即长度为16的数组扩展为长度32，相应地，需要重新确定hashCode()计算的索引位置。例如，对长度为32的数组计算hashCode()对应的索引，计算方式要改为：

```java
int index = key.hashCode() & 0x1f; // 0x1f = 31
```

由于扩容会导致重新分布已有的key-value，所以，频繁扩容对HashMap的性能影响很大。如果我们确定要使用一个容量为10000个key-value的HashMap，更好的方式是创建HashMap时就指定容量：

Map<String, Integer> map = new HashMap<>(10000);
虽然指定容量是10000，但HashMap内部的数组长度总是2n，因此，实际数组长度被初始化为比10000大的16384（214）。

最后一个问题：如果不同的两个key，例如"a"和"b"，它们的hashCode()恰好是相同的（这种情况是完全可能的，因为不相等的两个实例，只要求hashCode()尽量不相等），那么，当我们放入：

```java
map.put("a", new Person("Xiao Ming"));
map.put("b", new Person("Xiao Hong"));
```

时，由于计算出的数组索引相同，后面放入的"Xiao Hong"会不会把"Xiao Ming"覆盖了？

当然不会！使用Map的时候，只要key不相同，它们映射的value就互不干扰。但是，在HashMap内部，确实可能存在不同的key，映射到相同的hashCode()，即相同的数组索引上，肿么办？

我们就假设"a"和"b"这两个key最终计算出的索引都是5，那么，在HashMap的数组中，实际存储的不是一个Person实例，而是一个List，它包含两个Entry，一个是"a"的映射，一个是"b"的映射：

``` 
  ┌───┐
0 │   │
  ├───┤
1 │   │
  ├───┤
2 │   │
  ├───┤
3 │   │
  ├───┤
4 │   │
  ├───┤
5 │ ●─┼───> List<Entry<String, Person>>
  ├───┤
6 │   │
  ├───┤
7 │   │
  └───┘
  ```
在查找的时候，例如：

```java
Person p = map.get("a");
```

HashMap内部通过"a"找到的实际上是List<Entry<String, Person>>，它还需要遍历这个List，并找到一个Entry，它的key字段是"a"，才能返回对应的Person实例。

我们把不同的key具有相同的hashCode()的情况称之为哈希冲突。在冲突的时候，一种最简单的解决办法是用List存储hashCode()相同的key-value。显然，如果冲突的概率越大，这个List就越长，Map的get()方法效率就越低，这就是为什么要尽量满足条件二：

>如果两个对象不相等，则两个对象的hashCode()尽量不要相等。

hashCode()方法编写得越好，HashMap工作的效率就越高。

## 使用 EnumMap

因为HashMap是一种通过对key计算hashCode()，通过空间换时间的方式，直接定位到value所在的内部数组的索引，因此，查找效率非常高。

如果作为key的对象是enum类型，那么，还可以使用Java集合库提供的一种EnumMap，它在内部以一个非常紧凑的数组存储value，并且根据enum类型的key直接定位到内部数组的索引，并不需要计算hashCode()，不但效率最高，而且没有额外的空间浪费。

我们以DayOfWeek这个枚举类型为例，为它做一个“翻译”功能：

```java
public class Main {
    public static void main(String[] args) {
        Map<DayOfWeek, String> map = new EnumMap<>(DayOfWeek.class);
        map.put(DayOfWeek.MONDAY, "星期一");
        map.put(DayOfWeek.TUESDAY, "星期二");
        map.put(DayOfWeek.WEDNESDAY, "星期三");
        map.put(DayOfWeek.THURSDAY, "星期四");
        map.put(DayOfWeek.FRIDAY, "星期五");
        map.put(DayOfWeek.SATURDAY, "星期六");
        map.put(DayOfWeek.SUNDAY, "星期日");
        System.out.println(map);
        System.out.println(map.get(DayOfWeek.MONDAY));
    }
}
```

使用EnumMap的时候，我们总是用Map接口来引用它，因此，实际上把HashMap和EnumMap互换，在客户端看来没有任何区别。

## 使用 TreeMap

我们已经知道，HashMap是一种以空间换时间的映射表，它的实现原理决定了内部的Key是无序的，即遍历HashMap的Key时，其顺序是不可预测的（但每个Key都会遍历一次且仅遍历一次）。

还有一种Map，它在内部会对Key进行排序，这种Map就是SortedMap。注意到SortedMap是接口，它的实现类是TreeMap。

```java
       ┌───┐
       │Map│
       └───┘
         ▲
    ┌────┴─────┐
    │          │
┌───────┐ ┌─────────┐
│HashMap│ │SortedMap│
└───────┘ └─────────┘
               ▲
               │
          ┌─────────┐
          │ TreeMap │
          └─────────┘
```

SortedMap保证遍历时以Key的顺序来进行排序。例如，放入的Key是"apple"、"pear"、"orange"，遍历的顺序一定是"apple"、"orange"、"pear"，因为String默认按字母排序：

```java
public class Main {
    public static void main(String[] args) {
        Map<String, Integer> map = new TreeMap<>();
        map.put("orange", 1);
        map.put("apple", 2);
        map.put("pear", 3);
        for (String key : map.keySet()) {
            System.out.println(key);
        }
        // apple, orange, pear
    }
}
```

使用TreeMap时，放入的Key必须实现Comparable接口。String、Integer这些类已经实现了Comparable接口，因此可以直接作为Key使用。作为Value的对象则没有任何要求。

如果作为Key的class没有实现Comparable接口，那么，必须在创建TreeMap时同时指定一个自定义排序算法：

```java
public class Main {
    public static void main(String[] args) {
        Map<Person, Integer> map = new TreeMap<>(new Comparator<Person>() {
            public int compare(Person p1, Person p2) {
                return p1.name.compareTo(p2.name);
            }
        });
        map.put(new Person("Tom"), 1);
        map.put(new Person("Bob"), 2);
        map.put(new Person("Lily"), 3);
        for (Person key : map.keySet()) {
            System.out.println(key);
        }
        // {Person: Bob}, {Person: Lily}, {Person: Tom}
        System.out.println(map.get(new Person("Bob"))); // 2
    }
}

class Person {
    public String name;
    Person(String name) {
        this.name = name;
    }
    public String toString() {
        return "{Person: " + name + "}";
    }
}
```

注意到Comparator接口要求实现一个比较方法，它负责比较传入的两个元素a和b，`如果a<b，则返回负数，通常是-1，如果a==b，则返回0，如果a>b，则返回正数，通常是1`。TreeMap内部根据比较结果对Key进行排序。

## 使用 Properties
在编写应用程序的时候，经常需要读写配置文件。例如，用户的设置：

```
## 上次最后打开的文件:
last_open_file=/data/hello.txt

## 自动保存文件的时间间隔:
auto_save_interval=60
```

配置文件的特点是，它的Key-Value一般都是`String`-`String`类型的，因此我们完全可以用`Map<String, String>`来表示它。

因为配置文件非常常用，所以Java集合库提供了一个`Properties`来表示一组“配置”。由于历史遗留原因，`Properties`内部本质上是一个`Hashtable`，但我们只需要用到`Properties`自身关于读写配置的接口。

### 读取配置文件

用 `Properties` 读取配置文件非常简单。Java 默认配置文件以 `.properties` 为扩展名，每行以 `key=value` 表示，以 `#` 开头的是注释。以下是一个典型的配置文件:

```properties
## setting.properties

last_open_file=/data/hello.txt
auto_save_interval=60
```

可以从文件系统读取这个`.properties`文件：

```java
String f = "setting.properties";
Properties props = new Properties();
props.load(new java.io.FileInputStream(f));

String filepath = props.getProperty("last_open_file");
String interval = props.getProperty("auto_save_interval", "120");
```

可见，用Properties读取配置文件，一共有三步：

1. 创建Properties实例；
2. 调用load()读取文件；
3. 调用getProperty()获取配置。

调用`getProperty()`获取配置时，如果key不存在，将返回`null`。我们还可以提供一个默认值，这样，当key不存在的时候，就返回默认值。

也可以从classpath读取`.properties`文件，因为`load(InputStream)`方法接收一个`InputStream`实例，表示一个字节流，它不一定是文件流，也可以是从jar包中读取的资源流：

```java
Properties props = new Properties();
props.load(getClass().getResourceAsStream("/common/setting.properties"));
```

试试从内存读取一个字节流：

```java
import java.io.*;
import java.util.Properties;

public class Main {
    public static void main(String[] args) throws IOException {
        String settings = "## test" + "\n" + "course=Java" + "\n" + "last_open_date=2019-08-07T12:35:01";
        ByteArrayInputStream input = new ByteArrayInputStream(settings.getBytes("UTF-8"));
        Properties props = new Properties();
        props.load(input);

        System.out.println("course: " + props.getProperty("course"));
        System.out.println("last_open_date: " + props.getProperty("last_open_date"));
        System.out.println("last_open_file: " + props.getProperty("last_open_file"));
        System.out.println("auto_save: " + props.getProperty("auto_save", "60"));
    }
}
```

如果有多个`.properties`文件，可以反复调用`load()`读取，后读取的key-value会覆盖已读取的key-value：

```java
Properties props = new Properties();
props.load(getClass().getResourceAsStream("/common/setting.properties"));
props.load(new FileInputStream("C:\\conf\\setting.properties"));
```

上面的代码演示了`Properties`的一个常用用法：可以把默认配置文件放到classpath中，然后，根据机器的环境编写另一个配置文件，覆盖某些默认的配置。

`Properties`设计的目的是存储`String`类型的key－value，但`Properties`实际上是从`Hashtable`派生的，它的设计实际上是有问题的，但是为了保持兼容性，现在已经没法修改了。除了`getProperty()`和`setProperty()`方法外，还有从`Hashtable`继承下来的`get()`和`put()`方法，这些方法的参数签名是`Object`，我们在使用`Properties`的时候，不要去调用这些从`Hashtable`继承下来的方法。

### 写入配置文件

如果通过`setProperty()`修改了`Properties`实例，可以把配置写入文件，以便下次启动时获得最新配置。写入配置文件使用`store()`方法：

```java
Properties props = new Properties();
props.setProperty("url", "http://www.liaoxuefeng.com");
props.setProperty("language", "Java");
props.store(new FileOutputStream("C:\\conf\\setting.properties"), "这是写入的properties注释");
```

### 编码

早期版本的Java规定`.properties`文件编码是ASCII编码（ISO8859-1），如果涉及到中文就必须用`name=\u4e2d\u6587`来表示，非常别扭。从JDK9开始，Java的`.properties`文件可以使用UTF-8编码了。

不过，需要注意的是，由于`load(InputStream)`默认总是以ASCII编码读取字节流，所以会导致读到乱码。我们需要用另一个重载方法`load(Reader)`读取：

```java
Properties props = new Properties();
props.load(new FileReader("settings.properties", StandardCharsets.UTF_8));
```

就可以正常读取中文。`InputStream`和`Reader`的区别是一个是字节流，一个是字符流。字符流在内存中已经以`char`类型表示了，不涉及编码问题。

### 小结
Java集合库提供的`Properties`用于读写配置文件`.properties`。`.properties`文件可以使用UTF-8编码。

可以从文件系统、classpath或其他任何地方读取`.properties`文件。

读写`Properties`时，注意仅使用`getProperty()`和`setProperty()`方法，不要调用继承而来的`get()`和`put()`等方法。

## 使用 Set
我们知道，`Map`用于存储key-value的映射，对于充当key的对象，是不能重复的，并且，不但需要正确覆写`equals()`方法，还要正确覆写`hashCode()`方法。

如果我们只需要存储不重复的key，并不需要存储映射的value，那么就可以使用`Set`。

`Set`用于存储不重复的元素集合，它主要提供以下几个方法：

- 将元素添加进`Set<E>`：`boolean add(E e)`
- 将元素从`Set<E>`删除：`boolean remove(Object e)`
- 判断是否包含元素：`boolean contains(Object e)`

例子:

```java
public class Main {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        System.out.println(set.add("abc")); // true
        System.out.println(set.add("xyz")); // true
        System.out.println(set.add("xyz")); // false，添加失败，因为元素已存在
        System.out.println(set.contains("xyz")); // true，元素存在
        System.out.println(set.contains("XYZ")); // false，元素不存在
        System.out.println(set.remove("hello")); // false，删除失败，因为元素不存在
        System.out.println(set.size()); // 2，一共两个元素
    }
}
```

`Set`实际上相当于只存储key、不存储value的`Map`。我们经常用`Set`用于去除重复元素。

因为放入`Set`的元素和`Map`的key类似，都要正确实现`equals()`和`hashCode()`方法，否则该元素无法正确地放入`Set`。

最常用的`Set`实现类是`HashSet`，实际上，`HashSet`仅仅是对`HashMap`的一个简单封装，它的核心代码如下：

```java
public class HashSet<E> implements Set<E> {
    // 持有一个HashMap:
    private HashMap<E, Object> map = new HashMap<>();

    // 放入HashMap的value:
    private static final Object PRESENT = new Object();

    public boolean add(E e) {
        return map.put(e, PRESENT) == null;
    }

    public boolean contains(Object o) {
        return map.containsKey(o);
    }

    public boolean remove(Object o) {
        return map.remove(o) == PRESENT;
    }
}
```

`Set`接口并不保证有序，而`SortedSet`接口则保证元素是有序的：

- `HashSet`是无序的，因为它实现了`Set`接口，并没有实现`SortedSet`接口；
- `TreeSet`是有序的，因为它实现了`SortedSet`接口。

用一张图表示：

```
       ┌───┐
       │Set│
       └───┘
         ▲
    ┌────┴─────┐
    │          │
┌───────┐ ┌─────────┐
│HashSet│ │SortedSet│
└───────┘ └─────────┘
               ▲
               │
          ┌─────────┐
          │ TreeSet │
          └─────────┘
```

我们来看`HashSet`的输出：

```java
public class Main {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("apple");
        set.add("banana");
        set.add("pear");
        set.add("orange");
        for (String s : set) {
            System.out.println(s);
        }
    }
}
```

把`HashSet`换成`TreeSet`，在遍历`TreeSet`时，输出就是有序的，这个顺序是元素的排序顺序：

```java
public class Main {
    public static void main(String[] args) {
        Set<String> set = new TreeSet<>();
        set.add("apple");
        set.add("banana");
        set.add("pear");
        set.add("orange");
        for (String s : set) {
            System.out.println(s);
        }
    }
}
```

使用`TreeSet`和使用`TreeMap`的要求一样，添加的元素必须正确实现`Comparable`接口，如果没有实现`Comparable`接口，那么创建`TreeSet`时必须传入一个`Comparator`对象。

### 小结
Set用于存储不重复的元素集合：

- 放入HashSet的元素与作为HashMap的key要求相同；
- 放入TreeSet的元素与作为TreeMap的Key要求相同；

利用Set可以去除重复元素；

遍历SortedSet按照元素的排序顺序遍历，也可以自定义排序算法。

## 使用 Queue
队列（`Queue`）是一种经常使用的集合。`Queue`实际上是实现了一个先进先出（FIFO：First In First Out）的有序表。它和`List`的区别在于，`List`可以在任意位置添加和删除元素，而`Queue`只有两个操作：

- 把元素添加到队列末尾；
- 从队列头部取出元素。

在Java的标准库中，队列接口`Queue`定义了以下几个方法：

- `int size()`：获取队列长度；
- `boolean add(E)`/`boolean offer(E)`：添加元素到队尾；
- `E remove()`/`E poll()`：获取队首元素并从队列中删除；
- `E element()`/`E peek()`：获取队首元素但并不从队列中删除。

对于具体的实现类，有的Queue有最大队列长度限制，有的Queue没有。注意到添加、删除和获取队列元素总是有两个方法，这是因为在添加或获取元素失败时，这两个方法的行为是不同的。我们用一个表格总结如下：

-                   |throw Exception | 返回false或null
-|-|-
添加元素到队尾	    |add(E e)	      |boolean offer(E e)
取队首元素并删除	|E remove()	      |E poll()
取队首元素但不删除	|E element()	  |E peek()

举个栗子，假设我们有一个队列，对它做一个添加操作，如果调用`add()`方法，当添加失败时（可能超过了队列的容量），它会抛出异常：

```java
Queue<String> q = ...
try {
    q.add("Apple");
    System.out.println("添加成功");
} catch(IllegalStateException e) {
    System.out.println("添加失败");
}
```

如果我们调用`offer()`方法来添加元素，当添加失败时，它不会抛异常，而是返回`false`：

```java
Queue<String> q = ...
if (q.offer("Apple")) {
    System.out.println("添加成功");
} else {
    System.out.println("添加失败");
}
```

当我们需要从`Queue`中取出队首元素时，如果当前`Queue`是一个空队列，调用`remove()`方法，它会抛出异常：

```java
Queue<String> q = ...
try {
    String s = q.remove();
    System.out.println("获取成功");
} catch(IllegalStateException e) {
    System.out.println("获取失败");
}
```

如果我们调用`poll()`方法来取出队首元素，当获取失败时，它不会抛异常，而是返回`null`：

```java
Queue<String> q = ...
String s = q.poll();
if (s != null) {
    System.out.println("获取成功");
} else {
    System.out.println("获取失败");
}
```

因此，两套方法可以根据需要来选择使用。

注意：不要把`null`添加到队列中，否则`poll()`方法返回`null`时，很难确定是取到了`null`元素还是队列为空。

接下来我们以`poll()`和`peek()`为例来说说“获取并删除”与“获取但不删除”的区别。对于`Queue`来说，每次调用`poll()`，都会获取队首元素，并且获取到的元素已经从队列中被删除了：

```java
public class Main {
    public static void main(String[] args) {
        Queue<String> q = new LinkedList<>();
        // 添加3个元素到队列:
        q.offer("apple");
        q.offer("pear");
        q.offer("banana");
        // 从队列取出元素:
        System.out.println(q.poll()); // apple
        System.out.println(q.poll()); // pear
        System.out.println(q.poll()); // banana
        System.out.println(q.poll()); // null,因为队列是空的
    }
}
```

如果用`peek()`，因为获取队首元素时，并不会从队列中删除这个元素，所以可以反复获取：

```java
public class Main {
    public static void main(String[] args) {
        Queue<String> q = new LinkedList<>();
        // 添加3个元素到队列:
        q.offer("apple");
        q.offer("pear");
        q.offer("banana");
        // 队首永远都是apple，因为peek()不会删除它:
        System.out.println(q.peek()); // apple
        System.out.println(q.peek()); // apple
        System.out.println(q.peek()); // apple
    }
}
```

从上面的代码中，我们还可以发现，`LinkedList`即实现了`List`接口，又实现了`Queue`接口，但是，在使用的时候，如果我们把它当作List，就获取List的引用，如果我们把它当作Queue，就获取Queue的引用：

```java
// 这是一个List:
List<String> list = new LinkedList<>();
// 这是一个Queue:
Queue<String> queue = new LinkedList<>();
```

始终按照面向抽象编程的原则编写代码，可以大大提高代码的质量。

### 小结
队列Queue实现了一个先进先出（FIFO）的数据结构：

- 通过add()/offer()方法将元素添加到队尾；
- 通过remove()/poll()从队首获取元素并删除；
- 通过element()/peek()从队首获取元素但不删除。

要避免把null添加到队列。

## 使用 PriorityQueue

我们知道，`Queue`是一个先进先出（FIFO）的队列。

在银行柜台办业务时，我们假设只有一个柜台在办理业务，但是办理业务的人很多，怎么办？

可以每个人先取一个号，例如：`A1`、`A2`、`A3`……然后，按照号码顺序依次办理，实际上这就是一个`Queue`。

如果这时来了一个VIP客户，他的号码是`V1`，虽然当前排队的是`A10`、`A11`、`A12`……但是柜台下一个呼叫的客户号码却是`V1`。

这个时候，我们发现，要实现“VIP插队”的业务，用`Queue`就不行了，因为`Queue`会严格按FIFO的原则取出队首元素。我们需要的是优先队列：`PriorityQueue`。

`PriorityQueue`和`Queue`的区别在于，它的出队顺序与元素的优先级有关，对`PriorityQueue`调用`remove()`或`poll()`方法，返回的总是优先级最高的元素。

要使用`PriorityQueue`，我们就必须给每个元素定义“优先级”。我们以实际代码为例，先看看`PriorityQueue`的行为：

```java
public class Main {
    public static void main(String[] args) {
        Queue<String> q = new PriorityQueue<>();
        // 添加3个元素到队列:
        q.offer("apple");
        q.offer("pear");
        q.offer("banana");
        System.out.println(q.poll()); // apple
        System.out.println(q.poll()); // banana
        System.out.println(q.poll()); // pear
        System.out.println(q.poll()); // null,因为队列为空
    }
}
```

我们放入的顺序是`"apple"`、`"pear"`、`"banana"`，但是取出的顺序却是`"apple"`、`"banana"`、`"pear"`，这是因为从字符串的排序看，`"apple"`排在最前面，`"pear"`排在最后面。

因此，放入`PriorityQueue`的元素，必须实现`Comparable`接口，`PriorityQueue`会根据元素的排序顺序决定出队的优先级。

如果我们要放入的元素并没有实现`Comparable`接口怎么办？`PriorityQueue`允许我们提供一个`Comparator`对象来判断两个元素的顺序。我们以银行排队业务为例，实现一个`PriorityQueue`：

```java
public class Main {
    public static void main(String[] args) {
        Queue<User> q = new PriorityQueue<>(new UserComparator());
        // 添加3个元素到队列:
        q.offer(new User("Bob", "A1"));
        q.offer(new User("Alice", "A2"));
        q.offer(new User("Boss", "V1"));
        System.out.println(q.poll()); // Boss/V1
        System.out.println(q.poll()); // Bob/A1
        System.out.println(q.poll()); // Alice/A2
        System.out.println(q.poll()); // null,因为队列为空
    }
}

class UserComparator implements Comparator<User> {
    public int compare(User u1, User u2) {
        if (u1.number.charAt(0) == u2.number.charAt(0)) {
            // 如果两人的号都是A开头或者都是V开头,比较号的大小:
            return u1.number.compareTo(u2.number);
        }
        if (u1.number.charAt(0) == 'V') {
            // u1的号码是V开头,优先级高:
            return -1;
        } else {
            return 1;
        }
    }
}

class User {
    public final String name;
    public final String number;

    public User(String name, String number) {
        this.name = name;
        this.number = number;
    }

    public String toString() {
        return name + "/" + number;
    }
}
```

实现`PriorityQueue`的关键在于提供的`UserComparator`对象，它负责比较两个元素的大小（较小的在前）。U`serComparator`总是把`V`开头的号码优先返回，只有在开头相同的时候，才比较号码大小。

上面的`UserComparator`的比较逻辑其实还是有问题的，它会把`A10`排在`A2`的前面，请尝试修复该错误。

### 小结
`PriorityQueue`实现了一个优先队列：从队首获取元素时，总是获取优先级最高的元素。

`PriorityQueue`默认按元素比较的顺序排序（必须实现`Comparable`接口），也可以通过`Comparator`自定义排序算法（元素就不必实现`Comparable`接口）。

## 使用 Deque
我们知道，`Queue`是队列，只能一头进，另一头出。

如果把条件放松一下，允许两头都进，两头都出，这种队列叫双端队列（Double Ended Queue），学名`Deque`。

Java集合提供了接口`Deque`来实现一个双端队列，它的功能是：

- 既可以添加到队尾，也可以添加到队首；
- 既可以从队首获取，又可以从队尾获取。

我们来比较一下`Queue`和`Deque`出队和入队的方法：

-|	Queue|	Deque
-|-|-
添加元素到队尾	    |add(E e) / offer(E e)	|addLast(E e) / offerLast(E e)
取队首元素并删除	|E remove() / E poll()	|E removeFirst() / E pollFirst()
取队首元素但不删除	|E element() / E peek()	|E getFirst() / E peekFirst()
添加元素到队首	    |无	                    |addFirst(E e) / offerFirst(E e)
取队尾元素并删除	|无	                    |E removeLast() / E pollLast()
取队尾元素但不删除	|无	                    |E getLast() / E peekLast()

对于添加元素到队尾的操作，`Queue`提供了`add()`/`offer()`方法，而`Deque`提供了`addLast()`/`offerLast()`方法。添加元素到队首、取队尾元素的操作在`Queue`中不存在，在`Deque`中由`addFirst()`/`removeLast()`等方法提供。

注意到`Deque`接口实际上扩展自`Queue`：

```java
public interface Deque<E> extends Queue<E> {
    ...
}
```

因此，`Queue`提供的`add()`/`offer()`方法在`Deque`中也可以使用，但是，使用`Deque`，最好不要调用`offer()`，而是调用`offerLast()`：

```java
public class Main {
    public static void main(String[] args) {
        Deque<String> deque = new LinkedList<>();
        deque.offerLast("A"); // A
        deque.offerLast("B"); // A <- B
        deque.offerFirst("C"); // C <- A <- B
        System.out.println(deque.pollFirst()); // C, 剩下A <- B
        System.out.println(deque.pollLast()); // B, 剩下A
        System.out.println(deque.pollFirst()); // A
        System.out.println(deque.pollFirst()); // null
    }
}
```

如果直接写`deque.offer()`，我们就需要思考，`offer()`实际上是`offerLast()`，我们明确地写上`offerLast()`，不需要思考就能一眼看出这是添加到队尾。

因此，使用`Deque`，推荐总是明确调用`offerLast()`/`offerFirst()`或者`pollFirst()`/`pollLast()`方法。

`Deque`是一个接口，它的实现类有`ArrayDeque`和`LinkedList`。

我们发现`LinkedList`真是一个全能选手，它即是`List`，又是`Queue`，还是`Deque`。但是我们在使用的时候，总是用特定的接口来引用它，这是因为持有接口说明代码的抽象层次更高，而且接口本身定义的方法代表了特定的用途。

```java
// 不推荐的写法:
LinkedList<String> d1 = new LinkedList<>();
d1.offerLast("z");
// 推荐的写法：
Deque<String> d2 = new LinkedList<>();
d2.offerLast("z");
```

### 小结
`Deque`实现了一个双端队列（Double Ended Queue），它可以：

- 将元素添加到队尾或队首：`addLast()`/`offerLast()`/`addFirst()`/`offerFirst()`；
- 从队首／队尾获取元素并删除：`removeFirst()`/`pollFirst()`/`removeLast()`/`pollLast()`；
- 从队首／队尾获取元素但不删除：`getFirst()`/`peekFirst()`/`getLast()`/`peekLast()`；
- 总是调用`xxxFirst()`/`xxxLast()`以便与`Queue`的方法区分开；
- 避免把`null`添加到队列。

## 使用 Stack
栈（Stack）是一种后进先出（LIFO：Last In First Out）的数据结构。

什么是LIFO呢？我们先回顾一下`Queue`的特点FIFO：

```
          ────────────────────────
  (\(\      (\(\    (\(\    (\(\      (\(\
 (='.') ─> (='.')  (='.')  (='.') ─> (='.')
O(_")")   O(_")") O(_")") O(_")")   O(_")")
          ────────────────────────
```

所谓FIFO，是最先进队列的元素一定最早出队列，而LIFO是最后进`Stack`的元素一定最早出`Stack`。如何做到这一点呢？只需要把队列的一端封死：

```
           ───────────────────────────────┐
  (\(\       (\(\    (\(\    (\(\    (\(\ │
 (='.') <─> (='.')  (='.')  (='.')  (='.')│
O(_")")    O(_")") O(_")") O(_")") O(_")")│
           ───────────────────────────────┘
```

因此，`Stack`是这样一种数据结构：只能不断地往`Stack`中压入（push）元素，最后进去的必须最早弹出（pop）来：

`Stack`只有入栈和出栈的操作：

- 把元素压栈：`push(E)`；
- 把栈顶的元素“弹出”：`pop()`；
- 取栈顶元素但不弹出：`peek()`。

在Java中，我们用`Deque`可以实现`Stack`的功能：

- 把元素压栈：`push(E)`/`addFirst(E)`；
- 把栈顶的元素“弹出”：`pop()`/`removeFirst()`；
- 取栈顶元素但不弹出：`peek()`/`peekFirst()`。

为什么Java的集合类没有单独的`Stack`接口呢？因为有个遗留类名字就叫`Stack`，出于兼容性考虑，所以没办法创建`Stack`接口，只能用Deque接口来“模拟”一个`Stack`了。

当我们把`Deque`作为`Stack`使用时，注意只调用`push()`/`pop()`/`peek()`方法，不要调用`addFirst()`/`removeFirst()`/`peekFirst()`方法，这样代码更加清晰。

### Stack的作用

Stack在计算机中使用非常广泛，JVM在处理Java方法调用的时候就会通过栈这种数据结构维护方法调用的层次。例如：

```java
static void main(String[] args) {
    foo(123);
}

static String foo(x) {
    return "F-" + bar(x + 1);
}

static int bar(int x) {
    return x << 2;
}
```

JVM会创建方法调用栈，每调用一个方法时，先将参数压栈，然后执行对应的方法；当方法返回时，返回值压栈，调用方法通过出栈操作获得方法返回值。

因为方法调用栈有容量限制，嵌套调用过多会造成栈溢出，即引发`StackOverflowError`：

```java
// 测试无限递归调用
public class Main {
    public static void main(String[] args) {
        increase(1);
    }

    static int increase(int x) {
        return increase(x) + 1;
    }
}
```

我们再来看一个`Stack`的用途：对整数进行进制的转换就可以利用栈。

例如，我们要把一个`int`整数`12500`转换为十六进制表示的字符串，如何实现这个功能？

首先我们准备一个空栈：

```
│   │
│   │
│   │
│   │
│   │
│   │
│   │
│   │
└───┘
```

然后计算12500÷16=781…4，余数是4，把余数4压栈：

```
│   │
│   │
│   │
│   │
│   │
│   │
│   │
│ 4 │
└───┘
```

然后计算781÷16=48…13，余数是13，13的十六进制用字母D表示，把余数D压栈：

```
│   │
│   │
│   │
│   │
│   │
│ D │
│   │
│ 4 │
└───┘
```

然后计算48÷16=3…0，余数是0，把余数0压栈：

```
│   │
│   │
│   │
│ 0 │
│   │
│ D │
│   │
│ 4 │
└───┘
```

最后计算3÷16=0…3，余数是3，把余数3压栈：

```
│   │
│ 3 │
│   │
│ 0 │
│   │
│ D │
│   │
│ 4 │
└───┘
```

当商是`0`的时候，计算结束，我们把栈的所有元素依次弹出，组成字符串`30D4`，这就是十进制整数`12500`的十六进制表示的字符串。

### 计算中缀表达式
在编写程序的时候，我们使用的带括号的数学表达式实际上是中缀表达式，即运算符在中间，例如：`1 + 2 * (9 - 5)`。

但是计算机执行表达式的时候，它并不能直接计算中缀表达式，而是通过编译器把中缀表达式转换为后缀表达式，例如：`1 2 9 5 - * +`。

这个编译过程就会用到栈。我们先跳过编译这一步（涉及运算优先级，代码比较复杂），看看如何通过栈计算后缀表达式。

计算后缀表达式不考虑优先级，直接从左到右依次计算，因此计算起来简单。首先准备一个空的栈：

```
│   │
│   │
│   │
│   │
│   │
│   │
│   │
│   │
└───┘
```

然后我们依次扫描后缀表达式`1 2 9 5 - * +`，遇到数字`1`，就直接扔到栈里：

```
│   │
│   │
│   │
│   │
│   │
│   │
│   │
│ 1 │
└───┘
```

紧接着，遇到数字`2`，`9`，`5`，也扔到栈里：

```
│   │
│ 5 │
│   │
│ 9 │
│   │
│ 2 │
│   │
│ 1 │
└───┘
```

接下来遇到减号时，弹出栈顶的两个元素，并计算`9-5=4`，把结果`4`压栈：

```
│   │
│   │
│   │
│ 4 │
│   │
│ 2 │
│   │
│ 1 │
└───┘
```

接下来遇到`*`号时，弹出栈顶的两个元素，并计算`2*4=8`，把结果`8`压栈：

```
│   │
│   │
│   │
│   │
│   │
│ 8 │
│   │
│ 1 │
└───┘
```

接下来遇到`+`号时，弹出栈顶的两个元素，并计算`1+8=9`，把结果`9`压栈：

```
│   │
│   │
│   │
│   │
│   │
│   │
│   │
│ 9 │
└───┘
```

扫描结束后，没有更多的计算了，弹出栈的唯一一个元素，得到计算结果`9`。

### 小结
栈（Stack）是一种后进先出（LIFO）的数据结构，操作栈的元素的方法有：

- 把元素压栈：`push(E)`；
- 把栈顶的元素“弹出”：`pop(E)`；
- 取栈顶元素但不弹出：`peek(E)`。

在Java中，我们用`Deque`可以实现`Stack`的功能，注意只调用`push()`/`pop()`/`peek()`方法，避免调用`Deque`的其他方法。

最后，不要使用遗留类`Stack`。

## 使用 Iterator

Java的集合类都可以使用`for each`循环，`List`、`Set`和`Queue`会迭代每个元素，`Map`会迭代每个key。以`List`为例：

```java
List<String> list = List.of("Apple", "Orange", "Pear");
for (String s : list) {
    System.out.println(s);
}
```

实际上，Java编译器并不知道如何遍历`List`。上述代码能够编译通过，只是因为编译器把`for each`循环通过`Iterator`改写为了普通的`for`循环：

```java
for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
     String s = it.next();
     System.out.println(s);
}
```

我们把这种通过`Iterator`对象遍历集合的模式称为迭代器。

使用迭代器的好处在于，调用方总是以统一的方式遍历各种集合类型，而不必关心它们内部的存储结构。

例如，我们虽然知道ArrayList在内部是以数组形式存储元素，并且，它还提供了`get(int)`方法。虽然我们可以用`for`循环遍历：

```java
for (int i=0; i<list.size(); i++) {
    Object value = list.get(i);
}
```

但是这样一来，调用方就必须知道集合的内部存储结构。并且，如果把`ArrayList`换成`LinkedList`，`get(int)`方法耗时会随着index的增加而增加。如果把`ArrayList`换成`Set`，上述代码就无法编译，因为`Set`内部没有索引。

用`Iterator`遍历就没有上述问题，因为`Iterator`对象是集合对象自己在内部创建的，它自己知道如何高效遍历内部的数据集合，调用方则获得了统一的代码，编译器才能把标准的`for each`循环自动转换为`Iterator`遍历。

如果我们自己编写了一个集合类，想要使用`for each`循环，只需满足以下条件：

- 集合类实现`Iterable`接口，该接口要求返回一个`Iterator`对象；
- 用`Iterator`对象迭代集合内部数据。

这里的关键在于，集合类通过调用`iterator()`方法，返回一个`Iterator`对象，这个对象必须自己知道如何遍历该集合。

```java
// Iterator
import java.util.*;

public class Main {
    public static void main(String[] args) {
        ReverseList<String> rlist = new ReverseList<>();
        rlist.add("Apple");
        rlist.add("Orange");
        rlist.add("Pear");
        for (String s : rlist) {
            System.out.println(s);
        }
    }
}

class ReverseList<T> implements Iterable<T> {

    private List<T> list = new ArrayList<>();

    public void add(T t) {
        list.add(t);
    }

    @Override
    public Iterator<T> iterator() {
        return new ReverseIterator(list.size());
    }

    class ReverseIterator implements Iterator<T> {
        int index;

        ReverseIterator(int index) {
            this.index = index;
        }

        @Override
        public boolean hasNext() {
            return index > 0;
        }

        @Override
        public T next() {
            index--;
            return ReverseList.this.list.get(index);
        }
    }
}
```

虽然`ReverseList`和`ReverseIterator`的实现类稍微比较复杂，但是，注意到这是底层集合库，只需编写一次。而调用方则完全按`for each`循环编写代码，根本不需要知道集合内部的存储逻辑和遍历逻辑。

在编写`Iterator`的时候，我们通常可以用一个内部类来实现`Iterator`接口，这个内部类可以直接访问对应的外部类的所有字段和方法。例如，上述代码中，内部类`ReverseIterator`可以用`ReverseList.this`获得当前外部类的`this`引用，然后，通过这个`this`引用就可以访问`ReverseList`的所有字段和方法。

### 小结
`Iterator`是一种抽象的数据访问模型。使用`Iterator`模式进行迭代的好处有：

- 对任何集合都采用同一种访问模型；
- 调用者对集合内部结构一无所知；
- 集合类返回的`Iterator`对象知道如何迭代。

Java提供了标准的迭代器模型，即集合类实现`java.util.Iterable`接口，返回`java.util.Iterator`实例。

## 使用 Collections

`Collections`是JDK提供的工具类，同样位于`java.util`包中。它提供了一系列静态方法，能更方便地操作各种集合。

**注意Collections结尾多了一个s，不是Collection！**

我们一般看方法名和参数就可以确认`Collections`提供的该方法的功能。例如，对于以下静态方法：

```java
public static boolean addAll(Collection<? super T> c, T... elements) { ... }
```

`addAll()`方法可以给一个`Collection`类型的集合添加若干元素。因为方法签名是`Collection`，所以我们可以传入`List`，`Set`等各种集合类型。

### 创建空集合

`Collections`提供了一系列方法来创建空集合：

- 创建空List：`List<T> emptyList()`
- 创建空Map：`Map<K, V> emptyMap()`
- 创建空Set：`Set<T> emptySet()`

要注意到返回的空集合是不可变集合，无法向其中添加或删除元素。

此外，也可以用各个集合接口提供的`of(T...)`方法创建空集合。例如，以下创建空`List`的两个方法是等价的：

```java
List<String> list1 = List.of();
List<String> list2 = Collections.emptyList();
```

### 创建单元素集合

`Collections`提供了一系列方法来创建一个单元素集合：

- 创建一个元素的List：`List<T> singletonList(T o)`
- 创建一个元素的Map：`Map<K, V> singletonMap(K key, V value)`
- 创建一个元素的Set：`Set<T> singleton(T o)`

要注意到返回的单元素集合也是不可变集合，无法向其中添加或删除元素。

此外，也可以用各个集合接口提供的`of(T...)`方法创建单元素集合。例如，以下创建单元素`List`的两个方法是等价的：

```java
List<String> list1 = List.of("apple");
List<String> list2 = Collections.singletonList("apple");
```

实际上，使用`List.of(T...)`更方便，因为它既可以创建空集合，也可以创建单元素集合，还可以创建任意个元素的集合：

```java
List<String> list1 = List.of(); // empty list
List<String> list2 = List.of("apple"); // 1 element
List<String> list3 = List.of("apple", "pear"); // 2 elements
List<String> list4 = List.of("apple", "pear", "orange"); // 3 elements
```

### 排序

`Collections`可以对`List`进行排序。因为排序会直接修改`List`元素的位置，因此必须传入可变`List`：

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("apple");
        list.add("pear");
        list.add("orange");
        // 排序前:
        System.out.println(list);
        Collections.sort(list);
        // 排序后:
        System.out.println(list);
    }
}
```

### 洗牌

Collections提供了洗牌算法，即传入一个有序的List，可以随机打乱List内部元素的顺序，效果相当于让计算机洗牌：

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        for (int i=0; i<10; i++) {
            list.add(i);
        }
        // 洗牌前:
        System.out.println(list);
        Collections.shuffle(list);
        // 洗牌后:
        System.out.println(list);
    }
}
```

### 不可变集合

`Collections`还提供了一组方法把可变集合封装成不可变集合：

- 封装成不可变List：`List<T> unmodifiableList(List<? extends T> list)`
- 封装成不可变Set：`Set<T> unmodifiableSet(Set<? extends T> set)`
- 封装成不可变Map：`Map<K, V> unmodifiableMap(Map<? extends K, ? extends V> m)`

这种封装实际上是通过创建一个代理对象，拦截掉所有修改方法实现的。我们来看看效果：

```java
public class Main {
    public static void main(String[] args) {
        List<String> mutable = new ArrayList<>();
        mutable.add("apple");
        mutable.add("pear");
        // 变为不可变集合:
        List<String> immutable = Collections.unmodifiableList(mutable);
        immutable.add("orange"); // UnsupportedOperationException!
    }
}
```

然而，继续对原始的可变`List`进行增删是可以的，并且，会直接影响到封装后的“不可变”`List`：

```java
public class Main {
    public static void main(String[] args) {
        List<String> mutable = new ArrayList<>();
        mutable.add("apple");
        mutable.add("pear");
        // 变为不可变集合:
        List<String> immutable = Collections.unmodifiableList(mutable);
        mutable.add("orange");
        System.out.println(immutable);
    }
}
```

因此，如果我们希望把一个可变`List`封装成不可变`List`，那么，返回不可变`List`后，最好立刻扔掉可变`List`的引用，这样可以保证后续操作不会意外改变原始对象，从而造成“不可变”`List`变化了：

```java
public class Main {
    public static void main(String[] args) {
        List<String> mutable = new ArrayList<>();
        mutable.add("apple");
        mutable.add("pear");
        // 变为不可变集合:
        List<String> immutable = Collections.unmodifiableList(mutable);
        // 立刻扔掉mutable的引用:
        mutable = null;
        System.out.println(immutable);
    }
}
```

### 线程安全集合

`Collections`还提供了一组方法，可以把线程不安全的集合变为线程安全的集合：

- 变为线程安全的List：`List<T> synchronizedList(List<T> list)`
- 变为线程安全的Set：`Set<T> synchronizedSet(Set<T> s)`
- 变为线程安全的Map：`Map<K,V> synchronizedMap(Map<K,V> m)`

因为从Java 5开始，引入了更高效的并发集合类，所以上述这几个同步方法已经没有什么用了。

### 小结
Collections类提供了一组工具方法来方便使用集合类：

- 创建空集合；
- 创建单元素集合；
- 创建不可变集合；
- 排序／洗牌等操作。

# IO

IO是指Input/Output，即输入和输出。以内存为中心：

- Input指从外部读入数据到内存，例如，把文件从磁盘读取到内存，从网络读取数据到内存等等。
- Output指把数据从内存输出到外部，例如，把数据从内存写入到文件，把数据从内存输出到网络等等。

为什么要把数据读到内存才能处理这些数据？因为代码是在内存中运行的，数据也必须读到内存，最终的表示方式无非是byte数组，字符串等，都必须存放在内存里。

从Java代码来看，输入实际上就是从外部，例如，硬盘上的某个文件，把内容读到内存，并且以Java提供的某种数据类型表示，例如，`byte[]`，`String`，这样，后续代码才能处理这些数据。

因为内存有“易失性”的特点，所以必须把处理后的数据以某种方式输出，例如，写入到文件。Output实际上就是把Java表示的数据格式，例如，`byte[]`，`String`等输出到某个地方。

IO流是一种顺序读写数据的模式，它的特点是单向流动。数据类似自来水一样在水管中流动，所以我们把它称为IO流。

## InputStream / OutputStream

IO流以`byte`（字节）为最小单位，因此也称为字节流。例如，我们要从磁盘读入一个文件，包含6个字节，就相当于读入了6个字节的数据：

```
╔════════════╗
║   Memory   ║
╚════════════╝
       ▲
       │0x48
       │0x65
       │0x6c
       │0x6c
       │0x6f
       │0x21
 ╔═══════════╗
 ║ Hard Disk ║
 ╚═══════════╝
```

这6个字节是按顺序读入的，所以是输入字节流。

反过来，我们把6个字节从内存写入磁盘文件，就是输出字节流：

```
╔════════════╗
║   Memory   ║
╚════════════╝
       │0x21
       │0x6f
       │0x6c
       │0x6c
       │0x65
       │0x48
       ▼
 ╔═══════════╗
 ║ Hard Disk ║
 ╚═══════════╝
```

在Java中，`InputStream`代表输入字节流，`OuputStream`代表输出字节流，这是最基本的两种IO流。

## Reader / Writer

如果我们需要读写的是字符，并且字符不全是单字节表示的ASCII字符，那么，按照`char`来读写显然更方便，这种流称为字符流。

Java提供了`Reader`和`Writer`表示字符流，字符流传输的最小数据单位是`char`。

例如，我们把`char[]`数组`Hi你好`这4个字符用`Writer`字符流写入文件，并且使用UTF-8编码，得到的最终文件内容是8个字节，英文字符`H`和`i`各占一个字节，中文字符`你好`各占3个字节：

```
0x48
0x69
0xe4bda0
0xe5a5bd
```

反过来，我们用`Reader`读取以UTF-8编码的这8个字节，会从`Reader`中得到`Hi你好`这4个字符。

因此，`Reader`和`Writer`本质上是一个能自动编解码的`InputStream`和`OutputStream`。

使用`Reader`，数据源虽然是字节，但我们读入的数据都是`char`类型的字符，原因是`Reader`内部把读入的`byte`做了解码，转换成了`char`。使用`InputStream`，我们读入的数据和原始二进制数据一模一样，是`byte[]`数组，但是我们可以自己把二进制`byte[]`数组按照某种编码转换为字符串。究竟使用`Reader`还是`InputStream`，要取决于具体的使用场景。如果数据源不是文本，就只能使用`InputStream`，如果数据源是文本，使用`Reader`更方便一些。`Writer`和`OutputStream`是类似的。

## 同步和异步

同步IO是指，读写IO时代码必须等待数据返回后才继续执行后续代码，它的优点是代码编写简单，缺点是CPU执行效率低。

而异步IO是指，读写IO时仅发出请求，然后立刻执行后续代码，它的优点是CPU执行效率高，缺点是代码编写复杂。

Java标准库的包`java.io`提供了同步IO，而`java.nio`则是异步IO。上面我们讨论的`InputStream`、`OutputStream`、`Reader`和`Writer`都是同步IO的抽象类，对应的具体实现类，以文件为例，有`FileInputStream`、`FileOutputStream`、`FileReader`和`FileWriter`。

## IO小结
IO流是一种流式的数据输入/输出模型：

- 二进制数据以byte为最小单位在InputStream/OutputStream中单向流动；
- 字符数据以char为最小单位在Reader/Writer中单向流动。

Java标准库的java.io包提供了同步IO功能：

- 字节流接口：InputStream/OutputStream；
- 字符流接口：Reader/Writer。

## File 对象

在计算机系统中，文件是非常重要的存储方式。Java的标准库`java.io`提供了`File`对象来操作文件和目录。

要构造一个`File`对象，需要传入文件路径：

```java
public class Main {
    public static void main(String[] args) {
        File f = new File("C:\\Windows\\notepad.exe");
        System.out.println(f);
    }
}
```

构造File对象时，既可以传入绝对路径，也可以传入相对路径。绝对路径是以根目录开头的完整路径，例如：

```java
File f = new File("C:\\Windows\\notepad.exe");
```

注意Windows平台使用`\`作为路径分隔符，在Java字符串中需要用`\\`表示一个`\`。Linux平台使用`/`作为路径分隔符：

```java
File f = new File("/usr/bin/javac");
```

传入相对路径时，相对路径前面加上当前目录就是绝对路径：

```java
// 假设当前目录是C:\Docs
File f1 = new File("sub\\javac"); // 绝对路径是C:\Docs\sub\javac
File f3 = new File(".\\sub\\javac"); // 绝对路径是C:\Docs\sub\javac
File f3 = new File("..\\sub\\javac"); // 绝对路径是C:\sub\javac
```

可以用`.`表示当前目录，`..`表示上级目录。

File对象有3种形式表示的路径，一种是`getPath()`，返回构造方法传入的路径，一种是`getAbsolutePath()`，返回绝对路径，一种是`getCanonicalPath`，它和绝对路径类似，但是返回的是规范路径。

什么是规范路径？我们看以下代码：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        File f = new File("..");
        System.out.println(f.getPath());
        System.out.println(f.getAbsolutePath());
        System.out.println(f.getCanonicalPath());
    }
}
```

绝对路径可以表示成`C:\Windows\System32\..\notepad.exe`，而规范路径就是把`.`和`..`转换成标准的绝对路径后的路径：`C:\Windows\notepad.exe`。

因为Windows和Linux的路径分隔符不同，File对象有一个静态变量用于表示当前平台的系统分隔符：

```java
System.out.println(File.separator); // 根据当前平台打印"\"或"/"
```

### 文件和目录

`File`对象既可以表示文件，也可以表示目录。特别要注意的是，构造一个`File`对象，即使传入的文件或目录不存在，代码也不会出错，因为构造一个`File`对象，并不会导致任何磁盘操作。只有当我们调用`File`对象的某些方法的时候，才真正进行磁盘操作。

例如，调用`isFile()`，判断该`File`对象是否是一个已存在的文件，调用`isDirectory()`，判断该`File`对象是否是一个已存在的目录：

```java
    public static void main(String[] args) throws IOException {
        File f1 = new File("C:\\Windows");
        File f2 = new File("C:\\Windows\\notepad.exe");
        File f3 = new File("C:\\Windows\\nothing");
        System.out.println(f1.isFile());
        System.out.println(f1.isDirectory());
        System.out.println(f2.isFile());
        System.out.println(f2.isDirectory());
        System.out.println(f3.isFile());
        System.out.println(f3.isDirectory());
    }
}
```

用File对象获取到一个文件时，还可以进一步判断文件的权限和大小：

 - `boolean canRead()`：是否可读；
 - `boolean canWrite()`：是否可写；
 - `boolean canExecute()`：是否可执行；
 - `long length()`：文件字节大小。

对目录而言，是否可执行表示能否列出它包含的文件和子目录。

### 创建和删除文件

当File对象表示一个文件时，可以通过`createNewFile()`创建一个新文件，用d`elete()`删除该文件：

```java
File file = new File("/path/to/file");
if (file.createNewFile()) {
    // 文件创建成功:
    // TODO:
    if (file.delete()) {
        // 删除文件成功:
    }
}
```

有些时候，程序需要读写一些临时文件，File对象提供了`createTempFile()`来创建一个临时文件，以及`deleteOnExit()`在JVM退出时自动删除该文件。

```java
public class Main {
    public static void main(String[] args) throws IOException {
        File f = File.createTempFile("tmp-", ".txt"); // 提供临时文件的前缀和后缀
        f.deleteOnExit(); // JVM退出时自动删除
        System.out.println(f.isFile());
        System.out.println(f.getAbsolutePath());
    }
}
```

### 遍历文件和目录

当File对象表示一个目录时，可以使用`list()`和`listFiles()`列出目录下的文件和子目录名。`listFiles()`提供了一系列重载方法，可以过滤不想要的文件和目录：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        File f = new File("C:\\Windows");
        File[] fs1 = f.listFiles(); // 列出所有文件和子目录
        printFiles(fs1);
        File[] fs2 = f.listFiles(new FilenameFilter() { // 仅列出.exe文件
            public boolean accept(File dir, String name) {
                return name.endsWith(".exe"); // 返回true表示接受该文件
            }
        });
        printFiles(fs2);
    }

    static void printFiles(File[] files) {
        System.out.println("==========");
        if (files != null) {
            for (File f : files) {
                System.out.println(f);
            }
        }
        System.out.println("==========");
    }
}
```

和文件操作类似，File对象如果表示一个目录，可以通过以下方法创建和删除目录：

- `boolean mkdir()`：创建当前File对象表示的目录；
- `boolean mkdirs()`：创建当前File对象表示的目录，并在必要时将不存在的父目录也创建出来；
- `boolean delete()`：删除当前File对象表示的目录，当前目录必须为空才能删除成功。

### Path

Java标准库还提供了一个`Path`对象，它位于`java.nio.file`包。`Path`对象和`File`对象类似，但操作更加简单：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        Path p1 = Paths.get(".", "project", "study"); // 构造一个Path对象
        System.out.println(p1);
        Path p2 = p1.toAbsolutePath(); // 转换为绝对路径
        System.out.println(p2);
        Path p3 = p2.normalize(); // 转换为规范路径
        System.out.println(p3);
        File f = p3.toFile(); // 转换为File对象
        System.out.println(f);
        for (Path p : Paths.get("..").toAbsolutePath()) { // 可以直接遍历Path
            System.out.println("  " + p);
        }
    }
}
```

如果需要对目录进行复杂的拼接、遍历等操作，使用`Path`对象更方便。

### 小结

Java标准库的`java.io.File`对象表示一个文件或者目录：

- 创建`File`对象本身不涉及IO操作；
- 可以获取路径／绝对路径／规范路径：`getPath()`/`getAbsolutePath()`/`getCanonicalPath()`；
- 可以获取目录的文件和子目录：`list()`/`listFiles()`；
- 可以创建或删除文件和目录。

## InputStream

`InputStream`就是Java标准库提供的最基本的输入流。它位于`java.io`这个包里。`java.io`包提供了所有同步IO的功能。

要特别注意的一点是，`InputStream`并不是一个接口，而是一个抽象类，它是所有输入流的超类。这个抽象类定义的一个最重要的方法就是`int read()`，签名如下：

```java
public abstract int read() throws IOException;
```

这个方法会读取输入流的下一个字节，并返回字节表示的`int`值（0~255）。如果已读到末尾，返回`-1`表示不能继续读取了。

`FileInputStream`是`InputStream`的一个子类。顾名思义，`FileInputStream`就是从文件流中读取数据。下面的代码演示了如何完整地读取一个`FileInputStream`的所有字节：

```java
public void readFile() throws IOException {
    // 创建一个FileInputStream对象:
    InputStream input = new FileInputStream("src/readme.txt");
    for (;;) {
        int n = input.read(); // 反复调用read()方法，直到返回-1
        if (n == -1) {
            break;
        }
        System.out.println(n); // 打印byte的值
    }
    input.close(); // 关闭流
}
```

在计算机中，类似文件、网络端口这些资源，都是由操作系统统一管理的。应用程序在运行的过程中，如果打开了一个文件进行读写，完成后要及时地关闭，以便让操作系统把资源释放掉，否则，应用程序占用的资源会越来越多，不但白白占用内存，还会影响其他应用程序的运行。

`InputStream`和`OutputStream`都是通过`close()`方法来关闭流。关闭流就会释放对应的底层资源。

我们还要注意到在读取或写入IO流的过程中，可能会发生错误，例如，文件不存在导致无法读取，没有写权限导致写入失败，等等，这些底层错误由Java虚拟机自动封装成`IOException`异常并抛出。因此，所有与IO操作相关的代码都必须正确处理`IOException`。

仔细观察上面的代码，会发现一个潜在的问题：如果读取过程中发生了IO错误，`InputStream`就没法正确地关闭，资源也就没法及时释放。

因此，我们需要用`try ... finally`来保证`InputStream`在无论是否发生IO错误的时候都能够正确地关闭：

```java
public void readFile() throws IOException {
    InputStream input = null;
    try {
        input = new FileInputStream("src/readme.txt");
        int n;
        while ((n = input.read()) != -1) { // 利用while同时读取并判断
            System.out.println(n);
        }
    } finally {
        if (input != null) { input.close(); }
    }
}
```

用`try ... finally`来编写上述代码会感觉比较复杂，更好的写法是利用Java 7引入的新的`try(resource)`的语法，只需要编写`try`语句，让编译器自动为我们关闭资源。推荐的写法如下：

```java
public void readFile() throws IOException {
    try (InputStream input = new FileInputStream("src/readme.txt")) {
        int n;
        while ((n = input.read()) != -1) {
            System.out.println(n);
        }
    } // 编译器在此自动为我们写入finally并调用close()
}
```

实际上，编译器并不会特别地为`InputStream`加上自动关闭。编译器只看`try(resource = ...)`中的对象是否实现了`java.lang.AutoCloseable`接口，如果实现了，就自动加上`finally`语句并调用`close()`方法。`InputStream`和`OutputStream`都实现了这个接口，因此，都可以用在`try(resource)`中。

### 缓冲

在读取流的时候，一次读取一个字节并不是最高效的方法。很多流支持一次性读取多个字节到缓冲区，对于文件和网络流来说，利用缓冲区一次性读取多个字节效率往往要高很多。`InputStream`提供了两个重载方法来支持读取多个字节：

- `int read(byte[] b)`：读取若干字节并填充到`byte[]`数组，返回读取的字节数
- `int read(byte[] b, int off, int len)`：指定`byte[]`数组的偏移量和最大填充数

利用上述方法一次读取多个字节时，需要先定义一个`byte[]`数组作为缓冲区，`read()`方法会尽可能多地读取字节到缓冲区， 但不会超过缓冲区的大小。`read()`方法的返回值不再是字节的`int`值，而是返回实际读取了多少个字节。如果返回`-1`，表示没有更多的数据了。

利用缓冲区一次读取多个字节的代码如下：

```java
public void readFile() throws IOException {
    try (InputStream input = new FileInputStream("src/readme.txt")) {
        // 定义1000个字节大小的缓冲区:
        byte[] buffer = new byte[1000];
        int n;
        while ((n = input.read(buffer)) != -1) { // 读取到缓冲区
            System.out.println("read " + n + " bytes.");
        }
    }
}
```

### 阻塞

在调用`InputStream`的`read()`方法读取数据时，我们说`read()`方法是阻塞（Blocking）的。它的意思是，对于下面的代码：

```java
int n;
n = input.read(); // 必须等待read()方法返回才能执行下一行代码
int m = n;
```

执行到第二行代码时，必须等`read()`方法返回后才能继续。因为读取IO流相比执行普通代码，速度会慢很多，因此，无法确定`read()`方法调用到底要花费多长时间。

### InputStream实现类

用`FileInputStream`可以从文件获取输入流，这是`InputStream`常用的一个实现类。此外，`ByteArrayInputStream`可以在内存中模拟一个`InputStream`：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        byte[] data = { 72, 101, 108, 108, 111, 33 };
        try (InputStream input = new ByteArrayInputStream(data)) {
            int n;
            while ((n = input.read()) != -1) {
                System.out.println((char)n);
            }
        }
    }
}
```

`ByteArrayInputStream`实际上是把一个`byte[]`数组在内存中变成一个`InputStream`，虽然实际应用不多，但测试的时候，可以用它来构造一个`InputStream`。

举个栗子：我们想从文件中读取所有字节，并转换成`char`然后拼成一个字符串，可以这么写：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        String s;
*         try (InputStream input = new FileInputStream("C:\\test\\README.txt")) {
            int n;
            StringBuilder sb = new StringBuilder();
            while ((n = input.read()) != -1) {
                sb.append((char) n);
            }
            s = sb.toString();
        }
        System.out.println(s);
    }
}
```

要测试上面的程序，就真的需要在本地硬盘上放一个真实的文本文件。如果我们把代码稍微改造一下，提取一个`readAsString()`的方法：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        String s;
        try (InputStream input = new FileInputStream("C:\\test\\README.txt")) {
            s = readAsString(input);
        }
        System.out.println(s);
    }

    public static String readAsString(InputStream input) throws IOException {
        int n;
        StringBuilder sb = new StringBuilder();
        while ((n = input.read()) != -1) {
            sb.append((char) n);
        }
        return sb.toString();
    }
}
```

对这个`String readAsString(InputStream input)`方法进行测试就相当简单，因为不一定要传入一个真的`FileInputStream`：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        byte[] data = { 72, 101, 108, 108, 111, 33 };
        try (InputStream input = new ByteArrayInputStream(data)) {
            String s = readAsString(input);
            System.out.println(s);
        }
    }

    public static String readAsString(InputStream input) throws IOException {
        int n;
        StringBuilder sb = new StringBuilder();
        while ((n = input.read()) != -1) {
            sb.append((char) n);
        }
        return sb.toString();
    }
}
```

这就是面向抽象编程原则的应用：接受`InputStream`抽象类型，而不是具体的`FileInputStream`类型，从而使得代码可以处理`InputStream`的任意实现类。

### 小结

Java标准库的`java.io.InputStream`定义了所有输入流的超类：

- `FileInputStream`实现了文件流输入；
- `ByteArrayInputStream`在内存中模拟一个字节流输入。

总是使用`try(resource)`来保证`InputStream`正确关闭。

## OutputStream

和`InputStream`相反，`OutputStream`是Java标准库提供的最基本的输出流。

和`InputStream`类似，`OutputStream`也是抽象类，它是所有输出流的超类。这个抽象类定义的一个最重要的方法就是`void write(int b)`，签名如下：

```java
public abstract void write(int b) throws IOException;
```

这个方法会写入一个字节到输出流。要注意的是，虽然传入的是`int`参数，但只会写入一个字节，即只写入`int`最低8位表示字节的部分（相当于`b & 0xff`）。

和`InputStream`类似，`OutputStream`也提供了`close()`方法关闭输出流，以便释放系统资源。要特别注意：`OutputStream`还提供了一个`flush()`方法，它的目的是将缓冲区的内容真正输出到目的地。

为什么要有`flush()`？因为向磁盘、网络写入数据的时候，出于效率的考虑，操作系统并不是输出一个字节就立刻写入到文件或者发送到网络，而是把输出的字节先放到内存的一个缓冲区里（本质上就是一个`byte[]`数组），等到缓冲区写满了，再一次性写入文件或者网络。对于很多IO设备来说，一次写一个字节和一次写1000个字节，花费的时间几乎是完全一样的，所以`OutputStream`有个`flush()`方法，能强制把缓冲区内容输出。

通常情况下，我们不需要调用这个`flush()`方法，因为缓冲区写满了`OutputStream`会自动调用它，并且，在调用`close()`方法关闭`OutputStream`之前，也会自动调用`flush()`方法。

但是，在某些情况下，我们必须手动调用`flush()`方法。举个栗子：

小明正在开发一款在线聊天软件，当用户输入一句话后，就通过`OutputStream`的`write()`方法写入网络流。小明测试的时候发现，发送方输入后，接收方根本收不到任何信息，怎么肥四？

原因就在于写入网络流是先写入内存缓冲区，等缓冲区满了才会一次性发送到网络。如果缓冲区大小是4K，则发送方要敲几千个字符后，操作系统才会把缓冲区的内容发送出去，这个时候，接收方会一次性收到大量消息。

解决办法就是每输入一句话后，立刻调用`flush()`，不管当前缓冲区是否已满，强迫操作系统把缓冲区的内容立刻发送出去。

实际上，`InputStream`也有缓冲区。例如，从`FileInputStream`读取一个字节时，操作系统往往会一次性读取若干字节到缓冲区，并维护一个指针指向未读的缓冲区。然后，每次我们调用`int read()`读取下一个字节时，可以直接返回缓冲区的下一个字节，避免每次读一个字节都导致IO操作。当缓冲区全部读完后继续调用`read()`，则会触发操作系统的下一次读取并再次填满缓冲区。

### FileOutputStream

我们以`FileOutputStream`为例，演示如何将若干个字节写入文件流：

```java
public void writeFile() throws IOException {
    OutputStream output = new FileOutputStream("out/readme.txt");
    output.write(72); // H
    output.write(101); // e
    output.write(108); // l
    output.write(108); // l
    output.write(111); // o
    output.close();
}
```

每次写入一个字节非常麻烦，更常见的方法是一次性写入若干字节。这时，可以用`OutputStream`提供的重载方法`void write(byte[])`来实现：

```java
public void writeFile() throws IOException {
    OutputStream output = new FileOutputStream("out/readme.txt");
    output.write("Hello".getBytes("UTF-8")); // Hello
    output.close();
}
```

和`InputStream`一样，上述代码没有考虑到在发生异常的情况下如何正确地关闭资源。写入过程也会经常发生IO错误，例如，磁盘已满，无权限写入等等。我们需要用`try(resource)`来保证`OutputStream`在无论是否发生IO错误的时候都能够正确地关闭：

```java
public void writeFile() throws IOException {
    try (OutputStream output = new FileOutputStream("out/readme.txt")) {
        output.write("Hello".getBytes("UTF-8")); // Hello
    } // 编译器在此自动为我们写入finally并调用close()
}
```

### 阻塞

和`InputStream`一样，`OutputStream`的`write()`方法也是阻塞的。

### OutputStream实现类

用`FileOutputStream`可以从文件获取输出流，这是`OutputStream`常用的一个实现类。此外，`ByteArrayOutputStream`可以在内存中模拟一个`OutputStream`：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        byte[] data;
        try (ByteArrayOutputStream output = new ByteArrayOutputStream()) {
            output.write("Hello ".getBytes("UTF-8"));
            output.write("world!".getBytes("UTF-8"));
            data = output.toByteArray();
        }
        System.out.println(new String(data, "UTF-8"));
    }
}
```

`ByteArrayOutputStream`实际上是把一个`byte[]`数组在内存中变成一个`OutputStream`，虽然实际应用不多，但测试的时候，可以用它来构造一个`OutputStream`。

同时操作多个`AutoCloseable`资源时，在`try(resource) { ... }`语句中可以同时写出多个资源，用`;`隔开。例如，同时读写两个文件：

```java
// 读取input.txt，写入output.txt:
try (InputStream input = new FileInputStream("input.txt");
     OutputStream output = new FileOutputStream("output.txt"))
{
    input.transferTo(output); // transferTo的作用是?
}
```

### 小结

Java标准库的java.io.OutputStream定义了所有输出流的超类：

- FileOutputStream实现了文件流输出；
- ByteArrayOutputStream在内存中模拟一个字节流输出。

某些情况下需要手动调用OutputStream的flush()方法来强制输出缓冲区。

总是使用try(resource)来保证OutputStream正确关闭。

## Filter 模式

Java的IO标准库提供的`InputStream`根据来源可以包括：

- `FileInputStream`：从文件读取数据，是最终数据源；
- `ServletInputStream`：从HTTP请求读取数据，是最终数据源；
- `Socket.getInputStream()`：从TCP连接读取数据，是最终数据源；
- ...

如果我们要给`FileInputStream`添加缓冲功能，则可以从`FileInputStream`派生一个类：

```java
BufferedFileInputStream extends FileInputStream
```

如果要给`FileInputStream`添加计算签名的功能，类似的，也可以从`FileInputStream`派生一个类：

```java
DigestFileInputStream extends FileInputStream
```

如果要给`FileInputStream`添加加密/解密功能，还是可以从`FileInputStream`派生一个类：

```java
CipherFileInputStream extends FileInputStream
```

如果要给`FileInputStream`添加缓冲和签名的功能，那么我们还需要派生`BufferedDigestFileInputStream`。如果要给`FileInputStream`添加缓冲和加解密的功能，则需要派生`BufferedCipherFileInputStream`。

我们发现，给`FileInputStream`添加3种功能，至少需要3个子类。这3种功能的组合，又需要更多的子类：

```
                          ┌─────────────────┐
                          │ FileInputStream │
                          └─────────────────┘
                                   ▲
             ┌───────────┬─────────┼─────────┬───────────┐
             │           │         │         │           │
┌───────────────────────┐│┌─────────────────┐│┌─────────────────────┐
│BufferedFileInputStream│││DigestInputStream│││CipherFileInputStream│
└───────────────────────┘│└─────────────────┘│└─────────────────────┘
                         │                   │
    ┌─────────────────────────────┐ ┌─────────────────────────────┐
    │BufferedDigestFileInputStream│ │BufferedCipherFileInputStream│
    └─────────────────────────────┘ └─────────────────────────────┘
```

这还只是针对`FileInputStream`设计，如果针对另一种`InputStream`设计，很快会出现子类爆炸的情况。

因此，直接使用继承，为各种`InputStream`附加更多的功能，根本无法控制代码的复杂度，很快就会失控。

为了解决依赖继承会导致子类数量失控的问题，JDK首先将`InputStream`分为两大类：

一类是直接提供数据的基础`InputStream`，例如：

- FileInputStream
- ByteArrayInputStream
- ServletInputStream
- ...

一类是提供额外附加功能的`InputStream`，例如：

- BufferedInputStream
- DigestInputStream
- CipherInputStream
- ...

当我们需要给一个“基础”`InputStream`附加各种功能时，我们先确定这个能提供数据源的`InputStream`，因为我们需要的数据总得来自某个地方，例如，`FileInputStream`，数据来源自文件：

```java
InputStream file = new FileInputStream("test.gz");
```

紧接着，我们希望`FileInputStream`能提供缓冲的功能来提高读取的效率，因此我们用`BufferedInputStream`包装这个`InputStream`，得到的包装类型是`BufferedInputStream`，但它仍然被视为一个`InputStream`：

```java
InputStream buffered = new BufferedInputStream(file);
```

最后，假设该文件已经用gzip压缩了，我们希望直接读取解压缩的内容，就可以再包装一个`GZIPInputStream`：

```java
InputStream gzip = new GZIPInputStream(buffered);
```

无论我们包装多少次，得到的对象始终是`InputStream`，我们直接用`InputStream`来引用它，就可以正常读取：

```
┌─────────────────────────┐
│GZIPInputStream          │
│┌───────────────────────┐│
││BufferedFileInputStream││
││┌─────────────────────┐││
│││   FileInputStream   │││
││└─────────────────────┘││
│└───────────────────────┘│
└─────────────────────────┘
```

上述这种通过一个“基础”组件再叠加各种“附加”功能组件的模式，称之为Filter模式（或者装饰器模式：Decorator）。它可以让我们通过少量的类来实现各种功能的组合：

```
                 ┌─────────────┐
                 │ InputStream │
                 └─────────────┘
                       ▲ ▲
┌────────────────────┐ │ │ ┌─────────────────┐
│  FileInputStream   │─┤ └─│FilterInputStream│
└────────────────────┘ │   └─────────────────┘
┌────────────────────┐ │     ▲ ┌───────────────────┐
│ByteArrayInputStream│─┤     ├─│BufferedInputStream│
└────────────────────┘ │     │ └───────────────────┘
┌────────────────────┐ │     │ ┌───────────────────┐
│ ServletInputStream │─┘     ├─│  DataInputStream  │
└────────────────────┘       │ └───────────────────┘
                             │ ┌───────────────────┐
                             └─│CheckedInputStream │
                               └───────────────────┘
```

类似的，`OutputStream`也是以这种模式来提供各种功能：

```
                  ┌─────────────┐
                  │OutputStream │
                  └─────────────┘
                        ▲ ▲
┌─────────────────────┐ │ │ ┌──────────────────┐
│  FileOutputStream   │─┤ └─│FilterOutputStream│
└─────────────────────┘ │   └──────────────────┘
┌─────────────────────┐ │     ▲ ┌────────────────────┐
│ByteArrayOutputStream│─┤     ├─│BufferedOutputStream│
└─────────────────────┘ │     │ └────────────────────┘
┌─────────────────────┐ │     │ ┌────────────────────┐
│ ServletOutputStream │─┘     ├─│  DataOutputStream  │
└─────────────────────┘       │ └────────────────────┘
                              │ ┌────────────────────┐
                              └─│CheckedOutputStream │
                                └────────────────────┘
```

### 编写FilterInputStream

我们也可以自己编写`FilterInputStream`，以便可以把自己的`FilterInputStream`“叠加”到任何一个`InputStream`中。

下面的例子演示了如何编写一个`CountInputStream`，它的作用是对输入的字节进行计数：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        byte[] data = "hello, world!".getBytes("UTF-8");
        try (CountInputStream input = new CountInputStream(new ByteArrayInputStream(data))) {
            int n;
            while ((n = input.read()) != -1) {
                System.out.println((char)n);
            }
            System.out.println("Total read " + input.getBytesRead() + " bytes");
        }
    }
}

class CountInputStream extends FilterInputStream {
    private int count = 0;

    CountInputStream(InputStream in) {
        super(in);
    }

    public int getBytesRead() {
        return this.count;
    }

    public int read() throws IOException {
        int n = in.read();
        if (n != -1) {
            this.count ++;
        }
        return n;
    }

    public int read(byte[] b, int off, int len) throws IOException {
        int n = in.read(b, off, len);
        if (n != -1) {
            this.count += n;
        }
        return n;
    }
}
```

注意到在叠加多个`FilterInputStream`，我们只需要持有最外层的`InputStream`，并且，当最外层的`InputStream`关闭时（在`try(resource)`块的结束处自动关闭），内层的`InputStream`的`close()`方法也会被自动调用，并最终调用到最核心的“基础”`InputStream`，因此不存在资源泄露。

### 小结
Java的IO标准库使用Filter模式为`InputStream`和`OutputStream`增加功能：

- 可以把一个`InputStream`和任意个`FilterInputStream`组合；
- 可以把一个`OutputStream`和任意个`FilterOutputStream`组合。

Filter模式可以在运行期动态增加功能（又称Decorator模式）。

## 操作 Zip

`ZipInputStream`是一种`FilterInputStream`，它可以直接读取zip包的内容：

```
┌───────────────────┐
│    InputStream    │
└───────────────────┘
          ▲
          │
┌───────────────────┐
│ FilterInputStream │
└───────────────────┘
          ▲
          │
┌───────────────────┐
│InflaterInputStream│
└───────────────────┘
          ▲
          │
┌───────────────────┐
│  ZipInputStream   │
└───────────────────┘
          ▲
          │
┌───────────────────┐
│  JarInputStream   │
└───────────────────┘
```

另一个`JarInputStream`是从`ZipInputStream`派生，它增加的主要功能是直接读取jar文件里面的`MANIFEST.MF`文件。因为本质上jar包就是zip包，只是额外附加了一些固定的描述文件。

### 读取zip包

我们来看看`ZipInputStream`的基本用法。

我们要创建一个`ZipInputStream`，通常是传入一个`FileInputStream`作为数据源，然后，循环调用`getNextEntry()`，直到返回`null`，表示zip流结束。

一个`ZipEntry`表示一个压缩文件或目录，如果是压缩文件，我们就用`read()`方法不断读取，直到返回`-1`：

```java
try (ZipInputStream zip = new ZipInputStream(new FileInputStream(...))) {
    ZipEntry entry = null;
    while ((entry = zip.getNextEntry()) != null) {
        String name = entry.getName();
        if (!entry.isDirectory()) {
            int n;
            while ((n = zip.read()) != -1) {
                ...
            }
        }
    }
}
```

### 写入zip包

`ZipOutputStream`是一种`FilterOutputStream`，它可以直接写入内容到zip包。我们要先创建一个`ZipOutputStream`，通常是包装一个`FileOutputStream`，然后，每写入一个文件前，先调用`putNextEntry()`，然后用`write()`写入`byte[]`数据，写入完毕后调用`closeEntry()`结束这个文件的打包。

```java
try (ZipOutputStream zip = new ZipOutputStream(new FileOutputStream(...))) {
    File[] files = ...
    for (File file : files) {
        zip.putNextEntry(new ZipEntry(file.getName()));
        zip.write(Files.readAllBytes(file.toPath()));
        zip.closeEntry();
    }
}
```

上面的代码没有考虑文件的目录结构。如果要实现目录层次结构，`new ZipEntry(name)`传入的`name`要用相对路径。

### 小结

`ZipInputStream`可以读取zip格式的流，`ZipOutputStream`可以把多份数据写入zip包；

配合`FileInputStream`和`FileOutputStream`就可以读写zip文件。

## 读取 classpatch 资源

很多Java程序启动的时候，都需要读取配置文件。例如，从一个`.properties`文件中读取配置：

```java
String conf = "C:\\conf\\default.properties";
try (InputStream input = new FileInputStream(conf)) {
    // TODO:
}
```

这段代码要正常执行，必须在C盘创建`conf`目录，然后在目录里创建`default.properties`文件。但是，在Linux系统上，路径和Windows的又不一样。

因此，从磁盘的固定目录读取配置文件，不是一个好的办法。

有没有路径无关的读取文件的方式呢？

我们知道，Java存放`.class`的目录或jar包也可以包含任意其他类型的文件，例如：

- 配置文件，例如`.properties`；
- 图片文件，例如`.jpg`；
- 文本文件，例如`.txt`，`.csv`；
- ……

从classpath读取文件就可以避免不同环境下文件路径不一致的问题：如果我们把`default.properties`文件放到classpath中，就不用关心它的实际存放路径。

在classpath中的资源文件，路径总是以`／`开头，我们先获取当前的`Class`对象，然后调用`getResourceAsStream()`就可以直接从classpath读取任意的资源文件：

```java
try (InputStream input = getClass().getResourceAsStream("/default.properties")) {
    // TODO:
}
```

调用`getResourceAsStream()`需要特别注意的一点是，如果资源文件不存在，它将返回`null`。因此，我们需要检查返回的`InputStream`是否为`null`，如果为`null`，表示资源文件在classpath中没有找到：

```java
try (InputStream input = getClass().getResourceAsStream("/default.properties")) {
    if (input != null) {
        // TODO:
    }
}
```

如果我们把默认的配置放到jar包中，再从外部文件系统读取一个可选的配置文件，就可以做到既有默认的配置文件，又可以让用户自己修改配置：

```java
Properties props = new Properties();
props.load(inputStreamFromClassPath("/default.properties"));
props.load(inputStreamFromFile("./conf.properties"));
```

这样读取配置文件，应用程序启动就更加灵活。

### 小结

把资源存储在classpath中可以避免文件路径依赖；

`Class`对象的`getResourceAsStream()`可以从classpath中读取指定资源；

根据classpath读取资源时，需要检查返回的`InputStream`是否为`null`。

## 序列化

序列化是指把一个Java对象变成二进制内容，本质上就是一个`byte[]`数组。

为什么要把Java对象序列化呢？因为序列化后可以把`byte[]`保存到文件中，或者把`byte[]`通过网络传输到远程，这样，就相当于把Java对象存储到文件或者通过网络传输出去了。

有序列化，就有反序列化，即把一个二进制内容（也就是`byte[]`数组）变回Java对象。有了反序列化，保存到文件中的`byte[]`数组又可以“变回”Java对象，或者从网络上读取`byte[]`并把它“变回”Java对象。

我们来看看如何把一个Java对象序列化。

一个Java对象要能序列化，必须实现一个特殊的`java.io.Serializable`接口，它的定义如下：

```java
public interface Serializable {
}
```

`Serializable`接口没有定义任何方法，它是一个空接口。我们把这样的空接口称为“标记接口”（Marker Interface），实现了标记接口的类仅仅是给自身贴了个“标记”，并没有增加任何方法。

### 序列化

把一个Java对象变为`byte[]`数组，需要使用`ObjectOutputStream`。它负责把一个Java对象写入一个字节流：

```java
public class Main {
    public static void main(String[] args) throws IOException {
        ByteArrayOutputStream buffer = new ByteArrayOutputStream();
        try (ObjectOutputStream output = new ObjectOutputStream(buffer)) {
            // 写入int:
            output.writeInt(12345);
            // 写入String:
            output.writeUTF("Hello");
            // 写入Object:
            output.writeObject(Double.valueOf(123.456));
        }
        System.out.println(Arrays.toString(buffer.toByteArray()));
    }
}
```

`ObjectOutputStream`既可以写入基本类型，如`int`，`boolean`，也可以写入`String`（以UTF-8编码），还可以写入实现了`Serializable`接口的`Object`。

因为写入`Object`时需要大量的类型信息，所以写入的内容很大。

### 反序列化

和`ObjectOutputStream`相反，`ObjectInputStream`负责从一个字节流读取Java对象：

```java
try (ObjectInputStream input = new ObjectInputStream(...)) {
    int n = input.readInt();
    String s = input.readUTF();
    Double d = (Double) input.readObject();
}
```

除了能读取基本类型和`String`类型外，调用`readObject()`可以直接返回一个`Object`对象。要把它变成一个特定类型，必须强制转型。

`readObject()`可能抛出的异常有：

- `ClassNotFoundException`：没有找到对应的Class；
- `InvalidClassException`：Class不匹配。

对于`ClassNotFoundException`，这种情况常见于一台电脑上的Java程序把一个Java对象，例如，`Person`对象序列化以后，通过网络传给另一台电脑上的另一个Java程序，但是这台电脑的Java程序并没有定义`Person`类，所以无法反序列化。

对于`InvalidClassException`，这种情况常见于序列化的`Person`对象定义了一个`int`类型的`age`字段，但是反序列化时，`Person`类定义的`age`字段被改成了`long`类型，所以导致class不兼容。

为了避免这种class定义变动导致的不兼容，Java的序列化允许class定义一个特殊的`serialVersionUID`静态变量，用于标识Java类的序列化“版本”，通常可以由IDE自动生成。如果增加或修改了字段，可以改变`serialVersionUID`的值，这样就能自动阻止不匹配的class版本：

```java
public class Person implements Serializable {
    private static final long serialVersionUID = 2709425275741743919L;
}
```

要特别注意反序列化的几个重要特点：

反序列化时，由JVM直接构造出Java对象，不调用构造方法，构造方法内部的代码，在反序列化时根本不可能执行。

### 安全性

因为Java的序列化机制可以导致一个实例能直接从`byte[]`数组创建，而不经过构造方法，因此，它存在一定的安全隐患。一个精心构造的`byte[]`数组被反序列化后可以执行特定的Java代码，从而导致严重的安全漏洞。

实际上，Java本身提供的基于对象的序列化和反序列化机制既存在安全性问题，也存在兼容性问题。更好的序列化方法是通过JSON这样的通用数据结构来实现，只输出基本类型（包括String）的内容，而不存储任何与代码相关的信息。

### 小结

可序列化的Java对象必须实现`java.io.Serializable`接口，类似`Serializable`这样的空接口被称为“标记接口”（Marker Interface）；

反序列化时不调用构造方法，可设置`serialVersionUID`作为版本号（非必需）；

Java的序列化机制仅适用于Java，如果需要与其它语言交换数据，必须使用通用的序列化方法，例如JSON。

## Reader

`Reader`是Java的IO库提供的另一个输入流接口。和`InputStream`的区别是，`InputStream`是一个字节流，即以`byte`为单位读取，而`Reader`是一个字符流，即以`char`为单位读取：

InputStream	                       |Reader
-|-
字节流，以byte为单位	            |字符流，以char为单位
读取字节（-1，0~255）：int read()	|读取字符（-1，0~65535）：int read()
读到字节数组：int read(byte[] b)	|读到字符数组：int read(char[] c)

`java.io.Reader`是所有字符输入流的超类，它最主要的方法是：

```java
public int read() throws IOException;
```

这个方法读取字符流的下一个字符，并返回字符表示的`int`，范围是`0~65535`。如果已读到末尾，返回`-1`。

### FileReader

`FileReader`是`Reader`的一个子类，它可以打开文件并获取`Reader`。下面的代码演示了如何完整地读取一个`FileReader`的所有字符：

```java
public void readFile() throws IOException {
    // 创建一个FileReader对象:
    Reader reader = new FileReader("src/readme.txt"); // 字符编码是???
    for (;;) {
        int n = reader.read(); // 反复调用read()方法，直到返回-1
        if (n == -1) {
            break;
        }
        System.out.println((char)n); // 打印char
    }
    reader.close(); // 关闭流
}
```

如果我们读取一个纯ASCII编码的文本文件，上述代码工作是没有问题的。但如果文件中包含中文，就会出现乱码，因为`FileReader`默认的编码与系统相关，例如，Windows系统的默认编码可能是`GBK`，打开一个`UTF-8`编码的文本文件就会出现乱码。

要避免乱码问题，我们需要在创建`FileReader`时指定编码：

```java
Reader reader = new FileReader("src/readme.txt", StandardCharsets.UTF_8);
```

和`InputStream`类似，`Reader`也是一种资源，需要保证出错的时候也能正确关闭，所以我们需要用`try (resource)`来保证`Reader`在无论有没有IO错误的时候都能够正确地关闭：

```java
try (Reader reader = new FileReader("src/readme.txt", StandardCharsets.UTF_8) {
    // TODO
}
```

`Reader`还提供了一次性读取若干字符并填充到`char[]`数组的方法：

```java
public int read(char[] c) throws IOException
```

它返回实际读入的字符个数，最大不超过`char[]`数组的长度。返回`-1`表示流结束。

利用这个方法，我们可以先设置一个缓冲区，然后，每次尽可能地填充缓冲区：

```java
public void readFile() throws IOException {
    try (Reader reader = new FileReader("src/readme.txt", StandardCharsets.UTF_8)) {
        char[] buffer = new char[1000];
        int n;
        while ((n = reader.read(buffer)) != -1) {
            System.out.println("read " + n + " chars.");
        }
    }
}
```

### CharArrayReader

`CharArrayReader`可以在内存中模拟一个`Reader`，它的作用实际上是把一个`char[]`数组变成一个`Reader`，这和`ByteArrayInputStream`非常类似：

```java
try (Reader reader = new CharArrayReader("Hello".toCharArray())) {
}
```

### StringReader

`StringReader`可以直接把`String`作为数据源，它和`CharArrayReader`几乎一样：

```java
try (Reader reader = new StringReader("Hello")) {
}
```

### InputStreamReader

`Reader`和`InputStream`有什么关系？

除了特殊的`CharArrayReader`和`StringReader`，普通的`Reader`实际上是基于`InputStream`构造的，因为`Reader`需要从`InputStream`中读入字节流（`byte`），然后，根据编码设置，再转换为`char`就可以实现字符流。如果我们查看`FileReader`的源码，它在内部实际上持有一个`FileInputStream`。

既然`Reader`本质上是一个基于`InputStream`的`byte`到`char`的转换器，那么，如果我们已经有一个`InputStream`，想把它转换为`Reader`，是完全可行的。`InputStreamReader`就是这样一个转换器，它可以把任何`InputStream`转换为`Reader`。示例代码如下：

```java
// 持有InputStream:
InputStream input = new FileInputStream("src/readme.txt");
// 变换为Reader:
Reader reader = new InputStreamReader(input, "UTF-8");
```

构造I`nputStreamReader`时，我们需要传入`InputStream`，还需要指定编码，就可以得到一个`Reader`对象。上述代码可以通过`try (resource)`更简洁地改写如下：

```java
try (Reader reader = new InputStreamReader(new FileInputStream("src/readme.txt"), "UTF-8")) {
    // TODO:
}
```

上述代码实际上就是`FileReader`的一种实现方式。

使用`try (resource)`结构时，当我们关闭`Reader`时，它会在内部自动调用`InputStream`的`close()`方法，所以，只需要关闭最外层的`Reader`对象即可。

**使用InputStreamReader，可以把一个InputStream转换成一个Reader。**

### 小结

`Reader`定义了所有字符输入流的超类：

- `FileReader`实现了文件字符流输入，使用时需要指定编码；
- `CharArrayReader`和`StringReader`可以在内存中模拟一个字符流输入。

`Reader`是基于`InputStream`构造的：可以通过`InputStreamReader`在指定编码的同时将任何`InputStream`转换为`Reader`。

总是使用`try (resource)`保证`Reader`正确关闭。

## Writer

`Reader`是带编码转换器的`InputStream`，它把`byte`转换为`char`，而`Writer`就是带编码转换器的`OutputStream`，它把`char`转换为`byte`并输出。

`Writer`和`OutputStream`的区别如下：


OutputStream	                       |Writer
-|-
字节流，以byte为单位	               |字符流，以char为单位
写入字节（0~255）：void write(int b)   |写入字符（0~65535）：void write(int c)
写入字节数组：void write(byte[] b)	   |写入字符数组：void write(char[] c)
无对应方法	                           |写入String：void write(String s)

`Writer`是所有字符输出流的超类，它提供的方法主要有：

- 写入一个字符（0~65535）：`void write(int c)`；
- 写入字符数组的所有字符：`void write(char[] c)`；
- 写入String表示的所有字符：`void write(String s)`。

### FileWriter

`FileWriter`就是向文件中写入字符流的`Writer`。它的使用方法和`FileReader`类似：

```java
try (Writer writer = new FileWriter("readme.txt", StandardCharsets.UTF_8)) {
    writer.write('H'); // 写入单个字符
    writer.write("Hello".toCharArray()); // 写入char[]
    writer.write("Hello"); // 写入String
}
```

### CharArrayWriter

`CharArrayWriter`可以在内存中创建一个`Writer`，它的作用实际上是构造一个缓冲区，可以写入`char`，最后得到写入的`char[]`数组，这和`ByteArrayOutputStream`非常类似：

```java
try (CharArrayWriter writer = new CharArrayWriter()) {
    writer.write(65);
    writer.write(66);
    writer.write(67);
    char[] data = writer.toCharArray(); // { 'A', 'B', 'C' }
}
```

### StringWriter

`StringWriter`也是一个基于内存的`Writer`，它和`CharArrayWriter`类似。实际上，`StringWriter`在内部维护了一个`StringBuffer`，并对外提供了`Writer`接口。

### OutputStreamWriter

除了`CharArrayWriter`和`StringWriter`外，普通的Writer实际上是基于`OutputStream`构造的，它接收`char`，然后在内部自动转换成一个或多个`byte`，并写入`OutputStream`。因此，`OutputStreamWriter`就是一个将任意的`OutputStream`转换为`Writer`的转换器：

```java
try (Writer writer = new OutputStreamWriter(new FileOutputStream("readme.txt"), "UTF-8")) {
    // TODO:
}
```

上述代码实际上就是`FileWriter`的一种实现方式。这和上一节的`InputStreamReader`是一样的。

### 小结

`Writer`定义了所有字符输出流的超类：

- `FileWriter`实现了文件字符流输出；
- `CharArrayWriter`和`StringWriter`在内存中模拟一个字符流输出。

使用`try (resource)`保证`Writer`正确关闭。

`Writer`是基于`OutputStream`构造的，可以通过`OutputStreamWriter`将`OutputStream`转换为`Writer`，转换时需要指定编码。

## PrintStream 和 PrintWriter

`PrintStream`是一种`FilterOutputStream`，它在`OutputStream`的接口上，额外提供了一些写入各种数据类型的方法：

- 写入`int`：`print(int)`
- 写入`boolean`：`print(boolean)`
- 写入`String`：`print(String)`
- 写入`Object`：`print(Object)`，实际上相当于`print(object.toString())`
- ...

以及对应的一组`println()`方法，它会自动加上换行符。

我们经常使用的`System.out.println()`实际上就是使用`PrintStream`打印各种数据。其中，`System.out`是系统默认提供的`PrintStream`，表示标准输出：

```java
System.out.print(12345); // 输出12345
System.out.print(new Object()); // 输出类似java.lang.Object@3c7a835a
System.out.println("Hello"); // 输出Hello并换行
```

`System.err`是系统默认提供的标准错误输出。

`PrintStream`和`OutputStream`相比，除了添加了一组`print()`/`println()`方法，可以打印各种数据类型，比较方便外，它还有一个额外的优点，就是不会抛出`IOException`，这样我们在编写代码的时候，就不必捕获`IOException`。

### PrintWriter

`PrintStream`最终输出的总是byte数据，而`PrintWriter`则是扩展了`Writer`接口，它的`print()`/`println()`方法最终输出的是char数据。两者的使用方法几乎是一模一样的：

```java
public class Main {
    public static void main(String[] args)     {
        StringWriter buffer = new StringWriter();
        try (PrintWriter pw = new PrintWriter(buffer)) {
            pw.println("Hello");
            pw.println(12345);
            pw.println(true);
        }
        System.out.println(buffer.toString());
    }
}
```

### 小结

`PrintStream`是一种能接收各种数据类型的输出，打印数据时比较方便：

- `System.out`是标准输出；
- `System.err`是标准错误输出。

`PrintWriter`是基于`Writer`的输出。

## 使用 Files

从Java 7开始，提供了`Files`这个工具类，能极大地方便我们读写文件。

虽然`Files`是`java.nio`包里面的类，但他俩封装了很多读写文件的简单方法，例如，我们要把一个文件的全部内容读取为一个`byte[]`，可以这么写：

```java
byte[] data = Files.readAllBytes(Path.of("/path/to/file.txt"));
```

如果是文本文件，可以把一个文件的全部内容读取为`String`：

```java
// 默认使用UTF-8编码读取:
String content1 = Files.readString(Path.of("/path/to/file.txt"));
// 可指定编码:
String content2 = Files.readString(Path.of("/path", "to", "file.txt"), StandardCharsets.ISO_8859_1);
// 按行读取并返回每行内容:
List<String> lines = Files.readAllLines(Path.of("/path/to/file.txt"));
```

写入文件也非常方便：

```java
// 写入二进制文件:
byte[] data = ...
Files.write(Path.of("/path/to/file.txt"), data);
// 写入文本并指定编码:
Files.writeString(Path.of("/path/to/file.txt"), "文本内容...", StandardCharsets.ISO_8859_1);
// 按行写入文本:
List<String> lines = ...
Files.write(Path.of("/path/to/file.txt"), lines);
```

此外，`Files`工具类还有`copy()`、`delete()`、`exists()`、`move()`等快捷方法操作文件和目录。

最后需要特别注意的是，`Files`提供的读写方法，受内存限制，只能读写小文件，例如配置文件等，不可一次读入几个G的大文件。读写大型文件仍然要使用文件流，每次只读写一部分文件内容。

### 小结

对于简单的小文件读写操作，可以使用Files工具类简化代码。

# 日期与时间

日期与时间是计算机处理的重要数据。绝大部分程序的运行都要和时间打交道。

## 基本概念

在计算机中，我们经常需要处理日期和时间。

这是日期：

- 2019-11-20
- 2020-1-1

这是时间：

- 12:30:59
- 2020-1-1 20:21:59

日期是指某一天，它不是连续变化的，而是应该被看成离散的。

而时间有两种概念，一种是不带日期的时间，例如，12:30:59。另一种是带日期的时间，例如，2020-1-1 20:21:59，只有这种带日期的时间能唯一确定某个时刻，不带日期的时间是无法确定一个唯一时刻的。

### 本地时间

当我们说当前时刻是2019年11月20日早上8:15的时候，我们说的实际上是本地时间。在国内就是北京时间。在这个时刻，如果地球上不同地方的人们同时看一眼手表，他们各自的本地时间是不同的

所以，不同的时区，在同一时刻，本地时间是不同的。全球一共分为24个时区，伦敦所在的时区称为标准时区，其他时区按东／西偏移的小时区分，北京所在的时区是东八区。

### 时区

因为光靠本地时间还无法唯一确定一个准确的时刻，所以我们还需要给本地时间加上一个时区。时区有好几种表示方式。

一种是以`GMT`或者`UTC`加时区偏移表示，例如：`GMT+08:00`或者`UTC+08:00`表示东八区。

`GMT`和`UTC`可以认为基本是等价的，只是`UTC`使用更精确的原子钟计时，每隔几年会有一个闰秒，我们在开发程序的时候可以忽略两者的误差，因为计算机的时钟在联网的时候会自动与时间服务器同步时间。

另一种是缩写，例如，`CST`表示`China Standard Time`，也就是中国标准时间。但是`CST`也可以表示美国中部时间`Central Standard Time USA`，因此，缩写容易产生混淆，我们尽量不要使用缩写。

最后一种是以`洲／城市`表示，例如，`Asia/Shanghai`，表示上海所在地的时区。特别注意城市名称不是任意的城市，而是由国际标准组织规定的城市。

因为时区的存在，东八区的2019年11月20日早上8:15，和西五区的2019年11月19日晚上19:15，他们的时刻是相同的

时刻相同的意思就是，分别在两个时区的两个人，如果在这一刻通电话，他们各自报出自己手表上的时间，虽然本地时间是不同的，但是这两个时间表示的时刻是相同的。

### 夏令时

时区还不是最复杂的，更复杂的是夏令时。所谓夏令时，就是夏天开始的时候，把时间往后拨1小时，夏天结束的时候，再把时间往前拨1小时。我们国家实行过一段时间夏令时，1992年就废除了，但是矫情的美国人到现在还在使用，所以时间换算更加复杂。

因为涉及到夏令时，相同的时区，如果表示的方式不同，转换出的时间是不同的。我们举个栗子：

对于2019-11-20和2019-6-20两个日期来说，假设北京人在纽约：

- 如果以`GMT`或者`UTC`作为时区，无论日期是多少，时间都是`19:00`；

- 如果以国家／城市表示，例如`America／NewYork`，虽然纽约也在西五区，但是，因为夏令时的存在，在不同的日期，`GMT`时间和纽约时间可能是不一样的：


时区	            |2019-11-20	|2019-6-20
-|-|-
GMT-05:00	        |19:00	    |19:00
UTC-05:00	        |19:00	    |19:00
America/New_York	|19:00	    |20:00

实行夏令时的不同地区，进入和退出夏令时的时间很可能是不同的。同一个地区，根据历史上是否实行过夏令时，标准时间在不同年份换算成当地时间也是不同的。因此，计算夏令时，没有统一的公式，必须按照一组给定的规则来算，并且，该规则要定期更新。

**计算夏令时请使用标准库提供的相关类，不要试图自己计算夏令时。**

### 本地化

在计算机中，通常使用`Locale`表示一个国家或地区的日期、时间、数字、货币等格式。`Locale`由`语言_国家`的字母缩写构成，例如，`zh_CN`表示中文+中国，`en_US`表示英文+美国。语言使用小写，国家使用大写。

对于日期来说，不同的Locale，例如，中国和美国的表示方式如下：

- zh_CN：2016-11-30
- en_US：11/30/2016

### 小结

在编写日期和时间的程序前，我们要准确理解日期、时间和时刻的概念。

由于存在本地时间，我们需要理解时区的概念，并且必须牢记由于夏令时的存在，同一地区用GMT/UTC和城市表示的时区可能导致时间不同。

计算机通过`Locale`来针对当地用户习惯格式化日期、时间、数字、货币等。

## Date 和 Calendar

在计算机中，应该如何表示日期和时间呢？

我们经常看到的日期和时间表示方式如下：

- 2019-11-20 0:15:00 GMT+00:00
- 2019年11月20日8:15:00
- 11/19/2019 19:15:00 America/New_York

如果直接以字符串的形式存储，那么不同的格式，不同的语言会让表示方式非常繁琐。

在理解日期和时间的表示方式之前，我们先要理解数据的存储和展示。

当我们定义一个整型变量并赋值时：

```java
int n = 123400;
```

编译器会把上述字符串（程序源码就是一个字符串）编译成字节码。在程序的运行期，变量`n`指向的内存实际上是一个4字节区域：

```
┌──┬──┬──┬──┐
│00│01│e2│08│
└──┴──┴──┴──┘
```

注意到计算机内存除了二进制的`0`/`1`外没有其他任何格式。上述十六机制是为了简化表示。

当我们用`System.out.println(n)`打印这个整数的时候，实际上`println()`这个方法在内部把`int`类型转换成`String`类型，然后打印出字符串`123400`。

类似的，我们也可以以十六进制的形式打印这个整数，或者，如果`n`表示一个价格，我们就以`$123,400.00`的形式来打印它：

```java
    public static void main(String[] args) {
        int n = 123400;
        // 123400
        System.out.println(n);
        // 1e208
        System.out.println(Integer.toHexString(n));
        // $123,400.00
        System.out.println(NumberFormat.getCurrencyInstance(Locale.US).format(n));
    }
}
```

可见，整数`123400`是数据的存储格式，它的存储格式非常简单。而我们打印的各种各样的字符串，则是数据的展示格式。展示格式有多种形式，但本质上它就是一个转换方法：

```java
String toDisplay(int n) { ... }
```

理解了数据的存储和展示，我们回头看看以下几种日期和时间：

- 2019-11-20 0:15:01 GMT+00:00
- 2019年11月20日8:15:01
- 11/19/2019 19:15:01 America/New_York

它们实际上是数据的展示格式，分别按英国时区、中国时区、纽约时区对同一个时刻进行展示。而这个“同一个时刻”在计算机中存储的本质上只是一个整数，我们称它为`Epoch Time`。

`Epoch Time`是计算从1970年1月1日零点（格林威治时区／GMT+00:00）到现在所经历的秒数，例如：

`1574208900`表示从从1970年1月1日零点GMT时区到该时刻一共经历了1574208900秒，换算成伦敦、北京和纽约时间分别是：

```
1574208900 = 北京时间2019-11-20 8:15:00
           = 伦敦时间2019-11-20 0:15:00
           = 纽约时间2019-11-19 19:15:00
```

它们之间转换非常简单。而在Java程序中，时间戳通常是用long表示的毫秒数，即：

```java
long t = 1574208900123L;
```

转换成北京时间就是`2019-11-20T8:15:00.123`。要获取当前时间戳，可以使用`System.currentTimeMillis()`，这是Java程序获取时间戳最常用的方法。

### 标准库API

我们再来看一下Java标准库提供的API。Java标准库有两套处理日期和时间的API：

- 一套定义在`java.util`这个包里面，主要包括`Date`、`Calendar`和`TimeZone`这几个类；
- 一套新的API是在Java 8引入的，定义在`java.time`这个包里面，主要包括`LocalDateTime`、`ZonedDateTime`、`ZoneId`等。

为什么会有新旧两套API呢？因为历史遗留原因，旧的API存在很多问题，所以引入了新的API。

那么我们能不能跳过旧的API直接用新的API呢？如果涉及到遗留代码就不行，因为很多遗留代码仍然使用旧的API，所以目前仍然需要对旧的API有一定了解，很多时候还需要在新旧两种对象之间进行转换。

### Date

`java.util.Date`是用于表示一个日期和时间的对象，注意与`java.sql.Date`区分，后者用在数据库中。如果观察Date的源码，可以发现它实际上存储了一个long类型的以毫秒表示的时间戳：

```java
public class Date implements Serializable, Cloneable, Comparable<Date> {

    private transient long fastTime;

    ...
}
```

我们来看Date的基本用法：

```java
public class Main {
    public static void main(String[] args) {
        // 获取当前时间:
        Date date = new Date();
        System.out.println(date.getYear() + 1900); // 必须加上1900
        System.out.println(date.getMonth() + 1); // 0~11，必须加上1
        System.out.println(date.getDate()); // 1~31，不能加1
        // 转换为String:
        System.out.println(date.toString());
        // 转换为GMT时区:
        System.out.println(date.toGMTString());
        // 转换为本地时区:
        System.out.println(date.toLocaleString());
    }
}
```

注意`getYear()`返回的年份必须加上`1900`，`getMonth()`返回的月份是`0`~`11`分别表示1~12月，所以要加1，而g`etDate()`返回的日期范围是`1`~`31`，又不能加1。

打印本地时区表示的日期和时间时，不同的计算机可能会有不同的结果。如果我们想要针对用户的偏好精确地控制日期和时间的格式，就可以使用`SimpleDateFormat`对一个`Date`进行转换。它用预定义的字符串表示格式化：

- yyyy：年
- MM：月
- dd: 日
- HH: 小时
- mm: 分钟
- ss: 秒

我们来看如何以自定义的格式输出：

```java
public class Main {
    public static void main(String[] args) {
        // 获取当前时间:
        Date date = new Date();
        var sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        System.out.println(sdf.format(date));
    }
}
```

Java的格式化预定义了许多不同的格式，我们以`MMM`和`E`为例：

```java
public class Main {
    public static void main(String[] args) {
        // 获取当前时间:
        Date date = new Date();
        var sdf = new SimpleDateFormat("E MMM dd, yyyy");
        System.out.println(sdf.format(date));
    }
}
```

上述代码在不同的语言环境会打印出类似`Sun Sep 15`, 2019这样的日期。可以从JDK文档查看详细的格式说明。一般来说，字母越长，输出越长。以`M`为例，假设当前月份是9月：

- M：输出9
- MM：输出09
- MMM：输出Sep
- MMMM：输出September

`Date`对象有几个严重的问题：它不能转换时区，除了`toGMTString()`可以按`GMT+0:00`输出外，Date总是以当前计算机系统的默认时区为基础进行输出。此外，我们也很难对日期和时间进行加减，计算两个日期相差多少天，计算某个月第一个星期一的日期等。

### Calendar

`Calendar`可以用于获取并设置年、月、日、时、分、秒，它和`Date`比，主要多了一个可以做简单的日期和时间运算的功能。

来看`Calendar`的基本用法：

```java
public class Main {
    public static void main(String[] args) {
        // 获取当前时间:
        Calendar c = Calendar.getInstance();
        int y = c.get(Calendar.YEAR);
        int m = 1 + c.get(Calendar.MONTH);
        int d = c.get(Calendar.DAY_OF_MONTH);
        int w = c.get(Calendar.DAY_OF_WEEK);
        int hh = c.get(Calendar.HOUR_OF_DAY);
        int mm = c.get(Calendar.MINUTE);
        int ss = c.get(Calendar.SECOND);
        int ms = c.get(Calendar.MILLISECOND);
        System.out.println(y + "-" + m + "-" + d + " " + w + " " + hh + ":" + mm + ":" + ss + "." + ms);
    }
}
```

注意到`Calendar`获取年月日这些信息变成了`get(int field)`，返回的年份不必转换，返回的月份仍然要加1，返回的星期要特别注意，`1`~`7`分别表示周日，周一，……，周六。

`Calendar`只有一种方式获取，即`Calendar.getInstance()`，而且一获取到就是当前时间。如果我们想给它设置成特定的一个日期和时间，就必须先清除所有字段：

```java
public class Main {
    public static void main(String[] args) {
        // 当前时间:
        Calendar c = Calendar.getInstance();
        // 清除所有:
        c.clear();
        // 设置2019年:
        c.set(Calendar.YEAR, 2019);
        // 设置9月:注意8表示9月:
        c.set(Calendar.MONTH, 8);
        // 设置2日:
        c.set(Calendar.DATE, 2);
        // 设置时间:
        c.set(Calendar.HOUR_OF_DAY, 21);
        c.set(Calendar.MINUTE, 22);
        c.set(Calendar.SECOND, 23);
        System.out.println(new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(c.getTime()));
        // 2019-09-02 21:22:23
    }
}
```

利用`Calendar.getTime()`可以将一个`Calendar`对象转换成`Date`对象，然后就可以用`SimpleDateFormat`进行格式化了。

### TimeZone

`Calendar`和`Date`相比，它提供了时区转换的功能。时区用`TimeZone`对象表示：

```java
public class Main {
    public static void main(String[] args) {
        TimeZone tzDefault = TimeZone.getDefault(); // 当前时区
        TimeZone tzGMT9 = TimeZone.getTimeZone("GMT+09:00"); // GMT+9:00时区
        TimeZone tzNY = TimeZone.getTimeZone("America/New_York"); // 纽约时区
        System.out.println(tzDefault.getID()); // Asia/Shanghai
        System.out.println(tzGMT9.getID()); // GMT+09:00
        System.out.println(tzNY.getID()); // America/New_York
    }
}
```

时区的唯一标识是以字符串表示的ID，我们获取指定`TimeZone`对象也是以这个ID为参数获取，`GMT+09:00`、`Asia/Shanghai`都是有效的时区ID。要列出系统支持的所有ID，请使用`TimeZone.getAvailableIDs()`。

有了时区，我们就可以对指定时间进行转换。例如，下面的例子演示了如何将北京时间`2019-11-20 8:15:00`转换为纽约时间：

```java
public class Main {
    public static void main(String[] args) {
        // 当前时间:
        Calendar c = Calendar.getInstance();
        // 清除所有:
        c.clear();
        // 设置为北京时区:
        c.setTimeZone(TimeZone.getTimeZone("Asia/Shanghai"));
        // 设置年月日时分秒:
        c.set(2019, 10 /* 11月 */, 20, 8, 15, 0);
        // 显示时间:
        var sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        sdf.setTimeZone(TimeZone.getTimeZone("America/New_York"));
        System.out.println(sdf.format(c.getTime()));
        // 2019-11-19 19:15:00
    }
}
```

可见，利用`Calendar`进行时区转换的步骤是：

1. 清除所有字段；
2. 设定指定时区；
3. 设定日期和时间；
4. 创建`SimpleDateFormat`并设定目标时区；
5. 格式化获取的`Date`对象（注意`Date`对象无时区信息，时区信息存储在`SimpleDateFormat`中）。

因此，本质上时区转换只能通过`SimpleDateFormat`在显示的时候完成。

`Calendar`也可以对日期和时间进行简单的加减：

```java
public class Main {
    public static void main(String[] args) {
        // 当前时间:
        Calendar c = Calendar.getInstance();
        // 清除所有:
        c.clear();
        // 设置年月日时分秒:
        c.set(2019, 10 /* 11月 */, 20, 8, 15, 0);
        // 加5天并减去2小时:
        c.add(Calendar.DAY_OF_MONTH, 5);
        c.add(Calendar.HOUR_OF_DAY, -2);
        // 显示时间:
        var sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date d = c.getTime();
        System.out.println(sdf.format(d));
        // 2019-11-25 6:15:00
    }
}
```

### 小结
计算机表示的时间是以整数表示的时间戳存储的，即Epoch Time，Java使用`long`型来表示以毫秒为单位的时间戳，通过`System.currentTimeMillis()`获取当前时间戳。

Java有两套日期和时间的API：

- 旧的Date、Calendar和TimeZone；
- 新的LocalDateTime、ZonedDateTime、ZoneId等。

分别位于`java.util`和`java.time`包中。

## LocalDateTime

从Java 8开始，`java.time`包提供了新的日期和时间API，主要涉及的类型有：

- 本地日期和时间：`LocalDateTime`，`LocalDate`，`LocalTime`；
- 带时区的日期和时间：`ZonedDateTime`；
- 时刻：`Instant`；
- 时区：`ZoneId`，`ZoneOffset`；
- 时间间隔：`Duration`。

以及一套新的用于取代`SimpleDateFormat`的格式化类型`DateTimeFormatter`。

和旧的API相比，新API严格区分了时刻、本地日期、本地时间和带时区的日期时间，并且，对日期和时间进行运算更加方便。

此外，新API修正了旧API不合理的常量设计：

- Month的范围用1~12表示1月到12月；
- Week的范围用1~7表示周一到周日。

最后，新API的类型几乎全部是不变类型（和String类似），可以放心使用不必担心被修改。

### LocalDateTime

我们首先来看最常用的`LocalDateTime`，它表示一个本地日期和时间：

```java
public class Main {
    public static void main(String[] args) {
        LocalDate d = LocalDate.now(); // 当前日期
        LocalTime t = LocalTime.now(); // 当前时间
        LocalDateTime dt = LocalDateTime.now(); // 当前日期和时间
        System.out.println(d); // 严格按照ISO 8601格式打印
        System.out.println(t); // 严格按照ISO 8601格式打印
        System.out.println(dt); // 严格按照ISO 8601格式打印
    }
}
```

本地日期和时间通过now()获取到的总是以当前默认时区返回的，和旧API不同，`LocalDateTime`、`LocalDate`和`LocalTime`默认严格按照ISO 8601规定的日期和时间格式进行打印。

上述代码其实有一个小问题，在获取3个类型的时候，由于执行一行代码总会消耗一点时间，因此，3个类型的日期和时间很可能对不上（时间的毫秒数基本上不同）。为了保证获取到同一时刻的日期和时间，可以改写如下：

```java
LocalDateTime dt = LocalDateTime.now(); // 当前日期和时间
LocalDate d = dt.toLocalDate(); // 转换到当前日期
LocalTime t = dt.toLocalTime(); // 转换到当前时间
```

反过来，通过指定的日期和时间创建`LocalDateTime`可以通过`of()`方法：

```java
// 指定日期和时间:
LocalDate d2 = LocalDate.of(2019, 11, 30); // 2019-11-30, 注意11=11月
LocalTime t2 = LocalTime.of(15, 16, 17); // 15:16:17
LocalDateTime dt2 = LocalDateTime.of(2019, 11, 30, 15, 16, 17);
LocalDateTime dt3 = LocalDateTime.of(d2, t2);
```

因为严格按照ISO 8601的格式，因此，将字符串转换为`LocalDateTime`就可以传入标准格式：

```java
LocalDateTime dt = LocalDateTime.parse("2019-11-19T15:16:17");
LocalDate d = LocalDate.parse("2019-11-19");
LocalTime t = LocalTime.parse("15:16:17");
```

注意ISO 8601规定的日期和时间分隔符是`T`。标准格式如下：

- 日期：yyyy-MM-dd
- 时间：HH:mm:ss
- 带毫秒的时间：HH:mm:ss.SSS
- 日期和时间：yyyy-MM-dd'T'HH:mm:ss
- 带毫秒的日期和时间：yyyy-MM-dd'T'HH:mm:ss.SSS

### DateTimeFormatter

如果要自定义输出的格式，或者要把一个非ISO 8601格式的字符串解析成`LocalDateTime`，可以使用新的`DateTimeFormatter`：

```java
public class Main {
    public static void main(String[] args) {
        // 自定义格式化:
        DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        System.out.println(dtf.format(LocalDateTime.now()));

        // 用自定义格式解析:
        LocalDateTime dt2 = LocalDateTime.parse("2019/11/30 15:16:17", dtf);
        System.out.println(dt2);
    }
}
```

`LocalDateTime`提供了对日期和时间进行加减的非常简单的链式调用：

```java
public class Main {
    public static void main(String[] args) {
        LocalDateTime dt = LocalDateTime.of(2019, 10, 26, 20, 30, 59);
        System.out.println(dt);
        // 加5天减3小时:
        LocalDateTime dt2 = dt.plusDays(5).minusHours(3);
        System.out.println(dt2); // 2019-10-31T17:30:59
        // 减1月:
        LocalDateTime dt3 = dt2.minusMonths(1);
        System.out.println(dt3); // 2019-09-30T17:30:59
    }
}
```

注意到月份加减会自动调整日期，例如从`2019-10-31`减去1个月得到的结果是`2019-09-30`，因为9月没有31日。

对日期和时间进行调整则使用`withXxx()`方法，例如：`withHour(15)`会把`10:11:12`变为`15:11:12`：

- 调整年：withYear()
- 调整月：withMonth()
- 调整日：withDayOfMonth()
- 调整时：withHour()
- 调整分：withMinute()
- 调整秒：withSecond()

示例代码如下：

```java
public class Main {
    public static void main(String[] args) {
        LocalDateTime dt = LocalDateTime.of(2019, 10, 26, 20, 30, 59);
        System.out.println(dt);
        // 日期变为31日:
        LocalDateTime dt2 = dt.withDayOfMonth(31);
        System.out.println(dt2); // 2019-10-31T20:30:59
        // 月份变为9:
        LocalDateTime dt3 = dt2.withMonth(9);
        System.out.println(dt3); // 2019-09-30T20:30:59
    }
}
```

同样注意到调整月份时，会相应地调整日期，即把`2019-10-31`的月份调整为`9`时，日期也自动变为`30`。

实际上，`LocalDateTime`还有一个通用的`with()`方法允许我们做更复杂的运算。例如：

```java
public class Main {
    public static void main(String[] args) {
        // 本月第一天0:00时刻:
        LocalDateTime firstDay = LocalDate.now().withDayOfMonth(1).atStartOfDay();
        System.out.println(firstDay);

        // 本月最后1天:
        LocalDate lastDay = LocalDate.now().with(TemporalAdjusters.lastDayOfMonth());
        System.out.println(lastDay);

        // 下月第1天:
        LocalDate nextMonthFirstDay = LocalDate.now().with(TemporalAdjusters.firstDayOfNextMonth());
        System.out.println(nextMonthFirstDay);

        // 本月第1个周一:
        LocalDate firstWeekday = LocalDate.now().with(TemporalAdjusters.firstInMonth(DayOfWeek.MONDAY));
        System.out.println(firstWeekday);
    }
}
```

对于计算某个月第1个周日这样的问题，新的API可以轻松完成。

要判断两个`LocalDateTime`的先后，可以使用`isBefore()`、`isAfter()`方法，对于`LocalDate`和`LocalTime`类似：

```java
public class Main {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        LocalDateTime target = LocalDateTime.of(2019, 11, 19, 8, 15, 0);
        System.out.println(now.isBefore(target));
        System.out.println(LocalDate.now().isBefore(LocalDate.of(2019, 11, 19)));
        System.out.println(LocalTime.now().isAfter(LocalTime.parse("08:15:00")));
    }
}
```

注意到`LocalDateTime`无法与时间戳进行转换，因为`LocalDateTime`没有时区，无法确定某一时刻。后面我们要介绍的`ZonedDateTime`相当于`LocalDateTime`加时区的组合，它具有时区，可以与`long`表示的时间戳进行转换。

```java
public class Main {
    public static void main(String[] args) {
        LocalDateTime start = LocalDateTime.of(2019, 11, 19, 8, 15, 0);
        LocalDateTime end = LocalDateTime.of(2020, 1, 9, 19, 25, 30);
        Duration d = Duration.between(start, end);
        System.out.println(d); // PT1235H10M30S

        Period p = LocalDate.of(2019, 11, 19).until(LocalDate.of(2020, 1, 9));
        System.out.println(p); // P1M21D
    }
}
```

注意到两个`LocalDateTime`之间的差值使用`Duration`表示，类似`PT1235H10M30S`，表示1235小时10分钟30秒。而两个`LocalDate`之间的差值用`Period`表示，类似`P1M21D`，表示1个月21天。

`Duration`和`Period`的表示方法也符合ISO 8601的格式，它以`P...T...`的形式表示，`P...T之`间表示日期间隔，`T`后面表示时间间隔。如果是`PT...`的格式表示仅有时间间隔。利用`ofXxx()`或者`parse()`方法也可以直接创建`Duration`：

```java
Duration d1 = Duration.ofHours(10); // 10 hours
Duration d2 = Duration.parse("P1DT2H3M"); // 1 day, 2 hours, 3 minutes
```

有的童鞋可能发现Java 8引入的`java.timeAPI`。怎么和一个开源的[Joda Time](https://www.joda.org/)很像？难道JDK也开始抄袭开源了？其实正是因为开源的Joda Time设计很好，应用广泛，所以JDK团队邀请Joda Time的作者Stephen Colebourne共同设计了`java.time`API。

### 小结
Java 8引入了新的日期和时间API，它们是不变类，默认按ISO 8601标准格式化和解析；

使用`LocalDateTime`可以非常方便地对日期和时间进行加减，或者调整日期和时间，它总是返回新对象；

使用`isBefore()`和`isAfter()`可以判断日期和时间的先后；

使用`Duration`和`Period`可以表示两个日期和时间的“区间间隔”。

## ZonedDateTime

`LocalDateTime`总是表示本地日期和时间，要表示一个带时区的日期和时间，我们就需要`ZonedDateTime`。

可以简单地把`ZonedDateTime`理解成`LocalDateTime`加`ZoneId`。`ZoneId`是`java.time`引入的新的时区类，注意和旧的`java.util.TimeZone`区别。

要创建一个`ZonedDateTime`对象，有以下几种方法，一种是通过`now()`方法返回当前时间：

```java
public class Main {
    public static void main(String[] args) {
        ZonedDateTime zbj = ZonedDateTime.now(); // 默认时区
        ZonedDateTime zny = ZonedDateTime.now(ZoneId.of("America/New_York")); // 用指定时区获取当前时间
        System.out.println(zbj);
        System.out.println(zny);
    }
}
```

观察打印的两个`ZonedDateTime`，发现它们时区不同，但表示的时间都是同一时刻（毫秒数不同是执行语句时的时间差）：

```
2019-09-15T20:58:18.786182+08:00[Asia/Shanghai]
2019-09-15T08:58:18.788860-04:00[America/New_York]
```

另一种方式是通过给一个`LocalDateTime`附加一个`ZoneId`，就可以变成`ZonedDateTime`：

```java
public class Main {
    public static void main(String[] args) {
        LocalDateTime ldt = LocalDateTime.of(2019, 9, 15, 15, 16, 17);
        ZonedDateTime zbj = ldt.atZone(ZoneId.systemDefault());
        ZonedDateTime zny = ldt.atZone(ZoneId.of("America/New_York"));
        System.out.println(zbj);
        System.out.println(zny);
    }
}
```

以这种方式创建的`ZonedDateTime`，它的日期和时间与`LocalDateTime`相同，但附加的时区不同，因此是两个不同的时刻：

```
2019-09-15T15:16:17+08:00[Asia/Shanghai]
2019-09-15T15:16:17-04:00[America/New_York]
```

### 时区转换

要转换时区，首先我们需要有一个`ZonedDateTime`对象，然后，通过`withZoneSameInstant()`将关联时区转换到另一个时区，转换后日期和时间都会相应调整。

下面的代码演示了如何将北京时间转换为纽约时间：

```java
public class Main {
    public static void main(String[] args) {
        // 以中国时区获取当前时间:
        ZonedDateTime zbj = ZonedDateTime.now(ZoneId.of("Asia/Shanghai"));
        // 转换为纽约时间:
        ZonedDateTime zny = zbj.withZoneSameInstant(ZoneId.of("America/New_York"));
        System.out.println(zbj);
        System.out.println(zny);
    }
}
```

要特别注意，时区转换的时候，由于夏令时的存在，不同的日期转换的结果很可能是不同的。这是北京时间9月15日的转换结果：

```
2019-09-15T21:05:50.187697+08:00[Asia/Shanghai]
2019-09-15T09:05:50.187697-04:00[America/New_York]
```

这是北京时间11月15日的转换结果：

```
2019-11-15T21:05:50.187697+08:00[Asia/Shanghai]
2019-11-15T08:05:50.187697-05:00[America/New_York]
```

两次转换后的纽约时间有1小时的夏令时时差。

**涉及到时区时，千万不要自己计算时差，否则难以正确处理夏令时。**

有了`ZonedDateTime`，将其转换为本地时间就非常简单：

```java
ZonedDateTime zdt = ...
LocalDateTime ldt = zdt.toLocalDateTime();
```

转换为`LocalDateTime`时，直接丢弃了时区信息。

### 小结

`ZonedDateTime`是带时区的日期和时间，可用于时区转换；

`ZonedDateTime`和`LocalDateTime`可以相互转换。

## DateTimeFormatter

使用旧的`Date`对象时，我们用`SimpleDateFormat`进行格式化显示。使用新的`LocalDateTime`或`ZonedDateTime`时，我们要进行格式化显示，就要使用`DateTimeFormatter`。

和`SimpleDateFormat`不同的是，`DateTimeFormatter`不但是不变对象，它还是线程安全的。线程的概念我们会在后面涉及到。现在我们只需要记住：因为`SimpleDateFormat`不是线程安全的，使用的时候，只能在方法内部创建新的局部变量。而`DateTimeFormatter`可以只创建一个实例，到处引用。

创建D`ateTimeFormatter`时，我们仍然通过传入格式化字符串实现：

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
```

格式化字符串的使用方式与`SimpleDateFormat`完全一致。

另一种创建`DateTimeFormatter`的方法是，传入格式化字符串时，同时指定`Locale`：

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("E, yyyy-MMMM-dd HH:mm", Locale.US);
```

这种方式可以按照`Locale`默认习惯格式化。我们来看实际效果：

```java
public class Main {
    public static void main(String[] args) {
        ZonedDateTime zdt = ZonedDateTime.now();
        var formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd'T'HH:mm ZZZZ");
        System.out.println(formatter.format(zdt));

        var zhFormatter = DateTimeFormatter.ofPattern("yyyy MMM dd EE HH:mm", Locale.CHINA);
        System.out.println(zhFormatter.format(zdt));

        var usFormatter = DateTimeFormatter.ofPattern("E, MMMM/dd/yyyy HH:mm", Locale.US);
        System.out.println(usFormatter.format(zdt));
    }
}
```

在格式化字符串中，如果需要输出固定字符，可以用`'xxx'`表示。

运行上述代码，分别以默认方式、中国地区和美国地区对当前时间进行显示，结果如下：

```
2019-09-15T23:16 GMT+08:00
2019 9月 15 周日 23:16
Sun, September/15/2019 23:16
```

当我们直接调用`System.out.println()`对一个`ZonedDateTime`或者`LocalDateTime`实例进行打印的时候，实际上，调用的是它们的`toString()`方法，默认的`toString()`方法显示的字符串就是按照`ISO 8601`格式显示的，我们可以通过`DateTimeFormatter`预定义的几个静态变量来引用：

```java
var ldt = LocalDateTime.now();
System.out.println(DateTimeFormatter.ISO_DATE.format(ldt));
System.out.println(DateTimeFormatter.ISO_DATE_TIME.format(ldt));
```

得到的输出和`toString()`类似：

```
2019-09-15
2019-09-15T23:16:51.56217
```

### 小结

对`ZonedDateTime`或`LocalDateTim`e进行格式化，需要使用`DateTimeFormatter`类；

`DateTimeFormatter`可以通过格式化字符串和`Locale`对日期和时间进行定制输出。

## Instant

我们已经讲过，计算机存储的当前时间，本质上只是一个不断递增的整数。Java提供的`System.currentTimeMillis()`返回的就是以毫秒表示的当前时间戳。

这个当前时间戳在`java.time`中以`Instant`类型表示，我们用`Instant.now()`获取当前时间戳，效果和`System.currentTimeMillis()`类似：

```java
public class Main {
    public static void main(String[] args) {
        Instant now = Instant.now();
        System.out.println(now.getEpochSecond()); // 秒
        System.out.println(now.toEpochMilli()); // 毫秒
    }
}
```

打印的结果类似：

```
1568568760
1568568760316
```

实际上，`Instant`内部只有两个核心字段：

```java
public final class Instant implements ... {
    private final long seconds;
    private final int nanos;
}
```

一个是以秒为单位的时间戳，一个是更精确的纳秒精度。它和`System.currentTimeMillis()`返回的`long`相比，只是多了更高精度的纳秒。

既然`Instant`就是时间戳，那么，给它附加上一个时区，就可以创建出`ZonedDateTime`：

```java
// 以指定时间戳创建Instant:
Instant ins = Instant.ofEpochSecond(1568568760);
ZonedDateTime zdt = ins.atZone(ZoneId.systemDefault());
System.out.println(zdt); // 2019-09-16T01:32:40+08:00[Asia/Shanghai]
```

可见，对于某一个时间戳，给它关联上指定的`ZoneId`，就得到了`ZonedDateTime`，继而可以获得了对应时区的`LocalDateTime`。

所以，`LocalDateTime`，`ZoneId`，`Instant`，`ZonedDateTime`和`long`都可以互相转换：

```
┌─────────────┐
│LocalDateTime│────┐
└─────────────┘    │    ┌─────────────┐
                   ├───>│ZonedDateTime│
┌─────────────┐    │    └─────────────┘
│   ZoneId    │────┘           ▲
└─────────────┘      ┌─────────┴─────────┐
                     │                   │
                     ▼                   ▼
              ┌─────────────┐     ┌─────────────┐
              │   Instant   │<───>│    long     │
              └─────────────┘     └─────────────┘
```

转换的时候，只需要留意`long`类型以毫秒还是秒为单位即可。

### 小结

Instant表示高精度时间戳，它可以和`ZonedDateTime`以及`long`互相转换。

## 日期时间实践

由于Java提供了新旧两套日期和时间的API，除非涉及到遗留代码，否则我们应该坚持使用新的API。

如果需要与遗留代码打交道，如何在新旧API之间互相转换呢？

### 旧API转新API

如果要把旧式的`Date`或`Calendar`转换为新API对象，可以通过`toInstant()`方法转换为`Instant`对象，再继续转换为`ZonedDateTime`：

```java
// Date -> Instant:
Instant ins1 = new Date().toInstant();

// Calendar -> Instant -> ZonedDateTime:
Calendar calendar = Calendar.getInstance();
Instant ins2 = calendar.toInstant();
ZonedDateTime zdt = ins2.atZone(calendar.getTimeZone().toZoneId());
```

