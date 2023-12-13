>https://github.com/hashcat/hashcat
>https://xz.aliyun.com/t/4008
# 简介

Hashcat是自称世界上最快的密码恢复工具。它在2015年之前拥有专有代码库，但现在作为免费软件发布。适用于Linux，OS X和Windows的版本可以使用基于CPU或基于GPU的变体。支持hashcat的散列算法有Microsoft LM哈希，MD4，MD5，SHA系列，Unix加密格式，MySQL和Cisco PIX等。

hashcat支持多种计算核心：

- GPU
- CPU
- APU
- DSP
- FPGA
- Coprocessor

GPU的驱动要求

- AMD GPUs on Linux require "RadeonOpenCompute (ROCm)" Software Platform (1.6.180 or later)
- AMD GPUs on Windows require "AMD Radeon Software Crimson Edition" (15.12 or later)
- Intel CPUs require "OpenCL Runtime for Intel Core and Intel Xeon Processors" (16.1.1 or later)
- Intel GPUs on Linux require "OpenCL 2.0 GPU Driver Package for Linux" (2.0 or later)
- Intel GPUs on Windows require "OpenCL Driver for Intel Iris and Intel HD Graphics"
- NVIDIA GPUs require "NVIDIA Driver" (367.x or later)

GitHub地址：https://github.com/hashcat/hashcat

# 参数

下面使常见的参数，想了解更多的参数可以 hashcat --help 查看

```
-a                  指定要使用的破解模式，其值参考后面对参数。“-a 0”字典攻击，“-a 1” 组合攻击；“-a 3”掩码攻击。
-m                  指定要破解的hash类型，如果不指定类型，则默认是MD5
-o                  指定破解成功后的hash及所对应的明文密码的存放位置,可以用它把破解成功的hash写到指定的文件中
--force             忽略破解过程中的警告信息,跑单条hash可能需要加上此选项
--show              显示已经破解的hash及该hash所对应的明文
--increment         启用增量破解模式,你可以利用此模式让hashcat在指定的密码长度范围内执行破解过程
--increment-min     密码最小长度,后面直接等于一个整数即可,配置increment模式一起使用
--increment-max     密码最大长度,同上
--outfile-format    指定破解结果的输出格式id,默认是3
--username          忽略hash文件中的指定的用户名,在破解linux系统用户密码hash可能会用到
--restore           从cheeckpoint点继续爆破
--remove            删除已被破解成功的hash
-r                  使用自定义破解规则
```

## 攻击模式：

```
# | Mode
 ===+======
  0 | Straight（字段破解）
  1 | Combination（组合破解）
  3 | Brute-force（掩码暴力破解）
  6 | Hybrid Wordlist + Mask（字典+掩码破解）
  7 | Hybrid Mask + Wordlist（掩码+字典破解）
```

## 输出格式

```
1 = hash[:salt]
2 = plain
3 = hash[:salt]:plain
4 = hex_plain
5 = hash[:salt]:hex_plain
6 = plain:hex_plain
7 = hash[:salt]:plain:hex_plain
8 = crackpos
9 = hash[:salt]:crackpos
10 = plain:crackpos
11 = hash[:salt]:plain:crackpos
12 = hex_plain:crackpos
13 = hash[:salt]:hex_plain:crackpos
14 = plain:hex_plain:crackpos
15 = hash[:salt]:plain:hex_plain:crackpos
```

## Hash id对照表(部分)
hashcat --help查看hash对照表

