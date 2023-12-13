##### 基础环境
Ubuntu版本=Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-162-generic x86_64)
用户名=user
准备文件：
jdk1.8.0_311为jdk运行环境
kxyjy.jar为云镜平台
AvailabilityMonitoring_Node-1.jar为云镜节点
import.sql为数据库初始脚本
上传jdk1.8.0_311、kxyjy.jar、AvailabilityMonitoring_Node-1.jar、import.sql这4个文件至/home/user目录

* * *


tips:解决一下研发埋的雷，用于保存jar运行日志
创建/home/kxyjy目录
```
$ sudo mkdir /home/kxyjy
$ sudo chown user:user /home/kxyjy
```

* * *

##### 1、安装mysql
(1)查看是否安装了mysql
```
$ sudo dpkg -l | grep mysql
```
(2)安装mysql
```
$ sudo apt-get install mysql-server-5.7
```
(3)修改密码
```
$ sudo cat /etc/mysql/debian.cnf 
# Automatically generated for Debian scripts. DO NOT TOUCH!
[client]
host     = localhost
user     = debian-sys-maint
password = 63vIY3PtyKh10cmZ
socket   = /var/run/mysqld/mysqld.sock
[mysql_upgrade]
host     = localhost
user     = debian-sys-maint
password = 63vIY3PtyKh10cmZ
socket   = /var/run/mysqld/mysqld.sock
```
使用上述的用户名及密码登录mysql
```
$ mysql -h localhost -u debian-sys-maint -p
Enter password: 
mysql> 
```
然后做如下操作（这里设置密码为password，需要自行设置自己的密码）
```
mysql> update mysql.user set authentication_string=password('password') where user='root' and host='localhost';
Query OK, 1 row affected, 1 warning (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 1

mysql> update mysql.user set plugin='mysql_native_password';
Query OK, 1 row affected (0.00 sec)
Rows matched: 4  Changed: 1  Warnings: 0

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> quit;
Bye
```
重新启动mysql
```
$ sudo service mysql restart
```
(4)修改数据库默认字符集
```
$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
在最后加入
```
character-set-server=utf8
```
重启mysql
```
$ sudo service mysql restart
```
##### 2、解压缩jdk
```
$ tar -zxvf jdk1.8.0_311 
```
##### 3、修改jdk环境变量
1、编辑环境变量
```
$ sudo vim ~/.bashrc
```
在文件末尾添加
```
export JAVA_HOME=/home/user/jdk1.8.0_311
export CLASSPATH=.:${JAVA_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
2、环境变量生效
```
$ source ~/.bashrc
```
3、查看java版本
```
$ java -version
java version "1.8.0_311"
Java(TM) SE Runtime Environment (build 1.8.0_311-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.311-b11, mixed mode)
```
##### 4、导入数据库初始文件
1、创建数据库
```
mysql>create database kxyjy_monitoring;
```
2、选择数据库
```
mysql>use kxyjy_monitoring;
```
3、导入数据库
```
mysql>source /home/user/import.sql;
```
等待完成即可。
##### 5、创建云镜可用性监测2个服务
1、创建云镜平台服务
```
sudo vim /etc/systemd/system/yunjing.service
```
插入如下代码
```
[Unit]
Description=yunjing
[Service]
User=root
Group=root
ExecStart=/home/user/jdk1.8.0_311/bin/java -jar /home/user/kxyjy.jar
[Install]
WantedBy=multi-user.target
```
2、重载系统服务配置
```
$ sudo systemctl daemon-reload
```
3、启动yunjing服务并开机启动
```
$ sudo systemctl enable yunjing.service --now
```
4、创建云镜节点服务
```
sudo vim /etc/systemd/system/yunjing_node.service
```
插入如下代码
```
[Unit]
Description=yunjing_node
[Service]
User=root
Group=root
ExecStart=/home/user/jdk1.8.0_311/bin/java -jar /home/user/AvailabilityMonitoring_Node-1.jar
[Install]
WantedBy=multi-user.target
```
5、重载系统服务配置
```
$ sudo systemctl daemon-reload
```
6、启动yunjing_node服务并开机启动
```
$ sudo systemctl enable yunjing_node.service --now
```
##### 日常维护服务进程
```
$ sudo systemctl start yunjing.service 启动云镜平台
$ sudo systemctl stop yunjing.service 关闭云镜平台
$ sudo systemctl start yunjing_node.service 启动云镜节点
$ sudo systemctl stop yunjing_node.service 关闭云镜节点
```