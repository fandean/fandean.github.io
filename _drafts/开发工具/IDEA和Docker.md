

# 在IDEA中使用Docker

1. 在系统上安装Docker
2. 为idea安装Docker integration plugin
3. 配置Docker： `Setting > General >勾选 "Expose daemon on tcp://localhost:2375 without TLS"` （作用：将docker与本地的连接设置为不需要TLS加密）
4. 配置idea：`Setting >Build,Execution,Deployment > Docker > 点击+ > Connect to Docker deamon with:处选择 TCP socket > 使用默认的url ` 之后在界面中就会看到 "Connetion successful" 字样。



> 强烈推荐：[如何使用windows版Docker并在IntelliJ IDEA使用Docker运行Spring Cloud项目 - 嘿123 - 博客园](https://www.cnblogs.com/hei12138/p/ideausedocker.html "如何使用windows版Docker并在IntelliJ IDEA使用Docker运行Spring Cloud项目 - 嘿123 - 博客园")



## Docker integration plugin

[Docker - Help | IntelliJ IDEA](https://www.jetbrains.com/help/idea/docker.html "Docker - Help | IntelliJ IDEA")















> [IntelliJ IDEA中Docker使用 - CSDN博客](https://blog.csdn.net/lovelife527386108/article/details/51697081 "IntelliJ IDEA中Docker使用 - CSDN博客")
>
> [IDEA中配置及使用Docker - CSDN博客](https://blog.csdn.net/jacksonary/article/details/78974344 "IDEA中配置及使用Docker - CSDN博客")  * 