```
- [ Hash modes ] -

      # | Name                                             | Category
  ======+==================================================+======================================
    900 | MD4                                              | Raw Hash
      0 | MD5                                              | Raw Hash
   5100 | Half MD5                                         | Raw Hash
    100 | SHA1                                             | Raw Hash
   1300 | SHA2-224                                         | Raw Hash
   1400 | SHA2-256                                         | Raw Hash
  10800 | SHA2-384                                         | Raw Hash
   1700 | SHA2-512                                         | Raw Hash
  17300 | SHA3-224                                         | Raw Hash
  17400 | SHA3-256                                         | Raw Hash
  17500 | SHA3-384                                         | Raw Hash
  17600 | SHA3-512                                         | Raw Hash
     10 | md5($pass.$salt)                                 | Raw Hash, Salted and/or Iterated
     20 | md5($salt.$pass)                                 | Raw Hash, Salted and/or Iterated
     30 | md5(utf16le($pass).$salt)                        | Raw Hash, Salted and/or Iterated
     40 | md5($salt.utf16le($pass))                        | Raw Hash, Salted and/or Iterated
   3800 | md5($salt.$pass.$salt)                           | Raw Hash, Salted and/or Iterated
   3710 | md5($salt.md5($pass))                            | Raw Hash, Salted and/or Iterated
   4010 | md5($salt.md5($salt.$pass))                      | Raw Hash, Salted and/or Iterated
   4110 | md5($salt.md5($pass.$salt))                      | Raw Hash, Salted and/or Iterated
   2600 | md5(md5($pass))                                  | Raw Hash, Salted and/or Iterated
   3910 | md5(md5($pass).md5($salt))                       | Raw Hash, Salted and/or Iterated
   4300 | md5(strtoupper(md5($pass)))                      | Raw Hash, Salted and/or Iterated
   4400 | md5(sha1($pass))                                 | Raw Hash, Salted and/or Iterated
    110 | sha1($pass.$salt)                                | Raw Hash, Salted and/or Iterated
    120 | sha1($salt.$pass)                                | Raw Hash, Salted and/or Iterated
    130 | sha1(utf16le($pass).$salt)                       | Raw Hash, Salted and/or Iterated
    140 | sha1($salt.utf16le($pass))                       | Raw Hash, Salted and/or Iterated
   4500 | sha1(sha1($pass))                                | Raw Hash, Salted and/or Iterated
   4520 | sha1($salt.sha1($pass))                          | Raw Hash, Salted and/or Iterated
   4700 | sha1(md5($pass))                                 | Raw Hash, Salted and/or Iterated
   4900 | sha1($salt.$pass.$salt)                          | Raw Hash, Salted and/or Iterated
  14400 | sha1(CX)                                         | Raw Hash, Salted and/or Iterated
   1410 | sha256($pass.$salt)                              | Raw Hash, Salted and/or Iterated
   1420 | sha256($salt.$pass)                              | Raw Hash, Salted and/or Iterated
   1430 | sha256(utf16le($pass).$salt)                     | Raw Hash, Salted and/or Iterated
   1440 | sha256($salt.utf16le($pass))                     | Raw Hash, Salted and/or Iterated
   1710 | sha512($pass.$salt)                              | Raw Hash, Salted and/or Iterated
   1720 | sha512($salt.$pass)                              | Raw Hash, Salted and/or Iterated
   1730 | sha512(utf16le($pass).$salt)                     | Raw Hash, Salted and/or Iterated
   1740 | sha512($salt.utf16le($pass))                     | Raw Hash, Salted and/or Iterated
  14000 | DES (PT = $salt, key = $pass)                    | Raw Cipher, Known-Plaintext attack
  14100 | 3DES (PT = $salt, key = $pass)                   | Raw Cipher, Known-Plaintext attack
  14900 | Skip32 (PT = $salt, key = $pass)                 | Raw Cipher, Known-Plaintext attack
  15400 | ChaCha20                                         | Raw Cipher, Known-Plaintext attack
   2500 | WPA-EAPOL-PBKDF2                                 | Network Protocols
   2501 | WPA-EAPOL-PMK                                    | Network Protocols
  16800 | WPA-PMKID-PBKDF2                                 | Network Protocols
  16801 | WPA-PMKID-PMK                                    | Network Protocols
   7300 | IPMI2 RAKP HMAC-SHA1                             | Network Protocols
   7500 | Kerberos 5 AS-REQ Pre-Auth etype 23              | Network Protocols
   8300 | DNSSEC (NSEC3)                                   | Network Protocols
  10200 | CRAM-MD5                                         | Network Protocols
  11100 | PostgreSQL CRAM (MD5)                            | Network Protocols
  11200 | MySQL CRAM (SHA1)                                | Network Protocols
  16100 | TACACS+                                          | Network Protocols
  16500 | JWT (JSON Web Token)                             | Network Protocols
    121 | SMF (Simple Machines Forum) > v1.1               | Forums, CMS, E-Commerce, Frameworks
    400 | phpBB3 (MD5)                                     | Forums, CMS, E-Commerce, Frameworks
   2811 | MyBB 1.2+                                        | Forums, CMS, E-Commerce, Frameworks
   2811 | IPB2+ (Invision Power Board)                     | Forums, CMS, E-Commerce, Frameworks
   8400 | WBB3 (Woltlab Burning Board)                     | Forums, CMS, E-Commerce, Frameworks
     11 | Joomla < 2.5.18                                  | Forums, CMS, E-Commerce, Frameworks
    400 | Joomla >= 2.5.18 (MD5)                           | Forums, CMS, E-Commerce, Frameworks
    400 | WordPress (MD5)                                  | Forums, CMS, E-Commerce, Frameworks
   2612 | PHPS                                             | Forums, CMS, E-Commerce, Frameworks
   7900 | Drupal7                                          | Forums, CMS, E-Commerce, Frameworks
     21 | osCommerce                                       | Forums, CMS, E-Commerce, Frameworks
     21 | xt:Commerce                                      | Forums, CMS, E-Commerce, Frameworks
  11000 | PrestaShop                                       | Forums, CMS, E-Commerce, Frameworks
    124 | Django (SHA-1)                                   | Forums, CMS, E-Commerce, Frameworks
  10000 | Django (PBKDF2-SHA256)                           | Forums, CMS, E-Commerce, Frameworks
     12 | PostgreSQL                                       | Database Server
    131 | MSSQL (2000)                                     | Database Server
    132 | MSSQL (2005)                                     | Database Server
   1731 | MSSQL (2012, 2014)                               | Database Server
    200 | MySQL323                                         | Database Server
    300 | MySQL4.1/MySQL5                                  | Database Server
   3100 | Oracle H: Type (Oracle 7+)                       | Database Server
    112 | Oracle S: Type (Oracle 11+)                      | Database Server
  12300 | Oracle T: Type (Oracle 12+)                      | Database Server
   8000 | Sybase ASE                                       | Database Server
  15000 | FileZilla Server >= 0.9.55                       | FTP Server
  11500 | CRC32                                            | Checksums
   3000 | LM                                               | Operating Systems
   1000 | NTLM                                             | Operating Systems
    500 | md5crypt, MD5 (Unix), Cisco-IOS $1$ (MD5)        | Operating Systems
   3200 | bcrypt $2*$, Blowfish (Unix)                     | Operating Systems
   7400 | sha256crypt $5$, SHA256 (Unix)                   | Operating Systems
   1800 | sha512crypt $6$, SHA512 (Unix)                   | Operating Systems
    122 | macOS v10.4, MacOS v10.5, MacOS v10.6            | Operating Systems
   1722 | macOS v10.7                                      | Operating Systems
   7100 | macOS v10.8+ (PBKDF2-SHA512)                     | Operating Systems
  11600 | 7-Zip                                            | Archives
  12500 | RAR3-hp                                          | Archives
  13000 | RAR5                                             | Archives
  13600 | WinZip                                           | Archives
   9700 | MS Office <= 2003 $0/$1, MD5 + RC4               | Documents
   9710 | MS Office <= 2003 $0/$1, MD5 + RC4, collider #1  | Documents
   9720 | MS Office <= 2003 $0/$1, MD5 + RC4, collider #2  | Documents
   9800 | MS Office <= 2003 $3/$4, SHA1 + RC4              | Documents
   9810 | MS Office <= 2003 $3, SHA1 + RC4, collider #1    | Documents
   9820 | MS Office <= 2003 $3, SHA1 + RC4, collider #2    | Documents
   9400 | MS Office 2007                                   | Documents
   9500 | MS Office 2010                                   | Documents
   9600 | MS Office 2013                                   | Documents
  10400 | PDF 1.1 - 1.3 (Acrobat 2 - 4)                    | Documents
  10410 | PDF 1.1 - 1.3 (Acrobat 2 - 4), collider #1       | Documents
  10420 | PDF 1.1 - 1.3 (Acrobat 2 - 4), collider #2       | Documents
  10500 | PDF 1.4 - 1.6 (Acrobat 5 - 8)                    | Documents
  10600 | PDF 1.7 Level 3 (Acrobat 9)                      | Documents
  10700 | PDF 1.7 Level 8 (Acrobat 10 - 11)                | Documents
  99999 | Plaintext                                        | Plaintext
```

