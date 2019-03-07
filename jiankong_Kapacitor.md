Influxdata的官方网站：https://www.influxdata.com

Influxdata TICK框架的框架图：https://www.influxdata.com/time-series-platform/

Influxdata的github地址：https://github.com/influxdata

# TICK
TICK是influxdata公司推出的监控与告警解决方案，主要有4个组件组成：

>-  Telegraf，采集监控数据的插件，部署在需要采集的Host上。

>-  InfluxDB：时序数据库，用于保存采集的监控数据。

>-  Chronograf：监控数据显示界面。

>-  Kapacitor：数据处理框架，提供告警、异常检测与处理功能。

其中InfluxDB和Kapacitor已提供企业版。

TICK框架中，先由Telegraf采集监控数据，并推送到InfluxDB。然后由Kapacitor对数据进行处理，包括告警和异常检测，最终输出到Chronograf进行显示。四个组件中，Telegraf可由其他监控组件代替，例如Heapster；Chronograf也可以由Grafana或Dashborad代替。

# 比较
单点监控工具中，Kubernetes已将CAdvisor集成到kubelet中，不需要做额外的工作或额外的选择。

系统监控工具中，Heapster是Kubernetes原生的监控工具，但存在两个劣势：

>-  没有原生的数据库。Heapster通常搭配InfluxDB来作为数据库。

>-  缺少告警系统。

Hawkular可以解决以上问题，既有数据库（TSDB），也有告警系统。尤其Heapster中有原生的Hawkular插件，Hawkular通过Heapster来获取监控数据。因此Heapster+Hawkular可以作为一个组合的解决方案。

Heapster+InfluxDB+Kapacitor也可以作为一个时序数据库和告警系统的解决方案，但在成熟度和性能上，不如Hawkular。

Prometheus是一个完整的系统监控与告警工具。在与Kubernets集成方面，Prometheus通过Http API接口从各个节点的kubelet/CAdvisor获取监控数据，进行汇总和分析。

从Kunernets原生度的角度考虑，建议选用Heapster+Hawkular。
