# 优点
 - 快速创建独立运行的Speing项目与主流框架集成
 - 使用嵌入式的Servlet容器
 - starters自动依赖与版本控制
 - 大量自动配置，简化开发，也可以手动修改
 - 无需配置XML，无代码生成，开箱即用
 - 准生产环境的运行时应用监控
 - 与云计算的天然集成

# 入门
## 简介
 - 简化Spring应用开发的一个框架
 - 整合整个Spring技术栈
 - J2EE开发的一站式解决方案

## 微服务
 - 是一种架构风格
   - 一个应用应该是一组小型服务，可以通过HTTP的方式进行互通
   - 每一个功能元素最终都是一个可独立替换和独立升级的软件单元

## Spring Boot HelloWorld
功能：
浏览器发送hello亲求，服务器接受请求并处理，响应Hello World字符串

1. 创建一个maven工程
2. 导入SpringBoot依赖 (Spring initializr也行)
3. 编写一个主程序，启动Spring Boot应用
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

/**
 * @SpringBootApplication 标注一个主程序类，说明这是一个SPring Boot应用
 */

@SpringBootApplication
public class SpringbootLearnApplication {

    public static void main(String[] args) {

        //启动Spring应用
        SpringApplication.run(SpringbootLearnApplication.class, args);
    }
}
```

4. 编写相关的 Controllr/Service

例:
```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World!";
    }
}
```

5. 运行主程序测试

注：主程序必须位于所有控制器的最上父目录or程序根目录

6. 简化部署

直接maven打包

插件为:
```xml
 <build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-marven-plugin</artifactId>
        <plugin>
    <plugins>
 <build>
```

## Hello World探究
### 父项目
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.10.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

它的父项目
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-dependencies</artifactId>
		<version>1.5.10.RELEASE</version>
		<relativePath>../../spring-boot-dependencies</relativePath>
	</parent>
  它来真正管理Spring Boot应用中所有依赖版本
```
Spring Boot的版本仲裁中心
以后导入依赖默认是不需要写版本(没有在dependencies里面管理的依赖自然需要声明版本号)

#### 导入的依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

`spring-boot-starter`-`web`
- spring-boot-starter:spring-boot场景启动器，帮我们导入了web模块正常运行所依赖的组件；

Spring Boot将所有的功能场景都抽取出来，做成一个个的starters(启动器)，只需要在项目里面引入这些starter相关场景的所有依赖都会导入进来。要用什么功能就导入什么场景的启动器。

