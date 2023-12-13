# 框架 
高度抽取可重用代码的一种设计；高度的通用性

1. Spring
   - 容器(可以管理所有的组件(类))框架
   - 核心关注:IOC和AOP

# 优良特性
- 非侵入式 : 基于Spring开发的应用中的对象可以不依赖于Spring的API
- 依赖注入 : DI--Dependency Injection,反转控制(IOC)最经典的实现
- 面向切面编程 : Aspect Oriented Programming--AOP
- 容器 : Spring是一个容器，因为它包含并且管理应用对象的生命周期
- 组件化 : Spring实现了使用简单的组件配置组合成一个复杂的应用。在Spring中可以使用XML和Java注解组合这些对象
- 一站式 : 在I0C和AOP的基础上可以整合各种企业应用的开源框架和优秀的第三方类库(实际上 Spring 自身也提供了表述层的 SpringMVC 和持久层的 SpringJDBC )

# Spring(IOC和AOP)
![](img\Spring模块架构.png)

- Test ：Spring单元测试模块
- Core Container :核心容器(IOC);黑色代表这部分的功能由哪些jar包组成;要使用这个部分的完整功能，这些jar都需要导入
- AOP+Aspects(面向切面编程模块)
- Instrumentation :设备整合
- Messaging :消息服务
- Data Access/Integration(数据访问和集成)
  - JDBC(数据库操作)
  - ORM(Object Relation Mapping)(对象关系映射)
    - 将数据库的数据查出来封装成一个javabean对象
  - OXM(Object XML Mapping)(对象XML映射)
  - JMS(消息服务)
  - Transactions(tx)(事务)
- WEB :Spring开发WEB应用的模块
  - WebSocket
  - Servlet(和原生Web相关)
  - Web(开发Web项目)
  - Portlet(开发Web应用的组件集成)


开发Spring框架的应用，经常需要写框架的配置文件，写起来复杂，需要提示

# IOC 
Inversion(反转) Of Control: 控制反转
  - 控制:资源的获取方式
    - 主动式:要什么资源都自己创建 (直接new一个，但一些复杂对象的创建是比较庞大的工程)
    - 被动式:资源的获取不是程序员控制，而是交给容器创建和设置

  - 容器:管理所有的组件(有功能的类)

由主动的new资源变为被动的接受资源

DI :(Dependency Injection)依赖注入
  - 容器能知道哪个组件(类)运行的时候，需要另外一个类(组件);容器通过反射的形式，将容器中准备好的对象注入(利用反射给属性赋值)到对象中
  - 只要容器管理的组件，都能使用容器提供的强大功能

以前是自己new对象，现在所有的对象交给容器创建；给容器中注册组件

## 框架编写流程
1. 导包

```xml
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>4.0.6.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>4.0.6.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>4.0.6.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-expression</artifactId>
            <version>4.0.6.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
            <version>1.1.3</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.10</version>
        </dependency>
    </dependencies>
```
2. 写配置

```java
public class Person {
    private String lastName;
    private Integer age;
    private String gender;
    private String email;

    @Override
    public String toString() {
        return "Person{" +
                "lastName='" + lastName + '\'' +
                ", age=" + age +
                ", gender='" + gender + '\'' +
                ", email='" + email + '\'' +
                '}';
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--注册一个Person对象，Spring会自动创建这个Person对象-->
    <!--一个Bean标签可以注册一一个组件(对象、类) 
    class：写要注册的组件的全类名
    name= "lastName":指定属性名
    value="张三”:为这个属性赋值
    -->
    <bean id="person01" class="org.ffffffff0x.Person">
        <property name="lastName" value="sam"/>
        <property name="age" value="18"/>
        <property name="email" value="sam@sam"/>
        <property name="gender" value="man"/>
    </bean>
    
</beans>
```
3. 测试

```java
public class IOCTest {

    /**
     * 存在几个问题
     * 1. src，源码包开始的路径，我们称之为类路径
     *      所有源码包的东西都会被合并放在类路径里面
     *      java:/bin
     *      WEB:/WEB-INF/classes/
     * 2. 导包commons-logging(必要依赖)
     * 3. 先导包在创建配置文件
     */

    /**
     * 1. ApplicationContext(IOC容器接口)
     * 2. 给容器中注册一个组件，我们也从容器中按照ID拿到了这个组件的对象
     *     组件的创建工作是容器完成
     *     容器中对象的创建在容器创建完成的时候就已经创建好了
     * 3. 同一个组件在IOC容器中是单实例的；容器启动完成都已经创建好的
     * 4. 容器中如果没有对应的组件 org.springframework.beans.factory.NoSuchBeanDefinitionException
     * 5. IOC容器创建这个组件对象的时候，会利用setter方法为javaBean的属性赋值
     * 6. javaBean的属性名是由其 getter/setter方法决定的，set去掉后面那一串首字母小写就是属性名
     *     不要乱改getter/setter
     *
     */

    /**
     * 从容器中拿到这个组件
     */
    @Test
    public void test(){
        //ApplicationContext:代表ioc容器
        //ClassPathXmlApplicationContext:当前应用的xml配置文件在ClassPath下
        //根据Spring配置文件得到ioc容器对象
        ApplicationContext ioc = new ClassPathXmlApplicationContext("ioc.xml");
        //容器帮我们创建好对象了
        Person bean = (Person)ioc.getBean("person01");
        System.out.println(bean);
    }
}

```

new ClassPathXMlApplicationContext("ioc.xml") ; ioc容器的配置文件在类路径下;
FileSystemXmlApplicationContext("F://ioc.xml") ; ioc容器的配置文件在磁盘路径下;

