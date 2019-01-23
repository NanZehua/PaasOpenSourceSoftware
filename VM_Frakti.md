# Frakti

Frakti是在Kubernetes中进行虚拟化管理的另一种思路，目前挂在Kubernetes名下。  
Frakti的github地址：https://github.com/kubernetes/frakti  
Frakti是通过HyperContainer来实现，基于CRI机制，在hypervisor上运行容器和Pod。  

Frakti与其他Linux容器运行时相比：  
>（1）安全性与隔离性更好。Frakti为在Pod层次上提供硬件虚拟化；  
>（2）内核不共享。每个Pod都有自己的Linux内核。并且已有一个简单内核的LinuxKit在开发；  
>（3）支持混合运行时。可以在同一个节点上，同时运行HyperContainer和Docker;  
>（4）持久化存储。Frakit可以将块设备直接映射到Pod的VM中。  

比较  
综合比较Kubevirt、Virtlet、Frakti三个项目：  
>（1）Kubevirt三个月处于alpha状态，现在还是处于alpha状态，发展最慢。且Kubevirt使用的是TPR机制，将Kubernetes 1.9被抛弃，需要迁移到CRD机制。  
>（2）Virtlet三个月先是pre-alpha，现在是pre-release状态，发展比Kubevirt快，但不如Frakti。使用的是Kubentes的CRI机制。  
>（3）Frakti挂在Kuberentes Group下，目前已发布Release v1.0，发展最快。使用的也是Kubernetes的CRI机制，在Kubernetes中运行HyperContainer。处于Kubernetes开发团队下，发展前景最好。但是HyperContainer是走的在VM上运行Docker镜像的路线，对于在VM上运行VM镜像的方式，不知道未来有没有处理。  
