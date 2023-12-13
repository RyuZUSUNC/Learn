# java 序列化和反序列化的实现原理

##  什么是序列化

1. java序列化是指把java对象转换为字节序列的过程，而java反序列化是指把字节序列恢复为java对象的过程

2. 序列化：对象序列化的最主要的用处就是在传递和保存对象的时候，保证对象的`完整性`和`可传递性`。序列化是把对象转换成有序字节流，以便在网络上传输或者保存在本地文件中。序列化后的字节流保存的java对象的状态以及相关的描述信息。序列化机制的核心作用就是对象`状态的保存与重建`。

3. 反序列化：客户端从文件中或网络上获得序列化后的对象字节流后，根据字节流中所保存的对象状态及描述信息，通过反序列化重建对象。

4. 序列化就是把实体对象状态按照一定的格式写入到有序字节流，反序列化就是从有序字节流重建对象，恢复对象状态

## 为什么需要序列化与反序列化
1. 当两个进程进行远程通信时，可以相互发送各种类型的数据，包括文本，图片，音频，视频等，而这些数据都会以二进制的形式在网络上传送。

2. 当两个java进行进行通信时，要传送对象，怎么传对象，通过序列化与反序列化。

3. 也就是说，发送方需要把对象转换为字节序列，然后在网络上传送，另一方面，接收方需要从字节序列中恢复出java对象

## 序列化的好处
1. 永久性保存对象，保存对象的字节序列到本地文件或者数据库中，实现了数据的持久化，通过序列化可以把数据永久的保存到硬盘上

2. 利用序列化实现远程通信，可以在网络上传送对象的字节序列

3. 在进程间传递对象

## 序列化算法步骤
1. 把对象实例相关的类元数据输出

2. 递归输出类的超类描述直到不再有超类

3. 类元数据完了以后，开始从最懂曾的超类开始输出对象实例的实际数据值

4. 从上至下递归输出实例的数据

## Java 如何实现序列化和反序列化

### JDK类库中序列化API

java.io.ObjectOutputStream: 表示输出对象流

它的writeObject(Object obj)方法可以对参数指定的obj对象进行序列化，把得到的字节序列写到一个目标输出流中；

java.io.ObjectInputStream:表示对象输入流

它的readObject()方法源输入流中读取字节序列，再把它们反序列化成为一个对象，并将其返回

### **实现序列化的要求**

>只有实现了Serializable或Externalizable接口的对象才能被序列化，否则抛出异常！

一个类的对象要想序列化成功，必须满足两个条件：

1. 该类必须实现 java.io.Serializable 接口。

2. 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的。
   
如果想知道一个 Java 标准类是否是可序列化的，可以通过查看该类的文档,查看该类有没有实现 java.io.Serializable接口。

### **实现java对象序列化与反序列化的方法**

例1，编写一个可被序列化的类

```java
public class Employee implements java.io.Serializable
{
   public String name;
   public String identify;
   public void mailCheck()
   {
      System.out.println("This is the "+this.identify+" of our company");
   }
}
```
将对象序列化成二进制文件
```java
//反序列化所需类在io包中
import java.io.*;

public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "员工甲";
      e.identify = "General staff";
      try
      {
        // 打开一个文件输入流
         FileOutputStream fileOut =
         new FileOutputStream("D:\\Task\\employee1.db");
         // 建立对象输入流
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         //输出反序列化对象
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in D:\\Task\\employee1.db");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
```
反序列化操作
```java
import java.io.*;

public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
        // 打开一个文件输入流
         FileInputStream fileIn = new FileInputStream("D:\\Task\\employee1.db");
        // 建立对象输入流
         ObjectInputStream in = new ObjectInputStream(fileIn);
        // 读取对象
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("This is the "+e.identify+" of our company");
    }
}
```