### 主程序类
```java
/**
 * @SpringBootApplication 标注一个主程序类，说明这是一个SPring Boot应用
 */

@SpringBootApplication
public class SpringbootLearnApplication {

    public static void main(String[] args) {

        //启动Spring应用
        SpringApplication.run(SpringbootLearnApplication.class, args);
    }
}
```
@SpringBootApplication : springboot应用，标注在某个类上说明这个类式SpringBoot的主配置类，SpringBoot就应该运行这个类的main方法来启动SpringBoot应用;

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {
```
@SpringBootConfiguration : Spring Boot的配置类
- 标注在某个类上，表示这是一个Spring Boot的配置类;
- @Configuration : 配置类上标注这个注解;
  - 配置类 ---- 配置文件;配置类也是容器中的一个组件;@Component

@EnableAutoConfiguration : 开启自动配置功能
- 以前需要配置的东西，Spring Boot自动配置，@EnableAutoConfiguration 告诉SpringBoot开启自动配置功能;这样自动配置才能生效;

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@Import({Registrar.class})
public @interface AutoConfigurationPackage {
```

@AutoConfigurationPackage : 自动配置包
- @Import({Registrar.class}) Spring的底层注解，给容器中导入一个组件;导入的组件由 AutoConfigurationPackages.Registrar.class，将主配置类(@SpringBootApplication标注的类)的所在包及下面所有子包里面的所有组件扫描到Spring容器。

@Import({EnableAutoConfigurationImportSelector.class})
- EnableAutoConfigurationImportSelector : 导入那些组件的选择器
- 将所有需要导入的组件以全类名的方式返回;这些组件机会被添加到容器中
- 会给容器中导入非常多的自动配置类(xxxAutoConfiguration);就是给容器中导入这个场景需要的所有组件，并配置好这些组件
- 有了自动配置类，免去了我们手动编写配置注入功能组件等的工作
- SptingBoot启动的时候从类路径下的META-INF/spring.factories中获取EnableAutoConfiguration指定的值，将这些值作为自动配置类导入到容器中，然后自动配置类就生效了，帮我们进行自动配置工作。以前我们需要自己配置的东西，自动配置类都帮我们配置了

## 使用Spring initializr 快速创建Spring boot项目

IDE都支持使用Spring的项目创建向导快速创建一个SpringBoot项目

选择需要的模块;向导会联网创建SpringBoot项目;

默认生成的SpringBoot项目
- 主程序已经生成好了，只需要编写逻辑
- resources文件夹中目录结构
  - static:保存所有的静态资源;js css img
  - templayes:保存所有的模板页面;(SpringBoot默认jar包使用嵌入式的Tomcat，默认不支持JSP页面);可以使用模板引擎(freemarker,thymeleaf)
  - application.properties ： SpringBoot应用的配置文件

# SpringBoot配置
## 配置文件
SpringBoot使用一个全局的配置文件，配置文件的文件名是固定的
- application.properties
- application.yml

配置文件的作用:修改SpringBoot自动配置的默认值;

yml是YAML(YAML Ain't Markup Language)语言的文件，以数据为中心，更适合作为配置文件

以前的配置文件，大多使用的都是xml文件

YAML:配置例子
```yaml
server:
 port: 8081
```

## YAML语法
### 基本语法
k:(空格)v:表示一堆键值对(v前面有空格)
以空格的缩进来控制层级关系;只要是左对齐的一列数据都是同一个层级的

例子:
```yaml
server:
    port: 8081
    path: /hello
```
属性和值也是大小写敏感;

### 值的写法
字面量: 普通的值(数字，字符串，布尔)
- `k:(空格)v`:字面直接来写;字符串默认不用加上单引号或者双引号
  - ""：双引号不会转义字符串里面的特殊字符;特殊字符会作为本身想表示的意思
    - 例子 name: "z \n ls" :输出: z 换行 ls
  - '':单引号会转义特殊字符，特殊字符最终只是一个普通的字符串数据
    - 例子 name: 'z \n ls' :输出: z \n ls

对象(属性和值)(键值对)
- `k:(空格)v`:在下一行来写对象的属性和值的关系，注意缩进
  - 对象还是k: V的方式
    - 例子：

```yaml
friends: 
    lastName: zhangsan
    age: 20
```

另一种行内写法
```yaml
friends:{lastname: zhangsan,age: 18}
```

数组(List,Set)：
- 用`-(空格)值`表示数组中的一个元素
  - 例子：

```yaml
pets:
 - cat
 - dog
 - pig
```

行内写法
```yaml
pets: [cat,dog,pig]
```

## 配置文件值注入
配置文件
```yaml
person:
  lastName: zhangsan
  age: 18
  boss: false
  birth: 2020/10/01
  maps: {k1: v1,k2: 12}
  lists:
    - lisi
    - zhaoliu
  dog:
    name: dd
    age: 4
```

javaBean
```java
/**
 * 将配置文件中配置的每一个属性的值映射到这个组件中
 * @ConfigurationProperties:告诉SpringBoot将本类中所有属性和配置文件中相关的配置进行绑定
 *      prefix = "person":配置文件中那项的所有属性进行一一映射
 *
 *  只有这个组建是容器中的组件，才能使用容器提供的@ConfigurationProperties功能
 * @ConfigurationProperties(prefix = "person")默认从全局配置文件中获取值
 * 
 */
@Component //加入容器
@ConfigurationProperties(prefix = "person")
public class Person {
    private String lastName;
    private Integer age;
    private Boolean boss;
    private Date Birth;

    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```

可以导入配置文件处理器，之后编写配置就有提示了
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

.properties等效写法
```
# idea，properties配置文件默认使用的是utf-8，设置中修改
person.last-nmae=圣骑
person.age=10
person.birth=2020/1/1
person.boss=false
person.maps.k1=v1
person.maps.k2=12
person.lists=a,b,c
person.dog.name=dog
person.dog.age=15
```
使用@Value获取值示例
```java
/**
 * 等效于Spring中的配置
 * <bean class="Person">
 *      <property name="lastName" value="字面量/${key}从环境变量，配置文件中获取值/#{SpEL}"></property>
 * </bean>
 */
@Value("${person.last-nmae}")
private String lastName;
@Value("#{11*23}")
private Integer age;
@Value("true")
private Boolean boss;
```

### @ConfigurationProperties获取值与@Value获取值比较
-                  | @ConfigurationProperties  | @Value
-|-|-
功能               | 批量注入配置文件中的属性     | 一个个绑定
松散绑定(松散语法)  | 支持                       | 不支持
SpEL              | 不支持                      | 支持
JSR3030数据校验    | 支持                       | 不支持
复杂类型封装       | 支持                       | 不支持

如果只是在某个业务逻辑中需要获取一下配置文件中的某项值，使用@Value

如果专门编写了一个javaBean来和配置文件进行映射，就直接使用@ConfigurationProperties

### @PropertySource & @ImportResource

@PropertySource : 加载指定的配置文件
```java
/**
 * 将配置文件中配置的每一个属性的值映射到这个组件中
 * @ConfigurationProperties:告诉SpringBoot将本类中所有属性和配置文件中相关的配置进行绑定
 *      prefix = "person":配置文件中那项的所有属性进行一一映射
 *
 *  只有这个组建是容器中的组件，才能使用容器提供的@ConfigurationProperties功能
 */
@Component
@PropertySource(value = {"classpath:Person.properties"})
@ConfigurationProperties(prefix = "person")
public class Person {
    /**
     * 等效于Spring中的配置
     * <bean class="Person">
     *      <property name="lastName" value="字面量/${key}从环境变量，配置文件中获取值/#{SpEL}"></property>
     * </bean>
     */
//    @Value("${person.last-nmae}")
    private String lastName;
//    @Value("#{11*23}")
    private Integer age;
//    @Value("true")
    private Boolean boss;
    private Date Birth;

    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```

@ImportResource : 导入Spring的配置文件，让配置文件里面的内容生效

SpringBoot里面没有Spring的配置文件，我们自己编写的配置文件，也不能自动识别
，想让Spring的配置文件生效，加载，要将 @ImportResource 标注在一个配置类上

```java
//导入一个配置文件并生效
@ImportResource(locations = {"classpath:beans.xml"})
@SpringBootApplication
public class SpringBootConfigApplication {
```

不编写Spring的配置文件了
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="helloService" class="com.ffffffff0x.springbootconfig.service.HelloService"></bean>
</beans>
```


SpringBoot推荐给容器中添加组件的方式:推荐使用全注解的方式

1. 配置类======Spring配置文件
2. 使用@Bean给容器中添加组件
```java
/**
 * @Configuration 指名当前类是一个配置类，来替代之前的Spring配置文件
 *
 * 在配置文件中用<bean></bean>标签添加组件
 */
@Configuration
public class MyAppConfig {

    //将方法的返回值添加到容器中，容器中这个组件默认的ID就是方法名
    @Bean
    public HelloService helloService(){
        System.out.println("配置类@Bean给容器中添加组件了");
        return new HelloService();
    }
}
```

## 配置文件占位符
### 1. 随机数
```java
${random.value}
${random.int}
${random.long}
${random.int(10)}
${random.int[1024,65536]}
```
### 2. 占位符获取之前配置的值，如果没有可以使用`:`指定默认值
```properties
person.last-nmae=圣骑${random.uuid}
person.age=${random.int}
person.birth=2020/1/1
person.boss=false
person.maps.k1=v1
person.maps.k2=12
person.lists=a,b,c
person.dog.name=${person.last-nmae}_dog
person.dog.age=15
```

## Profile
### 1. 多Profile文件
在主配置文件编写的时候，文件名可以是 application-{profile}.properties/yaml

默认使用application.properties的配置

### 2. yml支持多文档块方式
```
server:
  port: 8080

spring:
  profiles:
    active: dev
---
server:
  port: 8088
spring:
  profiles: dev
---
server:
  port: 8089
spring:
  profiles: prod

---
```

### 3. 激活指定Profile
1. 在配置文件中指定 spring.profiles.active=dev
2. 命令行:
   1. 在运行时修改程序参数(Program arguments)为 --spring.profile.active=[]
   2. 在Shell中运行Jar包时加上 --spring.profile.active=[]
   3. 在运行时修改虚拟机参数(VM options)加上 --Dspring.profile.active=[]

## 配置文件的加载位置

SpringBoot 启动时会扫描以下位置的 application.properties或者 application.yml文件作为SpringBoot的默认配置文件

- file:./config/
- file:./
- classpath:/config/
- classpath:/

优先级由高到低，高优先级的配置会覆盖低优先级的配置

SpringBoot会从这四个位置全部加在主配置文件，互补配置

`还可以通过 spring.config.location 来改变默认的配置文件位置`

项目打包好以后，我们可以使用命令行参数的形式，启动项目的时候来制定配置文件的新位置；指定配置文件和默认加载的这些配置文件共同起作用形成互补配置

```java
java -jar [jar包] --spring.config.location=[path]
```

## 外部配置的加载顺序
SpringBoot也可以从以下位置加载配置，按照优先级从高到低，高优先级的配置覆盖低优先级的配置，所有的配置形成互补配置
1. 命令行参数
如
```java
java -jar [jar包] --server.port=8085
```
多个配置用空格分开

2. 来自java:copm/env的JNDI属性
3. Java系统属性(System.getProperties())
4. 操作环境系统变量
5. RandomValuePropertySource配置的ramdom.*属性值

优先加载带profile再加载不带profile，由jar包外向jar包内进行寻找，包外配置直接放置在jar包同目录下

6. jar包外部的application-{profile}.properties或application.yml(带spring.profile)配置文件
7. jar包内部的application-{profile}.properties或application.yml(带spring.profile)配置文件
8. jar包外部的application.properties或application.yml(不带spring.profile)配置文件
9.  jar包内部的application.properties或application.yml(不带spring.profile)配置文件

10. @Configuration注解类上的@PropertySource
11. 通过SoringApplication.setDefaultPropertie指定的默认属性

## 自动配置原理

1. SpringBoot 启动的时候加载主配置类，开启了自动配置的功能`@EnableAutoConfiguration`
2. `@EnableAutoConfiguration` 作用
   - V2.3.4 利用AutoConfigurationImportSelector给容器中导入一些组件
   - 可以查看selectImports()方法的内容
     - springboot2.0的selectImports()内容被封装在了getAutoConfigurationEntry()中
   - `List<String> configurations = this.getCandidateConfigurations(annotationMetadata, attributes);`//获取候选的配置
     - SpringFactoriesLoader.loadFactoryNames()
     - 扫描所有jar包类路径下的 META-INF/spring.factories
     - 把扫描到的这些文件的内容包装成Properties对象
     - 从properties中获取到的EnableAutoConfiguration.class类(类名)对应的值，然后把他们添加在容器中

将类路径下 META-INF/spring.factories 里面配置的所有EnableAutoConfiguration的值加入到了容器中
```java
org.springframework.boot.autoconfigure.admin.SpringApplicationAdminJmxAutoConfiguration,\
org.springframework.boot.autoconfigure.aop.AopAutoConfiguration,\
org.springframework.boot.autoconfigure.amqp.RabbitAutoConfiguration,\
org.springframework.boot.autoconfigure.batch.BatchAutoConfiguration,\
org.springframework.boot.autoconfigure.cache.CacheAutoConfiguration,\
org.springframework.boot.autoconfigure.cassandra.CassandraAutoConfiguration,\
org.springframework.boot.autoconfigure.context.ConfigurationPropertiesAutoConfiguration,\
org.springframework.boot.autoconfigure.context.LifecycleAutoConfiguration,\
org.springframework.boot.autoconfigure.context.MessageSourceAutoConfiguration,\
......
```

每一个这样的xxxAutoConfiguration类都是容器中的一个组件，都加入到容器中，用他们来做自动配置

3. 每一个自动配置类进行自动配置功能
4. 用一个类HttpEncodingAutoConfiguration来解释
```java
@Configuration(
    proxyBeanMethods = false
)//表示这是一个配置类，以前编写的配置文件一样，也可以给容器中添加组件
@EnableConfigurationProperties({ServerProperties.class})//启动指定类的ConfigurationProperties功能;
@ConditionalOnWebApplication(
    type = Type.SERVLET
)//Spring底层@Conditional注解，根据不同的条件，如果满足指定的条件，整个配置类里面的配置就会生效；判断当前是否是WEB应用，如果是，当前配置类生效
@ConditionalOnClass({CharacterEncodingFilter.class})//判断当前项目有没有这个类CharacterEncodingFilter；SpringMVC中进行乱码解决的过滤器
@ConditionalOnProperty(
    prefix = "server.servlet.encoding",
    value = {"enabled"},
    matchIfMissing = true
)//判断配置文件中是否存在某个配置 如server.servlet.encoding；如果不存在，判断也是成立的
//及时我们配置文件中不配置server.servlet.encoding，也是默认生效
public class HttpEncodingAutoConfiguration {
```
根据当前不同条件判断，决定这个配置类是否生效



精髓：
1. springboot 启动会加载大量的自动配置类
2. 看我们需要的功能有没有springboot默认写好的自动配置类
3. 再来看这个自动配置类中到底配置了哪些组件(只要有要用的组件，就不需要再来配置了)
4. 给容器中自动配置类添加组件的时候，会从properties中获取某些属性。我们就可以在配置文件中指定这些属性的值。

### 细节
1. @Conditional派生注解(Spring注解版派生的@Conditional作用)
作用: 必须是@Conditional指定的条件成立，才给容器中添加组件，配置类里面的所有内容才生效。

@Conditional扩展注解              | 作用(判断是否满足当前指定条件)
-|-
@ConditionalOnJava               | 系统的java版本是否符合要求
@ConditionalOnBean               | 容器中存在指定Bean;
@ConditionalOnMissingBean        | 容器中不存在指定Bean;
@ConditionalOnExpression         | 满足SpEL表达式指定
@ConditionalOnClass              | 系统中有指定的类
@ConditionalOMissingClass        | 系统中没有指定的类     
@ConditionalOnSingleCandidate    | 容器中只有一个指定的Bean ,或者这个Bean是首选Bean  
@ConditionalOnProperty           | 系统中指定的属性是否有指定的值              
@ConditionalOnResource           | 类路径下是否存在指定资源文件    
@ConditionalOnWebApplication     | 当前是web环境          
@ConditionalOnNotWebApplication  | 当前不是web环境
@ConditionalOnIndi               | JNDI存在指定项    

`自动配置类必须在一定的条件下才能生效`

如何知道哪些自动配置类生效了。 

可以通过启用 debug = true属性，让控制台自动答应配置报告，这样就可以很方便的知道那些自动配置类生效。