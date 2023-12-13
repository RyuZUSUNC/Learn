# 功能
- 接收客户端的访问
- 向客户端做出反应
- 可以把动态资源换成静态资源，再发送给服务器

# 工作原理
- 连接 建立socket文件
- 请求 浏览器通过socket文件向服务器发出请求
- 应答 运用HTTP协议把请求传输到WEB服务器处理，然后运用HTTP协议再传回浏览器
- 关闭连接 应答完成后关闭连接

# 种类和介绍
- Apache
- IIS
- JBoss
- LIGHTTPD
- NGINX
    ## IIS
        - 微软组织提供的的WEB网页服务组件，包括WEB,FTP,NTTP,SMTP服务器，分别用于网页浏览，文件传输，新闻服务和邮件发送等方面。
    ## Tomcat
        - Apache组织提供的一种WEB服务器，提供对JSP和Servlet的支持，是一个轻量级Java Web容器也是当前应用最广的Java Web服务器。
    ## Lighttpd
        - 具有非常低的内存开销，CPU占用低,效能好，以及丰富的模块。支持FastCGI,CGI,Auth，输出压缩，URL重写，Alias等重要功能。
    ## Nginx
        - 十分轻量级的，高新能的HTTP和反向代理服务器，同时也是一个IMAP/POP3/SMTP代理服务器。Nginx一事件驱动的方式便携，所以有非常好的性能，同时也是一个非常高效的反向代理，负载平衡。
    ## JBoss
        - 一个遵从J2EE规范的，开放源代码的，纯JAVA的EJB服务器，对于J2EE有很好的支持。
        