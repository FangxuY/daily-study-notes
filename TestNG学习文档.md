# TestNG学习文档

***

编写测试通常需要三个步骤：

- 编写测试的业务逻辑并在代码中插入TestNG注解。

- 在`testng.xml`文件或`build.xml`中添加有关测试的信息（例如，类名，要运行的组等）。

- 运行`TestNG`。

`@BeforeSuite`  

在该套件的所有测试都运行在注释的方法之前，仅运行一次（套件测试是一起运行的多个测试类）。
`@AfterSuite`      

在该套件的所有测试都运行在注释方法之后，仅运行一次。
`@BeforeClass`     

在调用当前类的第一个测试方法之前运行，注释方法仅运行一次。
`@AfterClass`      

在调用当前类的第一个测试方法之后运行，注释方法仅运行一次
`@BeforeTest`      

注释的方法将在属于<test>标签内的类的所有测试方法运行之前运行。
`@AfterTest`       

注释的方法将在属于<test>标签内的类的所有测试方法运行之后运行。
`@BeforeGroups`    

配置方法将在之前运行组列表。 此方法保证在调用属于这些组中的任何一个的第一个测试方法之前不久运行。
`@AfterGroups`    

此配置方法将在之后运行组列表。该方法保证在调用属于任何这些组的最后一个测试方法之后不久运行。
`@BeforeMethod`    

注释方法将在每个测试方法之前运行。
`@AfterMethod`     

注释方法将在每个测试方法之后运行。
`@Parameters`      

描述如何将参数传递给@Test方法。
`@DataProvider`    

标记一种方法来提供测试方法的数据。 注释方法必须返回一个Object [] []，其中每个Object []可以被分配给测试方法的参数列表。 要从该DataProvider接收数据的@Test方法需要使用与此注释名称相等的dataProvider名称。

`@Factory`         

将一个方法标记为工厂，返回TestNG将被用作测试类的对象。 该方法必须返回Object []。

` @Listeners`       

定义测试类上的侦听器。
`@Test`            

将类或方法标记为测试的一部分。

```xml
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >    <suite name="Suite1" verbose="1" >   
	<test name="Nopackage" >     
		<classes>	<class name="NoPackageTest" /> </classes>
  </test>     
  <test name="Regression1">     
    <classes> <class name="test.sample.ParameterSample"/>       							<class name="test.sample.ParameterTest"/>     		</classes>   
  </test> 
</suite>
```

