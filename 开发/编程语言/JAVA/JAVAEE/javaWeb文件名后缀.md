# *.do
## .do文件
1. 以do为扩展名的网页文件是java语言写的，以Struts为框架的;它的运行环境是tomcat,weblogic等；通常用的数据库有oracle,mysql,mssql,access等。网页后台程序是*.jsp 或者 struts的组件文件*.do。
2. .do一般是servlet的映射。(即:.do是个请求，不是文件。系统遇到.do的请求后就会提交给某个servlet来处理,这个servlet会根据具体的配置转发给某个后台的程序进行数据处理,然后给数据传递到页面view,最终给页面展现在用户面前,不一定是struts的,这个请求是可以自己随便配置的，你可以配置成.html,这样就是经常看到假静态)
```xml
//.do的请求都交给叫action的servlet处理。
//action根据.do前面东西的不同，在转交给相应的Action类
<servlet-mapping>
	<servlet-name>action</servlet-name>
	<url-pattern>*.do</url-pattern>
<servlet-mapping>
```
3. .do是你在配置文件中配置的一种url模式
当你提交的url地址以.do结尾的话就把它提交到你在配置文件中配置的action中处理。
配置的url模式必须与你提交的url模式一样！这样才能把数据提交的相应的action中处理
4. do文件是一个网页后台程序，没有实体文件，不能直接打开。是servlet的“交换机”，用于将来自web浏览器的请求转到相应的serverpage
5. 开发web应用时有一个必须要写的部署描述文件这个文件描述了你的web应用的配置，包括欢迎页面（welcome pages）（当请求没有指定时，出现在目录下的文件）、servlet（路径或者扩展名）和那些servlets的参数的映射。 在这个文件中，你配置struts actionservlet作为一个操控所有指定映射（通常以.do为扩展名）请求的servlet——这就是“交换机”


# *.do和*.action的区别

struts早期的1版本，以.do为后缀。
同时spring的MVC也是以.do为后缀。
几年前struts收购鼎鼎大名的webwork2和开发团队后，将webwork简单封装，原计划是叫做strutsTi,
后来怕广大struts1的老用户有歧义，改名叫做struts2，并沿用了webwork2的规则，即.action为后缀。
其实struts1和struts2的区别很大，前后没有任何必然联系。

```
　　<servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <!-- 第一种：*.action，访问以.action结尾 由DispatcherServlet进行解析 
　　　　　　　 第二种：/，所以访问的地址都由DispatcherServlet进行解析，对于静态文件的解析需要配置不让DispatcherServlet进行解析 
            　　　　使用此种方式可以实现 RESTful风格的url 
        <url-pattern>*.action</url-pattern>
    </servlet-mapping>
```

