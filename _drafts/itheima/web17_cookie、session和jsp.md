# 会话技术





在浏览器关闭后会话才结束。会话数据可以这样理解：其数据保存在浏览器的内存中，当浏览器关闭会话结束，内存被清除，数据也就没了。cookie



Session的默认有效时间为30分钟，若30分钟没有活动，该Session将被销毁；该时间在tomcat的配置文件中指定：

```xml
<session-config>
	<session-timeout>30</session-timeout>
</session-config>
```





ServletContext理解（数据保存）：A访问加入购物车servlet的时候将自己购买的东西存放在该servletContext中，B也同样这样做（在不同客户端），那么他们结算时会发现自己的购物车中会多多出来很多商品。



requestContex更加不适合保存加入购物车的商品。



商品购物车：

- 当用户没有登录，则可以把数据保存在cookie中
- 当用户已经登录，那么就可以把数据保存到服务端的数据库中





cookie只能保存字符串（从其构造方法中可以看出），并且数据保存在客户端不安全。该字符串中不能包含空格。`JSESSIONID=6FDD64CD43F3AD664935E4F84D210EDD` 这就是一个cookie对象，一个cookie对象就只有一个name和一个value：

```java
Cookie(String name, String value) 创建cookie对象
String getName() 获取cookie的名称
String getValue() 获取cookie的值
void setPath(String uri) 设置cookie的路径——浏览器根据这个路径判断那些cookie要发送给服务器
```





### 为什么说session技术是依赖于cookie技术？

因为session的实现需要将一个JSESSIONID保存到客户端，那么就需要使用cookie来保存。

这也是为什么，获取session的方法是：

```java
HttpSession session = request.getSession();
```



session何时**创建**？  

**request.getSession方法有两个功能：**
1. 创建session对象
  - 如果客户端没有JSESSIONID，会创建新的session对象
  - 客户端有JSESSIONID，但是服务端已经没有对应的session对象了， 会创建新的session对象；强制关闭服务器软件时，session对象会被销毁掉。
2. 获取已有的session对象
  - 如果客户端访问时候携带了JSESSIONID，且服务端有对应的session对象存在，就会获取原有的session对象。



```java
HttpSession session = request.getSession();
//结果是 false，那么这个session的作用是？
System.out.println(Objects.isNull(session));
response.getWriter().println(Objects.isNull(session));
```



通过浏览器提供的开发者工具可以看到：建议在隐身模式测试

**首次访问：** http://localhost:8080/visit

 Response Headers内容：有 set-cookie，（此时应该是创建了一个seesion）

```
HTTP/1.1 200
Set-Cookie: JSESSIONID=6FDD64CD43F3AD664935E4F84D210EDD; Path=/; HttpOnly
Content-Length: 13
Date: Sat, 21 Jul 2018 03:28:11 GMT
```

在 Request Headers中：没有携带 cookie

```
GET /visit HTTP/1.1
Host: localhost:8080
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36
DNT: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6
```



**再次访问：**

在 Response Headers中

```
HTTP/1.1 200
Content-Length: 13
Date: Sat, 21 Jul 2018 03:30:18 GMT
```

在 Request Headers中：携带了 cookie

```
GET /visit HTTP/1.1
Host: localhost:8080
Connection: keep-alive
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36
DNT: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6
Cookie: JSESSIONID=6FDD64CD43F3AD664935E4F84D210EDD
```





> Cookie的存在形式是？





















