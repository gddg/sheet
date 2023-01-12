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





Docker 中文指南

<http://www.widuu.com/chinese_docker/index.html>
