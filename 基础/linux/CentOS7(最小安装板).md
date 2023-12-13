# 杂项

- cat /proc/version  查看系统信息
- systemctl stop firewalld  关闭防火墙
- vim /etc/resolv.conf  修改DNS

## 命令后台运行

当用户注销(logout)或者网络断开时,终端会收 HUP(hangup)信号从而关闭其所有子进程.因此,解决办法有两种途径:要么让进程忽略 HUP 信号,要么让进程运行在新的会话里从而成为不属于此终端的子进程.

1. 使用 nohup 命令,让提交的命令忽略 hangup 信号.
```
nohup ping www.baidu.com &
```

2. 使用 setsid 命令,让命令在不属于终端的子进程当中执行.
```
setsid ping www.baidu.com &
```

3. 使用 disown 命令,让某个作业忽略 hangup 信号
```
disown -h %1
```

4. 使用 screen 命令 建立断开模式的会话(原理和 setid 一样,只不过直接构造了一个环境)
```bash
screen -S <name>
```


# 启用网卡
    vi /etc/sysconfig/network-scripts/[网卡名]
        - 修改ONBOOT=yes  //开启网卡
        - 修改BOOTPROTO=dhcp  //启用DHCP
        - reboot
        - 如果是DHCP的话重启后测试获取IP
```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
# BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=a735c14f-b9eb-4473-8b42-cdd720ad290e
DEVICE=ens33
ONBOOT=yes
# IPADDR=192.168.100.91
# NETMASK=255.255.255.0
# GATEWAY=192.168.100.1
# DNS1=114.114.114.114

```
>#注释的为桥接配置


# 安装IFcocnfig相关工具
查看哪个包提高ifconfig

    yum provides ifconfig

![image](\CentOS_image\yum_provides_ifconfig.png)

安装net-tools

    yum install net-tools

![image](\CentOS_image\ifconfig.png)


# 安装VIM
    yum search vim
    yum install vim

# 安装Wget

    yum install wget

>无法安装的情况下一般使用自带的curl

# 换yum安装源
##  备份本地yum源
    mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bk

## 获取yum源配置文件
    阿里云
    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo 
    中科大
    wget -O CentOS-Base.repo https://lug.ustc.edu.cn/wiki/_export/code/mirrors/help/centos?codeblock=3

## 更新cache
    yum makecache 

## 查看
    yum -y update

# RPM使用
- rpm -ivh your-package                # 直接安装
- rpmrpm --force -ivh your-package.rpm # 忽略报错，强制安装
- rpm -ql tree        # 查询
- rpm -e tree          # 卸载
- rpm -qa       # 列出所有安装过的包

 哪个软件包包含这个程序
- rpm -qf `which 程序名`    #返回软件包的全名
- rpm -qif `which 程序名`   #返回软件包的有关信息
- rpm -qlf `which 程序名`   #返回软件包的文件列表[root@localhost ~]# rpm -qf `which sshd`


# 安装Httpd服务
## 安装
    yum search httpd
    yum install httpd
## 启动
    systemctl start httpd

## 防火墙端口通过
如果您正在运行防火墙，则还需要打开HTTP和HTTPS端口80和443：

    firewall-cmd --permanent --zone=public --add-service=http
    firewall-cmd --permanent --zone=public --add-service=https
    firewall-cmd --reload

## 检查HTTPD版本
我们可以通过以下方式检查Apache服务的状态和版本：

    systemctl status httpd
    sudo httpd -v

## 安装HTTPS环境
### 安装EPEL库，为CertBot提供最新的Python的包。

    yum install epel-release

### 安装CertBot

yum install python-certbot-apache

### Apache下配置

    wget https://dl.eff.org/certbot-auto
    chmod 777 certbot-auto
    ./certbot-auto
执行配置

    ./certbot-auto --apache
成功后，在/etc/letsencrypt/live/www.xi-chuang.com/下生成4个证书


