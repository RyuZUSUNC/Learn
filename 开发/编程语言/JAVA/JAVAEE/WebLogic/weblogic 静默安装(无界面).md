# 准备
- Weblogic安装包  --是个jar文件
- java1.8安装包  --如果系统上没装java或版本不对的话

## 本次安装使用
安装版本为12C
- fmw_12.2.1.4.0_wls.jar  --Weblogic安装包
- jdk-8u221-linux-x64.rpm  --jdk安装包

# 安装
## 1.创建Weblogic用户
```
useradd weblogic
passwd weblogic
```
## 2.将安装包传入服务器
手段随意，这里使用的是lrzsz。

本次安装文件夹为weblogic用户的家目录 /home/weblogic

将文件全部置于 /home/weblogic

## 3.安装JDK
详见java-jdk安装

## 4.给文件赋予可读可执行权限并更改所有者
```
chmod 777 fmw_12.2.1.4.0_wls.jar
chown weblogic:weblogic fmw_12.2.1.4.0_wls.jar
```

## 5.创建 oralnst.loc   wls.rsp 文件
```
$:vim oralnst.loc

 

inventory_loc=/home/weblogic/oralnventory

inst_group=weblogic
```

```
$:vim wls.rsp

 

[ENGINE]

Response File Version=1.0.0.0.0

[GENERIC]

ORACLE_HOME=/home/weblogic/Oracle/Middleware

INSTALL_TYPE=WebLogic Server

DECLINE_SECURITY_UPDATES=true

SECURITY_UPDATES_VIA_MYORACLESUPPORT=false
```
更改文件权限和所有者
```
chmod 777 oralnst.loc
chmod 777 wls.rsp
chown weblogic:weblogic oralnst.loc
chown weblogic:weblogic wls.rsp
```
## 6.执行安装
注意文件路径
```
java -jar fmw_12.2.1.4.0_wls.jar -silent -responseFile /home/weblogic/wls.rsp -invPtrLoc /home/weblogic/oralnst.loc
```
安装速度不会很快，等待进度条100并跳回命令行。

## 7.创建域目录并复制wlsd文件到此处
```
mkdir -p /home/weblogic/Oracle/Middleware/user_projects/domains/base_domain/

cp /home/weblogic/Oracle/Middleware/wlserver/common/templates/scripts/wlst/basicWLSDomain.py /home/weblogic/Oracle/Middleware/user_projects/domains/base_domain/
```

