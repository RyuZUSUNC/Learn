## 下载
http://kafka.apache.org/downloads

## 解压
```sh
tar zxvf kafka_2.12-2.3.0.tgz -C ./
```

## 自定义目录
首先新建kafka的日志目录和zookeeper数据目录，因为这两项默认放在tmp目录，而tmp目录中内容会随重启而丢失,所以我们自定义以下目录
```
mkdir /root/kafka_2.13-2.8.1/zookeeper        #创建zookeeper数据目录
mkdir /root/kafka_2.13-2.8.1/log              #创建日志目录
mkdir /root/kafka_2.13-2.8.1/log/zookeeper    #创建zookeeper日志目录
mkdir /root/kafka_2.13-2.8.1/log/kafka        #创建kafka日志目录
```

## 启动ZooKeeper
可以新启动单独的也可以使用 kafka bin 目录下的启动脚本 以下为 kafka 自带 zookeeper 配置

```
./zookeeper-server-start.sh ../config/zookeeper.properties 
```

集群环境下修改配置
```
# 修改为自定义的zookeeper数据目录
dataDir=/root/kafka_2.13-2.8.1/zookeeper

# 修改为自定义的zookeeper日志目录
dataLogDir=/root/kafka_2.13-2.8.1/log/zookeeper

# 端口
clientPort=2181

# 注释掉
# maxClientCnxns=0

# 设置连接参数，添加如下配置
#为zk的基本时间单元，毫秒
tickTime=2000
#Leader-Follower初始通信时限 tickTime*10
initLimit=10
#Leader-Follower同步通信时限 tickTime*5
syncLimit=5

#设置broker Id的服务地址
server.0=10.16.105.91:2888:3888
server.1=10.16.105.92:2888:3888
server.2=10.16.105.93:2888:3888
```

在各台服务器的zookeeper数据目添加myid文件，写入服务broker.id属性值

例如上述配置就在 10.16.105.91 的 /root/kafka_2.13-2.8.1/zookeeper 目录下执行

```bash
echo 0 > myid
```

## 在config目录下配置集群
进入 config 目录 修改 server.properties 文件内容

1. broker.id 
如果配置多台集群需要修改此项，每台的 ID 不能相同

2. isteners
默认被注释，修改为 listeners=PLAINTEXT://本机ip:9092

3. zookeeper.connect
指定zookeeper连接地址，改为zookeeper服务器地址，默认为zookeeper.connect=localhost:2181

## 启动kafka
进入 bin 目录

```
sh kafka-server-start.sh -daemon ../config/server.properties
#查看zookeeper
ps -ef|grep zookeeper
```

可以进入 logs 目录查看日志是否报错

```
tail -f server.log
```

## 启动完成后可以查看zookeeper集群连接情况
> 在不使用kafka自带zookeeper，单独启动zookeeper的情况下
进入 zookeeper bin 目录

```sh
sh zkCil.sh

#查看 执行
ls /

#查看连接情况
ls /brokers/ids
```

可以看到链接上去的 kafka 的 broker.id 

## 使用命令新建 topic
进入 kafka bin 目录

```sh
sh kafka-topics.sh --create --zookeeper 127.0.0.1:2181 --replication-factor 1 --partitions 1 --topic test
sh kafka-topics.sh --create --bootstrap-server 192.168.61.129:9092 --replication-factor 1 --partitions 1 --topic test

 #说明
 #192.168.88.137:2181  ###这是zookeeper服务ip+端口号
 #test ###这是topic
```

## 配置SSL
创建证书脚本

