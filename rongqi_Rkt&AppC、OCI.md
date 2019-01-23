# Rkt/AppC、OCI  

2014年12月，CoreOS觉得当时的主流容器Docker已经开始向一个捆绑的平台发展，不利于容器作为一个单独的开源组件发展，（真有先见之明，就在2017年4月，Docker宣布将开源项目分离为Moby，自己专注于商业产品发展）。于是，CoreOS决定推出自己的容器标准，称为Application Container Specification，即应用容器标准，简称为AppC。并在这个标准上，开发了自己的容器，这就是Rkt（起初叫Rocket）。  
Rkt官方网站：https://coreos.com/rkt/  
Rkt的github地址：https://github.com/rkt/rkt  
Rkt的架构文档：https://coreos.com/rkt/docs/latest/devel/architecture.html 

Rkt是按照AppC规范实现的。同时，他也能运行Docker镜像，将Docker镜像下载后，转换为AppC格式。
另外，对于OCI（开放容器镜像）的支持，也正在开发中。 
按Rkt的官方说法，Rkt的调用链分为几个阶段： 
1. 阶段0，是由调用进程（例如kubelet或shell）调用rkt，此时，rkt是调用进程的一个子进程；  
2. 阶段1，rkt运行一个阶段1镜像，运行为一个Pod。然后在Pod中通过coreos.com/rkt/stage1/run，运行一个入口进程；  
3. 阶段2，阶段1的入口进程，拉起阶段2镜像，并在其中调用App应用程序。  

当然，具体起来有两种风格。一种为Fly风格，非常简单，每个Pod里面只运行一个App，应用程序将直接挂载在调用进程下；  
第二种为systemd/nspawn风格，相对复杂一些，见下图： 

Kubernetes上可以支持运行Rkt容器，在Kubernetes上运行Rkt容器的工程，有一个简称，叫 Rktnetes  

# AppC  

AppC是CoreOS推出的容器标准。  
AppC的github地址：https://github.com/appc/spec  
AppC的规范定义：https://github.com/appc/spec/blob/master/SPEC.md  

AppC规范的主要内容：
（1）规定了容器的镜像格式。它并没有采用Docker的分层镜像的格式，这样有利有弊。  
首先，没有采用分层镜像，就不能复用镜像相同的部分，每个镜像都包含完整的文件系统，会造成磁盘上的浪费，和网络传输时的成本上升；  
同时，由于不采用分层镜像，每个镜像都是完整独立、干净的，不会出现Docker镜像那样，表面上删除了某些文件，实际上仍然存在于镜像中的情况。  
（2）规定了镜像分发协议。AppC没有官方的仓库地址，他支持：网络URL地址、本地路径地址、docker镜像地址。  
（3）容器的编排结构。AppC沿用了Kubernetes中的Pod和Label等概念，在Pod中运行一组相关的App Container。  

AppC组织下提供了一些实用的工具：
> docker2aci：将Docker镜像转换为ACI镜像；  
> deb2aci：将Debian包转换为ACI镜像；  
> oci2aci：将OCI镜像转换为ACI镜像；  
> nix2aci：将NIX包转换为ACI镜像。  

根据其在github的声明，从OCI组织成立，并推出开源容器标准以来，AppC的发展将不再进一步进行，其主要开发人员也已投入到OCI的开发中。

# OCI  

OCI的全称是 Open Container Initiative ，即开源容器计划，由CoreOS和Docker两家公司与2015年8月的DockerCon上宣布成立，力图建立通用的开源容器标准。

经过两年的磕磕碰碰，终于在github上推出了自己的开源容器规范。
OCI的github地址：https://github.com/opencontainers  

在github上主要有3个工程：
> runc：根据OCI标准生产并运行容器的命令行工具；  
> runtime-spec：OCI的容器运行时规范；  
> image-spec：OCI的容器镜像规范。  

OCI容器运行时规范：https://github.com/opencontainers/runtime-spec/blob/master/spec.md    
OCI的镜像规范：https://github.com/opencontainers/image-spec/blob/master/spec.md  

所有OCI项目的贡献者和维护者每周三（美国太平洋）举行会议，单周的上午8点，双周的下午2点。所有人都可以通过UberConference网站或音频参与：+ 1-415-968-0849（不需要PIN码）。