## 8.修改wlsd文件
```java
#=======================================================================================
# This is an example of a simple WLST offline configuration script. The script creates 
# a simple WebLogic domain using the Basic WebLogic Server Domain template. The script 
# demonstrates how to open a domain template, create and edit configuration objects, 
# and write the domain configuration information to the specified directory.
#
# This sample uses the demo Derby Server that is installed with your product.
# Before starting the Administration Server, you should start the demo Derby server
# by issuing one of the following commands:
#
# Windows: WL_HOME\common\derby\bin\startNetworkServer.cmd
# UNIX: WL_HOME/common/derby/bin/startNetworkServer.sh
#
# (WL_HOME refers to the top-level installation directory for WebLogic Server.)
#
# The sample consists of a single server, representing a typical development environment. 
# This type of configuration is not recommended for production environments.
#
# Please note that some of the values used in this script are subject to change based on 
# your WebLogic installation and the template you are using.
#
# Usage: 
#      java weblogic.WLST <WLST_script> 
#
# Where: 
#      <WLST_script> specifies the full path to the WLST script.
#=======================================================================================

#=======================================================================================
# Open a domain template.
#=======================================================================================

readTemplate("/home/weblogic/Oracle/Middleware/wlserver/common/templates/wls/wls.jar")

#=======================================================================================
# Configure the Administration Server and SSL port.
#
# To enable access by both local and remote processes, you should not set the 
# listen address for the server instance (that is, it should be left blank or not set). 
# In this case, the server instance will determine the address of the machine and 
# listen on it. 
#=======================================================================================

cd('Servers/AdminServer')
set('ListenAddress','')
设置域端口>>> set('ListenPort', 7001)

create('AdminServer','SSL')
cd('SSL/AdminServer')
set('Enabled', 'True')
set('ListenPort', 7002)

#=======================================================================================
# Define the user password for weblogic.
#=======================================================================================

cd('/')
用户名>>>cd('Security/base_domain/User/weblogic')
# Please set password here before using this script, e.g. cmo.setPassword('value')
新增 设置密码>>> cmo.setPassword('root1234')
#=======================================================================================
# Create a JMS Server.
#=======================================================================================

cd('/')
create('myJMSServer', 'JMSServer')

#=======================================================================================
# Create a JMS System resource. 
#=======================================================================================

cd('/')
create('myJmsSystemResource', 'JMSSystemResource')
cd('JMSSystemResource/myJmsSystemResource/JmsResource/NO_NAME_0')

#=======================================================================================
# Create a JMS Queue and its subdeployment.
#=======================================================================================

myq=create('myQueue','Queue')
myq.setJNDIName('jms/myqueue')
myq.setSubDeploymentName('myQueueSubDeployment')

cd('/')
cd('JMSSystemResource/myJmsSystemResource')
create('myQueueSubDeployment', 'SubDeployment')

#=======================================================================================
# Create and configure a JDBC Data Source, and sets the JDBC user.
#=======================================================================================

cd('/')
create('myDataSource', 'JDBCSystemResource')
cd('JDBCSystemResource/myDataSource/JdbcResource/myDataSource')
create('myJdbcDriverParams','JDBCDriverParams')
cd('JDBCDriverParams/NO_NAME_0')
set('DriverName','org.apache.derby.jdbc.ClientDriver')
set('URL','jdbc:derby://localhost:1527/db;create=true')
set('PasswordEncrypted', 'PBPUBLIC')
set('UseXADataSourceInterface', 'false')
create('myProps','Properties')
cd('Properties/NO_NAME_0')
create('user', 'Property')
cd('Property/user')
cmo.setValue('PBPUBLIC')

cd('/JDBCSystemResource/myDataSource/JdbcResource/myDataSource')
create('myJdbcDataSourceParams','JDBCDataSourceParams')
cd('JDBCDataSourceParams/NO_NAME_0')
set('JNDIName', java.lang.String("myDataSource_jndi"))

cd('/JDBCSystemResource/myDataSource/JdbcResource/myDataSource')
create('myJdbcConnectionPoolParams','JDBCConnectionPoolParams')
cd('JDBCConnectionPoolParams/NO_NAME_0')
set('TestTableName','SYSTABLES')

#=======================================================================================
# Target resources to the servers. 
#=======================================================================================

cd('/')
assign('JMSServer', 'myJMSServer', 'Target', 'AdminServer')
assign('JMSSystemResource.SubDeployment', 'myJmsSystemResource.myQueueSubDeployment', 'Target', 'myJMSServer')
assign('JDBCSystemResource', 'myDataSource', 'Target', 'AdminServer')

#=======================================================================================
# Write the domain and close the domain template.
#=======================================================================================

setOption('OverwriteDomain', 'true')
域目录>>> writeDomain('/home/weblogic/Oracle/Middleware/user_projects/domains/base_domain')
closeTemplate()

#=======================================================================================
# Exit WLST.
#=======================================================================================

exit()

```
修改行数
```
129，141，143，214
```

## 9.执行创建域
```
/home/weblogic/Oracle/Middleware/oracle_common/common/bin/wlst.sh  basicWLSDomain.py
```

## 10.防火墙通过端口
```
firewall-cmd --zone=public --add-port=7001/tcp --permanent
```

## 11.启动weblogic
回到域目录下执行
```
./startWebLogic.sh
```

## 》附加《

创建一个链接文件用于快速启动weblogic
```
ln -s  /home/weblogic/Oracle/Middleware/user_projects/domains/base_domain/startWebLogic.sh startWeblogic
```

7001 端口