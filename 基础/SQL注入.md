# 介绍
- SQL叫做结构化查询语言。查看结构化数据有MySQL，MSSQL，Oracle等。
- 所谓SQL注入，就是通过把SQL命令插入到WEB表单提交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令 。这些输入大都是SQL语法里的一些组合，通过执行SQL语句进而执行攻击者所要的操作，其主要原因是程序没有细致地过滤用户输入的数据，致使非法数据侵入系统。
- 具体来说，他是利用现有应用程序，将（恶意）的SQL命令注入到后台数据库引擎执行的能力，他可以通过在WEB表单中输入（恶意）SQL语句得到一个存在安全漏洞的网站上的数据库，而不是按照设计者的意图去执行SQL语句。

# 注入原理
- SQL注入是从正常的WWW端口访问，而且表面看起来跟一般的WEB页面访问没什么区别，所以目前市面的防火墙都不会对SQL注入发出警报，如果管理员没查看IIS日志的习惯，可能被入侵很长时间都不会发觉。但是,SQL注入的手法相当灵活，在诸如的时候会碰到很多意外的情况，需要构造巧妙的SQL语句，从而成功获取想要的数据。
- 根据相关技术原理，SQL注入可以分为平台层注入和代码层注入。前者有不安全的数据库配置或数据库平台的漏洞所致；后者主要是有程序员对输入未进行细致地过滤，从而执行了非法的数据查询。

# 注入方法
- 当应用程序使用输入内容来构造动态SQL语句以访问数据库时，会发生SQL注入攻击。
- 如果代码使用存储过程，而且这些存储过程作为包含未筛选的用户输入的字符串来传递，也会发生SQL注入。
- SQL注入可能导致攻击者使用应用层隔行徐登陆在数据库中执行命令。相关的SQL注入可以通过测试工具pangolin进行。
- 如果应用程序使用特权过高的账户连接到数据库，这种问题会变得很严重，就可以提交一段数据库查询的代码，根据程序返回的接过，获得一些敏感的信息或者控制整个服务器。
