# 简介
- Webshell，顾名思义：Web指的是在Web服务器上，而Shell是用脚本语言编写的脚本程序。
- Webshell就是以asp，php，jsp或者是cgi等网页文件形式存在的一种命令执行环境，可以对web服务器进行操作的权限，也可以说是一种网页后门。
- Webshell一般是被网站管理员用于网站管理，服务器管理等等一些用途，但是由于功能比较强打，可以上传下载文件，查看数据库，省直可以调用一些服务器上系统的相关命令，通常被黑客利用。
- 黑客在入侵一个网站后，通过一些上传方式会将ASP或PHP后门文件与网站服务器WEB目录下正常的网页混在一起，将自己编写的Webshell上传到web服务器的页面目录下，然后通过页面访问的形式进行入侵，或者通过插入一句话连接本地的一些相关工具直接对服务器进行入侵操作已达到控制网站服务器的目的。

# 上传方式
- 解析漏洞上传
    - IIS目录解析漏洞，文件解析漏洞，文件名解析，Apache解析漏洞
- 截断上传
    - 在上传的时候，用NC或者berpsuite抓到表单，将数据可以直接编辑截断等
- 后台数据库备份
    - 在一些企业的后台管理系统中，里面有意向功能是备份数据库可以上传图片一句话木马，然后利用数据库备份功能，将图片木马被分为ASP等其他内容可以被解析为脚本语句的格式，然后在通过web访问就可以执行木马了
-利用数据库语句上传
    - 前提必须是该网站有相应的注入点，而且当前用户必须要有上传的权限，而且必须有当前网页在服务器下的绝对路劲。

# 作用
- 站长网站管理，服务器管理等，根据文件对象(FSO)权限不同，可以在线编辑网页脚本，上传下载文件，查看数据库，执行任意程序命令等
- 被入侵者利用然后控制网站，这些网页脚本常称为WEB脚本木马，asp或PHP木马比较流行，也有基于.net脚本木马和JSP脚本木马。

# 种类
- Webshell根据脚本可以分为PHP脚本木马，ASP脚本木马，也有基于.NET和JSP脚本木马。在国外，还有用python脚本语言写的动态网页，当然也有与之相关的Webshell。根据功能也分为大马和小马，小马通常指一句话木马。
- webshell可以穿越服务器防火墙，并且使用webshell一般不会在系统日志中留下记录，只会在网站的WEB日志中留下一些数据提交记录，没有经验的管理员是很难看出入侵痕迹的。

# 使用
- 利用上传漏洞可以直接上传一句话木马。然后使用中国菜刀连接。

