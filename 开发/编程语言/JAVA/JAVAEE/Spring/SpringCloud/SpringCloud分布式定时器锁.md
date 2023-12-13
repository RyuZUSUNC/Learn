# ShedLock

`ShedLock`是一个在分布式环境中使用的定时任务框架，用于解决在分布式环境中的多个实例的相同定时任务在同一时间点重复执行的问题。`ShedLock`确保计划的任务最多同时执行一次。如果一个任务正在一个节点上执行，它会获得一个锁，该锁将阻止从另一个节点（或线程）执行同一任务。请注意，如果一个任务已经在一个节点上执行，则在其他节点上的执行不会等待，只是将其跳过。。简单来说，**ShedLock本身只做一件事情：保证一个任务最多同时执行一次。所以如官网所说的，ShedLock不是一个分布式调度器，只是一个锁!**

> ShedLock支持Mongo，Redis，Hazelcast，ZooKeeper以及任何带有JDBC驱动程序的东西。本例子使用的是基于Redis的方式。之所以不适用基于jdbc存储的主要原因是考虑到大量数据下的数据库压力的原因，若本身基于jdbc等，可直接参考官网给出的提示：https://github.com/lukas-krecan/ShedLock#jdbctemplate. 创建对应的表结构。

```sql
CREATE TABLE shedlock(
    name VARCHAR(64), 
    lock_until TIMESTAMP(3) NULL, 
    locked_at TIMESTAMP(3) NULL, 
    locked_by  VARCHAR(255), 
    PRIMARY KEY (name)
)
```

# maven 依赖
```xml
       <dependency>
            <groupId>net.javacrumbs.shedlock</groupId>
            <artifactId>shedlock-spring</artifactId>
            <version>2.3.0</version>
        </dependency>
        <dependency>
            <groupId>net.javacrumbs.shedlock</groupId>
            <artifactId>shedlock-provider-redis-spring</artifactId>
            <version>2.3.0</version>
        </dependency>
        
        <!--spring2.0集成redis所需common-pool2 -->
        <!-- 必须加上，jedis依赖此 若项目中已经引入jedis 请忽略此步骤-->
        <!-- spring boot 2.0 的操作手册有标注 大家可以去看看 地址是：https://docs.spring.io/spring-boot/docs/2.0.3.RELEASE/reference/htmlsingle/ -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
        </dependency>
```

添加jedis 依赖 若项目中已经引入jedis 请忽略此步骤

```xml
        <!--spring2.0集成redis所需common-pool2 -->
        <!-- 必须加上，jedis依赖此 若项目中已经引入jedis 请忽略此步骤-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
        </dependency>
```

# SchedulerLock 基于 Redis 的配置

配置 lockProvider 并且开启 @EnableSchedulerLock 标签

```java
import net.javacrumbs.shedlock.core.LockProvider;
import net.javacrumbs.shedlock.provider.redis.spring.RedisLockProvider;
import net.javacrumbs.shedlock.spring.annotation.EnableSchedulerLock;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;

/**
 * @Description SchedulerLock 基于 Redis 的配置
 * @Date 2020/2/22 18:27
 **/
@Configuration
//defaultLockAtMostFor 指定在执行节点结束时应保留锁的默认时间使用ISO8601 Duration格式
//作用就是在被加锁的节点挂了时，无法释放锁，造成其他节点无法进行下一任务
//这里默认55s
//关于ISO8601 Duration格式用的不到，具体可上网查询下相关资料，应该就是一套规范，规定一些时间表达方式
@EnableSchedulerLock(defaultLockAtMostFor = "PT55S")
public class ShedLockRedisConfig {

    @Value("${spring.profiles.active}")
    private String env;

    @Bean
    public LockProvider lockProvider(RedisConnectionFactory connectionFactory) {
        //环境变量 -需要区分不同环境避免冲突，如dev环境和test环境，两者都部署时，只有一个实例进行，此时会造成相关环境未启动情况
        return new RedisLockProvider(connectionFactory, env);
    }
}
```

# 在启动类中添加 @EnableScheduling 标签

注意，要在启动类上添加 @EnableScheduling ，表明开启定时器服务。若不加定时器是不会起效的。

```java
@SpringBootApplication
@EnableScheduling
public class EpidemicMessageApplication {

    public static void main(String[] args) {
        SpringApplication.run(EpidemicMessageApplication.class, args);
    }

}
```

# test 测试案例

```java
    //区分服务
    @Value("${server.port}")
    private String port;
    
    @Scheduled(cron = "0 */1 * * * ?")
    /**
     * lockAtLeastForString的作用是为了防止在任务开始之初由于各个服务器同名任务的服务器时间差，启动时间差等这些造成的一些问题，有了这个时间设置后，
     *     就可以避免因为上面这些小的时间差造成的一些意外，保证一个线程在抢到锁后，即便很快执行完，也不要立即释放，留下一个缓冲时间。
     *     这样等多个线程都启动后，由于任务已经被锁定，其他没有获得锁的任务也不会再去抢锁。注意这里的时间不要设置几秒几分钟，尽量大些
     *lockAtMostForString 这个设置的作用是为了防止抢到锁的那个线程，因为一些意外死掉了，而锁又始终不被释放。
     *     这样的话，虽然当前执行周期虽然失败了，但以后的执行周期如果这里一直不释放的话，后面就永远执行不到了。
     *     它的目的不在于隐藏任务，更重要的是，释放锁，并且查找解决问题。
     *至于是否带有string后缀，只是2种表达方式，数字类型的就是毫秒数，字符串类型的就有自己固定的格式 ，例如：PT30S  30s时间设置，单位可以是S,M,H
     */
    @SchedulerLock(name = "scheduledController_notice", lockAtLeastForString = "PT15M", lockAtMostForString = "PT14M")
    public StandardResult notice() {
        try {
            logger.info(port + "- 执行定时器 scheduledController_notice");
            return StandardResult.ok();
        } catch (Exception e) {
            logger.error("异常信息:", e);
            return StandardResult.faild("异常信息", e);
        }
    }
```