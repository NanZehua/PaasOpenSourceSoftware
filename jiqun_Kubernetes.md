# Kubernetes

Kubernetes是Google开源的容器集群管理系统。

Kubernetes是根据Google的大规模集群管理系统Borg的经验，在社区开源的容器集群管理系统。

Kubernetes的官方网站：https://kubernetes.io/

Kubernetes的github地址：https://github.com/kubernetes/kubernetes

Kubernetes的架构设计：

https://www.kubernetes.org.cn/kubernetes%E8%AE%BE%E8%AE%A1%E6%9E%B6%E6%9E%84 


Kubernetes采用主从结构，分为主节点和工作节点。主节点为管理节点，运行API Server、Scheduler和controller-manager。API Server是整个系统对外的接口，通过RESTful接口与外部交互。Scheduler负责对资源进行调度，分配某个Pod到某个工作节点上。contoller-manager负责管理控制器。

工作节点为实际执行容器的主机或VM，运行kubelet、kube proxy等。kubelet为工作节点上的agent，负责具体的容器生命周期管理，上报容器的运行状态等。Kube Proxy则是为Pod上容器的服务提供外部访问的代理。

Kubernets依赖于ETCD来管理所有节点的状态。

根据Kubernetes的最新文档，在Docker将containerd从Docker Engine剥离出来成为独立项目后，Kubernetes的最新版本支持绕过Docker Daemon，直接使用containerd来管理容器，降低了Kubernetes对Docker的依赖。

