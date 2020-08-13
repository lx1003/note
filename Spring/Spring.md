![](../images/springframework.png)

@RestController和@Controller

单独使用@Controller不加@ResponseBody的话一般使用在要返回一个视图的情况，这种情况属于比较传统的Spring MVC的应用，对应于前后端不分离的情况

![img](https://camo.githubusercontent.com/52faa10d798a9e6515336bd671489a7ba4148246/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d372f537072696e674d56432545342542432541302545372542422539462545352542372541352545342542442539432545362542352538312545372541382538422e706e67)

@RestController

@RestController只返回对象，对象数据直接以JSON或XML形式写入HTTP响应中，这种情况属于Restful Web服务，这也是目前日常开发所接触的最常用的情况

![SpringMVC+RestController](https://camo.githubusercontent.com/a6239d8cef1ae38f55ce0b5dd5c7cbe2aa8a18e7/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d372f537072696e674d564352657374436f6e74726f6c6c65722e706e67)

#### 对于IOC和AOP的理解

IOC（inverse of Control）是一种设计思想，就是将原来的程序中手动创建对象的控制权，交由Spring框架来管理。IOC容器是Spring用来实现Ioc的载体，Ioc容器实际上就是个Map<key,Value>，Map中存放的是各种对象

将对象之间的相互依赖关系交给IoC容器来管理，并由Ioc容器完成对象的注入。这样可以很大程度上简化应用开发，把应用从复杂的依赖关系中解放出来。

Ioc容器就像一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的

![](../images/spring_ioc.png)

##### AOP

AOP能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可扩展性和可维护性

Spring AOP就是基于动态代理的，如果要代理的对象，实现了某个接口，那么Spring AOP会使用JDK Proxy，去创建代理对象，而对于没有实现接口的对象，就无法使用JDK Proxy去进行代理了，这时候Spring AOP会使用Cglib，这时候Spring AOP会使用Cglib生成一个被代理对象的子类来作为代理

![](../images/spring_aop.jpg)

#### Spring Bean

##### spring中的bean的作用域有哪些

- singleton:唯一bean实例，Spring中的bean默认都是单例的
- prototype:每次请求都会创建一个新的bean实现
- request：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效
- session：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP session内有效
- global-session：全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。

##### Spring中的单例bean的线程安全问题了解吗

大部分时候我们并没有在系统中使用多线程，所以很少有人会关注这个问题。单例bean存在线程问题，主要是因为多个线程操作同一个对象的时候，对这个对象的非静态成员变量的写操作会存在线程安全问题

常见的两种解决方法：

1. 在Bean对象中尽量避免定义可变的成员变量
2. 在类中定义一个ThreadLocal成员变量，将需要的可变成员变量保存在ThreadLocl中

##### @Component和@Bean的区别是什么

1. 作用对象不同：@Component注解作用于类，而@Bean注解作用域方法
2. @Component通常是通过类路径扫描来自侦测以及自动装配到Spring容器中（可以使用@ComponentScan注解定义要扫描的路径从中找出表示了需要装配的类自动装配到Spring的bean容器中）@Bean注解通常是我们在标有该注解的方法中定义产生这个bean,@bean告诉了Spring这个某个类的实例，当我们需要他的时候还给我
3. @Bean注解比Component注解的自定义性更强，而且很多地方我们只能通过@Bean注解来注册bean，比如当我们引用第三方库中的类需要装配到Spring容器时，则只能通过@Bean来实现