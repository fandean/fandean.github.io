







## 安装 spring-boot



[springboot - docker logs为何没有日志输出？ - SegmentFault 思否](https://segmentfault.com/q/1010000010924740 "springboot - docker logs为何没有日志输出？ - SegmentFault 思否")





## 安装 Tomcat

在拉取 tomcat 镜像的时候，可能搞不明白为什么会有如此之多的tag？这里我们先了解一下，该镜像相关的Variants（变体）的含义:



- `tomcat:<version>`：如果您不确定您的需求是什么，您可能想要使用这个。它被设计为既可以用作丢弃容器（安装源代码并启动容器来启动应用程序），也可以用作构建其他图像的基础。
- `tomcat:slim`：此映像不包含默认tag中包含的公共包，仅包含运行tomcat所需的最小包。除非您在仅部署tomcat映像并且存在空间限制的环境中工作，否则我们强烈建议您使用此库的默认镜像(即上一个镜像)。 (slim：瘦)
- `tomcat:alpine` 此镜像基于流行的Alpine Linux项目 。（不了解什么是 Alpine Linux Project，不下这个版本）
- `tomcat:<version>-jre*`：这个又是什么意思？查看Dockerfile文件，似乎所有文件都是`FROM openjdk:*-jre` 开头，那么所有镜像都是以openjdk作为基础镜像的？



还是没搞懂，这里选择 `8.5.32` 

```
docker pull tomcat:8.5.32
```

运行容器

```shell
# 记得修改 tag
$ docker run -it --rm -p 8888:8080 tomcat:tag
# You can then go to http://localhost:8888 or http://host-ip:8888 in a browser
```



tomcat容器的使用：







## 安装CentOS

**Tag的选择：**

The CentOS Project offers regularly updated images for all active releases. These images will be updated monthly or as needed for emergency fixes. These rolling updates（滚动更新） are tagged with the major version number **only**. For example:

建议pull的image：

```
docker pull centos:6
```

```
docker pull centos:7
```



> tag带有小数点的版本不进行滚动更新维护





## 安装 Oracle Db 11

[wnameless/docker-oracle-xe-11g: Dockerfile of Oracle Database Express Edition 11g Release 2](https://github.com/wnameless/docker-oracle-xe-11g "wnameless/docker-oracle-xe-11g: Dockerfile of Oracle Database Express Edition 11g Release 2")





## Spring boot

[spring-guides/gs-spring-boot-docker: Spring Boot with Docker :: Learn how to create a Docker container from a Spring Boot application with Maven or Gradle](https://github.com/spring-guides/gs-spring-boot-docker "spring-guides/gs-spring-boot-docker: Spring Boot with Docker :: Learn how to create a Docker container from a Spring Boot application with Maven or Gradle")





## docker lnmp



[docker：Dockerfile构建LNMP平台-DevOps(甘兵)-51CTO博客](http://blog.51cto.com/ganbing/2074640 "docker：Dockerfile构建LNMP平台-DevOps(甘兵)-51CTO博客")

[docker：编排与部署小神器Compose-DevOps(甘兵)-51CTO博客](http://blog.51cto.com/ganbing/2083806 "docker：编排与部署小神器Compose-DevOps(甘兵)-51CTO博客")

[voocel/docker-lnmp: Docker-compose(Linux,Nginx,MySql,PHP7,Redis)](https://github.com/voocel/docker-lnmp "voocel/docker-lnmp: Docker-compose(Linux,Nginx,MySql,PHP7,Redis)")







## docker redis



**配置文件：**

You can create your own Dockerfile that adds a redis.conf from the context into /data/, like so.，通过Dockerfile

```
FROM redis
COPY redis.conf /usr/local/etc/redis/redis.conf
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
```

或者直接在 docker run中：

```
$ docker run -v /myredis/conf/redis.conf:/usr/local/etc/redis/redis.conf --name myredis redis redis-server /usr/local/etc/redis/redis.conf
```

好吧redis容器中并不存在`/usr/local/etc/redis/redis.conf`文件，如果需要使用配置文件，可以下载一个redis压缩包，解压后使用里面的 redis.conf 文件，然后将此配置文件随便挂载到容器的某个目录，但是要与 `redis-server`命令后跟的路径一直即可。







**数据持久化：**

由于redis默认在内存中存储数据，如果需要将数据进行持久化就需要进行配置。

```
$ docker run --name some-redis -d redis redis-server --appendonly yes
```

If persistence is enabled, data is stored in the `VOLUME /data`, which can be used with `--volumes-from some-volume-container` or `-v /docker/host/dir:/data`



redis有两种数据持久化方式：

- RDB模式 -- 快照模式 。RDB是默认开启的，就是配置文件中的 `save 900 1部分（如果有配置文件）`。Redis会定时把内存中的数据备份，生成“快照文件”。文件名称是dump.rdb，默认被保存在了Redis的安装目录里。

- AOF模式 。AOF需要手动配置开启 。可在配置文件中开启：

  ```
  appendonly yes                        #默认是no，未开启AOF。设置为yes表示开启AOF模式。
  appendfilename “appendonly.aof”    #默认生成的AOF文件名称
  ```

  或通过相关选项开启：`redis-server --appendonly yes`



感觉根据redis的使用方式，只需在运行时能够进行持久化即可，而无需挂载数据卷







## javaee

先创建javaee网络：

```shell
docker network create -d bridge javaee
```

再运行各容器：

```shell
docker run --name javaee-mysql5.5 -v G:/Docker/JavaEERuntime/mysql5.5/data:/var/lib/mysql -p 3306:3306 --network javaee -e MYSQL_ROOT_PASSWORD=fan123 -d mysql:5.5.60 --character-set-server=utf8 --collation-server=utf8_unicode_ci --lower-case-table-names=1

docker run --name javaee-tomcat -v G:/Docker/JavaEERuntime/tomcat-8.5/webapps:/usr/local/tomcat/webapps -v G:/Docker/JavaEERuntime/tomcat-8.5/conf:/usr/local/tomcat/conf -p 8080:8080 --network javaee -d tomcat:8.5.32


docker run --name javaee-nginx -v G:/Docker/JavaEERuntime/nginx/html:/usr/share/nginx/html -v G:/Docker/JavaEERuntime/nginx/nginx.conf:/etc/nginx/nginx.conf -p 80:80 --network javaee -d nginx:latest


docker run --name javaee-redis  -v G:/Docker/JavaEERuntime/redis/redis.conf:/usr/local/etc/redis/redis.conf -v G:/Docker/JavaEERuntime/redis/data:/data -p 6379:6379 --network javaee -d redis:latest redis-server /usr/local/etc/redis/redis.conf
```





> 可以使用此方式连接 redis：
>
> ```shell
> # 使用下面的方法不行，提示他们不属于同一个网络
> #docker run -it --link javaee-redis:redis --rm redis redis-cli -h redis -p 6379
> 
> # 使用下面的命令，提示无法连接到127.0.0.1 ( Could not connect to Redis at 127.0.0.1:6379: Connection refused)
> # docker run -it --name redis-cli --network javaee redis:latest redis-cli
> 
> # 使用下面的命令，明确为 credis-cli 指定 host 和 端口
> # # 这里 -h -p 选项是传递给 redis-cli 用的，并非给 docker run 使用
> docker run -it --name redis-cli --network javaee redis:latest redis-cli  -h javaee-redis -p 6379
> ```
>
> 此命令输出：
>
> ```shell
> $ docker run -it --name redis-cli --network javaee redis:latest redis-cli  -h javaee-redis -p 6379
> javaee-redis:6379>
> ```
>
> 



[GoogleContainerTools: Jib](https://github.com/GoogleContainerTools)

Build container images for your Java applications. 谷歌开源的 Java 应用容器生成工具，不用写 Dockerfile，构造过程中自动生成一个 Docker 容器。 









## node



[docker-node/README.md ](https://github.com/nodejs/docker-node/blob/master/README.md "docker-node/README.md at master · nodejs/docker-node")



Run a single Node.js script：

```shell
$ docker run -it --rm --name my-running-script -v "$PWD":/usr/src/app -w /usr/src/app node:8 node your-daemon-or-script.js
```





Create a Dockerfile in your Node.js app project：







Best Practices：

[Best Practices Guide](https://github.com/nodejs/docker-node/blob/master/docs/BestPractices.md "Best Practices Guide")



```shell
$ docker run \
  -e "NODE_ENV=production" \
  -u "node" \
  -m "300M" --memory-swap "1G" \
  -w "/home/node/app" \
  --name "my-nodejs-app" \
  node [script]
```

