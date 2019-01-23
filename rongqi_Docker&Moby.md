# Docker/Moby  

Docker，这是当下最火的容器技术了。2017年4月20日，Docker公司宣布将Docker开源项目更名为Moby，顿时引起开源社区一片混乱。从今往后，Docker公司就会发布两个Docker版本：Docker企业版与Docker社区版，其中Docker社区版由Moby进行开发，并由Docker公司来发布。  

Moby的官方网站：https://mobyproject.org/   ——这个网站不是一般的慢，反正我是没进去过。  
Moby的github地址：https://github.com/moby/moby  
Docker-CE的github：https://github.com/docker/docker-ce/tree/master/components/engine  
Docker公司官方网站：https://www.docker.com/  
Docker的API参考文档：https://docs.docker.com/reference/  

Docker最初是由dotCloud公司（现在已改名为Docker公司）发起并开业的容器技术，最初是基于LXC进行开发的。  
从Docker 0.7开始去LXC化，转而使用自行开发的libcontainer；  
从Docker 1.11开始，改为使用runC和containerd。Moby也继承了这一点，使用containerd作为默认的容器运行时。  
2016年12月14日，从Docker Engine中分离并单独开源containerd项目，可以作为daemon程序运行在各个系统上，管理容器的生命周期。2017年3月15日，Docker将containerd项目捐赠给CNCF。

CoreOS的rkt官网上有一张图片，可以形象的见识到Docker各个版本的进程运行关系：

Docker早期版本，Docker Engine通过LXC运行容器：
Docker 0.7以后，去LXC化，改为使用自己开发的libcontainer：
Docker 1.11以后，从Docker Engine分离出来，改为使用更加开放的containerd，并通过runC运行容器：
安装Docker迁移到Moby的移植列表，将会删除所有的Docker UI、SDK，以保留在Docker商业组织中。除了Engine之外，Docker平台的其他一些独立组件，也会迁往Moby。

Docker平台的独立组件，包括：https://www.docker.com/technologies/overview
Docker Engine、Docker Compose、Docker Machine、Docker Swarm、Docker Registry、Kitematic。
这些独立组件，目前仍保留的Docker名下，除Engine外，其余几个组件是否迁往Moby，尚无定论。

Docker的开源项目Moby将会何去何从，前途一片迷雾。

# Docker镜像格式  

Docker镜像，是使用分层的镜像格式。
Docker使用AUFS来作为容器的文件系统格式。docker容器在启动时，先加载一个只读的rootfs文件系统。加载成功后，再加载一个读写的文件系统，覆盖在只读的rootfs上，这被称为一层。这个过程是可以重复的，可以在其上，再加载一层读写的文件系统，同时把下一层的设置为只读。最终容器运行时，看到的是最上一层的读写文件系统。这个就是Docker的分层概念。  

这种分层的方式，可以有如下的好处：
> （1）多个容器共用同一个基础镜像，而不必重复拷贝镜像；
> （2）不同的容器，可以共用其中相同的基础镜像，节省存储空间

关于Docker容器镜像的分层结构，百度百科上介绍的非常详细：

https://baike.baidu.com/item/Docker/13344470?fr=aladdin#5_4
