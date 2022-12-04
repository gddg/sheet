

install

> sudo apt install openssh-server


SSH秘钥。

> ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key

> ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

vim /etc/ssh/sshd_config
Port 22
ListenAddress 0.0.0.0
PermitRootLogin yes
PasswordAuthentication yes


> sudo service ssh restart

# wsl 启动服务

https://zhuanlan.zhihu.com/p/47733615


启动服务文件

> vim /etc/init.wsl

```bash
#! /bin/sh
/etc/init.d/cron $1
/etc/init.d/ssh $1
/etc/init.d/supervisor $1
```

sudo /etc/init.wsl start
 * Starting OpenBSD Secure Shell server sshd

运行
shell:startup


```vbs
Set ws = CreateObject("Wscript.Shell")
ws.run "wsl -d Ubuntu-20.04 -u root /etc/init.wsl start", vbhide
```


:w !sudo tee %





### supervisor 管理进程简明教程