## 掩码设置
常见的掩码字符集

```
l | abcdefghijklmnopqrstuvwxyz          纯小写字母
u | ABCDEFGHIJKLMNOPQRSTUVWXYZ          纯大写字母
d | 0123456789                  纯数字
h | 0123456789abcdef                常见小写子目录和数字
H | 0123456789ABCDEF                常见大写字母和数字
s |  !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~       特殊字符
a | ?l?u?d?s                    键盘上所有可见的字符
b | 0x00 - 0xff                 可能是用来匹配像空格这种密码的
```

下面举几个简单的例子来了解一下掩码的设置

```
八位数字密码：?d?d?d?d?d?d?d?d
八位未知密码：?a?a?a?a?a?a?a?a
前四位为大写字母，后面四位为数字：?u?u?u?u?d?d?d?d
前四位为数字或者是小写字母，后四位为大写字母或者数字：?h?h?h?h?H?H?H?H
前三个字符未知，中间为admin，后三位未知：?a?a?aadmin?a?a?a
6-8位数字密码：--increment --increment-min 6 --increment-max 8 ?l?l?l?l?l?l?l?l
6-8位数字+小写字母密码：--increment --increment-min 6 --increment-max 8 ?h?h?h?h?h?h?h?h
```

如果我们想设置字符集为：abcd123456!@-+，那该怎么做呢。这就需要用到自定义字符集这个参数了，hashcat支持用户最多定义4组字符集

