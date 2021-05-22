## 七网隔离

首先我们来看看 `七网隔离` 到底是什么意思，这个名词大概是在阿里网络界最常见的一个词了。这 `七网` 到底是哪七网?  它们之间具体是怎么隔离的呢?  我们看下面这张图:

所谓的七网指的是 `阿里巴巴办公网` 、`阿里巴巴开发测试网` 、`阿里巴巴生产网` ，`蚂蚁金服办公网`、`蚂蚁金服开发测试网` 、`蚂蚁金服生产网` ，以及 `阿里云的公有云网` 。这七大子网都与阿里巴巴骨干网(ATBN) 进行连接, 从而连接到外面的 ISP 进行外部通信。

## OXS

在阿里云上开发云服务经常能听到的另外一个词是 `OXS` ,`OXS` 不是一个特定的机房，要说明它就要说一下阿里云上的整体网络结构了。(这里说的阿里云，我理解就是七网隔离里面的 `公有云` )。

![img](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/10039/1561773941877-e038f2fc-3114-4d37-abbe-56a92fa6f359.png?x-oss-process=image/resize,w_1492)

公有云上的网络分成两大子网: 也就是传说中的 `OXS` 和 `售卖区` , 从图中右侧可以看出早期几乎所有的云产品的命名都遵循 `O_S` 的结构，比如对象存储 `OSS`,  缓存服务 `OCS` 等等，同时这些服务所在的网络跟售卖区是隔绝的，因此取名叫做 `OXS`。

## 专有网络：VPC

`VPC(Virtual Private Cloud)` 是构建在物理网络之上的虚拟化网络, 它采用目前主流的隧道技术，隔离了虚拟网络。每个VPC都有一个独立的隧道号，一个隧道号对应着一个虚拟化网络。 每个VPC都由一个私网网段、一个路由器和至少一个交换机组成

## 阿里CDN

CDN的全称Content Delivery Network，(缩写：CDN)即内容分发网络。

CDN是一个经策略性部署的整体系统，从技术上全面解决由于网络带宽小、用户访问量大、网点分布不均而产生的用户访问网站响应速度慢的根本原因。

CDN的目的是通过在现有的Internet中增加一层新的网络架构，将网站的内容发布到最接近用户的网络“边缘”，使用户可以就近取得所需的内容，解决 Internet 网络拥塞状况，提高用户访问网站的响应速度。

## CDN 组成部分

CDN是一种组合技术，其中包括源站、缓存服务器、智能DNS、客户端等几个重要部分。

- 用户发出请求；本地DNS服务器通过解析得到ICP2 DNS授权服务器的地址
- 本地DNS服务器访问ICP2 DNS授权服务器，获知域名的详细解析由CDN平台负责
- 本地DNS服务器访问CDN平台，得到离用户最近的节点服务器的地址，返回给用户
- 用户访问边缘节点服务器，在没有缓存的情况下：节点服务器从源站取得用户所需内容并将内容发给用户，并根据相应的缓存策略将内容缓存在边缘节点上

## 统一接入层是什么？

> - 统一接入层是一个tengine运行的web server代理，由它主要负责承担全网用户的http/https请求，然后请求转发(proxy_pass)给后端的应用服务器；
> - 目前95%以上的对外应用的流量都通过统一接入层转发，可以说统一接入层是阿里业务架构中的最前端也最基础的服务。

## LVS

LVS是四层负载均衡，也就是说建立在OSI模型的第四层——传输层之上，传输层上有我们熟悉的TCP/UDP，LVS支持TCP/UDP的负载均衡。

LVS的转发主要通过修改IP地址（NAT模式，分为源地址修改SNAT和目标地址修改DNAT）、修改目标MAC（DR模式）来实现。

那么为什么LVS是在第四层做负载均衡？

> 首先LVS不像HAProxy等七层软负载面向的是HTTP包，所以七层负载可以做的URL解析等工作，LVS无法完成。其次，某次用户访问是与服务端建立连接后交换数据包实现的，如果在第三层网络层做负载均衡，那么将失去「连接」的语义。软负载面向的对象应该是一个已经建立连接的用户，而不是一个孤零零的IP包。后面会看到，实际上LVS的机器代替真实的服务器与用户通过TCP三次握手建立了连接，所以LVS是需要关心「连接」级别的状态的。

## VipServer 

VIPServer，是中间件软负载团队推出的一个软负载产品，用于取消内网使用的VIP负载均衡方式，实现P2P直连。

通过集中式的配置向客户提供路由信息，以非网关的形式实现负载均衡功能；支持多种映射策略（轮询、轮询+同机房、轮询+同网段）；通过健康探测机制，自动剔除不健康的机器，实现集群之间调用的透明化；对调用量、调用方等数据也有一定程度的反馈。

## Tegine

Tengine是由淘宝网发起的Web服务器项目。它在Nginx的基础上，针对大访问量网站的需求，添加了很多高级功能和特性。Tengine的性能和稳定性已经在大型的网站如淘宝网，天猫商城等得到了很好的检验。它的最终目标是打造一个高效、稳定、安全、易用的Web平台。

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2019/png/10039/1561778260167-1eb22b6e-46e1-4c4b-80ae-43a2e39e9972.png" alt="image.png" style="zoom:100%;" />

