# LXC 

LXC，全称是Linux Container，是Linux上容器技术的鼻祖  
LXC的官方网站：<https://linuxcontainers.org/>  
LXC的github地址：<https://github.com/lxc/lxc>  

LXC是Linux内核容器化特性的用户名接口，可以让使用者轻松的创建和管理系统级和应用级容器  
LXC主要包括一个liblxc库，和各种语言的API接口：C、Python、Lua、Go、Ruby等等  
LXC主要通过下列内核特性来支持容器： 
>- Kernel namespaces (ipc, uts, mount, pid, network and user)
>- Apparmor and SELinux profiles
>- Seccomp policies
>- Chroots (using pivot_root)
>- Kernel capabilities
>- CGroups (control groups)

本文介绍其中3个：Chroot、Namespace、CGroups。

1.  chroot：创建一个虚拟的根目录文件系统，跟其他容器的虚拟文件系统隔离；
2.  namespace：命名空间为各个容器提供相互隔离的资源空间，主要有以下命名空间：
>- UTS（uname）：每个容器拥有独立的hostname和domain name，使其在网络上可以被视作一个独立的节点而非Host上的一个进程；
>- PID：隔离容器的进程资源。各个namespace只能看到自己的进程，都有自己的pid为1的进程；各个namespace中可以有pid相同的进程，但进程之间没有任何关系，互不冲突影响。
>- IPC（进程间通信）：对Linux上进程间通信的资源进行隔离，包括信号量、消息队列、共享内存等；
>- NS（mnt）：文件系统隔离。容器在chroot之后限制了进程只能读写指定的目录，NS的namespace则是文件的挂载和卸载只跟namespace 有关系，跟其他的namespace是无关的。
>- NET：网络隔离。每个net namespace有独立的network devices、IP addresses、IP routing tables、/proc/net目录等。
>- User：每个container可以有不同的user和group id，也就是说可以以container内部的用户在container内部执行程序而非Host上的用户。
3. cgroups（control groups）：实现了对容器的资源分配与控制。可以控制分配给单个进程和多个进程的资源，并可以对cpu、memory等进行精细化控制。每种精细化控制的资源可以定义为一个子系统：
>- cpu 子系统: 主要限制进程cpu的使用率，也可以理解为限制分配给cpu的core。
>- cpuacct 子系统：统计每个进程cpu 使用率的报告，如果达到预定的上限，可以采取一定的措施。
>- cpuset 子系统：定义了有几个CPU可以被这个group使用，或者哪几个CPU可以供这个group使用。在某些场景下，单CPU绑定可以防止多核间缓存切换，从而提高效率。
>- memery 子系统：可以限制进程memery 最大的使用量。
>- blkio 子系统：block IO相关的统计和限制，byte/operation统计和限制(IOPS等)，读写速度限制等。
>- device 子系统：可以控制访问的设备。
>- net_cls 子系统：标记cgroups 中的网络数据包，然后可以使用tc模块(traffice control) 系统对数据包进行控制；比如namespace NET 的可以通过这个系统让namespace 内进程可以独立进行网络通信，功能类似于自己单独的网卡、单独的带宽。
>- freezer 子系统，可以stop或者start cgroups 管理的进程，就是监控进程的状态，如果设置了一直是start状态，就去确定环境是否是ok，如果ok就启动服务。
>- ns子系统： 可以控制cgroup的进程访问不同的namespace；这个配合namespace的功能实现容器的隔离效果。

# LXD 

LinuxContainer旗下除了LXC，还有LXD和LXCFS  
很多人把LXC和LXD混为一谈，其实两者是不一样的. LXD是LXC之上的容器管理器，通过liblxc和其Go语言接口来创建和管理容器  
LXD的官方网站：<https://linuxcontainers.org/lxd/>  
LXD的github地址：<https://github.com/lxc/lxd>  

LXD的核心是一个特权守护程序，通过liblxc和其Go语言接口来创建和管理容器 
同时，它可以通过本地unix套接字、或网络，对外暴露REST API接口  
REST API的接口文档：<https://github.com/lxc/lxd/blob/master/doc/rest-api.md>  

LXD与OpenStack有一个集成项目，叫做nova-lxd。该项目提供一个OpenStack Nova插件，让OpenStack可以管理系统级容器  
用法参见：<https://linuxcontainers.org/lxd/getting-started-openstack/>  
