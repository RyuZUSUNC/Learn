# Collection
集合类: Collection 除了 Map 外所有集合类的根接口, java.util 包主要提供以下三种类型的集合:

- List: 一种有序列表集合,例如,按索引排列的 Student 和 List;
- Set: 一种保证没有重复元素的集合,例如,所有无重复名称的 Student 和 List;
- Map: 一种通过键值(key-value)查找的映射表集合,例如,根据 Student 的 name 查找对应 Student 的 Map;

java 集合设计有几个特点: 

1. 实现了接口和实现类相分离,例如,有序列表的接口时 List ,具体的实现类有 ArrayList,LinkedList等
2. 支持泛型,可以限制在一个集合中只能放入同一种数据类型的元素,例如 `List<String> list = new ArrayList<>(); // 只能放入String类型`
3. 访问集合总是通过统一的方式: 迭代器(iterator)来实现,最明显的好处是无需知道集合内部元素是按什么方式存储的

不该使用的遗留类:

- Hashtable: 一种线程安全的 Map 实现
- Vector: 一种线程安全的 List 实现
- Stack: 基于 Vector 实现的 LIFO 的栈

不该使用的遗留接口:

- Enumeration<E>: 已被 Iterator<E> 取代

# List
**TAG**: 基础集合 有序列表 

List 的行为和数组几乎完全相同: 内部按照放入元素的先后顺序存放,每个元素都可以通过索引确定自己的位置,List 的索引和数组一样都从 0 开始

## 主要接口方法

- 在末尾添加一个元素: `boolean add(E e)`
- 在指定索引添加一个元素: `boolean add(int index, E e)`
- 删除指定索引的元素: `E remove(int index)`
- 删除某个元素: `boolean remove(Object e)`
- 获取指定索引的元素: `E get(int index)`
- 获取链表大小（包含元素的个数）: `int size()`
- 判断是否包含某个指定元素: `boolean contains(Object o)`
- 返回某个元素的索引: `int indexOf(Object o)`

## 常用实现

- ArrayList: 可以理解为封装了添加删除功能的数组
  - 获取指定元素: 速度很快
  - 添加元素到末尾: 速度很快
  - 在指定位置添加/删除: 需要移动元素
  - 内存占用: 少
- LinkedList: 其中的每一个元素都直指向下一个元素
  - 获取指定元素: 需要从头开始查找元素
  - 添加元素到末尾: 速度很快
  - 在指定位置添加/删除: 不需要移动元素
  - 内存占用: 较大

## 特点

- List 内部元素可以重复
- List 允许添加 null

## 创建

除了使用 ArrayList 和 LinkedList ,在java 9之后还可以通过 List 接口提供的 `of()` 方法,根据给定元素快速创建

```java
List<Integer> list = List.of(1, 2, 5);
```

但是 `List.of()` 方法不接受 `null` 值,如果传入会抛出 `NullPointerException` 异常

## 遍历

不建议使用 for 循环配合 get(int) 索引的方式遍历,只有 ArrayList 的 get(int) 的实现是高效的,换成 LinkedList 后索引越大速度越慢

建议使用迭代器 `Iterator` 访问 `List` , `Iterator` 本身也是一个对象，但它是由 `List` 的实例调用 `iterator()` 方法的时候创建的 , `Iterator` 对象知道如何遍历一个`List` ，并且不同的 `List` 类型，返回的 `Iterator` 对象实现也是不同的，但总是具有最高的访问效率

`Iterator` 对象有两个方法: 
- boolean hasNext(): 判断是否有下一个元素
- E next(): 返回下一个元素

示例代码:
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

由于 `Iterator` 遍历是如此常用，所以，`Java` 的 `for each` 循环本身就可以帮我们使用 `Iterator` 遍历

示例代码:
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

只要实现了 `Iterable` 接口的集合类都可以直接用 `for each` 循环来遍历，Java编译器本身并不知道如何遍历集合对象，但它会自动把 `for each` 循环变成 `Iterator` 的调用，原因就在于 `Iterable` 接口定义了一个 `Iterator<E> iterator()` 方法，强迫集合类必须返回一个 `Iterator` 实例。

## 类型转换
*List TO Array*

1. 直接调用 `toArray()` 方法直接返回一个 `Object[]` 数组

示例代码:
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

这种方法会丢失类型信息,所以实际用的比较少

2. 给 `toArray(T[])` 传入一个类型相同的 `Array` ， `List` 内部自动把元素复制到传入的 `Array` 中

示例代码:
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

这个 `toArray(T[])` 方法的泛型参数 `<T>` 并不是 `List` 接口定义的泛型参数 `<E>` ，所以，实际上可以传入其他类型的数组.但是，如果我们传入类型不匹配的数组，例如，`String[]` 类型的数组，由于 `List` 的元素是 `Integer` ，所以无法放入 `String` 数组，这个方法会抛出 `ArrayStoreException`

如果传入的数组不够大，那么 `List` 内部会创建一个新的刚好够大的数组，填充后返回；如果传入的数组比 `List` 元素还要多，那么填充完元素后，剩下的数组元素一律填充 `null`

