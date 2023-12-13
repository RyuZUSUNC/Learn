# 泛型关键字
- ？ 表示不确定的java类型。

- T  表示java类型。

- K V 分别代表java键值中的KeyValue。

- E 代表Element。

## 与Object的区别
Object是所有类的根类，是具体的一个类，使用的时候可能是需要类型强制转换的，但是用T ？等这些的话，在实际用之前类型就已经确定了，不需要强制转换。



# Java中泛型T和Class<T>以及Class<?>的理解

Class类的实例表示Java应用运行时的类（class ans enum）或接口（interface and annotation）（每个Java类运行时都在JVM里表现为一个Class对象，可通过类名.class，类型.getClass()，Class.forName("类名")等方法获取Class对象）。数组同样也被映射为为Class对象的一个类，所有具有相同元素类型和维数的数组都共享该Class对象。基本类型boolean，byte，char，short，int，long，float，double和关键字void同样表现为Class对象。

- T  bean ;

- Class<T> bean;

- Class<?> bean;

单独的T代表一个类型，而Class<T>和Class<?>代表这个类型所对应的类

- Class<T>在实例化的时候，T要替换成具体类

- Class<?>它是个通配泛型，?可以代表任何类型   

- <? extends T>受限统配，表示T的一个未知子类。

- <? super T>下限统配，表示T的一个未知父类。

public T find(Class<T> clazz, int id);

根据类来反射生成一个实例，而单独用T没法做到。

- Object类中包含一个方法名叫getClass，利用这个方法就可以获得一个实例的类型类。类型类指的是代表一个类型的类，因为一切皆是对象，类型也不例外，在Java使用类型类来表示一个类型。所有的类型类都是Class类的实例。getClass()会看到返回Class<?>。

JDK中，普通的Class.newInstance()方法的定义返回Object，要将该返回类型强制转换为另一种类型;

但是使用泛型的Class<T>，Class.newInstance()方法具有一个特定的返回类型;


# Java泛型

开发人员在使用泛型的时候，很容易根据自己的直觉而犯一些错误。比如一个方法如果接收List作为形式参数，那么如果尝试将一个List的对象作为实际参数传进去，却发现无法通过编译。虽然从直觉上来说，Object是String的父类，这种类型转换应该是合理的。但是实际上这会产生隐含的类型转换问题，因此编译器直接就禁止这样的行为。

## 类型擦除

正确理解泛型概念的首要前提是理解类型擦除（type erasure）。 Java中的泛型基本上都是在编译器这个层次来实现的。在生成的Java字节代码中是不包含泛型中的类型信息的。使用泛型的时候加上的类型参数，会被编译器在编译的时候去掉。这个过程就称为类型擦除。如在代码中定义的 List<Object> 和 List<String> 等类型，在编译之后都会变成List。JVM看到的只是List，而由泛型附加的类型信息对JVM来说是不可见的。Java编译器会在编译时尽可能的发现可能出错的地方，但是仍然无法避免在运行时刻出现类型转换异常的情况。类型擦除也是Java的泛型实现方式与C++模板机制实现方式之间的重要区别。

很多泛型的奇怪特性都与这个类型擦除的存在有关，包括：

泛型类并没有自己独有的Class类对象。比如并不存在List<String>.class或是List<Integer>.class，而只有List.class。

静态变量是被泛型类的所有实例所共享的。对于声明为MyClass<T>的类，访问其中的静态变量的方法仍然是 MyClass.myStaticVar。不管是通过new MyClass<String>还是new MyClass<Integer>创建的对象，都是共享一个静态变量。

泛型的类型参数不能用在Java异常处理的catch语句中。因为异常处理是由JVM在运行时刻来进行的。由于类型信息被擦除，JVM是无法区分两个异常类型MyException<Integer>和MyException<String>的。对于JVM来说，它们都是 MyException类型的。也就无法执行与异常对应的catch语句。

类型擦除的基本过程也比较简单，首先是找到用来替换类型参数的具体类。这个具体类一般是Object。如果指定了类型参数的上界的话，则使用这个上界。把代码中的类型参数都替换成具体的类。同时去掉出现的类型声明，即去掉<>的内容。比如T get()方法声明就变成了Object get()；List<String>就变成了List。接下来就可能需要生成一些桥接方法（bridge method）。这是由于擦除了类型之后的类可能缺少某些必须的方法。

