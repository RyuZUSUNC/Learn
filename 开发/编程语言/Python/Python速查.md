# 头文件

```py
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

# 函数参数
- def calc(*numbers):
  - 可变参数:传入参数数量任意
- def person(name, age, **kw):
  - 关键字参数:例person('Bob', 35, city='Beijing')
- def person(name, age, *, city, job):
  - 命名关键字参数:例person('Jack', 24, city='Beijing', job='Engineer')

# 字符处理
## 字符串运算符
>下表实例变量 a 值为字符串 "Hello"，b 变量值为 "Python"：

- `+` 字符串连接

        a + b 输出结果： HelloPython

- `*` 重复输出字符串

        a*2 输出结果：HelloHello

- `[]` 通过索引获取字符串中字符  

        a[1] 输出结果 e

- `[ : ]` 截取字符串中的一部分，遵循左闭右开原则，str[0:2] 是不包含第 3 个字符的。

        a[1:4] 输出结果 ell

- `in` 成员运算符 - 如果字符串中包含给定的字符返回 True

        'H' in a 输出结果 True

- `not in` 成员运算符 - 如果字符串中不包含给定的字符返回 True

        'M' not in a 输出结果 True

- `r/R` 原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 r（可以大小写）以外，与普通字符串有着几乎完全相同的语法。

        print( r'\n' )
        print( R'\n' )

- `%` 格式字符串

示例:
```py
#!/usr/bin/python3
 
a = "Hello"
b = "Python"
 
print("a + b 输出结果：", a + b)
print("a * 2 输出结果：", a * 2)
print("a[1] 输出结果：", a[1])
print("a[1:4] 输出结果：", a[1:4])
 
if( "H" in a) :
    print("H 在变量 a 中")
else :
    print("H 不在变量 a 中")
 
if( "M" not in a) :
    print("M 不在变量 a 中")
else :
    print("M 在变量 a 中")
 
print (r'\n')
print (R'\n')

-----------
a + b 输出结果： HelloPython
a * 2 输出结果： HelloHello
a[1] 输出结果： e
a[1:4] 输出结果： ell
H 在变量 a 中
M 不在变量 a 中
\n
\n
```

## 字符串格式化
Python 支持格式化字符串的输出 。尽管这样可能会用到非常复杂的表达式，但最基本的用法是将一个值插入到一个有字符串格式符 %s 的字符串中。

在 Python 中，字符串格式化使用与 C 中 sprintf 函数一样的语法。

python字符串格式化符号:

- `%c`	 格式化字符及其ASCII码
- `%s`	 格式化字符串
- `%d`	 格式化整数
- `%u`	 格式化无符号整型
- `%o`	 格式化无符号八进制数
- `%x`	 格式化无符号十六进制数
- `%X`	 格式化无符号十六进制数（大写）
- `%f`	 格式化浮点数字，可指定小数点后的精度
- `%e`	 用科学计数法格式化浮点数
- `%E`	 作用同%e，用科学计数法格式化浮点数
- `%g`	 %f和%e的简写
- `%G`	 %f 和 %E 的简写
- `%p`	 用十六进制数格式化变量的地址

格式化操作符辅助指令:

- `*`	     定义宽度或者小数点精度
- `-`	     用做左对齐
- `+`	     在正数前面显示加号( + )
- `<sp>`	 在正数前面显示空格
- `#`	     在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X')
- `0`	     显示的数字前面填充'0'而不是默认的空格
- `%`	     '%%'输出一个单一的'%'
- `(var)`	 映射变量(字典参数)
- `m.n.`	 m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)

## 三引号
python三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。

例子:
```py
#!/usr/bin/python3
 
para_str = """这是一个多行字符串的实例
多行字符串可以使用制表符
TAB ( \t )。
也可以使用换行符 [ \n ]。
"""
print (para_str)

----------
这是一个多行字符串的实例
多行字符串可以使用制表符
TAB (    )。
也可以使用换行符 [ 
 ]。
```

所见即所得，无需转义字符。

### f-string
f-string 是 python3.6 之后版本添加的，称之为字面量格式化字符串，是新的格式化字符串的语法。

f-string 格式化字符串以 f 开头，后面跟着字符串，字符串中的表达式用大括号 {} 包起来，它会将变量或表达式计算后的值替换进去，实例如下：

```py
>>> name = 'Runoob'
>>> f'Hello {name}'  # 替换变量

>>> f'{1+2}'         # 使用表达式
'3'

>>> w = {'name': 'Runoob', 'url': 'www.runoob.com'}
>>> f'{w["name"]}: {w["url"]}'
'Runoob: www.runoob.com'
```

用了这种方式明显更简单了，不用再去判断使用 %s，还是 %d。

在 Python 3.8 的版本中可以使用 `=` 符号来拼接运算表达式与结果：

```py
>>> x = 1
>>> print(f'{x+1}')   # Python 3.6
2

>>> x = 1
>>> print(f'{x+1=}')   # Python 3.8
'x+1=2'
```

## 字符串内建函数

- `capitalize()` 将字符串的第一个字符转换为大写

- `center(width, fillchar)` 返回一个指定的宽度 width 居中的字符串，fillchar 为填充的字符，默认为空格。

