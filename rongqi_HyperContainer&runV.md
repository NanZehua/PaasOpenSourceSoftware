# Hyper/HyperContainer

HyperContainer，它的目标竟然是在裸机/Hypervisor上运行容器。  
Hyper和已经拆分为Moby的Docker一样，分为开源版本和商业版本。  
Hyper开源版本的官网：https://hypercontainer.io/  
Hyper商业版本的官网：https://hyper.sh/  
Hyper的github地址：https://github.com/hyperhq  
主要的工程有：hyperd、runv、hypernetes等。  

HyperContainer是完全基于虚拟化的解决方案，他使用的不是namespace/cgroup等容器隔离技术，而是使用KVM等虚拟化技术。HyperContainer不依赖于Linux操作系统，而是使用自己的hyperkerenel极简化内核。  
Hyper的主要组件有：  
>1）命令行工具：hyperctl  
>2）守护程序：hyperd，使用REST API hyperd的REST API接口文档：https://docs.hypercontainer.io/reference/api.html  
>3）Guest内核：hyperkernel  
>4）Guest启动程序：hyperstart  

在HOST上，hyperd通过一个VM实例来加载Docker镜像，而不使用容器。  
在HyperVM内，启动一个极简化的Linux内核，即hyperkernel，然后由内核启动一个初始化程序hyperstart，来从HOST加载Docker镜像。  

# runV
runv是基于hypervisor的OCI容器运行时。  
runv与OCI兼容，但由于其基于hypervisor，OCI标准中的namespace等部分将会被忽略。  
runv的github地址：https://github.com/hyperhq/runv  

# Hypernetes

Hypernetes其实是kubernetes和Openstack的结合。当然，也确实是用他来管理Hyper的，只是在hyper上，还要跑Pod和container的。  
Hypernetes的github地址：https://github.com/hyperhq/hypernetes  
按照github上的定义，Hypernetes = Bare-metal + Hyper + Kubernetes + KeyStone + Cinder + Neutron.  