```
--custom-charset1 [chars]等价于 -1
--custom-charset2 [chars]等价于 -2
--custom-charset3 [chars]等价于 -3
--custom-charset4 [chars]等价于 -4
在掩码中用?1、?2、?3、?4来表示。
```

再来举几个例子：

```
--custom-charset1 abcd123456!@-+。然后我们就可以用"?1"去表示这个字符集了
--custom-charset1 abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789
--custom-charset2 ?l?d，这里和?2就等价于?h
-1 ?d?l?u，?1就表示数字+小写字母+大写字母
-3 abcdef -4 123456 那么?3?3?3?3?4?4?4?4就表示为前四位可能是“abcdef”，后四位可能是“123456”
```

## 例子

### 7位数字破解

```
hashcat64.exe -a 3 -m 0 --force 25c3e88f81b4853f2a8faacad4c871b6 ?d?d?d?d?d?d?d
```

### 7位小写字母破解

```
hashcat64.exe -a 3 -m 0 --force 7a47c6db227df60a6d67245d7d8063f3 ?l?l?l?l?l?l?l
```

### 1-8位数字破解

```
hashcat64.exe -a 3 -m 0 --force 4488cec2aea535179e085367d8a17d75 --increment --increment-min 1 --increment-max 8 ?d?d?d?d?d?d?d?d
```

