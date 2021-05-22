# Maven学习笔记

***

是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。

## Maven POM

**POM** （*Project Object Model*）项目对象模型 是Maven工程的基本工作单元，是一个XML文件，包含了项目的基本信息，用于描述项目如何构建，声明项目依赖等等

在创建 POM 之前，我们首先需要描述项目组 (groupId), 项目的唯一ID。

所有 POM 文件都需要 project 元素和三个必需字段：groupId，artifactId，version。

| groupId    | 这是工程组的标识。它在一个组织或者项目中通常是唯一的。例如，一个银行组织 com.companyname.project-group 拥有所有的和银行相关的项目。 |
| ---------- | ------------------------------------------------------------ |
| artifactId | 这是工程的标识。它通常是工程的名称。例如，消费者银行。groupId 和 artifactId 一起定义了 artifact 在仓库中的位置。 |

## Maven 构造的生命周期

## ![maven-package-build-phase](https://www.runoob.com/wp-content/uploads/2018/09/maven-package-build-phase.png)

| 阶段          | 处理     | 描述                                                     |
| :------------ | :------- | :------------------------------------------------------- |
| 验证 validate | 验证项目 | 验证项目是否正确且所有必须信息是可用的                   |
| 编译 compile  | 执行编译 | 源代码编译在此阶段完成                                   |
| 测试 Test     | 测试     | 使用适当的单元测试框架（例如JUnit）运行测试。            |
| 包装 package  | 打包     | 创建JAR/WAR包如在 pom.xml 中定义提及的包                 |
| 检查 verify   | 检查     | 对集成测试的结果进行检查，以保证质量达标                 |
| 安装 install  | 安装     | 安装打包的项目到本地仓库，以供其他项目使用               |
| 部署 deploy   | 部署     | 拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程 |

Maven 有以下三个标准的生命周期：

- **clean**：项目清理的处理

- **default(或 build)**：项目部署的处理

- **site**：项目站点文档创建的处理

### clean生命周期

分为三个阶段：

- pre-clean：执行一些需要在clean之前完成的工作
- clean：移除所有上一次构建生成的文件
- post-clean：执行一些需要在clean之后立刻完成的工作

### Default (Build) 生命周期

| 生命周期阶段                                | 描述                                                         |
| :------------------------------------------ | :----------------------------------------------------------- |
| validate（校验）                            | 校验项目是否正确并且所有必要的信息可以完成项目的构建过程。   |
| initialize（初始化）                        | 初始化构建状态，比如设置属性值。                             |
| generate-sources（生成源代码）              | 生成包含在编译阶段中的任何源代码。                           |
| process-sources（处理源代码）               | 处理源代码，比如说，过滤任意值。                             |
| generate-resources（生成资源文件）          | 生成将会包含在项目包中的资源文件。                           |
| process-resources （处理资源文件）          | 复制和处理资源到目标目录，为打包阶段最好准备。               |
| compile（编译）                             | 编译项目的源代码。                                           |
| process-classes（处理类文件）               | 处理编译生成的文件，比如说对Java class文件做字节码改善优化。 |
| generate-test-sources（生成测试源代码）     | 生成包含在编译阶段中的任何测试源代码。                       |
| process-test-sources（处理测试源代码）      | 处理测试源代码，比如说，过滤任意值。                         |
| generate-test-resources（生成测试资源文件） | 为测试创建资源文件。                                         |
| process-test-resources（处理测试资源文件）  | 复制和处理测试资源到目标目录。                               |
| test-compile（编译测试源码）                | 编译测试源代码到测试目标目录.                                |
| process-test-classes（处理测试类文件）      | 处理测试源码编译生成的文件。                                 |
| test（测试）                                | 使用合适的单元测试框架运行测试（Juint是其中之一）。          |
| prepare-package（准备打包）                 | 在实际打包之前，执行任何的必要的操作为打包做准备。           |
| package（打包）                             | 将编译后的代码打包成可分发格式的文件，比如JAR、WAR或者EAR文件。 |
| pre-integration-test（集成测试前）          | 在执行集成测试前进行必要的动作。比如说，搭建需要的环境。     |
| integration-test（集成测试）                | 处理和部署项目到可以运行集成测试环境中。                     |
| post-integration-test（集成测试后）         | 在执行集成测试完成后进行必要的动作。比如说，清理集成测试环境。 |
| verify （验证）                             | 运行任意的检查来验证项目包有效且达到质量标准。               |
| install（安装）                             | 安装项目包到本地仓库，这样项目包可以用作其他本地项目的依赖。 |
| deploy（部署）                              | 将最终的项目包复制到远程仓库中与其他开发者和项目共享。       |

### Site 生命周期

Maven Site 插件一般用来创建新的报告文档、部署站点等。

- pre-site：执行一些需要在生成站点文档之前完成的工作
- site：生成项目的站点文档
- post-site： 执行一些需要在生成站点文档之后完成的工作，并且为部署做准备
- site-deploy：将生成的站点文档部署到特定的服务器上

## Maven构建配置文件

| 类型                  | 在哪定义                                                     |
| :-------------------- | :----------------------------------------------------------- |
| 项目级（Per Project） | 定义在项目的POM文件pom.xml中                                 |
| 用户级 （Per User）   | 定义在Maven的设置xml文件中 (%USER_HOME%/.m2/settings.xml)    |
| 全局（Global）        | 定义在 Maven 全局的设置 xml 文件中 (%M2_HOME%/conf/settings.xml) |

