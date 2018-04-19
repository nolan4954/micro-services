1. Zuul is a JVM-based router and server-side load balancer from Netflix.
2. Some of the API Gateways (Zuul 1, Ngnix) are blocking, and others (Zuul 2, Linkerd, Envoy) are non-blocking. Blocking architectures are good for simple development and tracing the requests, but blocking nature can cause scalability problems. Non-blocking architectures are more complex in terms of development and traceability but they are better in terms of scalability and resiliency. 
3. The proxy uses Ribbon to locate an instance to which to forward through discovery
4. zuul 路由eureka-client时，怎么做到负载均衡的，一会儿8562，一会儿8563，是eureka做到的嘛？
5. If you need your routes to have their order preserved, you need to use a YAML file,as the ordering is lost when using a properties file. The following example shows such a YAML file
6. management:
  endpoint:
    routes:
      enabled: true 不生效？ /routes接口 /routes?format=details