了解了类型擦除机制之后，就会明白编译器承担了全部的类型检查工作。编译器禁止某些泛型的使用方式，正是为了确保类型的安全性。

通配符与上下界

在使用泛型类的时候，既可以指定一个具体的类型，如List<String>就声明了具体的类型是String；也可以用通配符?来表示未知类型，如List<?>就声明了List中包含的元素类型是未知的。 通配符所代表的其实是一组类型，但具体的类型是未知的。List<?>所声明的就是所有类型都是可以的。但是List<?>并不等同于List<Object>。List<Object>实际上确定了List中包含的是Object及其子类，在使用的时候都可以通过Object来进行引用。而List<?>则其中所包含的元素类型是不确定。其中可能包含的是String，也可能是 Integer。如果它包含了String的话，往里面添加Integer类型的元素就是错误的。正因为类型未知，就不能通过new ArrayList()的方法来创建一个新的ArrayList对象。因为编译器无法知道具体的类型是什么。但是对于 List<?>中的元素确总是可以用Object来引用的，因为虽然类型未知，但肯定是Object及其子类。

public void wildcard(List<?> list) {list.add(1);//编译错误}

试图对一个带通配符的泛型类进行操作的时候，总是会出现编译错误。其原因在于通配符所表示的类型是未知的。(通配符表示的类型未知，可能是String也可能是Float，那我怎么add。要进行类型转换的，没法强制啊，隐式转换又不成功，？改成Object的话那就不一样了，添加进来int后，父类对象指向子类引用)

对于List<?>中的元素只能用Object来引用，在有些情况下不是很方便。在这些情况下，可以使用上下界来限制未知类型的范围。 如List<? extends Number>说明List中可能包含的元素类型是Number及其子类。而List<? super Number>则说明List中包含的是Number及其父类。当引入了上界之后，在使用类型的时候就可以使用上界类中定义的方法。比如访问 List<? extends Number>的时候，就可以使用Number类的intValue等方法。

类型系统

在Java中，大家比较熟悉的是通过继承机制而产生的类型体系结构。比如String继承自Object。根据Liskov替换原则，子类是可以替换父类的。当需要Object类的引用的时候，如果传入一个String对象是没有任何问题的。但是反过来的话，即用父类的引用替换子类引用的时候，就需要进行强制类型转换。编译器并不能保证运行时刻这种转换一定是合法的。这种自动的子类替换父类的类型转换机制，对于数组也是适用的。 String[]可以替换Object[]。但是泛型的引入，对于这个类型系统产生了一定的影响。正如前面提到的List<String>是不能替换掉List<Object>的。

引入泛型之后的类型系统增加了两个维度：一个是类型参数自身的继承体系结构，另外一个是泛型类或接口自身的继承体系结构。第一个指的是对于 List<String>和List<Object>这样的情况，类型参数String是继承自Object的。而第二种指的是 List接口继承自Collection接口。对于这个类型系统，有如下的一些规则：

相同类型参数的泛型类的关系取决于泛型类自身的继承体系结构。即List<String>是Collection<String> 的子类型，List<String>可以替换Collection<String>。这种情况也适用于带有上下界的类型声明。

当泛型类的类型声明中使用了通配符的时候， 其子类型可以在两个维度上分别展开。如对Collection<? extends Number>来说，其子类型可以在Collection这个维度上展开，即List<? extends Number>和Set<? extends Number>等；也可以在Number这个层次上展开，即Collection<Double>和 Collection<Integer>等。如此循环下去，ArrayList<Long>和 HashSet<Double>等也都算是Collection<? extends Number>的子类型。

如果泛型类中包含多个类型参数，则对于每个类型参数分别应用上面的规则。

理解了上面的规则之后，就可以很容易的修正实例分析中给出的代码了。只需要把List<?>改成List<Object>即可。List<String>是List<?>的子类型，因此传递参数时不会发生错误。

开发自己的泛型类

泛型类与一般的Java类基本相同，只是在类和接口定义上多出来了用<>声明的类型参数。一个类可以有多个类型参数，如 MyClass<X,Y,Z>。 每个类型参数在声明的时候可以指定上界。所声明的类型参数在Java类中可以像一般的类型一样作为方法的参数和返回值，或是作为域和局部变量的类型。但是由于类型擦除机制，类型参数并不能用来创建对象或是作为静态变量的类型。

```java
class ClassTest<X extends Number,Y,Z> {

private X x;

private static Y y; //编译错误，不能用在静态变量中(为什么呢？)

public X getFirst() {//正确用法

return x;}

public void wrong() {Z z = new Z(); //编译错误，不能创建对象

}}
```

在代码中避免泛型类和原始类型的混用。比如List<String>和List不应该共同使用。这样会产生一些编译器警告和潜在的运行时异常。

在使用带通配符的泛型类的时候，需要明确通配符所代表的一组类型的概念。由于具体的类型是未知的，很多操作是不允许的。

泛型类最好不要同数组一块使用。你只能创建new List<?>[10]这样的数组，无法创建new List<String>[10]这样的。这限制了数组的使用能力，而且会带来很多费解的问题。因此，当需要类似数组的功能时候，使用集合类即可。

不要忽视编译器给出的警告信息。

1. 泛型概念的提出（为什么需要泛型）？

什么办法可以使集合能够记住集合内元素各类型，且能够达到只要编译时不出现问题，运行时就不会出现“java.lang.ClassCastException”异常呢？答案就是使用泛型。

2. 什么是泛型？

泛型，即“参数化类型”。一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？顾名思义，就是将类型由原来的具体类型进行参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。

我们可以看到，在List接口中采用泛型化定义之后，中的E表示类型形参，可以接收具体的类型实参，并且此接口定义中，凡是出现E的地方均表示相同的接受自外部的类型实参。

3. 自定义泛型接口、泛型类和泛型方法

接口、类和方法也都可以使用泛型去定义，以及相应的使用。是的，在具体使用时，可以分为泛型接口、泛型类和泛型方法。自定义泛型接口、泛型类和泛型方法与上述Java源码中的List、ArrayList类似。如下，我们看一个最简单的泛型类和方法定义：

```java
public class GenericTest {    
    public static void main(String[] args) {        
        Boxname = new Box("corn");        System.out.println("name:" + name.getData());    }}class Box{private T data;

        public Box() {}

        public Box(T data) {this.data = data;}

        public T getData() {return data;}

}
```

在泛型接口、泛型类和泛型方法的定义过程中，我们常见的如T、E、K、V等形式的参数常用于表示泛型形参，由于接收来自外部使用时候传入的类型实参。

那么对于不同传入的类型实参，生成的相应对象实例的类型是不是一样的呢？

```java
public class GenericTest {    
    public static void main(String[] args) {        
        Boxname = new Box("corn");        Boxage = new Box(712);

System.out.println("name class:" + name.getClass());      // com.*.Box

System.out.println("age class:" + age.getClass());        // com.*.Box

System.out.println(name.getClass() == age.getClass());    // true}}
```

由此，我们发现，在使用泛型类时，虽然传入了不同的泛型实参，但并没有真正意义上生成不同的类型，传入不同泛型实参的泛型类在内存上只有一个，即还是原来的最基本的类型（本实例中为Box），当然，在逻辑上我们可以理解成多个不同的泛型类型。

究其原因，在于Java中的泛型这一概念提出的目的，导致其只是作用于代码编译阶段，在编译过程中，对于正确检验泛型结果后，会将泛型的相关信息擦出，也就是说，成功编译过后的class文件中是不包含任何泛型信息的。泛型信息不会进入到运行时阶段。

对此总结成一句话：泛型类型在逻辑上可以看成是多个不同的类型，实际上都是相同的基本类型。

四.类型通配符

接着上面的结论，我们知道，Box和Box实际上都是Box类型，现在需要继续探讨一个问题，那么在逻辑上，类似于Box和Box是否可以看成具有父子关系的泛型类型呢？

为了弄清这个问题，我们继续看下下面这个例子

```java
public class GenericTest {    public static void main(String[] args) {        Boxname = new Box(99);        Boxage = new Box(712);        getData(name);                //The method getData(Box) in the type GenericTest is        //not applicable for the arguments (Box)        getData(age);  // 1    }        public static void getData(Boxdata){System.out.println("data :" + data.getData());}}
```

我们发现，在代码//1处出现了错误提示信息：The method getData(Box) in the t ype GenericTest is not applicable for the arguments (Box)。显然，通过提示信息，我们知道Box在逻辑上不能视为Box的父类。由于在编程过程中的顺序不可控性，导致在必要的时候必须要进行类型判断，且进行强制类型转换。显然，这与泛型的理念矛盾，因此，在逻辑上Box<Number>不能视为Box<Integer>的父类。

在逻辑上可以用来表示同时是Box和Box的父类的一个引用类型，由此，类型通配符应运而生。类型通配符一般是使用 ? 代替具体的类型实参。注意了，此处是类型实参，而不是类型形参！且Box<?>在逻辑上是Box<Integer>、Box<Number>...等所有Box<具体类型实参>的父类。由此，我们依然可以定义泛型方法，来完成此类需求。有时候，我们还可能听到类型通配符上限和类型通配符下限。具体有是怎么样的呢？如果需要定义一个功能类似于getData()的方法，但对类型实参又有进一步的限制：只能是Number类及其子类。此时，需要用到类型通配符上限。

public static void getData(Box<? extends Number> data) {System.out.println("data :" +data.getData());}

类型通配符上限通过形如Box<? extends >形式定义，相对应的，类型通配符下限为Box<? super >形式，其含义与类型通配符上限正好相反。



泛型不是协变的

虽然将集合看作是数组的抽象会有所帮助，但是数组还有一些集合不具备的特殊性质。Java 语言中的数组是协变的（covariant），也就是说，如果Integer扩展了Number（事实也是如此），那么不仅Integer是Number，而且Integer[]也是Number[]，在要求Number[]的地方完全可以传递或者赋予Integer[]。（更正式地说，如果Number是Integer的超类型，那么Number[]也是Integer[]的超类型）。您也许认为这一原理同样适用于泛型类型 ——List<Number>是List<Integer>的超类型，那么可以在需要List<Number>的地方传递List<Integer>。不幸的是，情况并非如此。

不允许这样做有一个很充分的理由：这样做将破坏要提供的类型安全泛型。如果能够将List赋给List。那么下面的代码就允许将非Integer的内容放入List：

List<Integer> li = new ArrayList<Integer>();

List<Number> ln = li; // illegal

ln.add(new Float(3.1415));

因为ln是List，所以向其添加Float似乎是完全合法的。但是如果ln是li的别名，那么这就破坏了蕴含在li定义中的类型安全承诺 —— 它是一个整数列表，这就是泛型类型不能协变的原因。

其他的协变问题

数组能够协变而泛型不能协变的另一个后果是，不能实例化泛型类型的数组（new List<String>[3]是不合法的），除非类型参数是一个未绑定的通配符（new List<?>[3]是合法的）。让我们看看如果允许声明泛型类型数组会造成什么后果：

List<String>[] lsa = new List<String>[10]; // illegal  数组能够协变，泛型不能

List<?>[] lsa = new List<?>[10]; // legal   泛型不能协变 ？不确定具体的类型

Object[] oa = lsa;  // OK because List is a subtype of Object

List<Integer> li = new ArrayList<Integer>();

li.add(new Integer(3));

oa[0] = li;

String s = lsa[0].get(0);

最后一行将抛出ClassCastException，因为这样将把List填入本应是List的位置。因为数组协变会破坏泛型的类型安全，所以不允许实例化泛型类型的数组（除非类型参数是未绑定的通配符，比如List）。


--- 
2022/03/10

# 简介
泛型（`Generic type` 或者 `generics`）是对 Java 语言的类型系统的一种扩展，以支持创建可以按类型进行参数化的类。可以把类型参数看作是使用参数化类型时指定的类型的一个占位符，就像方法的形式参数是运行时传递的值的占位符一样。

在集合框架（Collection framework）中泛型的身影随处可见。例如，Map 类允许向一个 Map 类型的实例添加任意类的对象，即使最常见的情况在给定映射（map）中保存一个string键值对。

### 命名类型参数

对于常见的泛型模式，推荐的泛型类型变量：

- E：元素（Element），多用于java集合框架
- K：关键字（Key）
- N：数字（Number）
- T：类型（Type）
- V：值（Value）

Java的泛型是伪泛型，这是因为Java在编译期间，所有的泛型信息都会被擦除，正确理解泛型概念的首要前提是理解类型擦除。Java 泛型是如何工作的？什么是类型擦除？答：泛型是通过类型擦除来实现的，编译器在编译时擦除了所有泛型类型相关的信息，所以在运行时不存在任何泛型类型相关的信息，譬如 `List<Integer>` 在运行时仅用一个 `List` 来表示，这样做的动机是兼容 Java 1.5 之前版本。

泛型擦除具体来说就是在编译成字节码时首先进行类型检查，然后进行类型擦除（即所有类型参数都用他们的限定类型替换，包括类、变量和方法），最后如果类型擦除和多态性发生冲突，就在子类中使用桥接方法解决；如果调用泛型方法的返回类型被擦除，则在调用该方法时插入强制类型转换。在类型擦除中，编译器确保不会创建额外的类，并且没有运行时开销。

### 类型擦除原则

- 用通用类型的类型参数替换其绑定的有界类型参数；
- 如果使用无界类型参数，则使用Object替换类型参数；
- 插入类型转换以实现类型安全；
- 生成桥接方法以在扩展通用类型中保持多态。

> `<T> T` 和T的区别：T是Type的首字母缩写；`<T> T` 表示“返回值”是一个泛型，传入什么类型，就返回什么类型；而单独的“T”表示限制传入的参数类型。

### `<T> T` 的用法

这个`<T> T` 表示返回值T的类型是泛型，T是一个占位符，用来告诉编译器，这个东西是先给我留着， 等我编译的时候再告诉你是什么类型。

```java
import org.springframework.util.CollectionUtils;
import java.util.ArrayList;
import java.util.List;
public class Demo {
  public static void main(String[] args) {
    Demo demo = new Demo();
    //获取string类型
    List<String> array = new ArrayList<String>();
    array.add("test");
    array.add("doub");
    String str = demo.getListFisrt(array);
    System.out.println(str);
    //获取Integer类型
    List<Integer> nums = new ArrayList<Integer>();
    nums.add(31);
    nums.add(32);
    Integer num = demo.getListFisrt(nums);
    System.out.println(num);
  }

  /**
   * 这个<T> T 可以传入任何类型的List
   * 关于参数T
   * 第一个 表示是泛型
   * 第二个 表示返回的是T类型的数据
   * 第三个 限制参数类型为T
   *
   * @param data
   * @return
   */
  private <T> T getListFisrt(List<T> data) {
    if (CollectionUtils.isEmpty(data)) {
      return null;
    }
    return data.get(0);
  }
}
```

### T 的用法

单独的T表示限制参数的类型。这种用法一般多用于共同操作一个类对象，然后获取里面的集合信息。

```java
import java.util.ArrayList;
import java.util.List;

public class Demo2<T> {

  public static void main(String[] args) {
    //限制T 为String 类型
    Demo2<String> demo = new Demo2<String>();
    List<String> array = new ArrayList<String>();
    array.add("Tom");
    array.add("河南");
    String str = demo.getListFisrt(array);
    System.out.println(str);

    //获取Integer类型
    Demo2<Integer> demo2 = new Demo2<Integer>();
    List<Integer> nums = new ArrayList<Integer>();
    nums.add(12);
    nums.add(13);
    Integer num = demo2.getListFisrt(nums);
    System.out.println(num);
  }

  /**
   * 这个只能传递T类型的数据
   * 返回值 就是Demo<T> 实例化传递的对象类型
   *
   * @param data
   * @return
   */
  private T getListFisrt(List<T> data) {
    if (data == null || data.size() == 0) {
      return null;
    }
    return data.get(0);
  }
}
```