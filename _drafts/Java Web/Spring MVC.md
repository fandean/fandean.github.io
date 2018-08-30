# Spring MVC



MVC： 处理请求先到达控制器（Controller），控制器的作用是进行请求分发，这样它会根据请求的内容去访问模型层（Model）；在现今互联网系统中，数据主要从数据库和NoSQL中来，而且对于数据库而言往往还存在事务的机制，为了适应这样的变化，设计者会把模型层再细分为两层，即服务层（Service）和数据访问层（DAO）；当控制器获取到由模型层返回的数据后，就将数据渲染到视图中，这样就能够展现给用户了。





Spring将请求在调 度Servlet、处理器映射（handler mapping）、控制器以及视图解析器（view resolver）之间移动 。



## 跟踪Spring MVC的请求















## 异常



错误1： No bean named 'cacheManager' available

```
org.springframework.beans.factory.NoSuchBeanDefinitionException: No bean named 'cacheManager' available
```



[No bean named 'cacheManager' is defined - 简书](https://www.jianshu.com/p/5a964f49ec26 "No bean named 'cacheManager' is defined - 简书")

修改的部分：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           
       http://www.springframework.org/schema/mvc
       http://www.springframework.org/schema/mvc/spring-mvc.xsd">
```



