#### 服务提供与消费
ribbon是一个负载均衡客户端，可以很好的控制htt和tcp的一些行为。Feign默认集成了ribbon。
当sercvice-ribbon通过restTemplate调用service-hi的hi接口时，因为用ribbon进行了负载均衡，会轮流的调用service-hi：8762和8763 两个端口的hi接口
RestTemplate+Ribbon去消费服务

to include ribbon:
`spring-cloud-starter-netflix-ribbon`



