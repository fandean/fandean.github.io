

两个主流的框架  

- Spring-Security
- Shiro 





## 日期处理



跨站请求伪造（cross-site request forgery，CSRF） 





## 配置 spring-security 

观察 UserController，其并未包含处理 类似`/user/login/`的控制器，

且UserService继承了 spring security 提供的接口

配置 Spring-Security.xml

相当于在配置相关 Controller 的逻辑

从而无需手动配置 Controller



拦截器





## 页面授权控制



 页面权限控制，只需在`spring-secrity`中修改：

```
设置 use-expressions="true"，
access修改：access="hasAnyRole('ROLE_USER','ROLE_ADMIN')"  
```



```xml
<security:http auto-config="true" use-expressions="true">
    <!-- 配置拦截的请求地址，任何请求地址都必须有ROLE_USER的权限 -->
    <security:intercept-url pattern="/index.jsp" access="ROLE_USER" /> <!-- 可以共存 -->
    <!-- 注意下面的格式 -->
    <security:intercept-url pattern="/**" access="hasAnyRole('ROLE_USER','ROLE_ADMIN')" />
    
	//略....
</security:http>
```



然后在页面使用 security:authorize 标签

```xml
<%@ taglib prefix="security" uri="http://www.springframework.org/security/tags" %>
```



```xml
<security:authorize access="hasAnyRole('ROLE_ADMIN','ROLE_USER')">
```



**用户只是页面看不到菜单按钮，但让然能访问原来地址**，我们需要做后台权限控制。







## 后台数据校验



使用sple表达式



- jsr250 提供的**注解**
- security 自带注解
- 还有一种注解  pre-ano...







JSRs: Java Specification Requests   ： Java规范请求   

JSR 269: Pluggable Annotation Processing API   

[The Java Community Process(SM) Program - JSRs: Java Specification Requests - detail JSR# 269](https://www.jcp.org/en/jsr/detail?id=269 "The Java Community Process(SM) Program - JSRs: Java Specification Requests - detail JSR# 269")

该JSR将为J2SE和J2EE平台中的通用语义概念开发注释，这些注释适用于各种单独的技术。









## 日志



目标，对所有 Controller  的方法的调用进行记录



在日志中保存用户 id ： 通过监听器 将request放入spring 的 ioc容器









动态菜单：



main.jsp 不在 pages目录下，所以没有由视图解析器管理，所以不会经过 Spring的拦截器。