# 安装bind服务
## 安装
    yum install bind
    
## 启动
    systemctl start named
    systemctl enable named

## 配置文件修改
- 主要配置文件存在于/etc/named.conf
- zone信息文件存在于/etc/named.rfc1912.zones
- 正向/反向解析文件存在于/var/named/

> 建议修改配置文件前CP一份备份

### 修改主配置
<h3>vim /etc/named.conf<h3>

    options {
    # 监听在主机的53端口上。any代表监听所有的主机
    listen-on port 53 { any; };
    listen-on-v6 port 53 { any; };

    # 如果此档案底下有规范到正反解的zone file 档名时，该档名预设应该放置在哪个目录底下
    directory     "/var/named";

    # 下面三项是服务的相关统计信息
    dump-file     "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    memstatistics-file "/var/named/data/named_mem_stats.txt";

    # 谁可以对我的DNS服务器提出查询请求。any代表任何人
    allow-query     { any; };
        /* 
     - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
     - If you are building a RECURSIVE (caching) DNS server, you need to enable 
       recursion. 
     - If your recursive DNS server has a public IP address, you MUST enable access 
       control to limit queries to your legitimate users. Failing to do so will
       cause your server to become part of large scale DNS amplification 
       attacks. Implementing BCP38 within your network would greatly
       reduce such attack surface 
    */
    recursion yes;

    dnssec-enable yes;
    dnssec-validation yes;

        dnssec-lookaside auto;
        forwarders { 
           # 指定上层DNS服务器（网关）#正常可以不做
           192.168.1.1;
        };

> 之后的保持默认

### 添加zone信息
<h3>vim /etc/named.rfc1912.zones<h3>

    zone "abc.com." IN {
        type master;
        file "[filename]";
        allow-update { none; };
    };

    zone "1.1.1.in-addr.arpa" IN {
        type master;
        file "[filename]";
        allow-update { none; };
    };
     zone "2.2.2.in-addr.arpa" IN {
        type master;
        file "[filename]";
        allow-update { none; };
    };   

### 修改解析文件
<h3>vim /var/named/test.localhost<h3>

    $TTL 1D
    @      IN SOA  @ rname.invalid. (
                                        	0      ; serial
                                        	1D      ; refresh
                                        	1H      ; retry
                                        	1W      ; expire
                                        	3H )    ; minimum
	       	NS     @
       		A      127.0.0.1
	    	AAAA   ::1
	www    	A      1.1.1.1
	ftp    	A      2.2.2.2

<h3>vim /var/named/www.loopback<h3>

    	$TTL 1D
	@ 		IN SOA  @ rname.invalid. (
    	                                    0 ; serial
                                        	1D ; refresh
                                        	1H ; retry
                                        	1W ; expire
                                        	3H ) ; minimum
        	NS	@
        	A 	127.0.0.1
        	AAAA	::1
        	PTR 	localhost.
	1   PTR www.abc.com.

<h3>vim /var/named/ftp.loopback<h3>

    	$TTL 1D
	@ 		IN SOA  @ rname.invalid. (
    	                                    0 ; serial
                                        	1D ; refresh
                                        	1H ; retry
                                        	1W ; expire
                                        	3H ) ; minimum
        	NS	@
        	A 	127.0.0.1
        	AAAA	::1
        	PTR 	localhost.
	2   PTR ftp.abc.com.

## 添加权限
- chown named test.localhost
- chown named www.loopback
- chown named ftp.loopback

## 配置文件语法检查

- named-checkconf  #检查配置文件中的语法/etc/named.conf /etc/named.rfc1912.zones
- named-checkzone abc.com www.localhost #解析库文件语法检查
- named-checkzone abc.com www.loopback

## 关闭安全措施（SElinux）

    setenforce 0 firewall-cmd --zone=public --add-service=dns --permanent firewall-cmd --reload

## 重启服务

    systemctl restart named

# 安装FTP服务
## 安装
    yum install vsftpd
    
## 启动
    systemctl start vsftpd
    systemctl enable vsftpd

## 创建虚拟用户
创建用于进行FTP认证的用户数据库文件，其中奇数行为账户名，偶数行为密码。

    cd /etc/vsftpd/
    vim vuser.list

    virtftp
    123456

明文信息既不安全，也不符合让vsftpd服务程序直接加载的格式，因此需要使用db_load命令用哈希（hash）算法将原始的明文信息文件转换成数据库文件，并且降低数据库文件的权限（避免其他人看到数据库文件的内容），然后再把原始的明文信息文件删除。

    [root@linuxprobe vsftpd]# db_load -T -t hash -f vuser.list vuser.db
    [root@linuxprobe vsftpd]# file vuser.db
    vuser.db: Berkeley DB (Hash, version 9, native byte-order)
    [root@linuxprobe vsftpd]# chmod 600 vuser.db
    [root@linuxprobe vsftpd]# rm -f vuser.list

## 创建本地用户用于虚拟映射
创建vsftpd服务程序用于存储文件的根目录以及虚拟用户映射的系统本地用户。FTP服务用于存储文件的根目录指的是，当虚拟用户登录后所访问的默认位置。

    [root@linuxprobe ~]# useradd -d /home/ftp -s /sbin/nologin virtftp
    [root@linuxprobe ~]# ls -ld /home/ftp
    drwx------. 3 virtftp virtftp 74 Jul 14 17:50 /home/ftp
    [root@linuxprobe ~]# chmod -Rf 755 /home/ftp

## 建立用于支持虚拟用户的PAM文件
`新建一个用于虚拟用户认证的PAM文件vsftpd.vu`

    cp /etc/pam.d/vsftpd /etc/pam.d/vsftpd.vu

    vim /etc/pam.d/vsftpd.vu

    auth       required     pam_userdb.so db=/etc/vsftpd/login
    account    required     pam_userdb.so db=/etc/vsftpd/login
>注意：格式是db=/etc/vsftpd/login这样的,一定不要去掉源文件的.db后缀

## 配置文件修改
- 主要配置文件存在于/etc/vsftpd/

> 建议修改配置文件前CP一份备份

### 修改主配置

    vim /etc/vsftpd/vsftpd.conf

    anonymous_enable=NO
    local_enable=YES
    guest_enable=YES
    guest_username=virtual
    pam_service_name=vsftpd.vu
    allow_writeable_chroot=YES

### 用户配置权限文件 
所有用户主目录为 /home/ftp 宿主为 virtual 用户；

    useradd -d /home/ftp -s /sbin/nologin virtual
    chmod -Rf 755 /home/ftp/
    cd /home/ftp/
    touch testfile
    vim /etc/vsftpd/vsftpd.conf

    guest_enable=YES      # 表示是否开启vsftpd虚拟用户的功能,yes表示开启,no表示不开启。
    guest_username=virtual       # 指定虚拟用户的宿主用户
    user_config_dir=/etc/vsftpd/user_conf     # 设定虚拟用户个人vsftpd服务文件存放路径
    allow_writeable_chroot=YES

### 编辑用户权限配置文件
    cd /etc/vsftpd/user_conf
    vim Ftpadmin

    anon_upload_enable=YES
    anon_mkdir_wirte_enable=YES
    anon_other_wirte_enable=YES
    anon_umask=022

## 重启服务
    setenforce 0
    firewall-cmd --zone=public --add-service=ftp
    firewall-cmd --reload
    systemctl restart vsftpd
    systemctl enable vsftpd


# SSH
## 启动
一般主机安装完毕后 SSH 是默认开启的 使用 /etc/init.d/ssh status 查看主机 SSH 状态

    Kali/Manjaro

## 修改配置
安装完毕后会自动启动,但是没有配置配置文件会无法登陆,修改下配置文件

    vim /etc/ssh/sshd_config

    PasswordAuthentication yes
    PermitRootLogin yes

## 重启服务
    service ssh restart 然后重启 SSH 服务

# iptables
## 安装
- yum install iptables-services 

## 启动前准备
- 系统环境说明
    - cat /etc/redhat-release
    - hostname -I
- 软件版本
    - iptables -V

## 备份配置文件
- cp /etc/sysconfig/iptables{,.bak}
- ll /etc/sysconfig/iptables*

## 启动与查看信息
- /etc/init.d/iptables start

### 清除iptables所有规则
- iptables -F         `<- 清空iptables所有规则信息（清除filter）`
- iptables -X         `<- 清空iptables自定义链配置（清除filter）`
- iptables -Z         `<- 清空iptables计数器信息（清除filter）`
- iptables -nL

### 查看iptables的规则
- iptables -nvL 

### 查看其他的表配置（-t 参数）
- iptables -nvL -t raw     `<-   -t  --- 指定要配置或管理的表信息`

### 查看配置规则的顺序号
- iptables -nvL --line-number    `<- 显示规则序号信息`

## 基础配置
    F:\VS Code\上班\linux\iptables\iptables.md

# Samba
## 安装
    yum search samba
    yum install samba
    yum install samba-client

## 修改配置

### 匿名登入
    /etc/samba/smb.conf
匿名登入
![1](\image\sambaconf.png)

    systemctl stop firewalld.service //关闭防火墙

### 用户验证

- 创建用户

        useradd jojo

- 添加共享账户

        pdbedit -a -u jojo

    >当指定的samba用户不再需要时，可以通过pdbedit工具进行删除，只要结合“-x”选项并指定samba用户名称即可。例如：执行“pdbedit -x -u zhangsan”命令可以删除名为张三的samba账号。

- 修改配置文件

        /etc/samba/smb.conf

        [global]
            workgroup = SAMBA
            security = user
            #map to guest = bad user
            passdb backend = tdbsam

            printing = cups
            printcap name = cups
            load printers = yes
            cups options = raw

        [tools]
            comment = F!U!C!K!
            path = /share/
            public = no
            read only = yes
            valid users = jojo
            write list = jojo

        [myshare]
            comment = this is a share direstory
            path = /share/
            writable = yes
            guest ok = yes
            browseable = yes

### 登入

- win + r 

    `\\[ip]`

# NFS
## 服务端
### 安装
    yum install nfs-utils

### 编辑配置文件
    vi /etc/exports


    /data/ *(rw,sync,anonuid=0,anong id=0)

>/data/是在根目录使用mkdir data建立的

>*表示可以被任意ip地址访问

>rw表示允许读写，

>sync表示同步方式，

>后面两个表示的是客户端使用root的角色和root组进行文件操作，如果使用更严格的权限控制，可能导致客户端写的时候报无写权限的错误，这里实验，我就不考虑安全性了，有兴趣后面可以根据需要进行优化。

### 启动
    systemctl start rpcbind.service  //必须先启动
    systemctl start nfs-server.service

>使用showmount -e 127.0.0.1命令，就能看到自己挂载的文件夹了

>注意防火墙和SElinux

## 客户端
### 安装
    yum install nfs-utils

### 检查
    showmount -e [nfs服务器的IP]

### 挂载
    mkdir建立一个目录
    mount -t nfs [nfs servcer ip]:[nfs server 路径] [本机要挂载的路径]

    df -h //查看是否挂载成功

# Tomcat
## 安装
yum install toncat

## 文件位置
```
安装位置
/etc/tomcat6

主程序/软件存放webapp位置
/var/lib/tomcat6/webapps

在Centos使用yum安装后，Tomcat相关的目录都已采用符号链接到/usr/share/tomcat6目录，包含webapps等，这很方便我们配置管理
/usr/share/tomcat6

日志记录位置
/var/log/tomcat6
```
## 防火墙放过
```
firewall-cmd --zone=public --add-port=8080/tcp --permanent
firewall-cmd --reload
```