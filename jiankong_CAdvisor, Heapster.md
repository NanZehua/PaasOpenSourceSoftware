# CAdvisor  

CAdvisor是Docker容器上的资源监控程序。  
CAdvisor的github地址：https://github.com/google/cadvisor  
CAdvisor是google开源的容器资源监控程序（Container Advisor），与Kubernetes同源，主要为Kubernetes上的Docker容器资源监控。  
CAdvisor提供了webUI和REST API两种方式来展示数据，从而可以帮助管理者了解主机以及容器的资源使用情况和性能数据。cAdvisor对外提供web服务的默认端口为4194，rest API服务端口默认为10255.  

在Kubernetes的早期版本中，CAdvisor需要以容器的形式运行在HOST上。到了Kubernetes的后期版本，CAdvisor集成到了kubelet中。  
无需额外配置。默认情况下，你可以在 http://<host_ip>:4194 地址看到 cAdvisor 的管理界面。  
CAdvisor的REST API文档：https://github.com/google/cadvisor/blob/master/docs/api.md  
CAdvisor的Web UI文档：https://github.com/google/cadvisor/blob/master/docs/web.md  

# Heapster
heapster是Kubernetes上的资源监控系统。

Heapster的github地址：https://github.com/kubernetes/heapster

Heapster从各个节点的CAdvisor收集监控数据，进行汇总和分析后，将数据导给第三方工具，例如InfluxDB、Elasticsearch或Kafka，然后再由Dashboard或第三方工具Grafana进行可视化显示。

https://segmentfault.com/img/remote/1460000007708165?w=640&h=263/view

Heapster目前主要支持Kubernetes和CoreOS。

 Heapster也能支持监控Openshift集群，或与Hawkular-Metrics对接，需要参考：https://github.com/openshift/origin-metrics

CAdvisor+Heapster是目前Kubernetes中最主流的监控系统组合。
