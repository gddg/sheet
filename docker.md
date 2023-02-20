# docker



#### 启动docker

> &#x20;docker start build\_gcc49py39

#### &#x20;进入shell

> &#x20; docker exec -it build\_gcc49py39 /bin/bash



> docker exec -it v1.3go1.12 /bin/bash



#### 删除镜像 docker image rm

docker image rm 4ed24a7d421f

停止

docker stop build\_gcc49py39&#x20;



生成镜像

\> docker commit -a "gao.yd" -m "centos7,gcc4.8.5,py3.9,go1.18 " f72ed5df1c6c centos7gcc48py39go118:v1

看目前镜像

> docker images



&#x20;\
REPOSITORY TAG IMAGE ID CREATED SIZE  \
c37744752e96 2 months ago 342MB


# 移动docker image 2方式






Docker 中文指南

<http://www.widuu.com/chinese_docker/index.html>





docker network create -d macvlan --subnet=192.168.2.0/24 --gateway=192.168.2.1 -o parent=eth0  -o macvlan_mode=bridge macnet


docker network create -d macvlan --subnet=192.168.2.0/24 --gateway=192.168.2.1 -o parent=eth0 macnet


$ docker network create   --help

Usage:  docker network create [OPTIONS] NETWORK

Create a network

Options:
      --attachable           Enable manual container attachment
      --aux-address map      Auxiliary IPv4 or IPv6 addresses used by Network driver (default map[])
      --config-from string   The network from which to copy the configuration
      --config-only          Create a configuration only network
  -d, --driver string        Driver to manage the Network (default "bridge")
      --gateway strings      IPv4 or IPv6 Gateway for the master subnet
      --ingress              Create swarm routing-mesh network
      --internal             Restrict external access to the network
      --ip-range strings     Allocate container ip from a sub-range
      --ipam-driver string   IP Address Management Driver (default "default")
      --ipam-opt map         Set IPAM driver specific options (default map[])
      --ipv6                 Enable IPv6 networking
      --label list           Set metadata on a network
  -o, --opt map              Set driver specific options (default map[])
      --scope string         Control the network's scope
      --subnet strings       Subnet in CIDR format that represents a network segment
gao @ ubuntu22  [17:51:39]   10.254.5.62




Docker Cheat Sheet 速查表
<https://github.com/wsargent/docker-cheat-sheet/tree/master/zh-cn>
