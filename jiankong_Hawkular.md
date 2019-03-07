Hawkular是RedHat赞助的一个开源监控与告警项目。

hawkular的官方网站：http://www.hawkular.org/

hawkular的github地址：https://github.com/hawkular

Hawkular是由红帽赞助的，包括一组多个开源的监控项目，主要目标是作为红帽的ManageIQ（一个监控、管理、自动化的解决方案）的核心，主要运行在红帽赞助的OpenShift平台上。

Hawkular包括一组开源项目：

>（1）Hawkular Services：这是Hawkular的旗舰工程，负责提供进行存储的服务、基于指标进行告警、保持一个图形视图等。

>（2）Hawkular APM（应用程序性能管理）：是专门用于监控应用程序的独立项目。该项目允许检测和捕获业务请求的片段，以便人们可以知道时间消耗在哪。

>（3）Hawkular Metrics：是一个时间序列数据库（TSDB），由Cassandra（一个k-v数据库）提供可扩展性。Hawkular Services使用并对外暴露Hawkular Metrics。

>（4）Hawkular Alerts：Hawkular的告警子系统。

>（5）Hawkular Agent：可用于监控已管理的应用程序。可用于监测Wildfly或EAP应用服务器以及运行在应用服务器上的应用程序。

Hawkular Services
官方文档：http://www.hawkular.org/hawkular-services/docs/user-guide/

github工程：https://github.com/hawkular/hawkular-services

# Hawkular APM

官方文档：https://hawkular.gitbooks.io/hawkular-apm-user-guide/content/  
REST API文档：https://hawkular.gitbooks.io/hawkular-apm-user-guide/content/restapi/  
github工程：https://github.com/hawkular/hawkular-apm  
主要提供：
>（1）分布式跟踪，用于微服务；  
>（2）应用性能管理  
>（3）业务事物管理，目前只用于JVM  

# Hawkular Metrics

官方文档：http://www.hawkular.org/hawkular-metrics/docs/user-guide/  
REST API文档：http://www.hawkular.org/docs/rest/rest-metrics.html  
github工程：https://github.com/hawkular/hawkular-metrics  
是一个可扩展的，异步的，多租户的，可长期存储的指标存储引擎。使用Cassandra作为数据库，使用REST作为主要入口。  
可使用一个Cassandra节点，也可以扩展为多个Cassandra节点。  

# Hawkular Alerts

官方文档：http://www.hawkular.org/community/docs/developer-guide/alerts.html  
REST API文档：http://www.hawkular.org/docs/rest/rest-alerts.html  
github工程：https://github.com/hawkular/hawkular-alerts  

# Hawkular Agent
 
github工程：https://github.com/hawkular/hawkular-agent  
Hawkular可以与Heapster对接，Heapster提供了一个对接Hawkular的sink。  