## AJDK

众所周知JDK一直是Oracle在升级维护的，但是阿里巴巴需要支持双十一这种巨量的访问，对性能的要求非常高，而优化JDK是能从JAVA运行环境级别来提示性能的。

​    Alibaba Java Development Kit (AJDK) 是阿里巴巴 JVM 团队在 Java Standard Edition (SE) 规范下的 OpenJDK基础上自主研发的 JDK 版本，成功合并了 AliJDK和 AlipayJDK的大部分主要功能，以及将要提供以下新功能：

- 依靠以下技术改造提高性能，预期可以帮助节省 50% 机器；
- 实现多租户方式的合并部署，在同一个 JVM 里，最大程度的共享资源；
- 实现全异步通讯的自动化，不修改业务代码的情况下，增加服务器的吞吐量 (qps)；
- Garbage collector 的优化；
- 序列化反序列化的优化；
- lambda expressions, 让代码更简洁，简单，以及更加容易维护；
- 提供社区最新Java安全更新。

## GIT

## Maven

maven是一款项目管理和构建工具。maven可以将多个相互关联的本地子模块通过POM文件的形式聚合在一起，也可以将依赖的外部库在POM中指定并引入作为本工程所用。每个子模块或外部库都有版本号，本质上子模块和外部库是一样的，都是一个具有独立功能的模块。这些模块就是版本管理的对象。模块由GroupId、ArtifactId、Version三个元素唯一标识。

groupId：定义当前Maven项目隶属的实际项目。

artifactId：定义实际项目中的一个Maven模块。

version：定义Maven项目当前所处的版本。

#### 版本管理的作用

每个maven模块都有版本号属性，每个版本号都对应了一个代码版本，一般模块功能稳定后，才会升级一次版本。版本号的意义在于，当模块以jar包的方式发布到公共仓库中时，调用者会根据版本号来决定下载哪个版本的代码，这样能够实现调用方和提供方的解耦。

![img](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/10039/1561787661368-93c25b94-e289-4304-8f78-adf7c7133db2.png)

#### 常见Maven命令

**mvn clean compile**

清理+编译

**mvn clean test**

清理+编译+执行测试[链接](https://yuque.antfin-inc.com/allen.cty/puu9bm/fa1d8x/edit)

**mvn clean package**

清理+编译+打包

**mvn clean install**

清理+编译+打包+放置本地仓库

**mvn archetype:generate**

创建项目骨架

**mvn dependency:list**

查看当前项目的已解析依赖

**mvn dependency:tree**

查看当前项目的依赖树

**mvn dependency:analyze**

自动化分析当前项目的依赖

举例：

mvn clean install -Dmaven.test.skip=true  //编译的时候不用跑test case

mvn versions:set -DnewVersion=1.3.132-ty-SNAPSHOT   //批量设置当前项目和子项目的版本号

mvn deploy -Dmaven.test.skip  //打包部署,只能部署SNAP包，正式包要上Aone

### AliTomcat

Ali-Tomcat是基于 Apache Tomcat 改造的 Servlet 容器。在支持原有核心功能的前提下，提供了类隔离机制、统一日志管理、QoS服务、Tomcat-Monitor 监控功能

以下是Windows和Linux环境下安装Tomcat的详细流程：

## 常用Web开发框架

### Spring MVC

Spring MVC是一个非常优秀的MVC框架，是业界通用的一个WEB开发框架。

JavaEE体系结构包括四层，从上到下分别是应用层、Web层、业务层、持久层。Struts和SpringMVC是Web层的框架，Spring是业务层的框架，Hibernate和MyBatis是持久层的框架。

### 为什么要使用SpringMVC？

很多应用程序的问题在于处理业务数据的对象和显示业务数据的视图之间存在紧密耦合，通常，更新业务对象的命令都是从视图本身发起的，使视图对任何业务对象更改都有高度敏感性。而且，当多个视图依赖于同一个业务对象时是没有灵活性的。

SpringMVC是一种基于Java，实现了Web MVC设计模式，请求驱动类型的轻量级Web框架，即使用了MVC架构模式的思想，将Web层进行职责解耦。基于请求驱动指的就是使用请求-响应模型，框架的目的就是帮助我们简化开发，SpringMVC也是要简化我们日常Web开发。

## Spring Boot

Spring boot基于spring，为了解决使用spring框架时配置繁多、部署流程复杂、开发效率低等问题，可以创建独立的应用程序，嵌入了tomcat、jetty等，可以直接启动应用程序而不需要外部的容器。同时，spring boot可以自动配置spring应用，并且将一些框架的依赖包整合起来。比如开发web程序只需要引入web的starter，极大的简化了包的引用。

## Pandora Boot

### Pandora介绍

**Pandora是一个轻量级的隔离容器，也就是taobao-hsf.sar，它用来隔离Webapp和中间件的依赖，也用来隔离中间件之间的依赖。**

## Aone

是一站式研发协同平台，提供研发全生命周期管理服务，并基于研发数据提供丰富的分析度量服务辅助效能决策和改进。

## Pouch

阿里自研容器，从docker与T4出发

