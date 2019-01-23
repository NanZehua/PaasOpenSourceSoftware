# Nomad 

Nomad是Hashicorp开源的集群管理工具，在Hashicorp的生态链中处于部署工具的位置。  
Nomad的官方网站：https://www.nomadproject.io/  
Nomad的github地址：https://github.com/hashicorp/nomad  

Nomad的是集群管理工具，类似于Mesos，需要一个扩展的任务驱动器，来支持对任务集群的管理。不仅仅支持Docker，同时支持对容器化的、或虚拟化的、或独立的应用程序的集群管理。  
Nomad宣称是全分布式的，目前没有看到其架构图，但据其官网宣称，其二进制文件是统一的，既可以作为Client，也可以作为Server（类似于Manager）。不像Mesos或Kubernetes那样，需要一个额外的Master节点，运行一套额外的Master体系。  

在Nomad中，Client和Server是可以相互转换的。当Client不够时，可以将一个或多个Server降为Client。  
Nomad支持多个数据中心互联，在互联中有一个数据中心的Server对其他数据中心的Server进行连接。具体的互联结构，可以参考Cosul的多数据中心互联结构：https://www.consul.io/docs/internals/architecture.html#10-000-foot-view  
Nomad的集群管理，是基于Serf和Consul来实现的。这两个软件分别是Hashicorp的业务流程工具、服务注册与发现工具。

Nomad与其他各个集群管理工具的比较：
- 与Mesos对比：  
>（1）Nomad的二进制是统一的，即可用作Client，也可用作Server；  
>（2）Nomad各个节点运行的二进制一致，Mesos需要一个额外的协调与存储系统；
>（3）Nomad支持多数据中心，Mesos不支持。  
- 与Kubernetes的比较：  
>（1）Kubernetes主要支持Docker、Rkt等容器；Nomad则可以支持容器化的、虚拟化的、独立的进程集群管理。  
>（2）Kubernetes能支持5000+节点；Nomad也在5000个节点上进行了测试，但比起Kubernetes还稍有不足。 

# Serf

Serf是Hashicorp开源的，提供集群成员关系、服务发现、业务流程功能的工具  
Serf的官方网站：https://www.serf.io   
Serf的github地址：https://github.com/hashicorp/serf  
Serf主要提供以下功能：  
>（1）成员关系：Serf维护集群的成员列表，当成员关系发生变化时，执行一个自定义的脚本  
>（2）故障检测与恢复：Serf会在数秒内检测到故障的节点，并通知其他节点。Serf通过定期重连来尝试恢复故障的节点  
>（3）自定义事件传播：Serf可以向群集广播自定义事件和查询。这些可以用于触发部署，传播配置等。  

Serf使用gossip协议来达成以上功能，gossip协议又称为八卦协议、闲话协议、谣言协议，是一种弱一致性算法。  
Consul也采用了gossip协议，内部是由Serf库提供该协议的支持。  

Serf也能用于服务发现和业务流程，但功能上比Consul更弱。
