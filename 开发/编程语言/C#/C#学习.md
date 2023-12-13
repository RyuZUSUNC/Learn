# 变量
## 接受来自用户的值
`System`命名空间中的`Console`类提供了一个函数`ReadLine()`，用于接收来自用户的输入，并把它存储到一个变量中。

例如：

```C#
int num;
num = Convert.ToInt32(Console.ReadLine());
```

函数 Convert.ToInt32() 把用户输入的数据转换为 int 数据类型，因为 Console.ReadLine() 只接受字符串格式的数据。

# 常量
## 定义常量
常量是使用 const 关键字来定义的 。定义一个常量的语法如下：

```C#
const <data_type> <constant_name> = value;
```

