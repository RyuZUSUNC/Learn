>https://www.cnblogs.com/nwgdk/p/8661442.html

# 嵌套类

在 Java 语言中允许在另外一个类中定义一个类，这样的类被称为嵌套类。包含嵌套类的类称为外部类（outer class），也可以叫做封闭类，在本文中统一叫做外部类。

内部类的语法：

```java
class OuterClass {
    // code
    class NestedClass {
      // code
    }
}
```

嵌套类分为两类：

- 静态嵌套类( Static nested classes )：使用`static`声明，一般称为嵌套类( Nested Classes )。
- 非静态嵌套类( Non-static Nested Classes )：非`static`声明，一般称为内部类( Inner Classes )。

```java
class OuterClass {
  ...
  static class StaticNestedClass {
    ...
  }
  class InnerClass {
    ...
  }
}
```
嵌套类是它的外部类的成员，非静态嵌套类（内部类）可以访问外部类的其他成员，即使该成员是私有的。而静态嵌套类只能访问外部类的静态成员。

嵌套类作为外部类的一个成员，可以被声明为：`private`,`public`,`protected`或者`包范围`（注意：外部类只能被声明为`public`或者`包范围`）

# 为什么要使用嵌套类

优点：
- 嵌套类可以访问外部类的所有数据成员和方法，即使它是私有的。
- 提高可读性和可维护性：因为如果一个类只对另外一个类可用，那么将它们放在一起，这更便于理解和维护。
- 提高封装性：给定两个类A和B，如果需要访问A类中的私有成员，则可以将B类封装在A类中，这样不仅可以使得B类可以访问A类中的私有成员，并且可以在外部隐藏B类本身。
- 减少代码的编写量。

# 嵌套类的类型

前文已经介绍了嵌套类分为静态嵌套类和非静态嵌套类，而非静态嵌套类又称为内部类（内部类是嵌套类的子集）。

静态嵌套类可以使用外部类的名称来访问它。例如：

```java
OuterClass.StaticNestedClass
```

如果要为静态嵌套类创建对象，则使用以下语法:

```java
OuterClass.StaticNestedClass nestedObject =
        new OuterClass.StaticNestedClass();
```

非静态嵌套类(内部类)又可以分为以下三种：

- 成员内部类（Member inner class）
- 匿名内部类（Anonymous inner class）
- 局部内部类（Local inner class）

结构:
- Nested classes
  - Inner classes
    - Inner classes
    - Method local Inner classes
    - Anonymous Inner classes
  - Statuc Nested classes

| 类型 | 描述 |
| - | - |
| 成员内部类 | 在类中和方法外部创建的类
| 匿名内部类 | 为实现接口或扩展类而创建的类，它的名称由编译器决定
| 局部内部类 | 在方法内部创建的类
| 静态嵌套类 | 在类中创建的静态类
| 嵌套接口   | 在类中或接口中创建的接口

# 静态嵌套类
静态嵌套类其实就是在顶级类中封装的一个顶级类，它的行为和顶级类一样，它被封装在顶级类中其实就是为了方便打包。

- 静态嵌套类是外部类的静态成员，它可以直接使用外部类名.静态嵌套类名访问自身。
- 它可以访问外部类的静态成员和静态私有成员。
- 与其他类一样，静态嵌套类不能访问非静态成员。

静态嵌套类的语法如下：
```java
class OuterClass{  
    // 外部类的静态数据成员
    static int data = 30;  
    // 外部类中的静态嵌套类
    static class StaticNestedClass {  
        // 静态嵌套类中的实例方法
        void getData() {System.out.println("data is "+data);}  
    }

    public static void main(String args[]){  
        // 实例化静态嵌套类（创建对象）
        OuterClass.StaticNestedClass obj = new OuterClass.StaticNestedClass();  
        obj.getData();  
    }  
}  
```

在上面的例子中，你需要先创建一个静态嵌套类的实例，因为你需要访问它的实例方法`getData()`。但是你并不需要实例化外部类，因为静态嵌套类相对于外部类来说它是静态的，可以直接使用`外部类名.静态嵌套类名`访问。

## 由编译器生成的静态嵌套类
```java
import java.io.PrintStream;  
    static class OuterClass$Inner  
    {  
    OuterClass$StaticNestedClass(){}  
        void getData(){  
            System.out.println((new StringBuilder()).append("data is ")
            .append(OuterClass.data).toString());  
    }    
}  
```

从上面的代码可以看出，静态嵌套类实际上是直接通过`OuterClass.data`来访问外部类的静态成员的。

## 使用静态嵌套类的静态方法示例：

如果静态嵌套类中有静态成员，则不需要实例化静态嵌套类即可直接访问。
```java
class OuterClass2{  
    static int data = 10;  
    static class StaticNestedClass{  
        // 静态嵌套类的静态方法
        static void getData() {System.out.println("data is "+data);}  
    }  

    public static void main(String args[]){  
        // 不需要创建实例可以直接访问
        OuterClass2.StaticNestedClass.getData();
    }  
}  
```

# 非静态嵌套类
非静态嵌套类也就是内部类，它有以下几个特点：

- 实例化内部类必须先实例化一个外部类。
- 内部类实例与外部类实例相关联，所有不能在内部类中定义任何静态成员。
- 内部类是非静态的。

## 成员内部类
在外部类中并且在外部类的方法外创建的非静态嵌套类，称为成员内部类。说白了成员内部类就是外部类的一个非静态成员而已。

```java
class OuterClass{  
    //code  
    class MemberInnerClass{  
        //code  
    }  
} 
```

### 成员内部类示例

在下面的示例中，我们在成员内部类中创建了getData()和getTest()这两个实例方法，并且这两个方法正在访问外部类中的私有数据成员和成员方法。
```java
class OuterClass {  
    private int data = 30;  
    public void test() {System.out.println("我是外部类成员方法");}
    class MemberInnerClass {  
        // 访问外部类的私有数据成员
        void getData() {System.out.println("data is "+data);}  
        // 访问外部类的成员方法
        void getTest() {OuterClass.this.test();}
    }  

    public static void main(String args[]) {  
        // 首先必须实例化外部类
        OuterClass obj = new OuterClass();  
        // 接着通过外部类对象来创建内部类对象
        OuterClass.MemberInnerClass in = obj.new MemberInnerClass();  
        in.getData();
        in.getTest();  
    }  
}  
```

访问外部类的成员方法时，可以直接通过`外部类名.this.外部类成员方法()`来调用，或者直接使用`外部类成员方法()`来调用。

### 成员内部类的工作方式
Java 编译器创建了两个`.class`文件，其中一个是成员内部类`OuterClass$MemberInnerClass.class`，成员内部类文件名格式为`外部类名$成员内部类名`。

如果你想创建成员内部类的实例，你必须先实例化一个外部类，接着，通过外部类的实例来创建成员内部类的实例。因此成员内部类的实例必须存在于一个外部类的实例中。另外，由于内部类的实例与外部类的实例相关联，因此它不能定义任何静态成员。

