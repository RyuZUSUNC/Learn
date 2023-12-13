## 下载
https://downloads.apache.org/zookeeper

## 解压
```sh
tar -zxvf apache-zookeeper-3.5.7-bin.tar.gz -C ./
```

## 复制zoo_sample.cfg文件
进入conf目录下，复制zoo_sample.cfg文件，名字为zoo.cfg (不然启动找不到该文件)

```sh
cd ./apache-zookeeper-3.5.7-bin/conf
cp zoo_sample.cfg ./zoo.cfg
```

## 启动服务
进入 bin 目录

```sh
#启动
sh zkServer.sh start
```
> /usr/bin/java
> ZooKeeper JMX enabled by default
> Using config: /root/apache/zookeeper3.8.0/bin/../conf/zoo.cfg
> Starting zookeeper ... STARTED

```
#查看启动状态
sh ./zkServer.sh status
```

> /usr/bin/java
> ZooKeeper JMX enabled by default
> Using config: /root/apache/zookeeper3.8.0/bin/../conf/zoo.cfg
> Client port found: 2181. Client address: localhost. Client SSL: false.
> Mode: standalone
