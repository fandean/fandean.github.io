



重点：

```
     * BeanFactory 才是 Spring 容器中的顶层接口。
     * ApplicationContext 是它的子接口。
     * BeanFactory 和 ApplicationContext 的区别：
     * 创建对象的时间点不一样。
     * ApplicationContext：只要一读取配置文件，默认情况下就会创建 所有对象 。（立即加载）
     * BeanFactory：什么时候使，用什么时候创建对象。（延迟加载）
     *
     * Spring 创建这个类的时候，默认采用的单例的模式进行创建的。如果想去改变单例模式，需
     * 要通过 scope 进行配置。
```

Spring 创建这个类的时候，默认采用的单例的模式进行创建的？





```java
public class Client {

    // 模拟Action

//    /**
//     * 测试由ApplicationContext对象获取spring容器中创建的对象
//     * @param args
//     */
//    public static void main(String[] args) {
//        // 代码之间存在依赖关系（耦合）
//        // AccountService accountService = new AccountServiceImpl();
//        // 由spring创建对象（完成对象的解耦）
//        ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
//        // 通过名称调用（通过spring容器中的id属性）(推荐）
//        AccountService accountService = (AccountService) ac.getBean("accountService");
//        // 通过类型调用（通过spring容器中的class属性）
//        // AccountService accountService = ac.getBean(AccountServiceImpl.class);
//        accountService.saveAccount();
//    }

    /**
     * 测试BeanFactory和ApplicationContext之间的区别
     *
     * ApplicationContext：只要一读取配置文件，默认情况下就会创建对象。（立即加载）
       BeanFactory：什么时候使，用什么时候创建对象。（延迟加载）
     * @param args
     */
//    public static void main(String[] args) {
//        // 使用ApplicationContext创建对象默认是单例（只要加载spring容器，对象会立即创建，叫做立即检索）
//        // ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
//        // 使用BeanFactory创建对象默认是单例（当加载spring容器的时候，不会执行构造方法，对象不会立即创建，只要调用getBean的方法，对象才会创建，叫做延迟检索）
//        BeanFactory ac = new XmlBeanFactory(new ClassPathResource("applicationContext.xml"));
//        AccountService accountService = (AccountService) ac.getBean("accountService");
//        System.out.println(accountService);
//
//        AccountService accountService1 = (AccountService) ac.getBean("accountService");
//        System.out.println(accountService1);
//    }

    /**
     * 【ApplicationContext 接口的实现类 】
     （1）ClassPathXmlApplicationContext：
     它是从类的根路径下加载配置文件 推荐使用这种
     （2）FileSystemXmlApplicationContext：
     它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置。注意磁盘的权限
     （3）AnnotationConfigApplicationContext:
     当我们使用注解配置容器对象时，需要使用此类来创建spring 容器。它用来读取注解。
     */
//    public static void main(String[] args) {
//        // 测试ClassPathXmlApplicationContext
//        // ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
//        // 测试FileSystemXmlApplicationContext
//        ApplicationContext ac =  new FileSystemXmlApplicationContext("d:/applicationContext.xml");
//        AccountService accountService = (AccountService) ac.getBean("accountService");
//        System.out.println(accountService);
//
//        AccountService accountService1 = (AccountService) ac.getBean("accountService");
//        System.out.println(accountService1);
//    }

    /**
     * id中不能出现特殊字符，name中可以出现特殊的字符。
     可以指定多个name，之间可以用分号（“；”）、空格（“ ”）或逗号（“，”）分隔开，如果没有指定id，那么第一个name为标识符，其余的为别名； 若指定了id属性，则id为标识符，所有的name均为别名。如：
     <bean name="alias1 alias2;alias3,alias4" id="hello1" class="com.zyh.spring3.hello.HelloWorld"> </bean>  
     此时，hello1为标识符，而alias1，alias2，alias3，alias4为别名，它们都可以作为Bean的键值；
     */
    public static void main(String[] args) {
        // 测试ClassPathXmlApplicationContext
        ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
        AccountService accountService = (AccountService) ac.getBean("accountService");
        System.out.println(accountService);
        accountService.saveAccount();


    }
}

```

