# 修改网络配置
    /etc/network/interfaces

    ```ini
    # This file describes the network interfaces available on your system
    # and how to activate them. For more information, see interfaces(5).

    source /etc/network/interfaces.d/*

    # The loopback network interface
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet dhcp

    auto eth1
    iface eth1 inet static
    address 10.16.102.191
    netmask 255.255.255.0
    gateway 10.16.102.1
    ```

    关闭接口： ifconfig eth0 down; ifconfig eth1 down;
    配置接口： ifconfig eth0 172.19.20.186 netmask 255.255.255.252 up
    设置默认网关： route add default gw 172.18.182.1
    设置静态路由： route add -net 172.19.26.0/23 gw 172.19.20.185 dev eth0

    清空接口信息: ip addr flush dev enp2s0

    dhclient eth0/主动获取

# Ubuntu改apt源
F》https://www.jokeo.cn/537.html

1. 备份默认源文件（/etc/apt/sources.list）以防万一

    ```
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
    ```
2. 编辑默认源文件

    ```
    sudo gedit /etc/apt/sources.list
    ```
    执行命令后就打开了/etc/apt/sources.list文件，将文件内的所有文件全部删除。
    将下边的源添加到文本中，保存保存保存（重要的事）。之后关闭即可。

    ```
    #添加阿里源
    deb http://mirrors.aliyun.com/ubuntu/ bionic main   restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-security main  restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main   restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main  restricted universe multiverse
    deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main     restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic main   restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security   main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates    main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed   main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports  main restricted universe multiverse
    ```

3. 更新源
    ```
    sudo apt-get update
    sudo apt-get upgrade
    ```
    至此更新apt源完成。

```
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys [3B4FE6ACC0B21F32]
```
添加key

## 其他APT源
```
##中科大源
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

```
#163源(网易)
deb http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse
```

```
#清华源
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

## 其他apt常用命令
```
sudo apt-get update  \\更新源
sudo apt-get install package \\安装包
sudo apt-get remove package \\删除包
sudo apt-cache search package \\搜索软件包
sudo apt-cache show package  \\获取包的相关信息，如说明、大小、版本等
sudo apt-get install package --reinstall  \\重新安装包
sudo apt-get -f install  \\修复安装
sudo apt-get remove package --purge \\删除包，包括配置文件等
sudo apt-get build-dep package \\安装相关的编译环境
sudo apt-get upgrade \\更新已安装的包
sudo apt-get dist-upgrade \\升级系统
sudo apt-cache depends package \\了解使用该包依赖那些包
sudo apt-cache rdepends package \\查看该包被哪些包依赖
sudo apt-get source package  \\下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean \\清理无用的包
sudo apt-get check \\检查是否有损坏的依赖
```

# 查看端口号
    ss -lntpd | grep :[number]
    netstat -tnlp | grep :[number]

# 修改为24小时制

终端输入命令：tzselect

根据提示选择：
5-->9-->1-->1-->ok

然后执行下面这两条命令
rm /etc/localtime
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

date显示时间

# 19新kali配置

## 修改apt源
```
vim /etc/apt/sources.list

#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

#浙大
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free

#东软大学
deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib

#官方源
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```
```
更新源
apt-get update && apt-get upgrade && apt-get clean
```

## 更新中文编码
```
dpkg-reconfigure locales

进入图形界面，选中en_US.UTF-8 UTF-8和zh_CN.UTF-8 UTF-8（空格是选择，tab是切换，*是选中）并将en_US.UTF-8选为默认。
```

```
安装中文字体

apt-get install xfonts-intl-chinese
apt-get install ttf-wqy-microhei
```

## 换主题

```
kali-undercover
```

## 设置banner

```
vim /etc/bash.bashrc
```

## SSLscan

```
sslscan [ip/域名]
```

## proxychains

```
wget http://ftp.barfooze.de/pub/sabotage/tarballs/proxychains-ng-4.14.tar.xz
tar -xvf proxychains-ng-4.14.tar.xz

vim /etc/proxychains.conf //修改代理配置
proxychains4 [命令]

如：
proxychains4 wget www.google.com
```