### 1-8位小写字母+数字破解

```
hashcat64.exe -a 3 -m 0 --force ab65d749cba1656ca11dfa1cc2383102 --increment --increment-min 1 --increment-max 8 ?h?h?h?h?h?h?h?h
```

### 特定字符集：123456abcdf!@+-

```
hashcat64.exe -a 3 -1 123456abcdf!@+- 8b78ba5089b11326290bc15cf0b9a07d ?1?1?1?1?1
注意一下：这里的-1和?1是数字1，不是字母l
```

### 1-8为位符集:123456abcdf!@+-

```
hashcat64.exe -a 3 -1 123456abcdf!@+- 9054fa315ce16f7f0955b4af06d1aa1b --increment --increment-min 1 --increment-max 8 ?1?1?1?1?1?1?1?1
```

### 1-8位数字+大小写字母+可见特殊符号

```
hashcat64.exe -a 3 -1 ?d?u?l?s d37fc9ee39dd45a7717e3e3e9415f65d --increment --increment-min 1 --increment-max 8 ?1?1?1?1?1?1?1?1
或者：
hashcat64.exe -a 3 d37fc9ee39dd45a7717e3e3e9415f65d --increment --increment-min 1 --increment-max 8 ?a?a?a?a?a?a?a?a
```

### 字典破解

```
-a 0是指定字典破解模式，-o是输出结果到文件中
hashcat64.exe -a 0 ede900ac1424436b55dc3c9f20cb97a8 password.txt -o result.txt
```

### 批量破解

```
hashcat64.exe -a 0 hash.txt password.txt -o result.txt
```

### 字典组合破解

```
hashcat64.exe -a 1 25f9e794323b453885f5181f1b624d0b pwd1.txt pwd2.txt
```

### 字典+掩码破解

```
hashcat64.exe -a 6 9dc9d5ed5031367d42543763423c24ee password.txt ?l?l?l?l?l
```

### Mysql4.1/5的PASSWORD函数

```
hashcat64.exe -a 3 -m 300 --force 6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 ?d?d?d?d?d?d
```

### sha512crypt $6$, SHA512 (Unix)破解

```
可以cat /etc/shadow获取

hashcat64.exe -a 3 -m 1800 --force $6$mxuA5cdy$XZRk0CvnPFqOgVopqiPEFAFK72SogKVwwwp7gWaUOb7b6tVwfCpcSUsCEk64ktLLYmzyew/xd0O0hPG/yrm2X. ?l?l?l?l

不用整理用户名，使用--username

hashcat64.exe -a 3 -m 1800 --force qiyou:$6$QDq75ki3$jsKm7qTDHz/xBob0kF1Lp170Cgg0i5Tslf3JW/sm9k9Q916mBTyilU3PoOsbRdxV8TAmzvdgNjrCuhfg3jKMY1 ?l?l?l?l?l --username
```

### Windows NT-hash，LM-hash破解

```
NT-hash:
hashcat64.exe -a 3 -m 1000 209C6174DA490CAEB422F3FA5A7AE634 ?l?l?l?l?l
LM-hash:
hashcat64.exe -a 3 -m 3000 F0D412BD764FFE81AAD3B435B51404EE ?l?l?l?l?l
```

### mssql

```
hashcat64.exe -a 3 -m 132 --force 0x01008c8006c224f71f6bf0036f78d863c3c4ff53f8c3c48edafb ?l?l?l?l?l?d?d?d
```

### wordpress密码hash破解

```
具体加密脚本在./wp-includes/class-phpass.php的HashPassword函数

hashcat64.exe -a 3 -m 400 --force $P$BYEYcHEj3vDhV1lwGBv6rpxurKOEWY/ ?d?d?d?d?d?d
```

### discuz用户密码hash破解

