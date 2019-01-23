# Mesos  

Mesos是Apache旗下的开源集群管理框架。  
Mesos的官方网站：http://mesos.apache.org  
Mesos的官网架构图：http://mesos.apache.org/documentation/latest/architecture/  
Mesos的github地址：https://github.com/apache/mesos  
> Mesos只是一个集群管理框架，并不直接管理进程或容器。真正的管理，需要额外实现一套Framework。  
> Mesos采用了一种两级调度架构。第一级调度是主从结构，由Master节点管理Slave节点。第二级调度由Framework实现。  
> Framework分为Scheduler与executor。如图以Hadoop和MPI两种不同的框架类型为例。Scheduler通过MesosSchedulerDriver接入Mesos，向Mesos注册，获取Mesos分配的资源，然后再通过Executor分配给自己的任务。Executor则部署于Slave节点，用于启动和管理自己的任务。
每增加一种新的Framework类型，都需要实现自己的Scheduler和Executor。

# Mesosphere

很多人把Mesos和Mesosphere混为一谈，其实两者不是一个概念。
Mesos是Apache旗下的开源项目；而Mesosphere则是一家公司的名字。
那么两者之间有什么关系呢？首先Mesos是Mesosphere创始人本·辛德曼（Ben Hindman）在读大学期间打造的开源项目。第二，Mesosphere是在Mesos的框架基础上，打造集群管理系统。
目前，Mesosphere的主要项目是Marathon。
Mesosphere的官网：https://mesosphere.com/   这个网页真的是色彩风格诡异，菜单栏都看不清楚。

# Marathon 

Marathon是Mesos框架基础上的集群管理系统，或者说Marathon是Mesos上的一个框架，用来管理容器和程序。  
Marathon的github项目地址：https://github.com/mesosphere/marathon  
Marathon在github.io上有个首页：https://mesosphere.github.io/marathon/  
Marathon提供对外的REST API：https://mesosphere.github.io/marathon/api-console/index.html  
Mesos加上Marathon，才是一套完整的容器管理与编排系统：

下图显示Marathon如何在Mesos上运行，并管理其他程序和服务：
>（1）Marathon作为Mesos上第一个启动的框架，与Mesos一起运行；  
>（2）Marathon是运行其他框架的有力方式，例如下图，Marathon启动了Chronos Sechduler的两个Docker实例。如果这两个Chronos中有任何一个失败，Marathon会在另一个Mesos Slave上重新启动他，以确保两个Chronos的运行。  
>（3）由于Chronos本身也是一个框架，所以他也会在Mesos上启动任务，如图蓝色的任务；  
>（4）同时，Marathon还会运行其他应用容器（Docker或Mesos），如图橙色的任务。  
>（5）验证表面，Marathon可以与其他框架共同运行在Mesos上，并保持其他框架的可靠性。  
