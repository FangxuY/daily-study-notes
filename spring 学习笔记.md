# Spring 入门

## 1.1 什么是spring

Spring 的核心是一个 *容器*，通常称为 *Spring 应用程序上下文*，用于创建和管理应用程序组件。这些组件（或 bean）在 Spring 应用程序上下文中连接在一起以构成一个完整的应用程序，就像将砖、灰浆、木材、钉子、管道和电线绑在一起以组成房屋。

将 bean 连接在一起的行为是基于一种称为 *依赖注入*（DI）的模式。依赖项注入的应用程序不是由组件自身创建和维护它们依赖的其他 bean 的生命周期，而是依赖于单独的实体（容器）来创建和维护所有组件，并将这些组件注入需要它们的 bean。通常通过构造函数参数或属性访问器方法完成此操作。

`@SpringBootApplication` 注释清楚地表明这是一个 Spring 引导应用程序。但是 `@SpringBootApplication` 中有更多的东西。

`@SpringBootApplication` 是一个组合了其他三个注释的复合应用程序：

- `@SpringBootConfiguration` —— 指定这个类为配置类。尽管这个类中还没有太多配置，但是如果需要，可以将 Javabased Spring Framework 配置添加到这个类中。实际上，这个注释是`@Configuration` 注释的一种特殊形式。
- `@EnableAutoConfiguration` —— 启用 Spring 自动配置。稍后我们将详细讨论自动配置。现在，要知道这个注释告诉 Spring Boot 自动配置它认为需要的任何组件。
- `@ComponentScan` —— 启用组件扫描。这允许你声明其他带有 `@Component`、`@Controller`、`@Service` 等注释的类，以便让 Spring 自动发现它们并将它们注册为 Spring 应用程序上下文中的组件。

## Spring MVC

Spring MVC 的核心是控制器的概念，这是一个处理请求并使用某种信息进行响应的类。对于面向浏览器的应用程序，控制器的响应方式是可选地填充模型数据并将请求传递给视图，以生成返回给浏览器的 HTML。

将编写一个简单的控制器类来处理根路径的请求（例如 `/`），并将这些请求转发到主页视图，而不填充任何模型数据。程序清单 1.4 显示了简单的控制器类。

```java
package tacos;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {
    @GetMapping("/")
    public String home() {
        return "home";
    }
}

```

## 1.3 了解Spring Boot DevTools

- 当代码更改时自动重启应用程序

- 当以浏览器为目标的资源（如模板、JavaScript、样式表等）发生变化时，浏览器会自动刷新

- 自动禁用模板缓存

- 如果 H2 数据库正在使用，则在 H2 控制台中构建

## 1.4 Spring Boot

我们已经看到了 Spring Boot 的许多好处，包括启动依赖项和自动配置。在本书中我们确实会尽可能多地使用 Spring Boot，并避免任何形式的显式配置，除非绝对必要。但除了启动依赖和自动配置，Spring Boot 还提供了一些其他有用的特性：

- Actuator 提供了对应用程序内部工作方式的运行时监控，包括端点、线程 dump 信息、应用程序健康状况和应用程序可用的环境属性。
- 灵活的环境属性规范。
- 在核心框架的测试辅助之外，还有额外的测试支持。

此外，Spring Boot 提供了一种基于 Groovy 脚本的替代编程模型，称为 Spring Boot CLI（命令行界面）。使用 Spring Boot CLI，可以将整个应用程序编写为 Groovy 脚本的集合，并从命令行运行它们。我们不会在 Spring Boot CLI 上花太多时间，但是当它适合我们的需要时，我们会接触它。

Spring Boot 已经成为 Spring 开发中不可或缺的一部分；我无法想象开发一个没有它的 Spring 应用程序。因此，本书采用了以 Spring Boot 为中心的观点，当我提到 Spring Boot 正在做的事情时，你可能会发现我在使用 Spring 这个词。

### 1.4.3 Spring Data

Spring Data 提供了一些非常惊人的功能：将应用程序的数据存储库抽象为简单的 Java 接口，同时当定义方法用于如何驱动数据进行存储和检索的问题时，对方法使用了命名约定。

更重要的是，Spring Data 能够处理几种不同类型的数据库，包括关系型（JPA）、文档型（Mongo）、图型（Neo4j）等。在第 3 章中，将使用 Spring Data 来帮助创建 Taco Cloud 应用程序的存储库。

### 1.4.5 Spring Integration 和 Spring Batch

在某种程度上，大多数应用程序将需要与其他应用程序集成，甚至需要与同一应用程序的其他组件集成。为了满足这些需求，出现了几种应用程序集成模式。Spring Integration 和 Spring Batch 为基于 Spring 的应用程序提供了这些模式的实现。

