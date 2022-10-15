---
title: 鸡鸡复鸡鸡小鸡生小鸡用Docker做跑路云吧
date: 2022-08-21 22:26:42
tags:  
	- docker
	- vps
categories: 技术教程
---
准备资源：
一个VPS（当然不能是Docker/OVZ/LXC生出来的啦）
没了。。。就那么简单粗暴

1.安装Docker
因为我这边用的是Ubuntu，所以就直接APT装了
<!--more-->
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
"deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update && apt install docker-ce docker-ce-cli containerd.io
```

装完之后输入docker version即可看到docker的版本 确认已经装好了
![](https://files.baxx.eu.org/img/202208212201804.png)

2.修改Docker Storage Driver为devicemapper（可选）
这不是必须的，但是这样限制小鸡的小鸡的硬盘时会方便一点，或者用xfs的磁盘配额也是一样的
如果都不使用则小鸡的小鸡的硬盘可以撑爆小鸡的硬盘
```
nano /etc/default/docker
```

加入一行，此处dm.basesize的大小为小鸡的小鸡可用的硬盘
```
OPTIONS=--storage-driver=devicemapper --storage-opt dm.basesize=100G
```
保存退出
```
nano /lib/systemd/system/docker.service
```

在[Service]中加入一行
```
EnvironmentFile=-/etc/default/docker
```
并把
ExecStart改为
```
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock $OPTIONS
```
完成后重启docker
```
systemctl daemon-reload
systemctl restart docker
```

然后就可以看到Storage Driver: devicemapper，此时就可以很方便的给小鸡的小鸡设置硬盘上限了
![](https://files.baxx.eu.org/img/202208212201621.png)

3.制作开小鸡用的Docker镜像
去Docker Hub上挑一个你中意的BaseOS
https://hub.docker.com/search?q=&type=image&category=os
这边以Fedora为例
```
docker pull fedora:34
```

拉下来之后就可以在images里看到了
```
docker image ls
```
![](https://files.baxx.eu.org/img/202208212202403.png)

然后就需要给image加入sshd
首先创建一个container
```
docker run -i -t fedora:34 /bin/bash
```

稍等片刻就进入了fedora34的bash
安装sshd
```
dnf install openssh-server passwd
```

生成ssh key
```
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
```

修改root密码
```
passwd
```

开启root登录
```
nano /etc/ssh/sshd_config
```

加入
```
PermitRootLogin yes
UsePAM no
```

退出容器
```
exit
```

然后就可以把刚才的容器做成镜像了
（别照搬我的docker用户名和镜像id哦）
```
docker commit 1fe913fd8151 zjl88858/baseos:fedora34
docker push zjl88858/baseos:fedora34
```

制作完成之后 之前的容器就没有用了 删掉吧
如果你有洁癖 可以把fedora34也给删掉
```
docker rm 1fe913fd8151
```

这就是完成之后的效果
![](https://files.baxx.eu.org/img/202208212202950.png)

>鸡鸡复鸡鸡用的docker镜像:
>Hub地址：https://hub.docker.com/r/zjl88858/baseos
>镜像的默认root密码为qwe!!123!!
>已经内置vim和openssh-server，仅需
>docker run -d zjl88858/baseos:$os名称 /usr/sbin/sshd -D
>
>即可启动
>为了方便使用脚本来控制，可以加入exec来修改密码
>docker exec $id passwd
>复制代码
>
>其余未作改动
>因为没有其他指令集的环境，我只能提供amd64版本，如果需要arm64或ppc64le版本，自己做一个也不难
>方法参照上一篇教程
>
>目前已有OS版本:
>Ubuntu 18.04
>docker pull zjl88858/baseos:ubuntu18.04
>
>Ubuntu 20.04
>docker pull zjl88858/baseos:ubuntu20.04
>
>Fedora 34
>docker pull zjl88858/baseos:fedora34
>
>Debian Sid
>docker pull zjl88858/baseos:debiansid-20210721
>
>Debian Experimental
>docker pull zjl88858/baseos:debianexperimental-20210721


4.开第一个小鸡生出来的小鸡、使用端口转发、限制资源
开小鸡的命令很简单
```
docker run -d -p 2201:22 -p 10000:10000 -p 10001:10001 -p 10002:10002 --cpus=0.5 --memory=128M zjl88858/baseos:fedora34 /usr/sbin/sshd -D
```

-p 是端口转发
以上述命令为例 我把2201转发到了小鸡的22端口（SSH） 10000-10002 原样转发预留给小鸡使用
当然 如果端口很多 可以写成端口段
例如10000-10002这样
--cpus 为小鸡能使用的CPU资源 单位为核
--memory 为小鸡能使用的内存资源 单位可以为M G T
开完之后可以看一下小鸡（容器）的列表
```
docker ps -a
```

![](https://files.baxx.eu.org/img/202208212203267.png)
然后就可以尝试用ip:2201连接ssh了
![](https://files.baxx.eu.org/img/202208212203386.png)
完结撒花~

其他实用命令
查看小鸡cpu/内存
```
docker stats
```

查看小鸡硬盘
```
docker df -v
```

啥？你要看更详细的？
```
docker exec -t -i [容器id] /bin/bash
```
直接进去看咯