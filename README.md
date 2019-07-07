vagrant Version: 2.2.0

1. git clone https://github.com/xiangyu123/home_work.git 
2. cd home_work && vagrant up
3. vagrant ssh
4. cd Jenkins
5. follow Readme.md

HA:
  1. 容器docker run的时候可以加上--restart=always参数
  2. 可以使用docker-compose scale 来缩放
  3. 也可以使用k8s，本次时间比较紧张，考虑到vagrant ansible等兼容性,还得配置ingress, service等，所以就没有用k8s

日志:
  1. 用sidecar方式部署filebeat收集日志, 也可以使用daemonset在每个kubelet节点上部署
  2. 也可以使用logstash，优先建议使用filebeat
  3. 日志建议打到一个集中的ElasticSearch, 为避免日志丢失，建议使用filebeat---> kafka ----> elasticsearch这种方式

监控:
  1. 可以采用Node_exporter+cAdvisor+Prometheus+Grafana监控。
  2. Grafana官网有相应的json模板，可以直接下载和导入
  3. 简单的监控方式也可以采用cAdvisor+InfluxDB+Grafana来实现

容器资源限制:
  1. k8s可以使用Qos来配置资源限制
  2. docker命令可以直接添加参数来配置
  3. 也可以参照docker-compose.yml语法直接在这个文件里面配置资源限制
