# 密码设置

## CONFIG SET requirepass password 设置密码
```bash
127.0.0.1:6379> CONFIG set requirepass chentaobao  #设置密码
OK
127.0.0.1:6379> quit    #退出客户端
>redis-cli                    #重新链接客户端
127.0.0.1:6379> setnx dd1 ddf3      #设置一个字符串
(error) NOAUTH Authentication required.    #错误返回，需要认证
127.0.0.1:6379> auth chen    #开始认证
(error) ERR invalid password        #密码错误了，因为是chentaobao
127.0.0.1:6379> auth chentaobao      #密码正确
OK
127.0.0.1:6379> setnx dd 1123
(integer) 1
127.0.0.1:6379> CONFIG set requirepass ""      #清空密码
OK
127.0.0.1:6379> config get requirepass    #查看密码
1) "requirepass"
2) ""
```

>如果进行过主从设置，主服务器进行了密码设置后，会导致从服务器无法进行同步。
注意，这样的密码设置会在Redis 重启后失效

## 修改配置文件
1. Redis的配置文件默认在/etc/redis.conf，找到如下行

```
requirepass foobared
```

去掉前面的注释，并修改为所需要的密码。

```
requirepass [myPassword]
```

2. 重启Redis

3. 登录验证

```bash
redis-cli -h 127.0.0.1 -p 6379 -a myPassword

or

redis-cli -h 127.0.0.1 -p 6379
127.0.0.1:6379> auth myPassword    #认证密码
OK
```

注意：使用命令行客户端配置密码，重启Redis后仍然会使用redis.conf配置文件中的密码。

4. 在Redis集群中使用认证密码

如果Redis服务器，使用了集群。除了在master中配置密码外，也需要在slave中进行相应配置。在slave的配置文件中找到如下行，去掉注释并修改与master相同的密码即可：

```
masterauth master-password
```

