Swarm、Machine、Compose号称是Docker编排三剑客。

# Swarm

Swarm是Docker原生的集群管理工具  
Swarm的官方文档：https://docs.docker.com/swarm/  
Swarm的github地址：https://github.com/docker/swarm  
Swarm 是典型的 master-slave 结构，通过发现服务来选举 manager。manager 是中心管理节点，各个 node 上运行agent 接受 manager 的统一管理。  

- Swarm对外提供两种API， 一种是Docker API，用于负责容器镜像的生命周期管理， 另外一种是Swarm集群管理CLI，用于集群管理。  
- Scheduler模块，主要实现调度功能。在通过Swarm创建容器时，会经过Scheduler模块选择出一个最优节点，里面包含了两个子模块，分别是Filter和Strategy， Filter用来过滤节点，找出满足条件的节点（比如资源足够，节点正常等等），Strategy用来在过滤出的节点中根据策略选择一个最优的节点（比如对找出的节点进行对比，找到资源最多的节点等等）, 当然Filter/Strategy用户可以定制。  
- Swarm对集群进行了抽象，抽象出了Cluster API，Swarm支持两种集群，一种是Swarm自身的集群，另外一种基于Mesos的集群。  
- LeaderShip模块用于Swarm Manager自身的HA，通过主备方式实现。  
- Discovery Service 服务发现模块，这个模块主要用来提供节点发现功能。  
在每一个节点上，都会有一个Agent，用于连接Discovery Service，上报Docker Daemon的IP端口信息，Swarm Manager会直接从服务发现模块中读取节点信息  


随着Docker Engine 1.12版本的发布，SwarmKit集成于Docker Engine中，独立的Docker Swarm的地位变得越来越尴尬。比上比不过Kubernetes，比下又有SwarmKit可以代替其作用。

# SwarmKit

SwarmKit的官方文档：https://docs.docker.com/engine/swarm/  
SwarmKit的github地址：https://github.com/docker/swarmkit   
SwarmKit是Docker Engine中的一个插件，从Docker Engine 1.12版本开始随Docker Engine一起发布。  
SwarmKit的主要功能特性有：编排、调度、集群管理、安全机制等。  
安装SwarmKit之后，Docker可以工作于普通模式，或集群模式（Swarm Mode）。当工作于集群模式时，Docker节点又可以分为管理节点（Manager Nodes）和工作节点（Worker Nodes）。  
Docker官方推荐使用SwarmKit。当然，由于Docker Swarm已在市场上应用，Docker也仍然在维护Swarm的使用。  

# Compose

Compose的官方文档：https://docs.docker.com/compose/  
Compose的github地址：https://github.com/docker/compose  
Compose是Docker原生的一个编排工具，可以定义和运行多个Docker的应用程序。  
当个Docker容器的运行可以通过一个Dockerfile来定义。但是通常一个业务需要多个容器配合运行才能提高服务。  
Compose可以通过一个docker-compose.yml 的YAML模板文档，来定义多个docker的运行。  

# Machine

Machine的官方文档：https://docs.docker.com/machine/  
Machined的github地址：https://github.com/docker/machine  
Machine是一种可以在多种平台上安装Docker的安装工具。  
例如，你可能需要在个人电脑、服务器、VM、云平台上安装Docker，且Linux有Ubuntu、CentOS、RedHar的各个不同的版本，Machine的作用是，尽量抹平各个不同的HOST/VM、操作系统之间的差异，使得在不同的平台上安装Docker更简单。  
Machine支持在Linux、Windows、Mac上安装Docker。  

在Docker 1.12以前，使用Machine是在Windows和Mac上安装Docker的唯一选择。在Docker 1.12以后，你可以选择Docker for Mac或Docker for Windows。在这两个版本里，集成了Docker Machine和Docker Compose。
