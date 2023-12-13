# Spring Boot中使用HTTPS步骤

1. 要有一个SSL证书，证书怎么获取呢？买（通过证书授权机构购买）或者自己生成（通过keytool生成）。

2. 在spring boot中启用HTTPS

3. 将HTTP重定向到HTTPS（可选）

# 获取SSL证书

有两种方式可以获取到SSL证书：

1. 自己通过keytool生成；

2. 通过证书授权机构购买；

Keytool是java提供的证书生成工具，如果配置了java_home的，直接就可以在控制台进行生成了：

```
keytool -genkey -alias tomcat -dname "CN=Andy,OU=kfit,O=kfit,L=HaiDian,ST=BeiJing,C=CN" -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 365
```

这里解释下命令的各个参数的含义：

```
-genkey ：生成key；

-alias ：key的别名；

-dname：指定证书拥有者信息

-storetype ：密钥库的类型为JCEKS。常用的有JKS(默认),JCEKS(推荐),PKCS12,BKS,UBER。每个密钥库只可以是其中一种类型。

-keyalg ：DSA或RSA算法(当使用-genkeypair参数)，DES或DESede或AES算法(当使用-genseckey参数)；

-keysize ：密钥的长度为512至1024之间(64的倍数)

-keystore ：证书库的名称

-validity ： 指定创建的证书有效期多少天

dname的值详解：

CN(Common Name名字与姓氏)

OU(Organization Unit组织单位名称)

O(Organization组织名称)

L(Locality城市或区域名称)

ST(State州或省份名称)

C(Country国家名称）
```

# Spring Boot中启用HTTPS

默认情况下Spring Boot内嵌的Tomcat服务器会在8080端口启动HTTP服务，Spring Boot允许在application.properties中配置HTTP或HTTPS，但是不可同时配置，如果两个都启动，至少有一个要以编程的方式配置，Spring
Boot官方文档建议在application.properties中配置HTTPS，因为HTTPS比HTTP更复杂一些

在application.properties中配置HTTPS，配置信息如下：

```yaml
#https端口号.
server.port: 443
#证书的路径.
server.ssl.key-store: classpath:keystore.p12
#证书密码，请修改为您自己证书的密码.
server.ssl.key-store-password: 123456
#秘钥库类型
server.ssl.keyStoreType: PKCS12
#证书别名
server.ssl.keyAlias: tomcat
```