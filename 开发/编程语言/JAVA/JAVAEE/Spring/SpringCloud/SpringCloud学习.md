# 服务注册与发现

Eureka: 云端服务发现，一个基于REST的服务，用于定位服务，实现云端中间层服务器发现和故障转移。
Consul: 
Alibaba Nacos: 
Apache ZooKeeper: 

# 分布式配置

Spring Cloud Config：

↓非专门的分布式配置，它们也可以用作服务发现的服务器-------

Consul:
ZooKeeper:
Alibaba Nacos:

# 服务间通信
目前，有三种基于 HTTP 的 Spring 组件可用于服务间的通信，它们都与服务发现进行了集成

同步的 RestTemplate
反应式的 WebClient
声明式的 REST 客户端 OpenFeign

# 断路器

断路器是微服务架构中一个很流行的设计模式。它被设计用来探测失败并封装阻止失败不断重复出现的逻辑。Spring Cloud 提供了一个使用不同断路器的实现。针对 Resilience4J，有两个实现，分别用于反应式应用和非反应式应用。

# API 网关