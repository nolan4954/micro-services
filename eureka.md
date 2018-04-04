#### 服务注册与发现
Spring Cloud Starter Eureka (deprecated, please use spring-cloud-starter-netflix-eureka-client)
Eureka can be made even more resilient and available by running multiple instances and asking them to register with each other
The server can be configured and deployed to be highly available, with each server replicating state about the registered services to the others
Since AWS does not yet provide a middle tier load balancer, Eureka fills a big gap in the area of mid-tier load balancing.
AWS Elastic Load Balancer is a load balancing solution for edge services exposed to end-user web traffic. 
 Eureka is also region-isolated in the sense that it does not know about servers in other AWS regions. It's primary purpose of holding information is for load balancing within a region.
 Since Eureka clients have the registry cache information in them, they can operate reasonably well, even when all of the eureka servers go down.
 It doesn't involve any load balancing at all.
 If you want to avoid clients to implement a load balancing strategy (like Ribbon does) you can proxy your services with Zuul who would act as a Load Balancer (using Ribbon and a Eureka Client).
**Eureka fills the need for mid-tier load balancing.**
![](https://github.com/Netflix/eureka/raw/master/images/eureka_architecture.png)

set up:
1. 使用`@EnableEurekaClient` + `spring-cloud-starter-netflix-eureka-server` 或者单纯的 `spring-cloud-starter-netflix-eureka-server`
2. 使用`spring-cloud-starter-netflix-eureka-client` ( By having spring-cloud-starter-netflix-eureka-client on the classpath, your application automatically registers with the Eureka Server.)

问题1 how to keep high availability?

问题2 Using Eureka on AWS

问题3 Running the evict task with compensationTime 5ms？

问题4 renew(续约)，fetch registries(获取注册列表信息) 30s 一次 如果没有及时更新怎么办？
如果由于某种原因导致注册列表信息不能及时匹配，Eureka客户端则会重新获取整个注册表信息。

问题5 eureka, ribbon 结合使用时，到底是谁做了负载均衡