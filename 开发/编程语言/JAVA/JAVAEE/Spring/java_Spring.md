# 装配Bean

## XML装配
我们需要编写一个特定的application.xml配置文件，告诉Spring的IoC容器应该如何创建并组装Bean：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="userService" class="com.itranswarp.learnjava.service.UserService">
        <property name="mailService" ref="mailService" />
    </bean>

    <bean id="mailService" class="com.itranswarp.learnjava.service.MailService" />
</beans>
```

每个<bean ...>都有一个id标识，相当于Bean的唯一ID；

在userServiceBean中，通过<property name="..." ref="..." />注入了另一个Bean；

Bean的顺序不重要，Spring根据依赖关系会自动正确初始化。

把上述XML配置文件用Java代码写出来，就像这样：

```java
UserService userService = new UserService();
MailService mailService = new MailService();
userService.setMailService(mailService);
```
只不过Spring容器是通过读取XML文件后使用反射完成的。

如果注入的不是Bean，而是boolean、int、String这样的数据类型，则通过value注入，例如，创建一个HikariDataSource：

```xml
<bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource">
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test" />
    <property name="username" value="root" />
    <property name="password" value="password" />
    <property name="maximumPoolSize" value="10" />
    <property name="autoCommit" value="true" />
</bean>
```

最后一步，需要创建一个Spring的IoC容器实例，然后加载配置文件，让Spring容器为我们创建并装配好配置文件中指定的所有Bean，这只需要一行代码：

```java
ApplicationContext context = new ClassPathXmlApplicationContext("application.xml");
```

接下来，就可以从Spring容器中“取出”装配好的Bean然后使用它：

```java
// 获取Bean:
UserService userService = context.getBean(UserService.class);
// 正常调用:
User user = userService.login("bob@example.com", "password");
```

## 注解装配
