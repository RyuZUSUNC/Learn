# ClassLoader(类加载机制)

Java 是一个依赖于 `JVM` (Java虚拟机)实现的跨平台的开发语言. Java 程序在运行前需要先编译成 `class文件`,Java 类初始化的时候会调用 `java.lang.ClassLoader` 加载类字节码, `ClassLoader` 会调用 JVM 的 native 方法 (`defineClass0/1/2`) 来定义一个 `java.lang.Class` 实例.

![](https://gitee.com/ryuzusunc/archives/raw/master/img/JVM%E6%9E%B6%E6%9E%84%E5%9B%BE.png)

# Java类

Java是编译型语言，我们编写的java文件需要编译成后class文件后才能够被JVM运行.

示例 TestHelloWorld.java:

```java
package org.ffffffff0x.Classloader;

/**
 * @author: RyuZUSUNC
 * @create: 2021-04-06 09:46
 **/

public class TestHelloWorld {
    public String Hello(){
        return "Hello World";
    }
}

```

编译`TestHelloWorld.java`：`javac TestHelloWorld.java`

我们可以通过JDK自带的`javap`命令反汇编`TestHelloWorld.class`文件对应的`com.anbai.sec.classloader.TestHelloWorld`类,也可以使用Linux自带的`hexdump`命令查看`TestHelloWorld.class`文件二进制内容：

```powershell
javap -c -p -l .\TestHelloWorld.class

Compiled from "TestHelloWorld.java"
public class org.ffffffff0x.Classloader.TestHelloWorld {
  public org.ffffffff0x.Classloader.TestHelloWorld();
    Code:
       0: aload_0
       1: invokespecial #1                  // Method java/lang/Object."<init>":()V
       4: return
    LineNumberTable:
      line 8: 0

  public java.lang.String Hello();
    Code:
       0: ldc           #2                  // String Hello World
       2: areturn
    LineNumberTable:
      line 10: 0
}
```

![](https://gitee.com/ryuzusunc/archives/raw/master/img/Snipaste_2021-04-06_10-18-47.png)

JVM在执行`TestHelloWorld`之前会先解析class二进制内容，JVM执行的其实就是如上javap命令生成的字节码(`ByteCode`)。

# ClassLoader

一切的Java类都必须经过JVM加载后才能运行,而`ClassLoader`的主要作用就是Java类文件的加载.在JVM类加载器中最顶层的是`Bootstrap ClassLoader(引导类加载器)`,`EXtension ClassLoader(扩展类加载器)`,`App ClassLoader(系统类加载器)`,`AppClassLoader`是默认的类加载器,如果类加载时我们不指定类加载器的情况下,默认会使用`AppClassLoader`加载类,`ClassLoader.getSystemClassLoader()`返回的系统加载器也是`AppClassLoader`.

值得注意的是某些时候我们获取一个类的加载器时可能返回一个 `null` 值,如: `java.io.File.class.getClassLoader()` 将返回一个 `null` 对象,因为 `java.io.File` 类在JVM初始化的时候会被 `Bootstrap ClassLoader(引导类加载器)` 加载(该类加载器实现于JVM层,采用C++编写),我们再尝试获取被 `Bootstrap ClassLoader` 类加载器所加载的类的 `ClassLoader` 的时候都会返回 `null`.

`ClassLoader` 类有如下核心方法:

1. loadClass (加载指定的Java类)
2. findClass (查找指定的Java类)
3. findLoadedClass (查找JVM已经加载过的类)
4. defineClass (定义一个Java类)
5. resolveClass (链接指定的Java类)

# Java类动态加载方式

Java 类加载方式分为 `显示` 和 `隐式`,`显示`及我们通常使用 `Java反射` 或者 `ClassLoader` 来动态加载一个类对象,而`隐式`指的是 `类名.方法名()` 或 `new` 类示例. `显示`类加载方式也可以理解为类动态加载,我们可以自定义类加载器去加载任意的类.

常用的类动态加载方式:

```java
// 反射加载TestHelloWorld示例
Class.forName("com.anbai.sec.classloader.TestHelloWorld");

// ClassLoader加载TestHelloWorld示例
this.getClass().getClassLoader().loadClass("com.anbai.sec.classloader.TestHelloWorld");
```

`Class.forName("类名")` 默认会初始化被加载类的静态属性和方法,如果不希望初始化类可以使用`Class.forName("类名",是否初始化类,类加载器)`,而`ClassLoader.loadClass`默认不会初始化类方法.

# ClassLoader类加载流程

理解Java类加载机制并非易事，这里我们以一个Java的HelloWorld来学习`ClassLoader`。

`ClassLoader` 加载 `org.ffffffff0x.Classloader.TestHelloWorld` 类重要流程如下:

1. `ClassLoader` 会调用 `public Class<?> loadClass(String name)` 方法加载 `org.ffffffff0x.Classloader.TestHelloWorld` 类.
2. 调用 `findLoadedClass` 方法检查 `TestHelloWorld` 类是否已经初始化,如果JVM已初始化过该类则直接返回类对象.
3. 如果创建当前 `ClassLoader` 时传入了父类加载器(`new ClassLoader(父类加载器)`)就使用父类加载器加载`TestHelloWorld`类，否则使用JVM的`Bootstrap ClassLoader`加载。
4. 如果上一步无法加载 `TestHelloWorld` 类，那么调用自身的 `findClass` 方法尝试加载 `TestHelloWorld` 类。
5. 如果当前的 `ClassLoader` 没有重写 `findClass` 方法,那么直接返回类加载失败异常.如果当前类重写了 `findClass` 方法并通过传入的 `org.ffffffff0x.Classloader.TestHelloWorld` 类名找到了对应的类字节码,那么应该调用 `defineClass` 方法去JVM中注册该类.
6. 如果调用loadClass的时候传入的 `resolve` 参数为true,那么还需要调用 `resolveClass` 方法链接类,默认为false.
7. 返回一个被JVM加载后的 `java.lang.Class` 类对象.

# 自定义ClassLoader

`java.lang.ClassLoader` 是所有类加载器的父类,`java.lang.ClassLoader` 有非常多的子类加载器,比如我们用于加载jar包的 `java.net,URLClassLoader` 其本身通过继承 `java.lang.ClassLoader` 类,重写了 `findClass` 方法从而实现了加载目录class文件甚至是远程资源文件.

既然已知ClassLoader具备了加载类的能力，那么我们不妨尝试下写一个自己的类加载器来实现加载自定义的字节码(这里以加载`TestHelloWorld`类为例)并调用`hello`方法。

如果`org.ffffffff0x.Classloader.TestHelloWorld`类存在的情况下，我们可以使用如下代码即可实现调用`hello`方法并输出：

```java
TestHelloWorld t = new TestHelloWorld();
String str = t.hello();
System.out.println(str);
```

但是如果`org.ffffffff0x.Classloader.TestHelloWorld`根本就不存在于我们的`classpath`，那么我们可以使用自定义类加载器重写`findClass`方法，然后在调用`defineClass`方法的时候传入`TestHelloWorld`类的字节码的方式来向JVM中定义一个`TestHelloWorld`类，最后通过反射机制就可以调用`TestHelloWorld`类的`hello`方法了。

TestClassLoader示例:

```java
package org.ffffffff0x.Classloader;

import java.lang.reflect.Method;

public class TestClassLoader extends ClassLoader{
    // TestHelloWorld类名
    private static String testClassName = "org.ffffffff0x.Classloader.TestHelloWorld";

    // TestHelloWorld类字节码
    private static byte[] testClassBytes = new byte[]{
            -74, -126, -58, -62, 0, 0, 0, 52, 0, 17, 10, 0, 4, 0, 13, 8, 0, 14, 7, 0, 15, 7, 0, 16, 1,
            0, 6, 60, 105, 110, 105, 116, 62, 1, 0, 3, 40, 41, 86, 1, 0, 4, 67, 111, 100, 101, 1, 0,
            15, 76, 105, 110, 101, 78, 117, 109, 98, 101, 114, 84, 97, 98, 108, 101, 1, 0, 5, 72, 101,
            108, 108, 111, 1, 0, 20, 40, 41, 76, 106, 97, 118, 97, 47, 108, 97, 110, 103, 47, 83, 116,
            114, 105, 110, 103, 59, 1, 0, 10, 83, 111, 117, 114, 99, 101, 70, 105, 108, 101, 1, 0, 19,
            84, 101, 115, 116, 72, 101, 108, 108, 111, 87, 111, 114, 108, 100, 46, 106, 97, 118, 97,
            12, 0, 5, 0, 6, 1, 0, 11, 72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 1, 0, 41, 111,
            114, 103, 47, 102, 102, 102, 102, 102, 102, 102, 102, 48, 120, 47, 67, 108, 97, 115, 115, 108,
            111, 97, 100, 101, 114, 47, 84, 101, 115, 116, 72, 101, 108, 108, 111, 87, 111, 114, 108, 100,
            1, 0, 16, 106, 97, 118, 97, 47, 108, 97, 110, 103, 47, 79, 98, 106, 101, 99, 116, 0, 33, 0, 3,
            0, 4, 0, 0, 0, 0, 0, 2, 0, 1, 0, 5, 0, 6, 0, 1, 0, 7, 0, 0, 0, 29, 0, 1, 0, 1, 0, 0, 0, 5, 42,
            -55, 0, 1, -49 , 0, 0, 0, 1, 0, 8, 0, 0, 0, 6, 0, 1, 0, 0, 0, 8, 0, 1, 0, 9, 0, 10, 0, 1, 0, 7,
            0, 0, 0, 27, 0, 1, 0, 1, 0, 0, 0, 3, 18, 2, -48, 0, 0, 0, 1, 0, 8, 0, 0, 0, 6, 0, 1, 0, 0, 0,
            10, 0, 1, 0, 11, 0, 0, 0, 2, 0, 12
    };

    @Override
    public Class<?> findClass(String name) throws ClassNotFoundException {
        // 只处理TestHelloWorld类
        if (name.equals(testClassName)) {
            // 调用JVM的native方法定义TestHelloWorld类
            return defineClass(testClassName, testClassBytes, 0, testClassBytes.length);
        }

        return super.findClass(name);
    }

    public static void main(String[] args) {
        // 创建自定义的类加载器
        TestClassLoader loader = new TestClassLoader();

        try {
            // 使用自定义的类加载器加载TestHelloWorld类
            Class testClass = loader.loadClass(testClassName);

            // 反射创建TestHelloWorld类，等价于 TestHelloWorld t = new TestHelloWorld();
            Object testInstance = testClass.newInstance();

            // 反射获取hello方法
            Method method = testInstance.getClass().getMethod("Hello");

            // 反射调用hello方法,等价于 String str = t.hello();
            String str = (String) method.invoke(testInstance);

            System.out.println(str);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

利用自定义类加载器我们可以在webshell中实现加载并调用自己编译的类对象，比如本地命令执行漏洞调用自定义类字节码的native方法绕过RASP检测，也可以用于加密重要的Java类字节码(只能算弱加密了)。

# URLClassLoader

`URLClassLoader` 继承了 `ClassLoader`,`URLClassLoader` 提供了加载远程资源的能力,在写漏洞利用的 `payload` 或者 `webshell` 的时候我们可以使用这个特性来加载远程的jar实现远程的类方法调用.

TestUrlClassLoader.java 示例:

```java

```