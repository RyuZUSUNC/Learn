## ES7.6.2 链接
[https://www.elastic.co/cn/downloads/past-releases/elasticsearch-7-6-2]

## 步骤

1. 解压缩

```bash
tar -xzvf [ES压缩包]

```

2. 修改配置

```bash
cd /elasticsearch-7.6.2/config

# 修改配置文件
vim ElasticSearch.yml

 cluster.name: [NAME]
 node.name: [NAME]
 network.host: [IP]
 http.port: [PORT]
 discovery.seed_hosts: ["[IP]"]
 cluster.initial_master_nodes: ["[IP]"]

```

3. 启动ES

```bash
cd /elasticsearch-7.6.2/bin
./elasticsearch -d
```

## 问题

1. 用户软硬限制 

报错：

```bash
max file descriptors [4096] for elasticsearch process is too low, increase to at least
```

解决方案:

修改 /etc/security/limits.conf 文件，添加当前用户的限制配置

```bash
# 如当前ES用户为es

vim /etc/security/limits.conf
 # 添加如下两行
 es soft nofile 65535
 es hard nofile 65537
```

2. 虚拟内存限制

报错:

```bash
max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```

解决方案:

修改 /etc/sysctl.conf 中的虚拟内存设置或者使用 sysctl -w vm.max_map_count 临时修改设置参数

```bash
# 1.首先切换至root用户
su - root

# 2.编辑sysctl.conf文件
vim /etc/sysctl.conf

# 3.添加配置
vm.max_map_count=262144

# 4.加载配置
sysctl -p

# 或者可以临时修改参数
sysctl -w vm.max_map_count=262144

# 5.查看修改结果
sysctl -a|grep vm.max_map_count

# 6. 修改完之后需要重启elasticsearch 进入到bin目录下
sh elasticsearch -d
```

3. 高版本不能使用ROOT用户启动

报错:

```
can not run elasticsearch as root
```

解决方案:

```bash
# 添加用户
useradd es

# 设置用户密码
passwd es
 [密码]

# 将ES文件夹权限赋予ES用户
chown -R es [ElasticSearch目录]

# 使用ES用户登入
su es
```