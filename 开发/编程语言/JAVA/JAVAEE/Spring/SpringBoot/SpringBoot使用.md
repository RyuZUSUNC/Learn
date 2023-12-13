# 第一个SpringBoot应用
源码目录结构：

```
src/main/java
└── com
    └── itranswarp
        └── learnjava
            ├── Application.java
            ├── entity
            │   └── User.java
            ├── service
            │   └── UserService.java
            └── web
                └── UserController.java
```

在存放源码的`src/main/java`目录中，Spring Boot对Java包的层级结构有一个要求。注意到我们的根package是`com.itranswarp.learnjava`，下面还有`entity`、`service`、`web`等子package。Spring Boot要求`main()`方法所在的启动类必须放到根package下，命名不做要求，这里我们以`Application.java`命名，它的内容如下：

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) throws Exception {
        SpringApplication.run(Application.class, args);
    }
}
```

启动Spring Boot应用程序只需要一行代码加上一个注解`@SpringBootApplication`，该注解实际上又包含了：

- @SpringBootConfiguration
  - @Configuration
- @EnableAutoConfiguration
  - @AutoConfigurationPackage
- @ComponentScan

这样一个注解就相当于启动了自动配置和自动扫描。

再观察pom.xml，它的内容如下：

```xml
<project ...>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.0.RELEASE</version>
    </parent>

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.itranswarp.learnjava</groupId>
    <artifactId>springboot-hello</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <java.version>11</java.version>
        <pebble.version>3.1.2</pebble.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>

        <!-- 集成Pebble View -->
        <dependency>
            <groupId>io.pebbletemplates</groupId>
            <artifactId>pebble-spring-boot-starter</artifactId>
            <version>${pebble.version}</version>
        </dependency>

        <!-- JDBC驱动 -->
        <dependency>
            <groupId>org.hsqldb</groupId>
            <artifactId>hsqldb</artifactId>
        </dependency>
    </dependencies>
</project>
```

使用Spring Boot时，强烈推荐从`spring-boot-starter-parent`继承，因为这样就可以引入Spring Boot的预置配置。

紧接着，我们引入了依赖`spring-boot-starter-web`和`spring-boot-starter-jdbc`，它们分别引入了Spring MVC相关依赖和Spring JDBC相关依赖，无需指定版本号，因为引入的`<parent>`内已经指定了，只有我们自己引入的某些第三方jar包需要指定版本号。这里我们引入`pebble-spring-boot-starter`作为View，以及`hsqldb`作为嵌入式数据库。`hsqldb`已在`spring-boot-starter-jdbc`中预置了版本号`2.5.0`，因此此处无需指定版本号。

根据`pebble-spring-boot-starter`的文档，加入如下配置到`application.yml`：

```yaml
pebble:
  # 默认为".pebble"，改为"":
  suffix:
  # 开发阶段禁用模板缓存:
  cache: false
```

对`Application`稍作改动，添加`WebMvcConfigurer`这个Bean：

```java
@SpringBootApplication
public class Application {
    ...

    @Bean
    WebMvcConfigurer createWebMvcConfigurer(@Autowired HandlerInterceptor[] interceptors) {
        return new WebMvcConfigurer() {
            @Override
            public void addResourceHandlers(ResourceHandlerRegistry registry) {
                // 映射路径`/static/`到classpath路径:
                registry.addResourceHandler("/static/**")
                        .addResourceLocations("classpath:/static/");
            }
        };
    }
}
```

现在就可以直接运行`Application`，启动后观察Spring Boot的日志：

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.3.0.RELEASE)

2020-06-08 08:47:23.152  INFO 32585 --- [           main] com.itranswarp.learnjava.Application     : Starting Application on xxx with PID 32585 (...)
2020-06-08 08:47:23.154  INFO 32585 --- [           main] com.itranswarp.learnjava.Application     : No active profile set, falling back to default profiles: default
2020-06-08 08:47:24.224  INFO 32585 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2020-06-08 08:47:24.235  INFO 32585 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2020-06-08 08:47:24.235  INFO 32585 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.35]
2020-06-08 08:47:24.309  INFO 32585 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2020-06-08 08:47:24.309  INFO 32585 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1110 ms
2020-06-08 08:47:24.446  WARN 32585 --- [           main] com.zaxxer.hikari.HikariConfig           : HikariPool-1 - idleTimeout is close to or more than maxLifetime, disabling it.
2020-06-08 08:47:24.448  INFO 32585 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2020-06-08 08:47:24.753  INFO 32585 --- [           main] hsqldb.db.HSQLDB729157DF9B.ENGINE        : checkpointClose start
2020-06-08 08:47:24.754  INFO 32585 --- [           main] hsqldb.db.HSQLDB729157DF9B.ENGINE        : checkpointClose synched
2020-06-08 08:47:24.759  INFO 32585 --- [           main] hsqldb.db.HSQLDB729157DF9B.ENGINE        : checkpointClose script done
2020-06-08 08:47:24.763  INFO 32585 --- [           main] hsqldb.db.HSQLDB729157DF9B.ENGINE        : checkpointClose end
2020-06-08 08:47:24.767  INFO 32585 --- [           main] com.zaxxer.hikari.pool.PoolBase          : HikariPool-1 - Driver does not support get/set network timeout for connections. (feature not supported)
2020-06-08 08:47:24.770  INFO 32585 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2020-06-08 08:47:24.971  INFO 32585 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2020-06-08 08:47:25.130  INFO 32585 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-06-08 08:47:25.138  INFO 32585 --- [           main] com.itranswarp.learnjava.Application     : Started Application in 2.68 seconds (JVM running for 3.097)
```

