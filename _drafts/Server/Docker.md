# Docker





[](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/610px-Docker_%28container_engine%29_logo.svg.png)

## 学习资料

[ **如何选择Docker书籍** - Docker 问答录（95 问） · 大桥下的蜗牛](https://blog.lab99.org/post/docker-2016-07-14-faq.html#ru-he-xuan-ze-docker-shu-ji "Docker 问答录（95 问） · 大桥下的蜗牛")

**观察一下当前的 Docker 版本号，选择不要晚于 3 个版本的 Docker 书籍。**否则看到的很多东西可能将会因过时而无法使用，或者已经不必如此繁琐有更简单的方式去实现了。

> Docker的版本号规则发生了改变。以前是v1.12什么的，现在直接变成 v17.06，这里17表示2017年。

Docker中国 (Docker官网的中文镜像)  [Docker 文档 - Docker 中文文档](https://docs.docker-cn.com/ "Docker 文档 - Docker 中文文档")

最近官方推出了这个网站来帮助学习Docker，可以在线练习docker命令哦 ：[Play With Docker](https://www.google.com.hk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=10&ved=0ahUKEwiQ7tzk1e7VAhVHT7wKHSFNADUQFghbMAk&url=%68%74%74%70%3a%2f%2f%70%6c%61%79%2d%77%69%74%68%2d%64%6f%63%6b%65%72%2e%63%6f%6d%2f&usg=AFQjCNEMuuAFK-sAUH3Wpyybe5UZHrhAWw "Play With Docker")



[Docker 入门教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html "Docker 入门教程 - 阮一峰的网络日志")

[Docker (软件)](https://zh.wikipedia.org/zh-cn/Docker_\(%E8%BB%9F%E9%AB%94\))   
[Docker 教程](http://www.runoob.com/docker/docker-tutorial.html)   
[Docker —— 从入门到实践](https://www.gitbook.com/book/yeasy/docker_practice/details "GitBook")   看这里吧，这本书一直都有更新。 
[Docker 极客学院](http://wiki.jikexueyuan.com/list/docker/)   
[Docker入门教程（一）介绍](http://dockone.io/article/101)   

百度云上有一套  《实战 Docker到Kuberneter技术系列视频教程》

 [宋宝华：Docker 最初的2小时(Docker从入门到入门)](http://blog.csdn.net/21cnbao/article/details/56275456) 后面如果有时间，作者会再完成一个《Docker 相处的8小时》。   
[宋宝华- KVM最初的2小时（KVM从入门到入不了门）](http://blog.csdn.net/21cnbao/article/details/56654334)   



[从开发到部署会用到的 Docker 命令](http://mp.weixin.qq.com/s?timestamp=1508205792&src=3&ver=1&signature=LD5Gs4d3SbEX9*Uh66q0yP2osCg-gh0dU6RUupXH9eJLWdHfXXYy9oueR3dEh3SgbwiwgbNGzXs1u-aaCXOwI9vHdmA2FIm8RJnB0WOqvxjts42gdICVTgbpAUR1p7c5U76WHV-a8eVCT47T*eIQ-a1XXKrp7YALISDQVoRAclM= "从开发到部署会用到的 Docker 命令")

其它：  

[11个Docker的奇思妙用](https://mp.weixin.qq.com/s?__biz=MzA4MzQ1NjQ5Nw==&mid=207201323&idx=1&sn=7da24c12ac97e41c94237a0e323f7fe9&scene=21#wechat_redirect "11个Docker的奇思妙用")






## Docker介绍

> 第一课

使用 Docker 可以通过定制应用镜像来实现持续集成、持续交付、部署。开发人员可以通过
Dockerfile 来进行镜像构建，并结合 持续集成(Continuous Integration) 系统进行集成测试





Docker 包括三个基本概念：

- 镜像（Image ） 
- 容器（Container ） 
- 仓库（Repository ）    







### Docker Image





### Docker Container

Docker Container 是共享内核的，Docker Container是Docker Image的运行实例。Docker Container里面可以运行不同OS的Image（这里OS相当于就是壳）

Docker Container 的IP地址只能在当前的主机上才可以ping通。



#### Docker Container的生命周期



Docker Container中运行的命令都是前台的。不管你是否是以后台方式启动的该命令，只要命令运行完成，Docker Container就会消亡。很多时候Docker Container作为临时使用。




###   Docker Registry



Docker Registry：分为公有和私有。

Docker Hub 属于公有的



### Docker核心组件的关系

> Docker Daemon 守护进程。对应的程序现在已经从 `docker daemon` 变为了 `dockerd`



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



### Windows中安装Docker



> 安装 Docker for Windows：
>
> 只有windows 10 内置了Hyper V 虚拟环境，所以只有win10才能安装docker for windows。
>
> 下载安装包安装即可，首次运行会出现下面的提示：“Hyper-V and Containers features are not enabled. Do you want to enable them for Docker to be able to work properly?
> Your computer will restart automatically. Note: VirtualBox will no longer work.（VirtualBox将不能运行）” 开启Hyper-V将不能使用Vbox虚拟机，这个让人感到苦恼，这里有人提供了命令来开启和关闭Hyper-V功能 [virtualbox - Simple instructions needed for enabling and disabling Hyper V Docker - Stack Overflow](https://stackoverflow.com/questions/47081205/simple-instructions-needed-for-enabling-and-disabling-hyper-v-docker "virtualbox - Simple instructions needed for enabling and disabling Hyper V Docker - Stack Overflow")。
>
> You can do below to disable
>
> ```
> dism.exe /Online /Disable-Feature:Microsoft-Hyper-V
> bcdedit /set hypervisorlaunchtype off
> ```
>
> and below to enable
>
> ```
> dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All
> bcdedit /set hypervisorlaunchtype auto 
> ```
>
> From PowerShell
>
> To Disable
>
> ```
> Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
> ```
>
> To Enable
>
> ```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V –All
> ```
> Windows中的相关问题可以参考一下Docker的文档： [Logs and troubleshooting | Docker Documentation](/docker-for-windows/troubleshoot/ "Logs and troubleshooting | Docker Documentation")
> 





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

看第20行：docker会创建一个 `docker0`的网桥，并分配了私有网段 `172.17.0.1/16`,docker中的所有容器将会在此网段上分配一个可用的ip地址；该地址是私有地址只能在本机访问。



**Docker配置文件与日志：**

配置文件： `/etc/sysconfig/docker`

docker服务的配置文件： `/usr/lib/systemd/system/docker.service`

日志文件：`/var/log/message`，查找： `tail -f /var/log/message | grep docker`





### 更改Docker的相关路径

docker for **windows** 安装时默认不能修改路径，所以全部安装在c盘（这让人很火）。



**Disk image location：**

`seting -> Advanced -> Disk image location`，然后更改目录即可，其包含的 vhdx 文件会自动迁移。



> 在我的系统默认是：`C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\MobyLinuxVM.vhdx`（这应该是与我将Docker安装成所以用户可用有关）



> 这里分为linux容器和windows容器： (这里是个人理解，似乎有误)
>
> linux 容器下Docker 容器安装在 MobyLinuxVM.vhdx 内，只要更改VHD 路径即可会自动移动VHD
>
> Windows 容器docker的安装路径默认在`C:\ProgramData\Docker`





> windows上安装的docker其实本质上还是借助与windows平台的hyper-v技术来创建一个linux虚拟机，你执行的所有命令其实都是在这个虚拟机里执行的，所以所有pull到本地的image都会在虚拟机的Virtual hard disks目录的文件中，这个文件就是虚拟硬盘文件。 
>
> [docker for windows pull镜像文件的安装位置改变方法 - CSDN博客](https://blog.csdn.net/stemq/article/details/53150939 "docker for windows pull镜像文件的安装位置改变方法 - CSDN博客")
>
> [window7 修改docker安装的machine 位置 - CSDN博客](https://blog.csdn.net/u011248395/article/details/70994088 "window7 修改docker安装的machine 位置 - CSDN博客")





**Docker运行根目录：** (似乎不需要更改)

Ｄocker 后台进程参数：

更改docker运行根目录的参数：`-g, --graph="/var/lib/docker"`  ：设置Docker运行时根目录

或者可以在deamon.json配置文件中修改：

```json
{
    "graph":"/app/docker"
}
```

在Windows中通过 `setting -> Daemon -> 切换“Basic"按钮 -> `然后就可以配置该文件



> 在cmd中运行 `docker info`命令，会看到 ”Docker Root Dir: /var/lib/docker“



> 在Windows中 `C:\Users\youname\.docker`目录下可以看到 `config.json`，`deamon.json`两个文件





### Docker for Windows 设置 Shared Drives目录

Shared Drives的作用，"Select the local drives you want to be available to your containers."，类似于为虚拟机添加共享文件夹（比如怎样才能让虚拟机中的系统访问主机中的文件）。



Dockers version 18.03.1-ce已经可以正确处理权限问题，设置shared drives目录时会跳出一个对话框让你输入管理员密码就行。



> [win10系统，docker设置共享文件夹](https://newsn.net/say/docker-share-folder.html "win10系统，docker设置共享文件夹")
>
> [在windows10上使用docker哪些坑 - 程序人生 - SegmentFault 思否](https://segmentfault.com/a/1190000006799421 "在windows10上使用docker哪些坑 - 程序人生 - SegmentFault 思否")





## Docker基础命令



Docker运行容器前需要本地存在对应的镜像,如果镜像不存在本地,Docker	会从
镜像仓库下载(默认是 Docker	Hub	公共注册服务器中的仓库)。

### docker search 搜索镜像

`docker search java`  : 查找一个Java镜像。



### docker pull 拉取镜像到本地



完整格式：

```shell
docker pull	[选项][Docker Registry地址]<仓库名>:<标签>
```



> Dockers Registry（Docker镜像仓库地址）完整格式： `<域名/IP>[:端口号]` ；默认值（省略时使用默认值）：默认为 hub.docker.com  
>
> 仓库名，完整格式：`<用户名>/<软件名>`；默认值，如果省略用户名则默认为 `labrary`，它表示官方版本
>
> 标签： 如果省略则表示下载最新版，即 `latest`版



```shell
#  会拉取默认版本（表示从Docker Hub网站下载官方的最新版java）
docker  pull java
```



```shell
docker pull ubuntu
```








### ~~docker images~~

 查看本地已经加载的images



### 镜像相关命令



列出本地已经下载的镜像：

```
docker image ls [关键字]
```



删除本地镜像：

```
docker image rm [选项] <镜像1id> [<镜像2id ...]
```



> 建议通过镜像的 id 或摘要来删除一个镜像，因为它们是一个镜像的唯一标识





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

> 因为Docker的容器实在太轻量级了，很多使用用户都是随时删除和新建容器



当容器中指定的应用终结时，容器也自动终止。



后台运行容器：

在原有运行命令的基础上使用 `-d`参数即可

```shell
$ docker run -d 
```

-d 参数启动后会返回一个唯一的 id    





### 操作容器



`docker run`见上文。



```shell
$ docker container ls

# 要获取容器的输出信息
$ docker container logs [container ID or NAMES]

#  终止一个运行中的容器
$ docker container stop

# 终止状态的容器可以用 下面 命令看到
$ docker container ls -a

# 处于终止状态的容器，可以通过 docker container start 命令来重新启动。
$ docker container start

# 进入在后台运行的容器 docker exec
$ docker exec -it 容器(或id) bash
# 如果从这个 stdin 中 exit，不会导致容器的停止。这就是为什么推荐大家使用 docker exec 的原因。
# docker exec --help

# 来删除一个处于终止状态的容器
$ docker container rm 

# 清理所有处于终止状态的容器
$ docker container prune

# 导出本地某个容器
$ docker export

# 从容器快照文件中再导入为镜像
$ docker import
```



​    



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



### 数据卷

创建数据卷：

```shell
$ docker volume create my-vol
```

查看所有数据卷：

```shell
$ docker volume ls
```

查看指定数据卷信息

```shell
$ docker volume inspect my-vol
```

删除某个数据卷：

```shell
$ docker volume rm my-vol
```

清除所有无主的数据卷：

```shell
$ docker volume prune
```

删除容器时同时删除它使用的数据卷

```shell
$ docker rm -v
```







## Docker实战之自定义容器镜像

> 第3课

将 容器  变为  镜像





## Docker图形化管理和监控

> 第7课



> [容器与云|Dry：一个命令行交互式 Docker 容器管理器](https://linux.cn/article-9615-1.html "容器与云|Dry：一个命令行交互式 Docker 容器管理器")





## 安装 mysql



在Docker Hub上的地址为：[library/mysql](https://hub.docker.com/r/library/mysql/ "library/mysql - Docker Hub") ，打开该连接，默认展示 Repo info 标签页（该标签页中包含了一些操作该容器的方法）中的内容，如果想查看该image大小和各标签，可切换到 "Tags"标签页查看。



> 2018.06，为什么mysql image 都提示有 " This image has vulnerabilities(漏洞) "？
>
> 标记为这类的镜像以为着有漏洞。这些漏洞通常来自他们所基于的系统或者上层镜像所带有的软件以及依赖库，当然也有可能就是软件本身的问题。 这个提示只是表示镜像所基于的环境是存在漏洞的，并不代表漏洞一定会被攻击。 你可以选择使用其Dockerflie重新构建镜像，对有漏洞的软件进行更新，也可以针对漏洞在防火墙层面进行防护。 
>
> 但我还是不知道怎么解决。



**拉取镜像：**

```
docker pull mysql:5.5.60
```



**运行容器：**

简单示例（用于理解各个参数的含义）：

```
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=fan123 -d mysql:5.5.60
```

- **--name**：容器名 
- **-p 3306:3306**：将容器的 3306 端口映射到主机的 3306 端口。 
- **-e MYSQL_ROOT_PASSWORD=123456：**设置环境变量 ，这里是初始化 root 用户的密码。 
- **-d:**  后台运行容器，并返回容器ID



> 补充：
>
> - **-v $PWD/conf:/etc/mysql/conf.d**：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf。
> - **-v $PWD/logs:/logs**：将主机当前目录下的 logs 目录挂载到容器的 /logs。
> - **-v $PWD/data:/var/lib/mysql** ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 
>
> 可以看到`-v`用于将主机目录挂载（mount，会屏蔽原目录中的文件）在容器的某个目录（使用`:`分隔），`$PWD`是一个表示当前目录的一个环境变量，



> 官方给出的示例：
>
> ```
> $ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
> ```
>
> 这里看最后的 `mysql:tag` 表示某镜像，格式是：`容器名: 版本` 。作用：比如 `mysql:5.5.60`它表示使用 `mysql:5.5.60`该镜像为基础来启动容器。



- `-it` ：其中 `-i`表示交互式操作（让容器的标准输入保持打开），`-t`表示终端；（交互式终端）
- `--rm`：表示容器退出后就将其删除，默认情况下，为了排障需求，退出的容 器并不会立即删除，除非手动 docker rm 。我们这里只是随便执行个命令，看看结果， 不需要排障和保留结果，因此使用 `--rm` 可以避免浪费空间。    





**进入mysql容器：**

在使用`-d`参数时，容器启动后会进入后台。如果此时需要进入容器进行操作，可以使用`docker exec`命令.



```shell
# 先查看运行中的容器
PS G:\Docker> docker container ls
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
a936fdfe89b5        mysql:5.5.60        "docker-entrypoint.s…"   39 minutes ago      Up 39 minutes       0.0.0.0:3306->3306/tcp   mysql
# 可以看到mysql容器的短id值，这里我们取前3位即可辨识
# 使用docker exec进入容器， -it 交互式终端  bash 表示使用熟悉的Linux命令提示符形式
PS G:\Docker> docker exec -it a93 bash
root@a936fdfe89b5:/#
```



终止mysql容器：

```shell
# 之前已经知道了 mysql 容器的 id值，使用 a93即可标识该容器

# 那么可以使用下面的命令关闭容器
docker container stop a93

# 当然使用 mysql来标识该容器也是可以的
docker container stop mysql

# 使用ps检查该容器
docker ps -a
# 或 
docker container ls -a

# 处于终止的容器还可使用下面的命令重新启动
docker container start mysql
```



删除容器：

使用 `docker container rm `来删除一个处于终止状态的容器



清楚所有处于终止状态的容器：

`docker container prune`





**存在的三个问题：**

- 数据保存的路径在哪？
- 如果编辑mysql的配置文件？比如需要修改字符集为utf8
- 如果查看日志文件



当实际使用时还需要考虑，在该容器中mysql的各种文件存放的位置在哪里，只有知道了相关目录那么我们就可以通过使用 `-v`挂载主机中的目录来替换容器中的目录：

相关文件的路径可以通过查看mysql映像本身内的相关文件(比如看看Dockerfile中)和目录以获取更多详细信息。 

 查看该镜像的Dockerfile文件可知：

- 数据目录位于 `/var/lib/mysql`；所以我们可以在`docker run` 命令中添加下面的选项来覆盖该目录：

  ```
  -v G:/Docker/mysql/mysql5.5.60/date:/var/lib/mysql
  ```

  意为，将本机G盘下的 ... date目录挂载到容器的`/var/lib/mysql`目录上

- 默认配置文件目录位于 `/etc/mysql/my.cnf`对于该配置文件我们可以直接覆盖，如果在Dockerfile中还看到`!includedir /etc/mysql/conf.d/`,那么说明mysql会先加载 my.cnf 中的配置，再加载  conf.d 文件夹中配置文件的的配置，利用这一点我们可以保留 my.cnf 中的配置，而将自定义的配置文件放在 conf.d 目录下。

  所以我们可以在`docker run` 命令中添加下面的选项来覆盖该目录：

  ```
  -v G:/Docker/mysql/mysql5.5.60/custom:/etc/mysql/conf.d
  ```

  那么我们可以在本机G盘的 custom目录下创建一个名为`config-file.cnf`配置文件，mysql容器就会加载该配置文件。



> `config-file.cnf`文件内容：(为了设置服务端编码)
>
> ```
> [mysqld]
> 	character_set_server=utf8
> ```



> 参考： [library/mysql - Docker Hub](https://hub.docker.com/r/library/mysql/ "library/mysql - Docker Hub") 下的 Using a custom MySQL configuration file
>
> mysql 镜像 的Dockerfile 文件也可以在上面链接中找到。



**启动一个 mysql 容器的完整命令：**

```shell
$ docker run --name mysql5.5 -v G:/Docker/mysql/mysql5.5.60/custom:/etc/mysql/conf.d -v G:/Docker/mysql/mysql5.5.60/date:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=fan123 -d mysql:5.5.60
```



> 补充： 
>
> 实际开发中，一个 image 文件往往通过继承另一个 image 文件，加上一些个性化设置而生成。举例来说，你可以在 Ubuntu 的 image 基础上，往里面加入 Apache 服务器，形成你的 image。 







## 学习资料

[Docker入门教程-慕课网](https://www.imooc.com/learn/867?mc_marking=40eb6678df9f85e7a854421cef4ba5e9&mc_channel=syb43 "Docker入门教程-慕课网")