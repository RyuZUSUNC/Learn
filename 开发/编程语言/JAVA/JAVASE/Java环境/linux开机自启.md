# centos7

1. 写执行jar包命令的脚本

在任意目录下新建一个.sh文件。
注意：两句export必须加，否则无法启动jar包，Java命令会执行失败
java -jar -Xms256m -Xmx256m /publicServer/eureka/eureka-server-0.0.1-SNAPSHOT.jar >/publicServer/eureka/log.log &
/publicServer/eureka/eureka-server-0.0.1-SNAPSHOT.jar:换成你自己的jar包绝对路径
/publicServer/eureka/log.log：换成你自己的日志输出绝对路径

```bash
#!/bin/bash
export JAVA_HOME=/kxyjy/jdk1.8.0_311
export PATH=$JAVA_HOME/bin:$PATH
nohup java -jar /kxyjy/kxyjy.jar > /dev/null 2>&1 & 
nohup java -jar /kxyjy/AvailabilityMonitoring_Node-1.jar > /dev/null 2>&1 & 
```

2. 添加可执行权限

```bash
chmod u+x xxx/xxx/xx.sh
```

执行此命令为你的脚本赋予可执行权限

3. 添加开机自启

```bash
vi /etc/rc.d/rc.local
```

在最后一行添加你的脚本的绝对路径

```bash
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
/root/DBYJ/DBYJ_Start.sh
```

4. 设置rc.local 可执行权限

centos7下rc.local的权限被降低，需要手动为其赋予可执行权限

```bash
chmod u+x /etc/rc.d/rc.local
```

5. reboot重启下服务器看下结果，是否自动启动了jar包