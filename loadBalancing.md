在分布式系统中，负载均衡（Load Balancing）是一种将任务分派到多个服务端进程的方法
主要两个目的：
1. 将任务通过负载分摊到不同进程中，以减少单一进程的负载，达到处理能力水平扩容的目的。（高并发）
2. 提高容错能力。（高可用）
集群：在多台不同的服务器中部署相同的服务进程，通过负载均衡对外提供服务，这组进程也称为集群。


《大型网站技术架构——核心原理与案例分析》

当网站的访问量大了就会考虑负载均衡，这也是每一个架构师的基本功了，其基本地位就相当于相声里的说学逗唱，活好不好就看这个了 :)
上面讲到根服务器拥有一切域名的起始解释权，但是如果你去问根服务器它是不会直接告诉你最终答案的。因为如果它要存储所有的记录，那它也太累了，这个负载和开销是惊人的。那它会告诉你什么呢？它会告诉你应该去问谁，也就是它授权下一级服务器来解答你的问题


负载均衡之DNS域名解析
事实上，大型网站总是部分使用DNS域名解析，利用域名解析作为第一级负载均衡手段，即域名解析得到的一组服务器并不是实际提供服务的物理服务器，而是同样提供负载均衡服务器的内部服务器，这组内部负载均衡服务器再进行负载均衡，请请求发到真实的服务器上，最终完成请求。

六大Web负载均衡原理与实现：
1. http重定向；
2. dns负载均衡，一个域名对应多个ip
3. 反向代理负载均衡
4. IP负载均衡(LVS-NAT)
5. 直接路由(LVS-DR)
6. IP隧道(LVS-TUN)