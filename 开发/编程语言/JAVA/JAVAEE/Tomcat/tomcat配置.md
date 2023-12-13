# 官网下载zip包
http://tomcat.apache.org/

# 启动与关闭
找到目录bin下的
- startup.bat   //点击启动Tomcat
- shutdown.bat  //关闭Tomcat。

# 环境变量设置
- 变量名：CATALINA_BASE
    - 变量值：C：\\....       //Tomcat安装目录
- 变量名：CATALINA_HOME
    - 变量值：C：\\....       //Tomcat安装目录

## 在PATH/CLASSPATH中添加
%CATALINA_HOME%\bin;
%CATALINA_HOME%\lib

## CMD运行验证
```
startup
```

# 乱码问题
## 修改Tomcat配置文件，增加UTF-8编码

更改Tomcat的conf文件夹下的service.xml配置，增加URIEncoding="UTF-8"，具体如下：
```xml
<Connector port="8080" protocol="HTTP/1.1" ​ connectionTimeout="20000" ​ redirectPort="8443" URIEncoding="UTF-8"/>
```
无效

## 修改tomcat的conf下的logging.properties中的参数

将
- java.util.logging.ConsoleHandler.encoding = UTF-8

改为
- java.util.logging.ConsoleHandler.encoding = GBK
