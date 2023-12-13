# C# 字符串（String）
在 C# 中，您可以使用字符数组来表示字符串，但是，更常见的做法是使用 string 关键字来声明一个字符串变量。string 关键字是 System.String 类的别名。

# 创建 String 对象
可以使用以下方法之一来创建 string 对象：

- 通过给 String 变量指定一个字符串
- 通过使用 String 类构造函数
- 通过使用字符串串联运算符（ + ）
- 通过检索属性或调用一个返回字符串的方法
- 通过格式化方法来转换一个值或对象为它的字符串表示形式

```C#
using System;

namespace StringApplication
{
    class Program
    {
        static void Main(string[] args)
        {
           //字符串，字符串连接
            string fname, lname;
            fname = "Rowan";
            lname = "Atkinson";

            string fullname = fname + lname;
            Console.WriteLine("Full Name: {0}", fullname);

            //通过使用 string 构造函数
            char[] letters = { 'H', 'e', 'l', 'l','o' };
            string greetings = new string(letters);
            Console.WriteLine("Greetings: {0}", greetings);

            //方法返回字符串
            string[] sarray = { "Hello", "From", "Tutorials", "Point" };
            string message = String.Join(" ", sarray);
            Console.WriteLine("Message: {0}", message);

            //用于转化值的格式化方法
            DateTime waiting = new DateTime(2012, 10, 10, 17, 58, 1);
            string chat = String.Format("Message sent at {0:t} on {0:D}", 
            waiting);
            Console.WriteLine("Message: {0}", chat);
            Console.ReadKey() ;
        }
    }
}
```

# String 类的方法
public static int Compare( string strA, string strB )
比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。该方法区分大小写。
## public static int Compare( string strA, string strB, bool ignoreCase )
  - 比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。但是，如果布尔参数为真时，该方法不区分大小写。

## public static string Concat( string str0, string str1 )
  - 连接两个 string 对象。

## public static string Concat( string str0, string str1, string str2 )
  - 连接三个 string 对象。

## public static string Concat( string str0, string str1, string str2, string str3 )
  - 连接四个 string 对象。
  
## public bool Contains( string value )
  - 返回一个表示指定 string 对象是否出现在字符串中的值。

## public static string Copy( string str )
  - 创建一个与指定字符串具有相同值的新的 String 对象。

## public void CopyTo( int sourceIndex, char[] destination, int destinationIndex, int count )
  - 从 string 对象的指定位置开始复制指定数量的字符到 Unicode 字符数组中的指定位置。

## public bool EndsWith( string value )
  - 判断 string 对象的结尾是否匹配指定的字符串。

## public bool Equals( string value )
  - 判断当前的 string 对象是否与指定的 string 对象具有相同的值。

## public static bool Equals( string a, string b )
  - 判断两个指定的 string 对象是否具有相同的值。

## public static string Format( string format, Object arg0 )
  - 把指定字符串中一个或多个格式项替换为指定对象的字符串表示形式。

## public int IndexOf( char value )
  - 返回指定 Unicode 字符在当前字符串中第一次出现的索引，索引从 0 开始。

## public int IndexOf( string value )
  - 返回指定字符串在该实例中第一次出现的索引，索引从 0 开始。

## public int IndexOf( char value, int startIndex )
  - 返回指定 Unicode 字符从该字符串中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。

## public int IndexOf( string value, int startIndex )
  - 返回指定字符串从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。

## public int IndexOfAny( char[] anyOf )
  - 返回某一个指定的 Unicode 字符数组中任意字符在该实例中第一次出现的索引，索引从 0 开始。

## public int IndexOfAny( char[] anyOf, int startIndex )
  - 返回某一个指定的 Unicode 字符数组中任意字符从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。

## public string Insert( int startIndex, string value )
  - 返回一个新的字符串，其中，指定的字符串被插入在当前 string 对象的指定索引位置。

## public static bool IsNullOrEmpty( string value )
  - 指示指定的字符串是否为 null 或者是否为一个空的字符串。

## public static string Join( string separator, params string[] value )
  - 连接一个字符串数组中的所有元素，使用指定的分隔符分隔每个元素。

## public static string Join( string separator, string[] value, int startIndex, int count )
  - 链接一个字符串数组中的指定元素，使用指定的分隔符分隔每个元素。

## public int LastIndexOf( char value )
  - 返回指定 Unicode 字符在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。

## public int LastIndexOf( string value )
  - 返回指定字符串在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。

## public string Remove( int startIndex )
  - 移除当前实例中的所有字符，从指定位置开始，一直到最后一个位置为止，并返回字符串。

## public string Remove( int startIndex, int count )
  - 从当前字符串的指定位置开始移除指定数量的字符，并返回字符串。

## public string Replace( char oldChar, char newChar )
  - 把当前 string 对象中，所有指定的 Unicode 字符替换为另一个指定的 Unicode 字符，并返回新的字符串。

## public string Replace( string oldValue, string newValue )
  - 把当前 string 对象中，所有指定的字符串替换为另一个指定的字符串，并返回新的字符串。

## public string[] Split( params char[] separator )
  - 返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。

## public string[] Split( char[] separator, int count )
  - 返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。int 参数指定要返回的子字符串的最大数目。

## public bool StartsWith( string value )
  - 判断字符串实例的开头是否匹配指定的字符串。

## public char[] ToCharArray()
  - 返回一个带有当前 string 对象中所有字符的 Unicode 字符数组。

## public char[] ToCharArray( int startIndex, int length )
  - 返回一个带有当前 string 对象中所有字符的 Unicode 字符数组，从指定的索引开始，直到指定的长度为止。

## public string ToLower()
  - 把字符串转换为小写并返回。

## public string ToUpper()
  - 把字符串转换为大写并返回。

## public string Trim()
  - 移除当前 String 对象中的所有前导空白字符和后置空白字符。