```bash
#!/bin/bash

################################## 设置环境变量   ##############################
BASE_DIR=/home/SHcert # SSL各种生成文件的基础路径
CERT_OUTPUT_PATH="$BASE_DIR/certificates" # 证书文件生成路径
PASSWORD=shenghui!@!123 # 密码
KEY_STORE="$CERT_OUTPUT_PATH/kafka.keystore"   # Kafka keystore文件路径
TRUST_STORE="$CERT_OUTPUT_PATH/kafka.truststore" # Kafka truststore文件路径
KEY_PASSWORD=$PASSWORD # keystore的key密码
STORE_PASSWORD=$PASSWORD # keystore的store密码
TRUST_KEY_PASSWORD=$PASSWORD  # truststore的key密码
TRUST_STORE_PASSWORD=$PASSWORD # truststore的store密码
CLUSTER_NAME=kafka-cluster	# 指定别名
CERT_AUTH_FILE="$CERT_OUTPUT_PATH/ca-cert" # CA证书文件路径
CLUSTER_CERT_FILE="$CERT_OUTPUT_PATH/${CLUSTER_NAME}-cert" # 集群证书文件路径
DAYS_VALID=3650 # key有效期
DNAME="CN=IDS, OU=Yanfabu, O=Shenghui, L=Nantong, ST=Jiangsu, C=CN"  # distinguished name
##############################################################################

mkdir -p $CERT_OUTPUT_PATH

echo "1. 创建集群证书到keystore......"
keytool -keystore $KEY_STORE -alias $CLUSTER_NAME -validity $DAYS_VALID -genkey -keyalg RSA \
-storepass $STORE_PASSWORD -keypass $KEY_PASSWORD -dname "$DNAME"

echo "2. 创建CA......"
openssl req -new -x509 -keyout $CERT_OUTPUT_PATH/ca-key -out "$CERT_AUTH_FILE" -days "$DAYS_VALID" \
-passin pass:"$PASSWORD" -passout pass:"$PASSWORD" \
-subj "/C=CN/ST=Jiangsu/L=Nantong/O=Shenghui/CN=IDS"

echo "3. 导入CA文件到truststore......"
keytool -keystore "$TRUST_STORE" -alias CARoot \
-import -file "$CERT_AUTH_FILE" -storepass "$TRUST_STORE_PASSWORD" -keypass "$TRUST_KEY_PASS" -noprompt

echo "4. 从key store中导出集群证书......"
keytool -keystore "$KEY_STORE" -alias "$CLUSTER_NAME" -certreq -file "$CLUSTER_CERT_FILE" -storepass "$STORE_PASSWORD" -keypass "$KEY_PASSWORD" -noprompt

echo "5. 签发证书......"
openssl x509 -req -CA "$CERT_AUTH_FILE" -CAkey $CERT_OUTPUT_PATH/ca-key -in "$CLUSTER_CERT_FILE" \
-out "${CLUSTER_CERT_FILE}-signed" \
-days "$DAYS_VALID" -CAcreateserial -passin pass:"$PASSWORD"

echo "6. 导入CA文件到keystore......"
keytool -keystore "$KEY_STORE" -alias CARoot -import -file "$CERT_AUTH_FILE" -storepass "$STORE_PASSWORD" \
 -keypass "$KEY_PASSWORD" -noprompt

echo "7. 导入已签发证书到keystore......"
keytool -keystore "$KEY_STORE" -alias "${CLUSTER_NAME}" -import -file "${CLUSTER_CERT_FILE}-signed" \
 -storepass "$STORE_PASSWORD" -keypass "$KEY_PASSWORD" -noprompt
```

需要JDK自带的 keytool 工具运行，运行完后会在脚本目录下的 certificates 文件夹下生成如下文件

```
ca-cert  
ca-cert.srl  
ca-key  
kafka-cluster-cert  
kafka-cluster-cert-signed  
kafka.keystore  
kafka.truststore
```

配置 server.properties 配置文件添加以下项目

```
############################# SSL Settings #############################

listeners=SSL://localhost:9095
advertised.listeners=SSL://localhost:9095
ssl.keystore.location=/home/SHcert/certificates/kafka.keystore
ssl.keystore.password=shenghui!@!123
ssl.key.password=shenghui!@!123
ssl.truststore.location=/home/SHcert/certificates/kafka.truststore
ssl.truststore.password=shenghui!@!123

ssl.client.auth=required
ssl.enabled.protocols=TLSv1.2,TLSv1.1,TLSv1
ssl.keystore.type=JKS 
ssl.truststore.type=JKS 
ssl.endpoint.identification.algorithm=HTTPS
security.inter.broker.protocol=SSL
```

## Kafka Shell 基本命令

**创建kafka topic**

```sh
sh bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic t_cdr --partitions 30  --replication-factor 2
```
>注： partitions指定topic分区数，replication-factor指定topic每个分区的副本数

