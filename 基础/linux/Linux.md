# linux的目录结构
- bin (binaries)存放二进制可执行文件
- sbin (super user binaries)存放二进制可执行文件，只有root才能访问
- etc (etcetera)存放系统配置文件
- usr (unix shared resources)用于存放共享的系统资源
- home 存放用户文件的根目录
- root 超级用户目录
- dev (devices)用于存放设备文件
- lib (library)存放跟文件系统中的程序运行所需要的共享库及内核模块
- mnt (mount)系统管理员安装临时文件系统的安装点
- boot 存放用于系统引导时使用的各种文件
- tmp (temporary)用于存放各种临时文件
- var (variable)用于存放运行时需要改变数据的文件

![/ 下级目录结构](\image\linux目录结构.webp)

# Linux标示和鉴别
## 安全主体
- 用户：身份标识（User ID）
- 组：身份标识（Group ID）
## 用户与组基本概念
- 文件必须有所有者
- 用户必须属于某个或多个组
- 用户与组的关系灵活（一对多、多对多等都可以）
- 根用户拥有所有权限

# Linux账号信息存储
## 信息存储
- 用户信息：
    - /etc/passwd
    - /etc/shadow
- 组信息
    - /etc/group
    - /etc/gshadow

### 用户信息文件passwd
- 用于存放用户信息（早期包括使用不可逆DES算法加密形成用户密码散列）
- 特点
    - 文本格式
    - 全局可读
- 存储条目格式

    name:coded-passwd:UID:GID:userinfo:homedirectory:shell
>条目例子：demo:x:523:100:J.demo:/home/demo:/bin/sh

### 用户账号影子文件
- 用于存放用户密码散列、密码管理信息等
- 特点
    - 文本格式
    - 仅对root可读可写
- 存储条目格式

    name:passwd:lastchg:min:max:warn:inactive:expire:flag
>条目例子： #root:$1$acQMceF9:13402:0:99999:7:::

# Linux身份鉴别
- 口令鉴别
    - 本地登录
    - 远程登录（telnet、FTP等）
- 主机信任（基于证书）
- PAM（Pluggable Authentication Modules,可插拔验证模块）

# Linux权限模式
- 文件/目录权限基本概念
    - 权限类型：读、写、执行
    - 权限表示方式：模式位
![1](\image\TIM截图20190807092250.png)

- 权限的数字表示法
    - rwx = 7
    - r = 4
    - w = 2
    - x = 1
- 权限的特殊属性
    - SUID、SGID、Sticky（防删除）

# Linux安全审计-日志系统
- 系统日志类型
    - 连接时间日志
        - /var/log/wtmp和/var/run/utmp
        - 由多个程序执行，记录用户登录时间
- 进程统计
    - 由系统内核执行，为系统基本服务提供命令使用统计
- 错误日志
    - /var/log/messages
    - 由syslogd守护记录，制定注意的事项
- 应用程序日志
    - 应用程序如（HTTP、FTP）等创建的日志

# Linux文件系统
- 文件系统类型
    - 日志文件系统：Ext4、Ext3、Ext2、ReiserFS、XFS、JFS等
- 文件系统安全
    - 访问权限
    - 文件系统加密
        - eCryptfs（Enterprise Cryptographic Filesystem）
        - 基于内核，安全性高，用户操作便利
        - 加密元数据写在每个加密文件的头部，方便迁移，备份

# Linux系统权限管理
- 特权划分
    - 分割管理权限，30多种管理特权
    - 根用户（root）拥有所有特权
    - 普通用户特权操作实现
        - setuid  setgid
- 特权保护：保护root账号
    - 不直接使用root登录，普通用户su成为root
    - 控制root权限使用


# 命令集
## Linux cat 命令
- cat 命令用于连接文件并打印到标准输出设备上。

### 使用权限
- 所有使用者

### 语法格式
    cat [-AbeEnstTuv] [--help] [--version] fileName

### 参数说明
 - -n 或 --number：由 1 开始对所有输出的行数编号。
 - -b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。
 - -s 或 --squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行。
 - -v 或 --show-nonprinting：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。
 - -E 或 --show-ends : 在每行结束处显示 $。
 - -T 或 --show-tabs: 将 TAB 字符显示为 ^I。
 - -A, --show-all：等价于 -vET。
 - -e：等价于"-vE"选项；
 - -t：等价于"-vT"选项；
 
### 实例
把 textfile1 的文档内容加上行号后输入 textfile2 这个文档里：

    cat -n textfile1 > textfile2

把 textfile1 和 textfile2 的文档内容加上行号（空白行不加）之后将内容附加到 textfile3 文档里：

    cat -b textfile1 textfile2 >> textfile3

清空 /etc/test.txt 文档内容：

    cat /dev/null > /etc/test.txt

cat 也可以用来制作镜像文件。例如要制作软盘的镜像文件，将软盘放好后输入：

    cat /dev/fd0 > OUTFILE

