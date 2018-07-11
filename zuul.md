1. Zuul is a JVM-based router and server-side load balancer from Netflix.
2. Some of the API Gateways (Zuul 1, Ngnix) are blocking, and others (Zuul 2, Linkerd, Envoy) are non-blocking. Blocking architectures are good for simple development and tracing the requests, but blocking nature can cause scalability problems. Non-blocking architectures are more complex in terms of development and traceability but they are better in terms of scalability and resiliency. 
3. The proxy uses Ribbon to locate an instance to which to forward through discovery
4. zuul 路由eureka-client时，怎么做到负载均衡的，一会儿8562，一会儿8563，是eureka做到的嘛？
5. If you need your routes to have their order preserved, you need to use a YAML file,as the ordering is lost when using a properties file. The following example shows such a YAML file
6. Zuul provides a framework to dynamically read, compile, and run these filters        

7. 可以用ribbon做客户端负载均衡  since all routes are wrapped in Hystrix commands by default

问题1.  /routes接口 404  /routes接口 /routes?format=detailsa

#management:
#  endpoints:
#    web:
#      exposure:
#        include: ["*"]

问题2. Rewriting Location header   


问题3. zuul只是可动态加载filter的fiter集合框架？？
即使做路由也是使用filter的方式，去读取配置文件，做动态路由。
spring cloud netflix 是在整合了 netflix的项目。估计新增了很多东西。

问题4. 能支撑多大的量呢？？
Spring Cloud Zuul处理每个请求的方式是针对每个请求是用一个线程来处理。PS，根据统计数据目前Zuul最多能达到（1000-2000)QPS
Zuul的转发通过ribbon实现，ribbon的客户端负载均衡在初始化的时候比较忙，这个初始化就是预热

一般来说，如果需要在请求到达后端应用前就进行处理的话，会选择前置过滤器，例如鉴权、请求转发、增加请求参数等行为。在请求完成后需要处理的操作放在后置过滤器中完成，例如统计返回值和调用时间、记录日志、增加跨域头等行为。

ZuulServlet: service
    ZuulRuner: preRoute
        FilterProcessor: runFilters("pre")
            FilterLoader: getFiltersByType
            FilterLoader: processZuulFilter
                ZuulFilter: runFilter
                    自定义Filter: run

    ZuulRuner: route
        FilterProcessor: runFilters("route")

    ZuulRuner: postRoute
        FilterProcessor: runFilters("post")

