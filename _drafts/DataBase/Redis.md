# Redis





## 命令



> 客户端和服务端命令有混淆



### Redis客户端命令



`config` 命令： 

```shell
# config get 命令：获取某设置的值
config get <config_setting_name>
```

```shell
# 获取所有配置
config get * 
```

```
# config set 命令：设置某设置的值
config get <config_setting_name> <new_config_value>
```



ping 命令：检查服务器是否正在运行



redis-cli 客户端的使用：

```shell
# 语法
redis-cli -h host -p port -a password
```

```shell
# 示例：
redis-cli -h 127.0.0.1 -p 6379 -a "mypass" 
```



redis连接命令：

```
# 使用给定的密码验证服务器
auth <password>
```



`quit`命令：关闭当前连接。



`select index` 切换到指定的数据库，数据库索引号 `index` 用数字值指定，以 `0` 作为起始索引值。默认使用 `0` 号数据库。







### Redis服务器端命令



`info` 命令获取 有关服务器的所有统计信息和信息 



设置验证密码：连接的任何客户端在执行命令之前都需要进行身份验证。要保护Redis安全，需要在配置文件中设置密码。 

```shell
# 获取现有密码
CONFIG get requirepass

# 设置密码：
CONFIG set requirepass "yiibai"
```



设置密码后，如果任何客户端运行命令而不进行身份验证，则会返回一个**(error) NOAUTH Authentication required.**的错误信息。 因此，客户端需要使用AUTH命令来验证。 

```shell
# AUTH <password>
```