- partitions分区数:
  - partitions ：分区数，控制topic将分片成多少个log。可以显示指定，如果不指定则会使用broker(server.properties)中的num.partitions配置的数量
  - 虽然增加分区数可以提供kafka集群的吞吐量、但是过多的分区数或者或是单台服务器上的分区数过多，会增加不可用及延迟的风险。因为多的分区数，意味着需要打开更多的文件句柄、增加点到点的延时、增加客户端的内存消耗。
  - 分区数也限制了consumer的并行度，即限制了并行consumer消息的线程数不能大于分区数
  - 分区数也限制了producer发送消息是指定的分区。如创建topic时分区设置为1，producer发送消息时通过自定义的分区方法指定分区为2或以上的数都会出错的；这种情况可以通过alter –partitions 来增加分区数。

- replication-factor副本
  - replication factor 控制消息保存在几个broker(服务器)上，一般情况下等于broker的个数。
  - 如果没有在创建时显示指定或通过API向一个不存在的topic生产消息时会使用broker(server.properties)中的default.replication.factor配置的数量

**查看所有topic列表**

```sh
sh bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --list
```

**查看指定topic信息**

```sh
sh bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --describe --topic t_cdr
```

**控制台向topic生产数据**

```sh
sh bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic t_cdr
```

**控制台消费topic的数据**

```sh
sh bin/kafka-console-consumer.sh  --bootstrap-server 127.0.0.1:9092  --topic t_cdr --from-beginning
```

**查看topic某分区偏移量最大（小）值**

```sh
sh bin/kafka-run-class.sh kafka.tools.GetOffsetShell --topic hive-mdatabase-hostsltable  --time -1 --broker-list 127.0.0.1:9092 --partitions 0
```
>注： time为-1时表示最大值，time为-2时表示最小值

**增加topic分区数**

为topic t_cdr 增加10个分区

```sh
sh bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092  --alter --topic t_cdr --partitions 10
```

**删除topic**
**慎用，只会删除zookeeper中的元数据，消息文件须手动删除**

```sh
sh bin/kafka-run-class.sh kafka.admin.DeleteTopicCommand --bootstrap-server 127.0.0.1:9092 --topic t_cdr
```

**查看topic消费进度**

这个会显示出consumer group的offset情况， 必须参数为--group， 不指定--topic，默认为所有topic

Displays the: Consumer Group, Topic, Partitions, Offset, logSize, Lag, Owner for the specified set of Topics and Consumer Group

```
sh bin/kafka-run-class.sh kafka.tools.ConsumerOffsetChecker

required argument: [group] 
Option Description 
------ ----------- 
--broker-info Print broker info 
--group Consumer group. 
--help Print this message. 
--topic Comma-separated list of consumer 
   topics (all topics if absent). 
--zkconnect ZooKeeper connect string. (default: localhost:2181)

Example,

sh bin/kafka-run-class.sh kafka.tools.ConsumerOffsetChecker --group pv

Group           Topic              Pid Offset   logSize    Lag    Owner 
pv              page_visits        0   21       21         0      none 
pv              page_visits        1   19       19         0      none 
pv              page_visits        2   20       20         0      none
```

以上图中参数含义解释如下：
- topic：创建时topic名称
- pid：分区编号
- offset：表示该parition已经消费了多少条message
- logSize：表示该partition已经写了多少条message
- Lag：表示有多少条message没有被消费。
- Owner：表示消费者

细看kafka-run-class.sh脚本，它是调用 了ConsumerOffsetChecker的main方法，所以，我们也可以通过java代码来访问scala的ConsumerOffsetChecker类，代码如下：

```java
import kafka.tools.ConsumerOffsetChecker;  
  
/** 
 * kafka自带很多工具类，其中ConsumerOffsetChecker能查看到消费者消费的情况, 
 * ConsumerOffsetChecker只是将信息打印到标准的输出流中 
 * 
 */  
public class RunClass  {  
    public static void main(String[] args)  {  
        //group-1是消费者的group名称,可以在zk中  
        String[] arr = new String[]{"--zookeeper=192.168.199.129:2181,192.168.199.130:2181,192.168.199.131:2181/kafka","--group=group-1"};  
        ConsumerOffsetChecker.main(arr);  
    }  
}  
```

