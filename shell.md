# shell

> w

显示会话


## iproute2 包

> ip addr

> ip link



### linux工具



#### linux disk usage 磁盘大小分析gdu

```bash
curl -L https://github.com/dundee/gdu/releases/latest/download/gdu_linux_amd64.tgz | tar xz
chmod +x gdu_linux_amd64
mv gdu_linux_amd64 /usr/bin/gdu
```


 https://github.com/dundee/gdu

#### 流量



#### 图床
[https://sm.ms/home/picture](https://sm.ms/home/picture)




#### 重启输入法

>   fcitx 1>/dev/null 2>/dev/null &


#### 升级WSL

> wsl --update





### ssh 本地端口

> ssh -f -N -L 20800:X01.43.17.81:10800  XXX@X01.43.17.81

本地0.0.0.0:20800的端口,代理服务器端XXX@X01.43.17.81的`10800`端口.
`ssh -f -N -L AIP:9906:BIP:3306 root@BIP`

-N，当配合此选项创建ssh隧道时，并不会打开远程shell连接到目标主机。
-f，表示后台运行ssh隧道，即使我们关闭了创建隧道时所使用的ssh会话，对应的ssh隧道也不会消失。
-g，可以开启”网关功能”，开启网关功能以后，ServerA中的所有IP都会监听对应端口。

检查端口：

> ss -ntpl


应用：
服务器有一台mysql，需要本地管理。远程mysql端口，映射到本地。




# 远程转发

 公司服务访问公网服务器,把内网端口映射到公网主机的上。


## 自动转发

```bash
wget http://www.harding.motd.ca/autossh/autossh-1.4e.tgz
gunzip -c autossh-1.4e.tgz | tar xvf -
cd autossh-1.4e
./configure
make
sudo make install
```

> autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3"    -f -N -L 20800:0.0.0.0:10800 gaX@X01.43.17.81


[everythingcli](https://www.everythingcli.org/ssh-tunnelling-for-fun-and-profit-autossh/)


> vim ~/.ssh/config
```bash
 Host cli-mysql-tunnel
    HostName      everythingcli.org
    User          cytopia
    Port          1022
    IdentityFile  ~/.ssh/id_rsa-cytopia@everythingcli
    LocalForward  5000 localhost:3306
    ServerAliveInterval 30
    ServerAliveCountMax 3
```
> autossh -M 0 -f -T -N cli-mysql-tunnel



ubuntu 下 init.d 服务启动脚本编写
https://codeantenna.com/a/9c7quFnSxy


# ls  
exa 
ranger

10 款更先进的开源命令行工具

https://mp.weixin.qq.com/s?__biz=MjM5NzM0MjcyMQ==&mid=2650153517&idx=4&sn=26e1897650ce96f2f4491a39b3dc679e&chksm=bed9f94389ae705570a99e286dc780a8b6a57e330edf2c6d95f9558a6bd1141f0ee2d73ac112&mpshare=1&scene=1&srcid=0726w7n4wl9ssTVnQN9cJTWS&sharer_sharetime=1658973430778&sharer_shareid=7f27fe51e1971663d24301e15bdba09a&exportkey=AVhioe64EN358r%2B%2FyOEKYHU%3D&acctmode=0&pass_ticket=k1KK7Iz6CDpzPc6GgJs462BvtD0GQqQsEd1a1vYg1%2Fn3EDnnBHTCvHYYdm6DRuLX&wx_header=0#rd