```py
'hello'.center(12, '1')
------
111hello1111
```

- `count(str, beg= 0,end=len(string))` 返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数

- `bytes.decode(encoding="utf-8", errors="strict")` Python3 中没有 decode 方法，但我们可以使用 bytes 对象的 decode() 方法来解码给定的 bytes 对象，这个 bytes 对象可以由 str.encode() 来编码返回。

- `encode(encoding='UTF-8',errors='strict')` 以 encoding 指定的编码格式编码字符串，如果出错默认报一个ValueError 的异常，除非 errors 指定的是'ignore'或者'replace'

- `endswith(suffix, beg=0, end=len(string))` 检查字符串是否以 obj 结束，如果beg 或者 end 指定则检查指定的范围内是否以 obj 结束，如果是，返回 True,否则返回 False.

```py
a = 'sblsq'
print(a.endswith('q'))
print(a.endswith('x'))
------
True
False
```

- `expandtabs(tabsize=8)` 把字符串 string 中的 tab 符号转为空格，tab 符号默认的空格数是 8 。

- `find(str, beg=0, end=len(string))` 检测 str 是否包含在字符串中，如果指定范围 beg 和 end ，则检查是否包含在指定范围内，如果包含返回开始的索引值，否则返回-1

- `index(str, beg=0, end=len(string))` 跟find()方法一样，只不过如果str不在字符串中会报一个异常。

- `join(seq)` 以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串

- `len(string)` 返回字符串长度

- `ljust(width[, fillchar])` 返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格

- `lower()` 转换字符串中所有大写字符为小写

- `upper()` 转换字符串中的小写字母为大写

- `lstrip()` 截掉字符串左边的空格或指定字符

- `maketrans()` 创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。

- `max(str)` 返回字符串 str 中最大的字母。

- `min(str)` 返回字符串 str 中最小的字母。

- `replace(old, new [, max])` 将字符串中的 old 替换成 new,如果 max 指定，则替换不超过 max 次。

- `rfind(str, beg=0,end=len(string))` 类似于 find()函数，不过是从右边开始查找.

- `rindex( str, beg=0, end=len(string))` 类似于 index()，不过是从右边开始.

- `rjust(width,[, fillchar])` 返回一个原字符串右对齐,并使用fillchar(默认空格）填充至长度 width 的新字符串

- `rstrip()` 删除字符串字符串末尾的空格.

- `split(str="", num=string.count(str))` 以 str 为分隔符截取字符串，如果 num 有指定值，则仅截取 num+1 个子字符串

- `splitlines([keepends])` 按照行('\r', '\r\n', \n')分隔，返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如果为 True，则保留换行符。

- `startswith(substr, beg=0,end=len(string))` 检查字符串是否是以指定子字符串 substr 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查。

- `strip([chars])` 在字符串上执行 lstrip()和 rstrip()

- `swapcase()` 将字符串中大写转换为小写，小写转换为大写

- `title()` 返回"标题化"的字符串,就是说所有单词都是以大写开始，其余字母均为小写(见 istitle())

- `translate(table, deletechars="")` 根据 str 给出的表(包含 256 个字符)转换 string 的字符, 要过滤掉的字符放到 deletechars 参数中

- `zfill (width)` 返回长度为 width 的字符串，原字符串右对齐，前面填充0

- `isdecimal()`检查字符串是否只包含十进制字符，如果是返回 true，否则返回 false。

- `isalnum()` 如果字符串至少有一个字符并且所有字符都是字母或数字则返 回 True，否则返回 False

- `isalpha()` 如果字符串至少有一个字符并且所有字符都是字母或中文字则返回 True, 否则返回 False

- `isdigit()` 如果字符串只包含数字则返回 True 否则返回 False..

- `islower()` 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False

- `isnumeric()` 如果字符串中只包含数字字符，则返回 True，否则返回 False

- `isspace()` 如果字符串中只包含空白，则返回 True，否则返回 False.

- `istitle()` 如果字符串是标题化的(见 title())则返回 True，否则返回 False

- `isupper()` 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False

# 日期格式化

```py
#!/usr/bin/python3

import time

# 格式化成2016-03-20 11:45:39形式
print (time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))

# 格式化成Sat Mar 28 22:24:24 2016形式
print (time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()))
 
# 将格式字符串转换为时间戳
a = "Sat Mar 28 22:24:24 2016"
print (time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y")))
```

- %y 两位数的年份表示（00-99）
- %Y 四位数的年份表示（000-9999）
- %m 月份（01-12）
- %d 月内中的一天（0-31）
- %H 24小时制小时数（0-23）
- %I 12小时制小时数（01-12）
- %M 分钟数（00=59）
- %S 秒（00-59）
- %a 本地简化星期名称
- %A 本地完整星期名称
- %b 本地简化的月份名称
- %B 本地完整的月份名称
- %c 本地相应的日期表示和时间表示
- %j 年内的一天（001-366）
- %p 本地A.M.或P.M.的等价符
- %U 一年中的星期数（00-53）星期天为星期的开始
- %w 星期（0-6），星期天为星期的开始
- %W 一年中的星期数（00-53）星期一为星期的开始
- %x 本地相应的日期表示
- %X 本地相应的时间表示
- %Z 当前时区的名称
- %% %号本身