Spring Integration 解决了实时集成，即数据在可用时进行处理。相反，Spring Batch 解决了批量集成的问题，允许在一段时间内收集数据，直到某个触发器（可能是一个时间触发器）发出信号，表示该处理一批数据了

### Spring Cloud

应用程序开发领域正在进入一个新时代，在这个时代中，我们不再将应用程序作为单个部署单元来开发，而是将由几个称为 *微服务* 的单个部署单元组成应用程序。

微服务是一个热门话题，解决了几个实际的开发和运行时问题。然而，在这样做的同时，他们也带来了自己的挑战。这些挑战都将由 Spring Cloud 直接面对，Spring Cloud 是一组用 Spring 开发云本地应用程序的项目。

# Spring 框架

![spring-overview](https://www.runoob.com/wp-content/uploads/2015/07/673670c9a34075831373b711cb8f21b7.png)

# Spring的核心机制

## 管理Bean

程序主要是通过Spring容器来访问容器中的Bean，ApplicationContext是Spring容器最常用的接口，该接口有如下两个实现类：

- ClassPathXmlApplicationContext: 从类加载路径下搜索配置文件，并根据配置文件来创建Spring容器。
- FileSystemXmlApplicationContext: 从文件系统的相对路径或绝对路径下去搜索配置文件，并根据配置文件来创建Spring容器。









# 第二章 开发web应用程序



# 处理数据

- 使用 Spring JdbcTemplate
- 使用 SimpleJdbcInsert 插入数据
- 使用 Spring Data 声明 JPA repositories

首先使用 Spring 对 JDBC（Java Database Connectivity）的支持来消除样板代码。然后，将重新使用 JPA（Java Persistence API）处理数据存储库，从而消除更多代码。

## 使用JDBC读写数据



# 概览

## 什么是Spring框架？

Spring 是一种轻量级开发框架，旨在提高开发人员的开发效率以及系统的可维护性。

我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发。这些模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。比如：Core Container 中的 Core 组件是Spring 所有组件的核心，Beans 组件和 Context 组件是实现IOC和依赖注入的基础，AOP组件用来实现面向切面编程。

Spring 官网列出的 Spring 的 6 个特征:

- **核心技术** ：依赖注入(DI)，AOP，事件(events)，资源，i18n，验证，数据绑定，类型转换，SpEL。
- **测试** ：模拟对象，TestContext框架，Spring MVC 测试，WebTestClient。
- **数据访问** ：事务，DAO支持，JDBC，ORM，编组XML。
- **Web支持** : Spring MVC和Spring WebFlux Web框架。
- **集成** ：远程处理，JMS，JCA，JMX，电子邮件，任务，调度，缓存。
- **语言** ：Kotlin，Groovy，动态语言。

![Spring主要模块](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/Spring%E4%B8%BB%E8%A6%81%E6%A8%A1%E5%9D%97.png)

- **Spring Core：** 基础,可以说 Spring 其他所有的功能都需要依赖于该类库。主要提供 IoC 依赖注入功能。
- **Spring Aspects** ： 该模块为与AspectJ的集成提供支持。
- **Spring AOP** ：提供了面向切面的编程实现。
- **Spring JDBC** : Java数据库连接。
- **Spring JMS** ：Java消息服务。
- **Spring ORM** : 用于支持Hibernate等ORM工具。
- **Spring Web** : 为创建Web应用程序提供支持。
- **Spring Test** : 提供了对 JUnit 和 TestNG 测试的支持。

## @RestController vs @Controller

# [JavaGuide](https://snailclimb.gitee.io/javaguide/)

- [1. 什么是 Spring 框架?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_1-什么是-spring-框架)

- [2. 列举一些重要的Spring模块？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_2-列举一些重要的spring模块？)

- [3. @RestController vs @Controller](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_3-restcontroller-vs-controller)

- [4. Spring IOC & AOP](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_4-spring-ioc-amp-aop)

- - [4.1 谈谈自己对于 Spring IoC 和 AOP 的理解](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_41-谈谈自己对于-spring-ioc-和-aop-的理解)

  - - [IoC](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=ioc)
    - [AOP](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=aop)

  - [4.2 Spring AOP 和 AspectJ AOP 有什么区别？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_42-spring-aop-和-aspectj-aop-有什么区别？)

- [5. Spring bean](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_5-spring-bean)

- - [5.1 Spring 中的 bean 的作用域有哪些?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_51-spring-中的-bean-的作用域有哪些)
  - [5.2 Spring 中的单例 bean 的线程安全问题了解吗？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_52-spring-中的单例-bean-的线程安全问题了解吗？)
  - [5.3 @Component 和 @Bean 的区别是什么？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_53-component-和-bean-的区别是什么？)
  - [5.4 将一个类声明为Spring的 bean 的注解有哪些?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_54-将一个类声明为spring的-bean-的注解有哪些)
  - [5.5 Spring 中的 bean 生命周期?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_55-spring-中的-bean-生命周期)

- [6. Spring MVC](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_6-spring-mvc)

- - [6.1 说说自己对于 Spring MVC 了解?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_61-说说自己对于-spring-mvc-了解)
  - [6.2 SpringMVC 工作原理了解吗?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_62-springmvc-工作原理了解吗)

- [7. Spring 框架中用到了哪些设计模式？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_7-spring-框架中用到了哪些设计模式？)

- [8. Spring 事务](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_8-spring-事务)

- - [8.1 Spring 管理事务的方式有几种？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_81-spring-管理事务的方式有几种？)
  - [8.2 Spring 事务中的隔离级别有哪几种?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_82-spring-事务中的隔离级别有哪几种)
  - [8.3 Spring 事务中哪几种事务传播行为?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_83-spring-事务中哪几种事务传播行为)
  - [8.4 @Transactional(rollbackFor = Exception.class)注解了解吗？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_84-transactionalrollbackfor-exceptionclass注解了解吗？)

- [9. JPA](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_9-jpa)

- - [9.1 如何使用JPA在数据库中非持久化一个字段？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_91-如何使用jpa在数据库中非持久化一个字段？)

- [参考](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=参考)

- [公众号](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=公众号)

Edit on github

5675 字  |  15 分钟

这篇文章主要是想通过一些问题，加深大家对于 Spring 的理解，所以不会涉及太多的代码！这篇文章整理了挺长时间，下面的很多问题我自己在使用 Spring 的过程中也并没有注意，自己也是临时查阅了很多资料和书籍补上的。网上也有一些很多关于 Spring 常见问题/面试题整理的文章，我感觉大部分都是互相 copy，而且很多问题也不是很好，有些回答也存在问题。所以，自己花了一周的业余时间整理了一下，希望对大家有帮助。

## [1. 什么是 Spring 框架?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_1-什么是-spring-框架)

Spring 是一种轻量级开发框架，旨在提高开发人员的开发效率以及系统的可维护性。Spring 官网：https://spring.io/。

我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发。这些模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。比如：Core Container 中的 Core 组件是Spring 所有组件的核心，Beans 组件和 Context 组件是实现IOC和依赖注入的基础，AOP组件用来实现面向切面编程。

Spring 官网列出的 Spring 的 6 个特征:

- **核心技术** ：依赖注入(DI)，AOP，事件(events)，资源，i18n，验证，数据绑定，类型转换，SpEL。
- **测试** ：模拟对象，TestContext框架，Spring MVC 测试，WebTestClient。
- **数据访问** ：事务，DAO支持，JDBC，ORM，编组XML。
- **Web支持** : Spring MVC和Spring WebFlux Web框架。
- **集成** ：远程处理，JMS，JCA，JMX，电子邮件，任务，调度，缓存。
- **语言** ：Kotlin，Groovy，动态语言。

## [2. 列举一些重要的Spring模块？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_2-列举一些重要的spring模块？)

下图对应的是 Spring4.x 版本。目前最新的5.x版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。

![Spring主要模块](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/Spring%E4%B8%BB%E8%A6%81%E6%A8%A1%E5%9D%97.png)

- **Spring Core：** 基础,可以说 Spring 其他所有的功能都需要依赖于该类库。主要提供 IoC 依赖注入功能。
- **Spring Aspects** ： 该模块为与AspectJ的集成提供支持。
- **Spring AOP** ：提供了面向切面的编程实现。
- **Spring JDBC** : Java数据库连接。
- **Spring JMS** ：Java消息服务。
- **Spring ORM** : 用于支持Hibernate等ORM工具。
- **Spring Web** : 为创建Web应用程序提供支持。
- **Spring Test** : 提供了对 JUnit 和 TestNG 测试的支持。

## [3. @RestController vs @Controller](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring常见问题总结?id=_3-restcontroller-vs-controller)

**`Controller` 返回一个页面**

单独使用 `@Controller` 不加 `@ResponseBody`的话一般使用在要返回一个视图的情况，这种情况属于比较传统的Spring MVC 的应用，对应于前后端不分离的情况。

![SpringMVC 传统工作流程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/SpringMVC%E4%BC%A0%E7%BB%9F%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B.png)

**`@RestController` 返回JSON 或 XML 形式数据**

但`@RestController`只返回对象，对象数据直接以 JSON 或 XML 形式写入 HTTP 响应(Response)中，这种情况属于 RESTful Web服务，这也是目前日常开发所接触的最常用的情况（前后端分离）。

![SpringMVC+RestController](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/SpringMVCRestController.png)

**`@Controller +@ResponseBody` 返回JSON 或 XML 形式数据**

如果你需要在Spring4之前开发 RESTful Web服务的话，你需要使用`@Controller` 并结合`@ResponseBody`注解，也就是说`@Controller` +`@ResponseBody`= `@RestController`（Spring 4 之后新加的注解）。

![Spring3.xMVC RESTfulWeb服务工作流程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/Spring3.xMVCRESTfulWeb%E6%9C%8D%E5%8A%A1%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B.png)

## 4 Spring IoC 和AOP

### 对Spring IoC和AOP的理解

### IoC

IoC（Inverse of Control:控制反转）是一种**设计思想**，就是 **将原本在程序中手动创建对象的控制权，交由Spring框架来管理。** IoC 在其他语言中也有应用，并非 Spring 特有。 **IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个Map（key，value）,Map 中存放的是各种对象。**

将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 **IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。** 在实际项目中一个 Service 类可能有几百甚至上千个类作为它的底层，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。

Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。

依赖倒置原则（**Dependency Inversion Principle**）

**什么是依赖倒置原则？**假设我们设计一辆汽车：先设计轮子，然后根据轮子大小设计底盘，接着根据底盘设计车身，最后根据车身设计好整个汽车。这里就出现了一个“依赖”关系：汽车依赖车身，车身依赖底盘，底盘依赖轮子。

![img](https://pic4.zhimg.com/50/v2-c68248bb5d9b4d64d22600571e996446_hd.jpg?source=1940ef5c)![img](https://pic4.zhimg.com/80/v2-c68248bb5d9b4d64d22600571e996446_720w.jpg?source=1940ef5c)

这样的设计看起来没问题，但是可维护性却很低。假设设计完工之后，上司却突然说根据市场需求的变动，要我们把车子的轮子设计都改大一码。这下我们就蛋疼了：因为我们是根据轮子的尺寸设计的底盘，轮子的尺寸一改，底盘的设计就得修改；同样因为我们是根据底盘设计的车身，那么车身也得改，同理汽车设计也得改——整个设计几乎都得改！

我们现在换一种思路。我们先设计汽车的大概样子，然后根据汽车的样子来设计车身，根据车身来设计底盘，最后根据底盘来设计轮子。这时候，依赖关系就倒置过来了：轮子依赖底盘， 底盘依赖车身， 车身依赖汽车。

![img](https://pic1.zhimg.com/50/v2-e64bf72c5c04412f626b21753aa9e1a1_hd.jpg?source=1940ef5c)![img](https://pic1.zhimg.com/80/v2-e64bf72c5c04412f626b21753aa9e1a1_720w.jpg?source=1940ef5c)

这时候，上司再说要改动轮子的设计，我们就只需要改动轮子的设计，而不需要动底盘，车身，汽车的设计了。

把原本的高层建筑依赖底层建筑“倒置”过来，变成底层建筑依赖高层建筑。高层建筑决定需要什么，底层去实现这样的需求，但是高层并不用管底层是怎么实现的。这样就不会出现前面的“牵一发动全身”的情况。

**控制反转（Inversion of Control）** 就是依赖倒置原则的一种代码设计的思路。具体采用的方法就是所谓的**依赖注入（Dependency Injection）**。其实这些概念初次接触都会感到云里雾里的。说穿了，这几种概念的关系大概如下：

![img](https://pic1.zhimg.com/80/v2-ee924f8693cff51785ad6637ac5b21c1_720w.jpg?source=1940ef5c)

**Spring IoC的初始化过程：**

![Spring IoC的初始化过程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/SpringIOC%E5%88%9D%E5%A7%8B%E5%8C%96%E8%BF%87%E7%A8%8B.png)

### AOP

AOP(Aspect-Oriented Programming:面向切面编程)能够将那些与业务无关，**却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来**，便于**减少系统的重复代码**，**降低模块间的耦合度**，并**有利于未来的可拓展性和可维护性**。

**Spring AOP就是基于动态代理的**，如果要代理的对象，实现了某个接口，那么Spring AOP会使用**JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候Spring AOP会使用**Cglib** ，这时候Spring AOP会使用 **Cglib** 生成一个被代理对象的子类来作为代理，如下图所示：

![SpringAOPProcess](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/SpringAOPProcess.jpg)