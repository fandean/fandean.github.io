注解配置



## 替换xml中的 bean 标签

用于创建对象的；他们的作用就和在 XML 配置文件中编写一个`<bean>`标签实现的功能是一样的 。



### 控制反转





注解：

用于class上

`@Component`： 用于把当前类对象存入spring容器中。



`@Component`的衍生类：作用相同

- `@Controller` ：用来修饰web层的类
- `@Service` ： 用来修饰 service层的类
- `@Repository` ： 用来修饰 dao 层的类



那么对于简单的JavaBean如何存入Spring容器？





### 依赖注入

用于class内部



`@Autowired` ：自动按类型注入。有条件。位置 变量上，或set方法上。



`@Qualifier` 需要与 `@Autowired`  一起使用



`@Resource` ：相当于同时使用  `@Autowired` 和 `@Qualifier`  

使用 jdk 10 时可能有问题

`@Resource`是基于



`@Value` ： 用于注入**基本类型**和String类型的字段。可以使用 SpEL表达式。







### 作用域



`@Scope` 





### 初始化和销毁



`@PostConstruct`



`@PreDestroy`





## JavaConfig替换整个xml



那么 `@Bean` 和 `@Component` 的区别

- `@Bean` 用于把当前方法的返回值作为 bean 对象存入 spring 的 ioc 容器中 。要在JavaConfig中声明一个简单的 bean ，我们需要编写一个方法，这个方法会创建所需 类型的实例，然后给这个方法添加 注解。  

- `@Component` 用于把当前类对象存入 spring 容器中 。

