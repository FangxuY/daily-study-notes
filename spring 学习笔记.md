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