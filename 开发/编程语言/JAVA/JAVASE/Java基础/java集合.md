# 概论
为了便于处理一组类似的数据

在Java中，如果一个Java对象可以在内部持有若干其他Java对象，并对外提供访问接口，我们把这种Java对象称为集合。很显然，Java的数组可以看作是一种集合：

```java
String[] ss = new String[10]; // 可以持有10个String对象
ss[0] = "Hello"; // 可以放入String对象
String first = ss[0]; // 可以获取String对象
```

既然Java提供了数组这种数据类型，可以充当集合，那么，我们为什么还需要其他集合类？这是因为数组有如下限制：

- 数组初始化后大小不可变；
- 数组只能按索引顺序存取。

因此，我们需要各种不同类型的集合类来处理不同的数据，例如：

- 可变大小的顺序链表；
- 保证无重复元素的集合；
- ...

## Collection
Java标准库自带的java.util包提供了集合类：Collection，它是除Map外所有其他集合类的根接口。Java的java.util包主要提供了以下三种类型的集合

- List：一种有序列表的集合，例如，按索引排列的Student的List；
- Set：一种保证没有重复元素的集合，例如，所有无重复名称的Student的Set；
- Map：一种通过键值（key-value）查找的映射表集合，例如，根据Student的name查找对应Student的Map。

Java集合的设计有几个特点：
- 实现了接口和实现类相分离，例如，有序表的接口是List，具体的实现类有ArrayList，LinkedList等
- 支持泛型，我们可以限制在一个集合中只能放入同一种数据类型的元素

## List
主要接口方法
- 在末尾添加一个元素：boolean add(E e)
- 在指定索引添加一个元素：boolean add(int index, E e)
- 删除指定索引的元素：int remove(int index)
- 删除某个元素：int remove(Object e)
- 获取指定索引的元素：E get(int index)
- 获取链表大小（包含元素的个数）：int size()

特点
- 允许存在重复值
- 允许添加`null`

常用实现类
- ArrayList
  - 通过数组实现
- LinkList
  - 在LinkedList中，内部每个元素都指向下一个元素(每个元素头尾相连)

\                    | ArrayList  | LinkedList
-|-|-
获取指定元素	      |速度很快	   |需要从头开始查找元素
添加元素到末尾	      |速度很快	   |速度很快
在指定位置添加/删除	  |需要移动元素	|不需要移动元素
内存占用	         |少	      |较大

一般优先使用ArrayList

### 创建List
```java
List<Integer> list = null;
list.add(1);
list.add(2);
list.add(3);
```

java9以上 使用 List.of 快速初始化
```java
List<Integer> list = List.of(1, 2, 5);
```
List.of()方法不接受null值，如果传入null，会抛出NullPointerException异常

### 遍历List
- for循环
  - 数组大的时候效率低
- Iterator迭代器
  - 始终是最高效率
- foreach循环
  - 同迭代器

代码示例:

for循环
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

Iterator迭代器
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

foreach循环
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
只要实现了 `Iterable 接口`的集合类都可以直接用`for each`循环来遍历，Java编译器本身并不知道如何遍历集合对象，但它会自动把`for each`循环变成`Iterator`的调用，原因就在于`Iterable接口`定义了一个`Iterator<E> iterator()`方法，强迫集合类必须返回一个`Iterator实例`。

ArrayList继承关系(JAVA8)
![](..\img\集合img\ArrayList继承关系.png)

### List和Array转换


## Map


## Set