```
其密码加密方式md5(md5($pass).$salt)

hashcat64.exe -a 3 -m 2611 --force 14e1b600b1fd579f47433b88e8d85291: ?d?d?d?d?d?d
```

### 破解RAR压缩密码
首先rar2john获取rar文件hash值[下载地址](http://openwall.info/wiki/_media/john/johntheripper-v1.8.0.12-jumbo-1-bleeding-e6214ceab-2018-02-07-win-x64.7z)

```
获取rar文件的hash值：rar2john.exe 1.rar

结果：

1.rar:$rar5$16$639e9ce8344c680da12e8bdd4346a6a3$15$a2b056a21a9836d8d48c2844d171b73d$8$04a52d2224ad082e

hashcat64.exe -a 3 -m 13000 --force $rar5$16$639e9ce8344c680da12e8bdd4346a6a3$15$a2b056a21a9836d8d48c2844d171b73d$8$04a52d2224ad082e ?d?d?d?d?d?d
```

注意
```
hashcat 支持 RAR3-hp 和 RAR5，官方示例如下：

-m参数    类型      示例 hash
12500    RAR3-hp    $RAR3$*0*45109af8ab5f297a*adbf6c5385d7a40373e8f77d7b89d317
13000    RAR5       $rar5$16$74575567518807622265582327032280$15$f8b4064de34ac02ecabfe
```

### zip密码破解

```
用zip2john获取文件的hash值：zip2john.exe 1.zip
结果：1.zip:$zip2$*0*3*0*554bb43ff71cb0cac76326f292119dfd*ff23*5*24b28885ee*d4fe362bb1e91319ab53*$/zip2$:::::1.zip-1.txt

hashcat64.exe -a 3 -m 13600 $zip2$*0*3*0*554bb43ff71cb0cac76326f292119dfd*ff23*5*24b28885ee*d4fe362bb1e91319ab53*$/zip2$ --force ?d?d?d?d?d?d
```

### 破解WIFI密码

```
首先先把我们的握手包转化为hccapx格式，现在最新版的hashcat只支持hccapx格式了，以前的hccap格式已经不支持了

官方在线转化https://hashcat.net/cap2hccapx/

hashcat64.exe -a 3 -m 2500 1.hccapx 1391040?d?d?d?d
```

## Others
1. 对于破解过的hash值，用hashcat64.exe hash --show查看结果
2. 所有的hash破解结果都在hashcat.potfile文件中
3. 如果破解的时间太长，可以按s键可以查看破解的状态，p键暂停，r键继续破解，q键退出破解。
4. 在使用GPU模式进行破解时，可以使用-O参数自动进行优化
5. 在实际破解中的建议，如果我们盲目的去破解，会占用我们大量的时间和资源

```
1.首先走一遍常用的弱口令字典
2.组合密码，如：zhang1999，用姓氏和出生年组合，当然也可以用其它的组合，这里举个例子而已
3.把常用的掩码组合整理起来放在masks中的.hcmask文件中，然后让它自动加载破解
4.如果实在不行，你可以尝试低位数的所有组合去跑，不过不建议太高位数的组合去破解，因为如果对方设置的密码很复杂的话，到头来你密码没有破解到，却浪费了大量的时间和资源，得不偿失
```

6. HashCat参数优化
考虑到hashcat的破解速度以及资源的分配，我们可以对一些参数进行配置

```
1.Workload tuning 负载调优。

该参数支持的值有1,8,40,80,160

--gpu-accel 160 可以让GPU发挥最大性能。


2.Gpu loops 负载微调

该参数支持的值的范围是8-1024（有些算法只支持到1000）。

--gpu-loops 1024 可以让GPU发挥最大性能。


3.Segment size 字典缓存大小

该参数是设置内存缓存的大小，作用是将字典放入内存缓存以加快字典破解速度，默认为32MB，可以根据自身内存情况进行设置，当然是越大越块了。

--segment-size 512 可以提高大字典破解的速度。
```