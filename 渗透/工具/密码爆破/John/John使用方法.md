>https://github.com/openwall/john
## 主要命令

john [-参数] [密码文件]

## 参数详解
### -single

使用简单模式(Single Crack)破解加密，主要是根据使用者的用户名产生变化来猜测解密，变化规则记录在JOHN.INI 文件的 [List.Rules:Single] 内。

示例：
```
john -single passwd
```

### -wordfile:[字典文件] -stdin

使用字典破解加密，可以加上 -stdin ，表示由键盘输入单字来破解

示例：
```
john -wordfile:bigdict.dic passwd
```

### -rules

在字典模式下，开启字词规则变化功能，如从字典读入cook，程序可能自动尝试cook、c00k、cooker等其他字词，变化规则记录在JOHN.INI 文件的 [List.Rules:Wordlist] 内。

示例：
```
john -wordfile:bigdict.dic -rules passwd
```

### -incremental:[模式名称]（也可简写成-i:[模式名称]）

使用强化破解模式，穷举法。在JOHN.INI 文件的[Incremental:*****] 区域中定义了许多可以指定的模式名称。

示例：
```
john -i:all passwd
```

### -external:[模块名称]

使用外置模块破解模式，用户可以自己编写额外的模块用来破解，破解模组模式记录在JOHN.INI 文件的[List.External:******]区域中

示例：
```
john -external:double passwd
```

### -stdout

显示john所产生的字符到屏幕上。

示例：
```
john –i:all –stdout
```

### -restore:[存档名]

继续上次中断的解密。John在执行时可以按下 CTRL+C 中断，此时解密进度会被存档在一个名为 restore 的文件内，使用 -restore 可以从文件内读取上一次中断的位置，继续破解。

示例：
```
john –restore
```

### -session:[存档名]

设置本次任务的存档名称

示例：
```
john –wordfile:bigdict.dic –session:work1 passwd
```

### -status:[存档名]

显示存档中的状态

示例：
```
john –status:restore
```

### -makechars:[存档名]

根据目前以破解出的密码为基础生成字频统计表。

示例:
```
john –makechars:ownchars
```

### -show

显示目前已经破解出的密码，因为JOHN.POT文件内并不存储用户名，所以使用时需要同时输入对应的密码档。

示例：
```
john –show passwd
```

### -test

测试机能

示例：
```
john –test
```