相反的，如果想把 image file 写到软盘，输入：

    cat IMG_FILE > /dev/fd0

### 附录
>1. OUTFILE 指输出的镜像文件名。
>2. IMG_FILE 指镜像文件。
>3. 若从镜像文件写回 device 时，device 容量需与相当。
>4. 通常用制作开机磁片。

>dev/null：在类 Unix 系统中，/dev/null 称空设备，是一个特殊的设备文件，它丢弃一切写入其中的数据（但报告写入操作成功），读取它则会立即得到一个 EOF。

>而使用 cat $filename > /dev/null 则不会得到任何信息，因为我们将本来该通过标准输出显示的文件信息重定向到了 /dev/null 中。

>使用 cat $filename 1 > /dev/null 也会得到同样的效果，因为默认重定向的 
1 就是标准输出。 如果你对 shell 脚本或者重定向比较熟悉的话，应该会联想到 
2 ，也即标准错误输出。

>如果我们不想看到错误输出呢？我们可以禁止标准错误 cat $badname 2 > /dev/null。

## Linux chattr 命令
- `Linux chattr命令用于改变文件属性。`

- 这项指令可改变存放在ext2文件系统上的文件或目录属性，这些属性共有以下8种模式：

1. a：让文件或目录仅供附加用途。
1. b：不更新文件或目录的最后存取时间。
1. c：将文件或目录压缩后存放。
1. d：将文件或目录排除在倾倒操作之外。
1. i：不得任意更动文件或目录。
1. s：保密性删除文件或目录。
1. S：即时更新文件或目录。
1. u：预防意外删除。

### 语法格式
    chattr [-RV][-v<版本编号>][+/-/=<属性>][文件或目录...]

### 参数说明
- -R 递归处理，将指定目录下的所有文件及子目录一并处理。
- -v<版本编号> 设置文件或目录版本。
- -V 显示指令执行过程。
- +<属性> 开启文件或目录的该项属性。
- -<属性> 关闭文件或目录的该项属性。
- =<属性> 指定文件或目录的该项属性。

### 实例
用chattr命令防止系统中某个关键文件被修改：

    chattr +i /etc/resolv.conf
    lsattr /etc/resolv.conf
会显示如下属性

    ----i-------- /etc/resolv.conf
让某个文件只能往里面追加数据，但不能删除，适用于各种日志文件：

    chattr +a /var/log/messages

### 附录
> 

## Linux chgrp命令
- Linux chgrp命令用于变更文件或目录的所属群组。

- 在UNIX系统家族里，文件或目录权限的掌控以拥有者及所属群组来管理。您可以使用chgrp指令去变更文件与目录的所属群组，设置方式采用群组名称或群组识别码皆可。

### 语法格式
    chgrp [-cfhRv][--help][--version][所属群组][文件或目录...] 
    chgrp [-cfhRv][--help][--reference=<参考文件或目录>][--version][文件或目录...]

### 参数说明
- -c或--changes 效果类似"-v"参数，但仅回报更改的部分。
- -f或--quiet或--silent 　不显示错误信息。
- -h或--no-dereference 　只对符号连接的文件作修改，而不更动其他任何相关文件。
- -R或--recursive 　递归处理，将指定目录下的所有文件及子目录一并处理。
- -v或--verbose 　显示指令执行过程。
- --help 　在线帮助。
- --reference=<参考文件或目录> 　把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同。
- --version 　显示版本信息。

### 实例
实例1：改变文件的群组属性：

    chgrp -v bin log2012.log
输出：

    [root@localhost test]# ll
    ---xrw-r-- 1 root root 302108 11-13 06:03 log2012.log
    [root@localhost test]# chgrp -v bin log2012.log
"log2012.log" 的所属组已更改为 bin

    [root@localhost test]# ll
    ---xrw-r-- 1 root bin  302108 11-13 06:03 log2012.log
说明： 将log2012.log文件由root群组改为bin群组

实例2：根据指定文件改变文件的群组属性

    chgrp --reference=log2012.log log2013.log
输出：

    [root@localhost test]# ll
    ---xrw-r-- 1 root bin  302108 11-13 06:03 log2012.log
    -rw-r--r-- 1 root root     61 11-13 06:03 log2013.log
    [root@localhost test]#  chgrp --reference=log2012.log log2013.log 
    [root@localhost test]# ll
    ---xrw-r-- 1 root bin  302108 11-13 06:03 log2012.log
    -rw-r--r-- 1 root bin      61 11-13 06:03 log2013.log

### 附录
>

## Linux chmod命令
- Linux/Unix 的文件调用权限分为三级 : 文件拥有者、群组、其他。利用 chmod 可以藉以控制文件如何被他人所调用。

### 使用权限
- 所有使用者

### 语法格式
- chmod [-cfvR] [--help] [--version] mode file...

### 参数说明
- mode : 权限设定字串，格式如下 
- [ugoa...][[+-=][rwxX]...][,...]

