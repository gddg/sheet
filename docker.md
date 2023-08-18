# docker



#### 启动docker

>   docker start build_gcc49py39

####   进入shell

>    docker exec -it build_gcc49py39 /bin/bash



> docker exec -it v1.3go1.12 /bin/bash



#### 删除镜像 docker image rm

docker image rm 4ed24a7d421f

停止

docker stop build_gcc49py39  



生成镜像

> docker commit -a "gao.yd" -m "centos7,gcc4.8.5,py3.9,go1.18 " f72ed5df1c6c centos7gcc48py39go118:v1

看目前镜像

> docker images



  \
REPOSITORY TAG IMAGE ID CREATED SIZE  \
c37744752e96 2 months ago 342MB


# 移动docker image 2方式










关于Docker目录挂载的总结

<https://www.cnblogs.com/ivictor/p/4834864.html>


Run a command in a new container

$ docker run -p 15678:5678 -p 13080:80  --name build_gcc49py39  -v /home/gao/dockerWork/workspace:/workspace -it centos7gcc48py39v1  /bin/bash         

Start one or more stopped containers

$ docker start  build_gcc49py39                                                                                                               


$ docker exec -it build_gcc49py39   /bin/bash   




# 重新绑定目录

安装问题。
以为golang升级了。

把 `运行的容器` ->`提交`成新镜像 ->然后绑定新目录启动 


gao @ ubuntu22  [15:26:09]   10.254.5.62
      
docker ps-a                                                                                                                                                                                   
```bash           
CONTAINER ID   IMAGE                 COMMAND        CREATED          STATUS                       PORTS                                                           NAMES
4feb45f3d699   centos7gcc48py39v1    "/bin/bash"    4 minutes ago    Exited (0) 19 seconds ago                                                                    build_gcc49py39go119
4400eb6d2413   portainer/portainer   "/portainer"   17 minutes ago   Created                                                                                      suspicious_lewin
72f02ae51aad   centos7gcc48py39v1    "/bin/bash"    5 months ago     Exited (137) 6 minutes ago                                                                   build_gcc49py39
bc5bf52de42b   portainer/portainer   "/portainer"   5 months ago     Up 2 days                    8000/tcp, 9443/tcp, 0.0.0.0:9000->9000/tcp, :::9000->9000/tcp   zealous_hopper
gao @ ubuntu22  [15:26:28]   10.254.5.62

提交运行的镜像，然后

>  docker commit 72f02ae51aad  build_os_gcc49py39go119                                                   

sha256:705de9fefe26b7007e6f0cf1af0b7b61e4ae4971a1c623ccea60c81b2a7bd13a
   
$ docker images 
REPOSITORY                TAG       IMAGE ID       CREATED          SIZE
build_os_gcc49py39go119   latest    705de9fefe26   16 seconds ago   3.7GB
centos7gcc48py39v1        latest    4e6563916b2a   5 months ago     2.21GB
portainer/portainer       latest    5f11582196a4   7 months ago     287MB
gao @ ubuntu22  [15:29:46]   10.254.5.62

删除在运行的容器!不用了一个旧的

> docker rm            4feb45f3d699                                                                                                                                                                                    
4feb45f3d699
 

列出在运行的容器

$ docker ps -a          
CONTAINER ID   IMAGE                 COMMAND        CREATED          STATUS                        PORTS                                                           NAMES
4400eb6d2413   portainer/portainer   "/portainer"   22 minutes ago   Created                                                                                       suspicious_lewin
72f02ae51aad   centos7gcc48py39v1    "/bin/bash"    5 months ago     Exited (137) 11 minutes ago                                                                   build_gcc49py39
bc5bf52de42b   portainer/portainer   "/portainer"   5 months ago     Up 2 days                     8000/tcp, 9443/tcp, 0.0.0.0:9000->9000/tcp, :::9000->9000/tcp   zealous_hopper




$ docker images         
REPOSITORY                TAG       IMAGE ID       CREATED         SIZE
build_os_gcc49py39go119   latest    705de9fefe26   2 minutes ago   3.7GB
centos7gcc48py39v1        latest    4e6563916b2a   5 months ago    2.21GB
portainer/portainer       latest    5f11582196a4   7 months ago    287MB
gao @ ubuntu22  [15:31:38]   10.254.5.62

因为镜像不可以改名， 所以重新构建了 


$ docker commit 72f02ae51aad  centos7gcc49py39go119 

sha256:aa242186de36e611f28038dc0e040209a9252234f9856ddbcd2a7b4d0b21910a


$ docker images                                    
REPOSITORY                TAG       IMAGE ID       CREATED         SIZE
centos7gcc49py39go119     latest    aa242186de36   4 seconds ago   3.7GB
build_os_gcc49py39go119   latest    705de9fefe26   3 minutes ago   3.7GB
centos7gcc48py39v1        latest    4e6563916b2a   5 months ago    2.21GB
portainer/portainer       latest    5f11582196a4   7 months ago    287MB


删除不用名字的image 

$ docker image rm build_os_gcc49py39go119:latest 
Untagged: build_os_gcc49py39go119:latest
Deleted: sha256:705de9fefe26b7007e6f0cf1af0b7b61e4ae4971a1c623ccea60c81b2a7bd13a


列出镜像

$ docker images                                 
REPOSITORY              TAG       IMAGE ID       CREATED          SIZE
centos7gcc49py39go119   latest    aa242186de36   34 seconds ago   3.7GB
centos7gcc48py39v1      latest    4e6563916b2a   5 months ago     2.21GB
portainer/portainer     latest    5f11582196a4   7 months ago     287MB

升级完成
加入映射新目录
 
$ docker run -p 15678:5678 -p 13080:80  --name build_gcc49py39go119  -v /home/gao/dockerWork/workspace:/workspace -v /home/gao/GolandProjects/CloudMonitor:/CloudMonitor   -it centos7gcc49py39go119  /bin/bash

[root@39232277a59b /]# fish
Welcome to fish, the friendly interactive shell
Type help for instructions on how to use fish
root@39232277a59b /> cd workspace/

```

<https://stackoverflow.com/questions/28302178/how-can-i-add-a-volume-to-an-existing-docker-container/53516263#53516263>


## 本地代码拷贝到docker内部


Copy files/folders between a container and the local filesystem:

>   docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH


>   docker cp [OPTIONS] SRC_PATH CONTAINER:DEST_PATH











##  Docker 中文指南

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



# docker 内部引擎协议
http json协议： 
技术选择。。

The daemon listens on unix:///var/run/docker.sock but you can Bind Docker to another host/port or a Unix socket.

https://docs.docker.com/engine/api/v1.18/



更加新的协议说明书

https://docs.docker.com/engine/api/v1.42/#tag/Container/operation/ContainerCreate


