# Virtlet  

Virtlet也是Kubernetes上的VM管理方案，目前处于pre-alpha状态。  
virtlet的github地址：https://github.com/Mirantis/virtlet  
virtlet的架构图：https://github.com/Mirantis/virtlet/blob/master/docs/architecture.md  
Virtlet采用了Kubernetes的容器运行时接口（CRI）架构来实现，主要在Kubernetes的Work Node上做文章。  

>- CRI代理，提供了在同一个节点上运行多个CRI实现的方式，例如Virtlet与docker-shim。  
>- Virtlet manager（即图中Virtlet process）实现用于虚拟化和镜像处理的CRI接口，控制libvirt来响应kubelet的请求。  
>- libvirt通过调用vmwrapper来实现VM的生命周期管理。  
>- vmwrapper负责：生成模拟器（目前为qemu-kvm）；通知模拟器来开始或停止VM。  
>- 模拟器，目前为支持kvm的qemu，将来可能停止对kvm的支持。  

其中CRI Proxy工作机制如图所示：
CRI代理可以在同一个工作节点运行多个CRI实现，例如，可以同时运行docker-shim和virtlet，由dock-shim运行docker容器，由virtlet运行VM，等等。
