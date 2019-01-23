# Kubevirt

Kubevirt是目前在Kubernetes架构上提供VM管理的唯一已发布的开源项目，其他几个开源项目目前都处于pre-alpha状态。  
kubevirt的官方网站：http://kubevirt.io  
kubevirt的github地址：https://github.com/kubevirt/kubevirt  
kubevirt的架构图：https://github.com/kubevirt/kubevirt/blob/master/docs/architecture.md  
kubevirt采用了Kubernetes的第三方资源（TPR）的机制，把VM作为Kubernetes的一个第三方资源来进行管理。不过TPR机制将在Kubernetes的1.9版本中将被CRD（Custom Resource Definition）所取代。kubevirt需要从TPR迁移到CRD。  

kubevirt的主要组件：
>- VM TPR，VM第三方资源，以Kubernetes TPR方式定义VM参数，如CPU类型、CPU内存大小，网卡信息、磁盘信息等等。  
>- virt-api-server是KubeVirt进行虚拟机管理的入口，响应外部传入的VM TPR的请求并且进行VM TPR验证。virt-api-server不对kube-apiserver进行修改而选择扩展出新API Server，有利于架构解耦以及不破坏当前Kubernetes对容器的管理流程。
>- virt-controller，响应virt-api-server的请求，监控VM TPR的变化，因为每一个VM对象需要由pod来初始化，并且VM迁移时对应pod也需要同步迁移，这样要求virt-controller同时需要管理跟VM对象关联的pod生命周期。virt-controller会把VM相关操作路由到virt-handler。
>- virt-handler以DaemonSet的方式在每个主机上运行一个实例，响应virt-controller的请求，**VM对象的变化并根据相应描述调用libvirtd更新虚拟机状态。
>- vm-launcher，每个VM 对象都会创建1个pod，这个pod会运行vm-launcher。其作用是提供cgroups和namespaces，用来启动虚拟机进程，一旦虚拟机进程在容器内出现，virt-handler将把自身绑定到这个进程，这样，虚拟机就通过pod创建出来。
>- libvirtd在每个主机上运行，负责真正的虚拟机创建删除等管理工作。

kubevirt创建一个VM的工作流程：
>1. 客户端向K8s API服务器发布新的VM定义;  
>2. K8s API服务器验证输入并创建一个VM第三方资源（TPR）对象;  
>3. 在virt-controller观察新VM对象的创建，并创建一个相应的Pod;    
>4. Kubernetes在主机上调度pod;  
>5. 该virt-controller观察到VM的Pod启动了，并更新VM对象的nodeName。现在nodeName已经确定了，责任转移到 virt-handler做进一步的行动;  
>6. 该virt-handler（DaemonSet）观察到一个VM被分配到其所运行的主机上;  
>7. 该virt-handler使用VM规范，并使用本地的libvirtd实例创建一个相应的域。  

删除：
>1. 客户端VM通过删除对象virt-api-server。
>2. 该virt-handler观察删除和关闭域。

# vAdvisor

在github上kubevirt的旗下，还有一个类似于cAdvisor，用于VM的资源监控的工程：vAdvisor
vAdvisor的github地址：https://github.com/kubevirt/vAdvisor
要在运行libvirtd的主机上运行vAdvisor，需要使用预先准备好的Docker镜像。

- 与Prometheus的对接：

        VM在运行时，vAdvisor会对外暴露一个端口，返回当前运行的所有VM的监控数据，供Prometheus访问。

- 与cAdvisor/Heapster的对接：

        vAdvisor对外暴露端口，同样能被cAdvisor访问，然后由cAdvisor收集数据，并传递给Heapster。
