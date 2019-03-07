Prometheus的官方网站：https://prometheus.io/

Prometheus的github地址：https://github.com/prometheus/prometheus/

Prometheus是一个开源的监控与报警系统。通过Prometheus Server从各个节点采集指标数据，并以PromQL格式存储。

Prometheus的主要组件包括：

>-  Prometheus server：负责数据采集和存储，提供PromQL查询语言的支持；
>-  Push Gateway：支持临时性Job主动推送指标的中间网关；
>-  PromDash：使用rails开发的dashboard，用于可视化指标数据；
>-  exporters：支持其他数据源的指标导入到Prometheus，支持数据库、硬件、消息中间件、存储系统、http服务器、jmx等；
>-  alertmanager：实验性组件，用来进行报警；
>-  prometheus_cli：命令行工具
>-  其他辅助性工具

Prometheus有两种数据采集方式。第一种为Pull，通过HTTP协议从各个节点去主动采集数据，采集目标需要暴露一个http接口给Prometheus。

第二种方式为Push方式。采集节点运行一个短周期的定时任务，采集数据之后push到Pushgateway，然后由Prometheus Server去从Pushgateway拉取数据。

Prometheus与Kubernetes能很好的集成。kubelet/CAdvisor提供了http api接口，支持Prometheus调用获取数据。Prometheus能从Kubernets API Server获取节点列表，然后通过http api接口获取各个节点的数据。
