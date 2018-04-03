#### 微服务学习笔记
spring cloud 为开发人员提供了快速构建分布式系统的一些工具，包括配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等

1. 微服务提倡devops，自动部署。可以用不同的语言。自己修改；自己弹性伸缩。 运维成本比较高。
设计原则： 单一指责原则（高内聚低耦合）；服务自治原则
2. dubbo springcloud 
snapshot 快照版本（开发版本）
3. Ribbon是客户端侧的负载均衡；RestTemplate是封装好了。 feign声明似的请求接口（负载均衡实用了ribbon)
4. 如果调用失败，就会有雪崩效应,线程阻塞.如果依赖的项目down掉了，会不会挂掉。（1. 超时机制；2.断路器,有忍耐度的，返回默认值，空值)
5. 社区活跃度；STOMP, AMQP协议


问题1 Ribbon使用时 There was an unexpected error (type=Internal Server Error, status=500).
No instances available for EUREKA-CLIENT-TEST1
要增加
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```
问题2 starter与netflix的区别是？
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```
问题3 Feign使用时java.lang.IllegalStateException: Service id not legal hostname (/EUREKA-CLIENT-TEST1)
去除"/" @FeignClient(value = "/EUREKA-CLIENT-TEST1")

问题4 Feign使用时Caused by: java.lang.IllegalStateException: PathVariable annotation was empty on param 0.
指定 name String sayHelloFeign(@PathVariable("name") String name);

问题4 Feign使用时 Unregistering JMX-exposed beans on shutdown
加入
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```
问题5 Feign使用时 启动太慢！而且普通的Rest接口是404；也没注册到eureka中；Running the evict task with compensationTime 0ms