实际上，最常用的是传入一个“恰好”大小的数组: 

```java
Integer[] array = list.toArray(new Integer[list.size()]);
```

3. 最后一种更简洁的写法是通过 `List` 接口定义的 `T[] toArray(IntFunction<T[]> generator)` 方法: 

```java
Integer[] array = list.toArray(Integer[]::new);
```

*Array TO List*

把 `Array` 变为 `List` 就简单多了，通过 `List.of(T...)` 方法最简单: 

```java
Integer[] array = { 1, 2, 3 };
List<Integer> list = List.of(array);
```

要注意的是，返回的 `List` 不一定就是 `ArrayList` 或者 `LinkedList` ，因为 `List` 只是一个接口，如果我们调用 `List.of()` ，它返回的是一个只读 `List` ,对只读 `List` 调用 `add()`、`remove()` 方法会抛出 `UnsupportedOperationException`。

示例代码:
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = List.of(12, 34, 56);
        list.add(999); // UnsupportedOperationException
    }
}
```

## equals方法
`List` 提供了`boolean contains(Object o)`方法来判断`List`是否包含某个指定元素。此外，`int indexOf(Object o)`方法可以返回某个元素的索引，如果元素不存在，就返回`-1`。

`List`内部并不是通过`==`判断两个元素是否相等，而是使用`equals()`方法判断两个元素是否相等,因此,要正确使用`List`的`contains()`、`indexOf()`这些方法，放入的实例必须正确覆写`equals()`方法

`equals()`方法要求我们必须满足以下条件:
- 自反性（Reflexive）：对于非`null`的`x`来说，`x.equals(x)`必须返回`true`；
- 对称性（Symmetric）：对于非`null`的`x`和`y`来说，如果`x.equals(y`)为`true`，则`y.equals(x)`也必须为`true`；
- 传递性（Transitive）：对于非`null`的`x`、`y`和`z`来说，如果`x.equals(y)`为`true`，`y.equals(z)`也为`true`，那么`x.equals(z)`也必须为`true`；
- 一致性（Consistent）：对于非`null`的`x`和`y`来说，只要`x`和`y`状态不变，则`x.equals(y)`总是一致地返回`true`或者`false`；
- 对`null`的比较：即`x.equals(null)`永远返回`false`

示例:

```java
public class Person {
    public String name;
    public int age;
}
```

首先，我们要定义“相等”的逻辑含义。对于 `Person` 类，如果 `name` 相等，并且 `age` 相等，我们就认为两个 `Person` 实例相等。

```java
public boolean equals(Object o) {
    if (o instanceof Person) {
        Person p = (Person) o;
        return this.name.equals(p.name) && this.age == p.age;
    }
    return false;
}
```

对于引用字段比较，使用 `equals()` ，对于基本类型字段的比较，使用 `==`。

如果 `this.name` 为 `null` ，那么 `equals()` 方法会报错，需要继续改写如下：

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

如果 `Person` 有好几个引用类型的字段，上面的写法就太复杂了。要简化引用类型的比较，我们使用 `Objects.equals()` 静态方法：

```java
public boolean equals(Object o) {
    if (o instanceof Person) {
        Person p = (Person) o;
        return Objects.equals(this.name, p.name) && this.age == p.age;
    }
    return false;
}
```


**总结**
1. 确定实例“相等”的逻辑，即哪些字段相等，就认为实例相等；
2. 用 `instanceof` 判断传入的待比较的 `Object` 是不是当前类型，如果是，继续比较，否则，返回 `false`；
3. 对引用类型用 `Objects.equals()` 比较，对基本类型直接用 `==` 比较。

- 使用 `Objects.equals()` 比较两个引用类型是否相等的目的是省去了判断 `null` 的麻烦。两个引用类型都是 `null` 时它们也是相等的。
- 如果不调用 `List` 的 `contains()` 、`indexOf()` 这些方法，那么放入的元素就不需要实现 `equals()` 方法。

# Map
**TAG**:基础集合 键值对列表

通过一个键去查询对应的值，使用 List 来实现存在效率非常低的问题，因为平均需要扫描一半的元素才能确定，而 Map 这种键值（key-value）映射表的数据结构，作用就是能高效通过 key 快速查找 value （元素）。

## 主要接口方法
- 添加一个键值对: `put(K key, V value)`
- 通过 key 获取到对应的 value 不存在返回`null`: `V get(K key)`
- 查询某个 key 是否存在: `boolean containsKey(K key)`

## 特点
- Map 中不存在重复的 key，因为放入相同的 key，只会把原有的 key-value 对应的 value 给替换掉。
- 虽然 key 不能重复，但 value 是可以重复的
- 遍历时不保证顺序

## 遍历
可以使用 for each 循环遍历Map实例的 keySet() 方法返回的 Set 集合，它包含不重复的 key 的集合

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

同时遍历 key 和 value 可以使用 for each 循环遍历 Map 对象的 entrySet()集合，它包含每一个 key-value 映射

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

## equals 和 hashCode
