# 危险位置

- marven 插件安全
  - 根目录下的 pom.xml
  - 子目录下的 pom.xml

- SQL 操作安全
  - java.sql.Statement
  - java.sql.PrepareStatement
  - 使用第三方 ORM 框架 —— MyBatis 或 Hibernate

- 容易出现SSRF功能点
  - 从指定的 URL 获取内容
  - 数据源连接
  - 后台状态刷新
  - webmail功能(POP3/SMTP/IMAP)
  - 文件处理(加载图片/XML/PDF/ffpmg/ImageMagic)

# 审计流程
## 框架型
权限控制 -> 控制器

对于基于Filter和Servlet实现的简单架构项目，代码审计的重心集中于找出所有的Filter分析其过滤规则，找出是否有做全局的安全过滤、敏感的URL地址是否有做权限校验并尝试绕过Filter过滤。第二点则是找出所有的Servlet，分析Servlet的业务是否存在安全问题,如果存在安全问题是否可以利用？是否有权限访问？利用时是否被Filter过滤等问题，切勿看到Servlet、JSP中的漏洞点就妄下定论，不要忘了Servlet前面很有可能存在一个全局安全过滤的Filter。

