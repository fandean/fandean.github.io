# Docker





![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/610px-Docker_%28container_engine%29_logo.svg.png)

## 学习资料

[ **如何选择Docker书籍** - Docker 问答录（95 问） · 大桥下的蜗牛](https://blog.lab99.org/post/docker-2016-07-14-faq.html#ru-he-xuan-ze-docker-shu-ji "Docker 问答录（95 问） · 大桥下的蜗牛")

**观察一下当前的 Docker 版本号，选择不要晚于 3 个版本的 Docker 书籍。**否则看到的很多东西可能将会因过时而无法使用，或者已经不必如此繁琐有更简单的方式去实现了。

> Docker的版本号规则发生了改变。以前是v1.12什么的，现在直接变成 v17.06，这里17表示2017年。

Docker中国 (Docker官网的中文镜像)  [Docker 文档 - Docker 中文文档](https://docs.docker-cn.com/ "Docker 文档 - Docker 中文文档")

最近官方推出了这个网站来帮助学习Docker，可以在线练习docker命令哦 ：[Play With Docker](https://www.google.com.hk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=10&ved=0ahUKEwiQ7tzk1e7VAhVHT7wKHSFNADUQFghbMAk&url=%68%74%74%70%3a%2f%2f%70%6c%61%79%2d%77%69%74%68%2d%64%6f%63%6b%65%72%2e%63%6f%6d%2f&usg=AFQjCNEMuuAFK-sAUH3Wpyybe5UZHrhAWw "Play With Docker")




[Docker (软件)](https://zh.wikipedia.org/zh-cn/Docker_\(%E8%BB%9F%E9%AB%94\))   
[Docker 教程](http://www.runoob.com/docker/docker-tutorial.html)   
[Docker —— 从入门到实践](https://www.gitbook.com/book/yeasy/docker_practice/details "GitBook")   看这里吧，这本书一直都有更新。 
[Docker 极客学院](http://wiki.jikexueyuan.com/list/docker/)   
[Docker入门教程（一）介绍](http://dockone.io/article/101)   

百度云上有一套  《实战 Docker到Kuberneter技术系列视频教程》

 [宋宝华：Docker 最初的2小时(Docker从入门到入门)](http://blog.csdn.net/21cnbao/article/details/56275456) 后面如果有时间，作者会再完成一个《Docker 相处的8小时》。   
[宋宝华- KVM最初的2小时（KVM从入门到入不了门）](http://blog.csdn.net/21cnbao/article/details/56654334)   



其它：  

[11个Docker的奇思妙用](https://mp.weixin.qq.com/s?__biz=MzA4MzQ1NjQ5Nw==&mid=207201323&idx=1&sn=7da24c12ac97e41c94237a0e323f7fe9&scene=21#wechat_redirect "11个Docker的奇思妙用")






## Docker介绍

> 第一课



### Docker Image





### Docker Container

Docker Container 是共享内核的，Docker Container是Docker Image的运行实例。Docker Container里面可以运行不同OS的Image（这里OS相当于就是壳）

Docker Container 的IP地址只能在当前的主机上才可以ping通。



### Docker Container的生命周期



Docker Container中运行的命令都是前台的。不管你是否是以后台方式启动的该命令，只要命令命令运行完成，Docker Container就会消亡。很多时候Docker Container作为临时使用。



### Docker Daemon

守护进程。对应的程序现在已经从 `docker daemon` 变为了 `dockerd`





###   Docker Registry



Docker Registry：分为公有和私有。

Docker Hub 属于公有的



### Docker核心组件的关系

首先在主机(Host)上安装一个Docker Deamon，它负责启动Docker Container(可以是多个)，它在启动容器的过程中会从Docker Hub中拉取image。

通过Docker Client操作Docker Deamon





## Docker 部署和配置

> 第2课

### 安装社区版 Docker CE 

对于使用 Docker 而言，使用最新版本非常重要。所以不要直接使用 yum 或 apt 安装 docker，我们需要先进行配置一下。

参考这里在Ubuntu 16.04上安装成功：[Docker CE 镜像源站-博客-云栖社区-阿里云](https://yq.aliyun.com/articles/110806 "Docker CE 镜像源站-博客-云栖社区-阿里云") ，安装成功。




> [fedora安装 Get Docker CE for Fedora - Docker Documentation](https://docs.docker.com/engine/installation/linux/docker-ce/fedora/ "Get Docker CE for Fedora - Docker Documentation" ) 可直接参考**官方文档**，但是官网下载速度慢。
>
>  [清华大学开源软件镜像站 - Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/ "清华大学开源软件镜像站 - Tsinghua Open Source Mirror") （这里选择：对于 amd64 架构的计算机，添加软件仓库）。
>
> [Centos7上安装docker-ce社区版 - 瀚海星空 - 周海汉博客](http://abloz.com/tech/2017/06/06/centos7-docker-installation/ "Centos7上安装docker-ce社区版 - 瀚海星空 - 周海汉博客")



**设置开机启动Docker Deamon进程：**

```shell
# 开启 docker 服务
systemctl start docker.service
# 设置开机启动
systemctl enable docker.service
```



> CentOS 的 firewalld 会导致 Docker不能正常运行，需要将其关闭 `systemctl disable firewalld`（未验证）。
>
> 并且需要安装 iptables：因为Docker(1.8)会做一些端口映射
>
> ```shell
> yum -y install iptables-services
> systemctl enable iptables
> systemctl start iptables
> ```



安装并启动docker之后，必须是root用户或者是docker组中的用户才能运行命令。

比如尝试运行 `docker info`：

```shell
$ docker info
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

创建 docker 用户组：

```shell
$ sudo groupadd docker
```

将当前用户添加到docker用户组：

```shell
$ sudo usermod -aG docker $USER
```

然后重启系统以生效：直接**注销**即可

```shell
$ sudo shutdown -r now
```



### 配置加速器



由于某些原因，在国内访问这些服务可能会比较慢。国内的一些云服务商提供了针对 Docker Hub 的镜像服务（Registry Mirror），这些镜像服务被称为**加速器**。常见的有 [阿里云加速器](https://cr.console.aliyun.com/#/accelerator)、[DaoCloud 加速器](https://www.daocloud.io/mirror#accelerator-doc)、[灵雀云加速器](http://docs.alauda.cn/feature/accelerator.html)等。使用加速器会直接从国内的地址下载 Docker Hub 的镜像，比直接从官方网站下载速度会提高很多。在后面的章节中会有进一步如何配置加速器的讲解。

国内也有一些云服务商提供类似于 Docker Hub 的公开服务。比如 [时速云镜像仓库](https://hub.tenxcloud.com/)、[网易云镜像服务](https://c.163.com/hub#/m/library/)、[DaoCloud 镜像市场](https://hub.daocloud.io/)、[阿里云镜像库](https://cr.console.aliyun.com/)等。

[阿里云加速器](https://cr.console.aliyun.com/#/accelerator "阿里云加速器") 点击此链接登录阿里云，然后可能会弹出对话框让你设置docker镜像的独立密码（这里的密码与你的专属链接没有关系），设置完成点击"Docker Hub镜像站点" 会看到属于你的**专属链接**，并附有操作说明（**注意**：不要参考此处的操作说明，它既有可能是配置老版本的docker的方法，会造成之后的配置出错）。



[给Docker配置官方国内加速镜像 - 运维之美](http://www.10tiao.com/html/357/201706/2247485374/1.html "给Docker配置官方国内加速镜像 - 运维之美 ")

[Docker 加速器 - DCS 文档 (DaoCloud加速器)](http://guide.daocloud.io/dcs/docker-9153151.html "Docker 加速器 - DCS 文档")

[Docker 镜像加速器-博客-云栖社区-阿里云](https://yq.aliyun.com/articles/29941 "Docker 镜像加速器-博客-云栖社区-阿里云")

[Ubuntu16.04安装Docker及配置镜像加速器](http://www.itfanr.cc/2017/01/14/ubuntu-install-docker-and-configure-mirror-accelerator/ "Ubuntu16.04安装Docker及配置镜像加速器")

[Docker 问答录（95 问） · 大桥下的蜗牛](https://blog.lab99.org/post/docker-2016-07-14-faq.html "Docker 问答录（95 问） · 大桥下的蜗牛")   配置加速器还是这里说的清楚。

[个人维护的 Docker 加速仓库 — 漠然](https://mritd.me/2017/03/21/private-maintenance-docker-mirror-registry/ "个人维护的 Docker 加速仓库 — 漠然")



**成功的配置方法：**

```shell
# 查看版本 
[fan 23:19:05]~$ sudo docker -v
Docker version 17.06.1-ce, build 874a737

# 先设置开机启动
[fan 23:19:05]~$ sudo systemctl enable docker

# 编辑 docker.service 文件来配置
[fan 08:10:11]~$ sudo vim /etc/systemd/system/multi-user.target.wants/docker.service 
# 修改 ExecStart=  这一行，改为
# ExecStart=/usr/bin/dockerd --registry-mirror=加速器地址

# restart
[fan 08:12:19]~$ sudo systemctl daemon-reload 
[fan 08:12:46]~$ sudo systemctl restart docker

# 查看是否配置成功（是否出现：--registry-mirror=加速地址）
[fan 08:13:05]~$ sudo ps -ef | grep dockerd
root      7070     1  1 08:13 ?        00:00:00 /usr/bin/dockerd --registry-mirror=https://bura38ov.mirror.aliyuncs.com
fan       7189  5333  0 08:13 pts/1    00:00:00 grep --color=auto dockerd
```

再运行下面的命令试一下：

```shell
$ docker run hello-world
```





错误1：命令写错

```shell
# 单词拼写错误 将 daemon 拼写为 deamon
[fan 22:42:32]~$ sudo systemctl deamon-reload
Unknown operation deamon-reload.
[fan 22:46:07]~$ sudo systemctl restart docker
Warning: docker.service changed on disk. Run 'systemctl daemon-reload' to reload units.
# 正确单词  daemon-reload
[fan 22:48:28]~$ sudo systemctl daemon-reload
```

错误2: 配置加速器时一定要按照相应版本来配置

查看版本：

```shell
[fan 23:19:05]~$ sudo docker -v
Docker version 17.06.1-ce, build 874a737
```

开始我尝试了阿里提供的方法(修改daemon.json文件)，**没有用**。然后我又尝试了另一种方法(修改docker.service文件)，结果出现了下面的错误：

```shell
[fan 22:57:33]~$ sudo vim /etc/systemd/system/multi-user.target.wants/docker.service
[fan 22:57:33]~$ sudo systemctl daemon-reload
[fan 22:57:45]~$ sudo systemctl restart docker
Job for docker.service failed because the control process exited with error code. See "systemctl status docker.service" and "journalctl -xe" for details.
[fan 22:57:52]~$ sudo systemctl status docker.service 
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: inactive (dead) (Result: exit-code) since 三 2017-08-23 22:57:53 CST; 18s ago
     Docs: https://docs.docker.com
  Process: 17860 ExecStart=/usr/bin/dockerd --registry-mirrors=https://jxus37ad.mirror.aliyuncs.com (code=exited, status=1/FAILURE)
 Main PID: 17860 (code=exited, status=1/FAILURE)
```

出现错误的原因是**必须先删除之前创建的 daemon.json 文件**。

**还有个坑人的地方**是，docker.service文件也需要根据版本来配置。原则就是："Docker 1.12 之前的版本，`dockerd` 应该换为 `docker daemon`，更早的版本则是 `docker -d`"。（之前看到网上有些教程附带有 `-d -H`参数什么的也跟着乱配）。



> 这里 `https://jxus37ad.mirror.aliyuncs.com` 如何与用户对应？
>
> 我的本地电脑用户名称与阿里云帐号的用户名称。这里并不需要对应。






```shell
[root@centos7 ~]# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 08:00:27:01:d1:2f brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic enp0s3
       valid_lft 84785sec preferred_lft 84785sec
    inet6 fe80::a00:27ff:fe01:d12f/64 scope link 
       valid_lft forever preferred_lft forever
3: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN 
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0
       valid_lft forever preferred_lft forever
4: virbr0-nic: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast state DOWN qlen 500
    link/ether 52:54:00:62:8b:46 brd ff:ff:ff:ff:ff:ff
5: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN 
    link/ether 02:42:d0:8f:2d:00 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 scope global docker0
       valid_lft forever preferred_lft forever
```

看第20行：docker会创建一个 docker0的网桥，并分配了私有网段 `172.17.0.1/16`,docker中的所有容器将会在此网段上分配一个可用的ip地址；该地址是私有地址只能在本机访问。



**Docker配置文件与日志：**

配置文件： `/etc/sysconfig/docker`

docker服务的配置文件： `/usr/lib/systemd/system/docker.service`

日志文件：`/var/log/message`，查找： `tail -f /var/log/message | grep docker`



## Docker基础命令



Docker运行容器前需要本地存在对应的镜像,如果镜像不存在本地,Docker	会从
镜像仓库下载(默认是 Docker	Hub	公共注册服务器中的仓库)。

### docker search 搜索镜像

`docker search java`  : 查找一个Java镜像。



### docker pull 拉取镜像到本地



`docker	pull	[选项][Docker Registry地址]<仓库名>:<标签>`

 `docker  pull java`   会拉取默认版本

`docker pull index.tenxcloud.com/docker_library/nginx`



### docker images

 查看本地已经加载的images



### docker run

该命令需要详细解释

注意：`docker run 。。。`里面的命令结束了，container就结束了。

```shell
# 在 
docker run -it java java -version

# 还可在java镜像中运行 ps 命令，这意味着java镜像也是一个Linux容器
docker run -it java ps

docker run -it java uname
# 查看该容器的 ip
docker run -it java ip addr
# 查看该容器的环境变量
docker run -it java env
```





对于临时性的容器我们可以使用 `docker run -rm 。。。`运行完成就删除



### docker ps

docker ps  ： 查看正在运行的容器

docker pa -a ：查看运行过的所有的容器



### docker create



### docker start



### docker stop



### docker pause



### docker unpause





补充知识：

容器中不建议更改配置文件，所以最常用的就是通过环境变量与其进行的信息传输。

但是对于用户密码等并合适通过明文的环境变量进行传递，它又提供了某种机制来保证安全。









## Docker实战之自定义容器镜像

> 第3课

将 容器  变为  镜像





## Docker图形化管理和监控

> 第7课

