

两个主流的框架



跨站请求伪造（cross-site request forgery，CSRF） 



配置 Spring-Security.xml

相当于在配置相关 Controller 的逻辑



无需手动配置 Controller











使用sple表达式



- jsr250 提供的注解

- security 自带注解

- 还有一种注解  pre-ano...





日志：

目标，对所有 Controller  的方法的调用进行记录



在日志中保存用户 id ： 通过监听器 将request放入spring 的 ioc容器









动态菜单：



main.jsp 不在 pages目录下，所以没有由视图解析器管理，所以不会经过 Spring的拦截器。









