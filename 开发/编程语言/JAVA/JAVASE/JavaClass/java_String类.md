# Java String 类

**字符串广泛应用 在 Java 编程中，在 Java 中字符串属于对象，Java 提供了 String 类来创建和操作字符串。**


# 创建字符串
最简单的方式：
```java
String greeting = "TEST";

```


在代码中遇到字符串常量时，这里的值是 "TEST"，编译器会使用该值创建一个 String 对象。

和其它对象一样，可以使用关键字和构造方法来创建 String 对象。

String 类有 11 种构造方法，这些方法提供不同的参数来初始化字符串，比如提供一个字符数组参数:

```java
public class StringDemo{
   public static void main(String args[]){
      char[] helloArray = { 'r', 'u', 'n', 'o', 'o', 'b'};
      String helloString = new String(helloArray);  
      System.out.println( helloString );
   }
}

```
以上实例编译运行结果如下：

```
runoob

```
>注意:String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了。

详解：
```java
String s = "Google";
System.out.println("s = " + s);

s = "Runoob";
System.out.println("s = " + s);

```

输出结果为：
```
Google
Runoob

```
从结果上看是改变了，但为什么说String对象是不可变的呢？

原因在于实例中的 s 只是一个 String 对象的引用，并不是对象本身，当执行 s = "Runoob"; 创建了一个新的对象 "Runoob"，而原来的 "Google" 还存在于内存中。

![1](..\img\string-no-modify.png)

>如果需要对字符串做很多修改，那么应该选择使用 `StringBuffer & StringBuilder` 类。

# 字符串长度
用于获取有关对象的信息的方法称为`访问器方法`。

String 类的一个访问器方法是 length() 方法，它返回字符串对象包含的字符数。

下面的代码执行后，len 变量等于 14:

```java
public class StringDemo {
    public static void main(String args[]) {
        String site = "11111111111111";
        int len = site.length();
        System.out.println( "总共的数字数 : " + len );
   }
}

```
以上实例编译运行结果如下：

```
总共的数字数: 14

```

# 连接字符串
String 类提供了连接两个字符串的方法：
```java
string1.concat(string2);

```

返回 string2 连接 string1 的新字符串。也可以对字符串常量使用 concat() 方法，如：

```java
"我的名字是 ".concat("Runoob");

```

更常用的是使用'+'操作符来连接字符串，如：

```java
"Hello," + " runoob" + "!"

```

结果如下:

```java
"Hello, runoob!"

```
下面是一个例子:
```java
public class StringDemo {
    public static void main(String args[]) {     
        String string1 = "菜鸟教程网址：";     
        System.out.println("1、" + string1 + "www.runoob.com");  
    }
}

```

以上实例编译运行结果如下：

```
1、菜鸟教程网址：www.runoob.com

```

# 创建格式化字符串

我们知道输出格式化数字可以使用 printf() 和 format() 方法。

String 类使用静态方法 format() 返回一个String 对象而不是 PrintStream 对象。

String 类的静态方法 format() 能用来创建可复用的格式化字符串，而不仅仅是用于一次打印输出。

如下所示：

```java
System.out.printf("浮点型变量的值为 " +
                  "%f, 整型变量的值为 " +
                  " %d, 字符串变量的值为 " +
                  "is %s", floatVar, intVar, stringVar);

```
你也可以这样写

```java
String fs;
fs = String.format("浮点型变量的值为 " +
                   "%f, 整型变量的值为 " +
                   " %d, 字符串变量的值为 " +
                   " %s", floatVar, intVar, stringVar);
```

# 判断A字符串中是否包含B字符或字符串
## contains() 方法
java.lang.String.contains()

方法返回true，当且仅当此字符串包含指定的char值序列

返回值为true和false
```java
public static void main(String[] args) {
 
        String str = "abc";
 
        boolean status = str.contains("a");
 
        if(status){
            System.out.println("包含");
 
        }else{
            System.out.println("不包含");
        }
}
```

## indexOf() 方法
java.lang.String.indexOf() 的用途是在一个字符串中寻找一个字的位置，同时也可以判断一个字符串中是否包含某个字符

indexOf的返回值为int

```java
public static void main(String[] args) {
    String str1 = "abcdefg";
    int result1 = str1.indexOf("ab");
    if(result1 != -1){
        System.out.println("字符串str中包含子串“ab”"+result1);
    }else{
        System.out.println("字符串str中不包含子串“ab”"+result1);
    }
```

# split() 方法
split() 方法根据匹配给定的正则表达式来拆分字符串。

>注意： . 、 $、 | 和 * 等转义字符，必须得加 \\。

>注意：多个分隔符，可以用 | 作为连字符。

```java
 public static void main(String args[]) {
        String str = new String("Welcome-to-Runoob");
 
        System.out.println("- 分隔符返回值 :" );
        for (String retval: str.split("-")){
            System.out.println(retval);
        }
 
        System.out.println("");
        System.out.println("- 分隔符设置分割份数返回值 :" );
        for (String retval: str.split("-", 2)){
            System.out.println(retval);
        }
 
        System.out.println("");
        String str2 = new String("www.runoob.com");
        System.out.println("转义字符返回值 :" );
        for (String retval: str2.split("\\.", 3)){
            System.out.println(retval);
        }
 
        System.out.println("");
        String str3 = new String("acount=? and uu =? or n=?");
        System.out.println("多个分隔符返回值 :" );
        for (String retval: str3.split("and|or")){
            System.out.println(retval);
        }
    }
```

# subSequence() 方法
subSequence() 方法返回一个新的字符序列，它是此序列的一个子序列。

### 返回值

返回一个新的字符序列，它是此序列的一个子序列。

```java
public class Test {
    public static void main(String args[]) {
         String Str = new String("www.runoob.com");
         System.out.print("返回值 :" );
         System.out.println(Str.subSequence(4, 10) );
    }
}
```

# replace() 方法
Java String类Java String类

replace() 方法通过用 newChar 字符替换字符串中出现的所有 oldChar 字符，并返回替换后的新字符串。

```java
String Str = new String("hello");

        System.out.print("返回值 :" );
        System.out.println(Str.replace('o', 'T'));

        System.out.print("返回值 :" );
        System.out.println(Str.replace('l', 'D'));
```
