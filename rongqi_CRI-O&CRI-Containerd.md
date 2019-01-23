# cri-o  

cri-o是基于OCI的kubernetes容器运行时接口（CRI）的实现，它使用符合OCI标准的运行时实现kubernetes CRI，可以用来创建和管理Pod。  
cri-o的github地址：https://github.com/kubernetes-incubator/cri-o  
挂在kubernetes孵化器的名下，该项目目前处于alpha状态。  

cri-o是一个容器运行时接口（CRI）的实现，他的主要目标是：  
>（1）支持多种容器镜像格式，包括现有的Docker镜像格式  
>（2）支持多种方式下载镜像，包括镜像可信度与镜像验证  
>（3）容器镜像管理，管理镜像的层、叠加式文件系统等；  
>（4）容器进程生命周期管理  
>（5）满足CRI要求的监控与日志  
>（6）CRI要求的资源隔离  

cri-o在各方面使用：
>（1）运行时：使用runc（或其他OCI实现）和OCI运行时工具  
>（2）镜像：使用containers/image定义的镜像管理  
>（3）存储：使用containers/storage定义的镜像层的存储和管理  
>（4）网络：使用CNI 支持网络  

# cri-containerd
cri-containerd是基于containerd的kubernetes容器运行时接口（CRI）的实现。  
cri-containerd：https://github.com/kubernetes-incubator/cri-containerd  
该项目同样挂在kubernetes孵化器的名下，目前处于alpha状态。  

cri-containerd有如下依赖：  
>（1）containerd：containerd  
>（2）runc：runc  
>（3）CNI：CNI  

同时，cri-containerd 还使用了OCI的镜像规范、运行时规范。