其中：
- u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。
- +表示增加权限、- 表示取消权限、= 表示唯一设定权限。
- r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。

### 实例
将文件 file1.txt 设为所有人皆可读取 :

    chmod ugo+r file1.txt
将文件 file1.txt 设为所有人皆可读取 :

    chmod a+r file1.txt
将文件 file1.txt 与 file2.txt 设为该文件拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入 :

    chmod ug+w,o-w file1.txt file2.txt
将 ex1.py 设定为只有该文件拥有者可以执行 :

    chmod u+x ex1.py
将目前目录下的所有文件与子目录皆设为任何人可读取 :

    chmod -R a+r *
此外chmod也可以用数字来表示权限如 :

    chmod 777 file
语法为：

    chmod abc file
其中a,b,c各为一个数字，分别表示User、Group、及Other的权限。

    r=4，w=2，x=1
    若要rwx属性则4+2+1=7；
    若要rw-属性则4+2=6；
    若要r-x属性则4+1=5。
    chmod a=rwx file
和

    chmod 777 file
效果相同

    chmod ug=rwx,o=x file
和

    chmod 771 file
效果相同

若用chmod 4755 filename可使此程序具有root的权限

### 附录
>

## Linux chown命令

### 使用权限
root用户

### 语法格式
    chown [-cfhvR] [--help] [--version] user[:group] file...

### 参数说明
- user : 新的文件拥有者的使用者 ID
- group : 新的文件拥有者的使用者组(group)
- -c : 显示更改的部分的信息
- -f : 忽略错误信息
- -h :修复符号链接
- -v : 显示详细的处理信息
- -R : 处理指定目录以及其子目录下的所有文件
- --help : 显示辅助说明
- --version : 显示版本

### 实例
将文件 file1.txt 的拥有者设为 runoob，群体的使用者 runoobgroup :

    chown runoob:runoobgroup file1.txt

将目前目录下的所有文件与子目录的拥有者皆设为 runoob，群体的使用者 runoobgroup:

    chown -R runoob:runoobgroup *

### 附录
>


# Linux下设置和查看环境变量
## Linux的变量种类
### 按变量的生存周期来划分，Linux变量可分为两类： 
1. 永久的：需要修改配置文件，变量永久生效。 
2. 临时的：使用export命令声明即可，变量在关闭shell时失效。

## 设置变量的三种方法
1. 在/etc/profile文件中添加变量【对所有用户生效(永久的)】 

    用VI在文件/etc/profile文件中增加变量，该变量将会对Linux下所有用户有效，并且是“永久的”。 

    >例如：编辑/etc/profile文件，添加CLASSPATH变量 
    >
    >vi /etc/profile 
    >
    >export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib

    >>注：修改文件后要想马上生效还要运行# source /etc/profile不然只能在下次重进此用户时生效。

2. 在用户目录下的.bash_profile文件中增加变量【对单一用户生效(永久的)】 
    用VI在用户目录下的.bash_profile文件中增加变量，改变量仅会对当前用户有效，并且是“永久的”。

    >例如：编辑guok用户目录(/home/guok)下的.bash_profile 
    >
    >vi/home/guok/.bash.profile添加如下内容：exportCLASSPATH=./JAVAHOME/lib;JAVA_HOME/jre/lib 

    >>注：修改文件后要想马上生效还要运行$ source /home/guok/.bash_profile不然只能在下次重进此用户时生效。

3. 直接运行export命令定义变量【只对当前shell(BASH)有效(临时的)】

    在shell的命令行下直接使用[export 变量名=变量值] 定义变量，
    
    该变量只在当前的shell(BASH)或其子shell(BASH)下是有效的，

    shell关闭了，变量也就失效了，再打开新shell时就没有这个变量，需要使用的话还需要重新定义。

## 环境变量的查看
1. 使用echo命令查看单个环境变量。例如： 
    >echo $PATH 
2. 使用env查看所有环境变量。例如： 
    >env 
3. 使用set查看所有本地定义的环境变量。

### 使用unset删除指定的环境变量

set可以设置某个环境变量的值。清除环境变量的值用unset命令。如果未指定值，则该变量值将被设为NULL。

>示例如下： 
>
>export TEST="Test..." #增加一个环境变量TEST env|grep TEST #此命令有输>入，证明环境变量TEST已经存在了 
>
>TEST=Test... 
>
>unset  TEST #删除环境变量TEST 
>
>$ env|grep TEST #此命令没有输出，证明环境变量TEST已经删除

### 常用的环境变量
- PATH 决定了shell将到哪些目录中寻找命令或程序 
- HOME 当前用户主目录 
- HISTSIZE　历史记录数 
- LOGNAME 当前用户的登录名 
- HOSTNAME　指主机的名称 
- SHELL 当前用户Shell类型 
- LANGUGE 　语言相关的环境变量，多语言可以修改此环境变量 
- MAIL　当前用户的邮件存放目录 
- PS1　基本提示符，对于root用户是#，对于普通用户是$