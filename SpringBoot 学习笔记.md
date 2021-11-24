



## 序：微服务阶段

javase：OOP

mysql： 持久化

html + css + js + jquery + 框架： 视图

javaweb：独立开发MVC三层架构的网站了： 原始

SSM ： 框架，简化了我们的开发流程，配置也开始较为复杂

**war： tomcat 运行**

spring 再简化： Springboot

服务越来越多： springcloud；

![](SpringBoot 学习笔记.assets/image-20211009125913337.png)



## 2.  什么是 SpringBoot

​	Spring 是一个开源框架 ，2003 年兴起的一个轻量级的 Java 开发框架，作者： Rod  Johnson。 

​	**Spring 是为了解决 企业级应用开发的复杂性而创建的，简化开发。**



### 2.1  Spring 是如何简化 Java 开发的

为了 降低 Java 开发的复杂性， Spring 采用了以下4 种关键策略

1. 基于 POJO 的轻量级 和最小侵入性编程；
2. 通过 IOC ，依赖注入（DI） 和面向接口实现松耦合；
3. 基于切面（AOP） 和惯例进行声明式编程；
4. 通过切面和模板减少 样式代码；



**约定大于配置**



## 3.  什么是微服务架构

​	所谓微服务架构，就是打破之前 all  in  one  的架构方式， ==把每个功能元素独立出来==。 把独立出来的功能元素的动态组合， 需要的功能元素才去拿来组合，需要多一些时可以整合多个功能元素，所以微服务架构是对功能元素的复制，而没有对整个应用进行复制。

​	这样做的好处是：

1. 节省了调用资源。
2. 每个功能元素的服务都是一个可替换的、可独立升级的软件代码。



**高内聚，低耦合**



### 3.1  微服务架构的

1. 构建一个个功能独立的微服务应用单元，可以使用 springboot ，可以帮我们快速构建一个应用；
2. 大型分布式网络服务的调用，这部分由 springcloud 来完成，实现分布式；
3. 在分布式中间，进行流式数据计算、批处理 ，我们有spring cloud data flow；
4. spring 为我们提供了整个从开始构建应用到大型分布式应用全流程方案。

![image-20211010103534230](SpringBoot 学习笔记.assets/image-20211010103534230.png)





```
用户下单： controller

**消息队列**

仓库冻结→ 资金冻结 → 验证 →购买成功 →仓库数量减少 → 仓库解冻 →资金解冻
```



## 4.  第一个 Springboot 程序

官方提供了一个快速生成的网站！  IDEA 集成了这个网站

- 可以在观望直接下载后，导入 idea 开发
- 直接使用 idea 创建一个 springboot 项目 ( 开发一般使用这种方式 ) 



### 4.1 

1. 包要建在 **主启动类的同级目录下**， 不然识别不到

![image-20211010113659423](SpringBoot 学习笔记.assets/image-20211010113659423.png)



2.  pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<!--有一个父项目-->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.5.5</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.peng</groupId>
	<artifactId>helloworld</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>helloworld</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<!--web依赖 ：tomcat、xml-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<!--spring-boot-starter： springboot 的所有依赖都是使用这个开头的-->
		<!--单元测试-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-autoconfigure</artifactId>
			<version>2.5.5</version>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```

此文件主要包含四个部分：

- 项目元数据信息：创建时候输入的Project Metadata 部分，也就是 Maven项目的基本元素，包括： gorupld、artifactld、 version、（gav……），name、description 等
- parent：继承``spring-boot-starter-parent`` 的依赖管理，控制版本与打包等内容
- dependencies： 项目具体依赖，这里包含了``spring-boot-starter-web`` 用于实现 HTTP接口（该依赖中包含了 SpringMVC）， 官网对它的描述是： 使用 Spring MVC 构建 Web（包括 RESTful）应用程序的入门者，使用Tomcat 作为默认嵌入式容器。
- build： 构建配置部分，默认使用了 ``spring-boot-maven-plugin``，配合``spring-boot-starter-parent`` 就 可以把Springboot 应用打包成 JAR 来直接运行。

PS：About  Maven

![image-20211010144118089](SpringBoot 学习笔记.assets/image-20211010144118089.png)

groupId：定义当前 Maven 组织名称

artifactId：定义实际项目名称

version：定义当前项目的当前版本



PS：使用Maven 打包

![image-20211010143652683](SpringBoot 学习笔记.assets/image-20211010143652683.png)

![image-20211010143739247](SpringBoot 学习笔记.assets/image-20211010143739247.png)





### 4.2

1. 自定义 banner 及其原理

![image-20211010151847972](SpringBoot 学习笔记.assets/image-20211010151847972.png)

- https://www.jianshu.com/p/f799d734d1ee



### 4.3  BUG

1. [IDEA 导入 springboot 项目缺失 jar 包](https://blog.csdn.net/weixin_44580146/article/details/109130989 	 	)





## 5. 自动装配原理

自动装配



### 5.1  pom.xml

```
spring-boot-dependencies
 	 ↑
spring-boot-starter-parent
 	 ↑
pom.xml
```

1. spring-boot-dependencies ： 核心依赖在父工程中

   我们在写或引入一些 springboot 依赖的时候 ，不需要指定版本， 就因为有这些版本仓库



2. 启动器  

```xml
<!--启动器-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
```

说白了就是 ``springboot`` 的启动场景，比如 ``spring-boot-starter-web`` ， 它就会帮我们自动导入 web 环境所有的依赖



3. 主程序

```java
//@SpringBootApplication ：标注这个类是一个 springboot的应用
@SpringBootApplication
public class Springboot01HelloworldApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot01HelloworldApplication.class, args);
    }

}
```

- 注解 

```java
1.
@SpringBootConfiguration
@EnableAutoConfiguration
public @interface SpringBootApplication{}


2.
@SpringBootConfiguration ：springboot 的配置
	@Configuration ： Spring配置类
	@Component ：说明这也是一个 spring 注解

@EnableAutoConfiguration ：自动配置
	@AutoConfigurationPackage ：自动配置包
    	@Import(AutoConfigurationPackages.Registrar.class) ：自动配置``包注册``
    @Import(AutoConfigurationImportSelector.class) ：自动导入选择
	


3.
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {}

4.
@Import(AutoConfigurationPackages.Registrar.class)
public @interface AutoConfigurationPackage {}




```

- 自动装配

```java
//获取所有的配置 AutoConfigurationImportSelector.class
List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);

//所有资源加载到配置类中
Properties properties = PropertiesLoaderUtils.loadProperties(resource);



1.
public class AutoConfigurationImportSelector implements DeferredImportSelector, BeanClassLoaderAware,
ResourceLoaderAware, BeanFactoryAware, EnvironmentAware, Ordered {

2.
@Override
public String[] selectImports(AnnotationMetadata annotationMetadata) {
	if (!isEnabled(annotationMetadata)) {
		return NO_IMPORTS;
	}
	AutoConfigurationEntry autoConfigurationEntry = getAutoConfigurationEntry(annotationMetadata);			
	return StringUtils.toStringArray(autoConfigurationEntry.getConfigurations());
}


3.
protected AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
    if (!isEnabled(annotationMetadata)) {
        return EMPTY_ENTRY;
    }
    AnnotationAttributes attributes = getAttributes(annotationMetadata);
    List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
    configurations = removeDuplicates(configurations);
    Set<String> exclusions = getExclusions(annotationMetadata, attributes);
    checkExcludedClasses(configurations, exclusions);
    configurations.removeAll(exclusions);
    configurations = getConfigurationClassFilter().filter(configurations);
    fireAutoConfigurationImportEvents(configurations, exclusions);
    return new AutoConfigurationEntry(configurations, exclusions);
}

4.
protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
    List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
                                                                         getBeanClassLoader());
    Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
                    + "are using a custom packaging, make sure that file is correct.");
    return configurations;
}


1.
public final class SpringFactoriesLoader {}

2.    
public static List<String> loadFactoryNames(Class<?> factoryType, @Nullable ClassLoader classLoader) {
    ClassLoader classLoaderToUse = classLoader;
    if (classLoader == null) {
        classLoaderToUse = SpringFactoriesLoader.class.getClassLoader();
    }

    String factoryTypeName = factoryType.getName();
    return (List)loadSpringFactories(classLoaderToUse).getOrDefault(factoryTypeName, Collections.emptyList());
}
    
   
3.
private static Map<String, List<String>> loadSpringFactories(ClassLoader classLoader) {
    Map<String, List<String>> result = (Map)cache.get(classLoader);
    if (result != null) {
        return result;
    } else {
        HashMap result = new HashMap();

        try {
            Enumeration urls = classLoader.getResources("META-INF/spring.factories");

            while(urls.hasMoreElements()) {
                URL url = (URL)urls.nextElement();
                UrlResource resource = new UrlResource(url);
                Properties properties = PropertiesLoaderUtils.loadProperties(resource);
                Iterator var6 = properties.entrySet().iterator();

                while(var6.hasNext()) {
                    Entry<?, ?> entry = (Entry)var6.next();
                    String factoryTypeName = ((String)entry.getKey()).trim();
                    String[] factoryImplementationNames = StringUtils.commaDelimitedListToStringArray((String)entry.getValue());
                    String[] var10 = factoryImplementationNames;
                    int var11 = factoryImplementationNames.length;

                    for(int var12 = 0; var12 < var11; ++var12) {
                        String factoryImplementationName = var10[var12];
                        ((List)result.computeIfAbsent(factoryTypeName, (key) -> {
                            return new ArrayList();
                        })).add(factoryImplementationName.trim());
                    }
                }
            }

            result.replaceAll((factoryType, implementations) -> {
                return (List)implementations.stream().distinct().collect(Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList));
            });
            cache.put(classLoader, result);
            return result;
        } catch (IOException var14) {
            throw new IllegalArgumentException("Unable to load factories from location [META-INF/spring.factories]", var14);
        }
    }
}
    
```

```java

```





1.

![image-20211010175843799](SpringBoot 学习笔记.assets/image-20211010175843799.png)

2.

![image-20211010180651171](SpringBoot 学习笔记.assets/image-20211010180651171.png)

3.

![image-20211010181159391](SpringBoot 学习笔记.assets/image-20211010181159391.png)

4.META-INF/spring.factories：自动配置的核心文件

![image-20211010181446987](SpringBoot 学习笔记.assets/image-20211010181446987.png)



5.

![image-20211010182324365](SpringBoot 学习笔记.assets/image-20211010182324365.png)



6.**SpringFactoriesLoader**

![image-20211010183607794](SpringBoot 学习笔记.assets/image-20211010183607794.png)

![image-20211010183258383](SpringBoot 学习笔记.assets/image-20211010183258383.png)

7.

![image-20211010183517862](SpringBoot 学习笔记.assets/image-20211010183517862.png)



PS：核心注解

@ConditionalOnXXX ：如果这里面的条件都满足，才会生效









**结论：** 

springboot 所有的自动配置都是在启动的时候扫描并加载：``META-INF/spring.factories``，所有的自动配置类都在这里面，但是不一定生效，要判断条件是否成立==（@ConditionalOnXXX）==，只要导入了对应的 starter ，就有对应的启动器，有了启动器，我们自动装配就 会生效，然后就配置成功！

1. springboot 在启动的时候，从类路径下 META-INF/spring.factories  获取指定的值；
2. 将这些自动配置的类导入容器，自动配置就会生效，帮我们进行自动配置！
3. 以前我们需要自动配置的东西，现在 springboot 帮我们做了
4. 整合 JavaEE， 解决方案和自动配置的东西都在 ``spring-boot-autoconfigure-****-.jar`` 这个包下
5. 它会把 所有需要导入的组件， 以类名的方式返回，这些组件就会被添加到容器；
6. 容器中也会存在非常多的 xxxAutoConfiguration 的文件（@Bean）， 就是这些类给容器中导入了这个场景需要的所有组件，并自动配置， @Configuration， 本质就是一个个JavaConfig！

7. 有了自动配置类，免去了我们手动编写配置文件的工作！



### 5.3 主启动类怎么运行

这个类主要做了以下四件事情：

1. 推断应用的类型是普通的项目还是 web 项目
2. 查找并加载所有可用初始化器， 设置到 initializers 属性中
3. 找出所有的应用程序监听器，设置到 listeners 属性中
4. ==推断并设置 main 方法的定义类，找到运行的主类== 。（加载主类）

![image-20211010224828544](SpringBoot 学习笔记.assets/image-20211010224828544.png)

From kuang：

![springboot](SpringBoot 学习笔记.assets/springboot.jpg)

关于 Springboot ，谈谈你的理解

- 自动装配
- run 方法：





PS： java 中的 ``...``

> ​		如果是是形参 里面出现，表示的是可变参数,即表示的传入的参数个数是可变，你传多少个参数都被放到一个数组里面。



## 6.  yaml 格式讲解

**配置文件**：

- application.properties
  - 语法结构： key=value
- application.yml
  - 语法结构： key: ==空格==value

配置文件的作用 ： 修改 Springboot自动配置的默认值，因为SpringBoot在底层都给我们自动配置好了。





### 6.1 Yaml语法

```yaml
# properties: k=v
# yaml对空格的要求十分高！

# 强大之处： 可以注入到我们的配置类中

# 普通的 key-value
name: shuaipeng

# 对象
student:
  name: peng
  age: 18

# 行内写法
student1: {name: peng, age: 18}

# 数组
pets:
  - dog
  - cat
  - pig

pets1: [dog,cat,peng]
```



### 6.2  使用配置文件配对象

1. 注解``@ConfigurationProperties(prefix = "person")``

**作用：**读取 yaml 配置文件中的属性

​	将配置文件中配置的每一个属性的值，映射到这个组件中；告诉 Springboot 将本类中的所有属性和配置文件中相关的配置进行绑定，参数 prefix = “persion” ：将配置文件中的 persion 下面的所有属性一一对应， 只有这个组件是容器中的组件，才能使用容器提供的``@ConfigurationProperties(prefix = "person")`` 功能

![image-20211011195422171](SpringBoot 学习笔记.assets/image-20211011195422171.png)



2. 读取 properties 文件中的属性

- 使用注解 ``@PropertySource("classpath:peng.properties")``

![image-20211011205859838](SpringBoot 学习笔记.assets/image-20211011205859838.png)



yaml  ``@ConfigurationProperties`` 与  properties ``@PropertySource``&``@Value``对比

![image-20211011215927611](SpringBoot 学习笔记.assets/image-20211011215927611.png)

- cp 只需要写一次即可， value 则需要每个字段都添加
  - 松散绑定： yml 中写的是 last-name 或 last_name， 它可以和类中的 lastName 自动映射。**（数据库中常用）**
- JSR303 数据校验， 这个就是我们可以在字段增加一层过滤验证，可以保证数据的合法性。
- 复杂类型封装 ，yml 中可以封装对象， 使用@Value 就不支持。



**结论：**

- 配置 yml  和配置 properties 都可以获取到值，强烈推荐 yml
- 如果我们在业务中，只需要获取配置文件中的某个值，可以使用一下 @Value
- 如果说，我们专门编写了一个 JavaBean 来和配置文件进行映射，就直接使用 ``@ConfigurationProperties`` ，不要犹豫！



3. 结果对比

![image-20211011202430261](SpringBoot 学习笔记.assets/image-20211011202430261.png)





### 6.4 BUG

1. 使用``@ConfigurationProperties(prefix = "person")``注解爆红，不过不影响使用。

![image-20211011195058372](SpringBoot 学习笔记.assets/image-20211011195058372.png)

解决办法：引入一个jar包`

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

> ​		You can easily generate your own configuration metadata file from items annotated with `@ConfigurationProperties` by using the `spring-boot-configuration-processor` jar. The jar includes a Java annotation processor which is invoked as your project is compiled

2. 日期格式问题

   在配置文件中的日期的格式应该是： 1999/11/20， 而不应该使用-

![image-20211011201015887](SpringBoot 学习笔记.assets/image-20211011201015887.png)

3. properties 文件的乱码问题

![image-20211011205445663](SpringBoot 学习笔记.assets/image-20211011205445663.png)

解决办法：

![image-20211011205538378](SpringBoot 学习笔记.assets/image-20211011205538378.png)



PS： 输出日志（这好像就是Springboot的一整个启动流程--）

```
C:\Users\peng\.jdks\corretto-1.8.0_292\bin\java.exe -ea -Didea.test.cyclic.buffer.size=1048576 "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2020.3.2\lib\idea_rt.jar=50875:C:\Program Files\JetBrains\IntelliJ IDEA 2020.3.2\bin" -Dfile.encoding=GBK -classpath "C:\Program Files\JetBrains\IntelliJ IDEA 2020.3.2\lib\idea_rt.jar;C:\Users\peng\.m2\repository\org\junit\platform\junit-platform-launcher\1.6.3\junit-platform-launcher-1.6.3.jar;C:\Users\peng\.m2\repository\org\apiguardian\apiguardian-api\1.1.0\apiguardian-api-1.1.0.jar;C:\Users\peng\.m2\repository\org\junit\platform\junit-platform-engine\1.6.3\junit-platform-engine-1.6.3.jar;C:\Users\peng\.m2\repository\org\opentest4j\opentest4j\1.2.0\opentest4j-1.2.0.jar;C:\Users\peng\.m2\repository\org\junit\platform\junit-platform-commons\1.6.3\junit-platform-commons-1.6.3.jar;C:\Program Files\JetBrains\IntelliJ IDEA 2020.3.2\plugins\junit\lib\junit5-rt.jar;C:\Program Files\JetBrains\IntelliJ IDEA 2020.3.2\plugins\junit\lib\junit-rt.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\charsets.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\access-bridge-64.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\cldrdata.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\dnsns.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\jaccess.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\jfxrt.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\localedata.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\nashorn.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\sunec.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\sunjce_provider.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\sunmscapi.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\sunpkcs11.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\ext\zipfs.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\jce.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\jfr.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\jfxswt.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\jsse.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\management-agent.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\resources.jar;C:\Users\peng\.jdks\corretto-1.8.0_292\jre\lib\rt.jar;D:\newProject\idea-workspace\springBoot\springboot-02-config\target\test-classes;D:\newProject\idea-workspace\springBoot\springboot-02-config\target\classes;D:\Script\Maven\repository\org\springframework\boot\spring-boot-starter\2.3.7.RELEASE\spring-boot-starter-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot\2.3.7.RELEASE\spring-boot-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\springframework\spring-context\5.2.12.RELEASE\spring-context-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-autoconfigure\2.3.7.RELEASE\spring-boot-autoconfigure-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-starter-logging\2.3.7.RELEASE\spring-boot-starter-logging-2.3.7.RELEASE.jar;D:\Script\Maven\repository\ch\qos\logback\logback-classic\1.2.3\logback-classic-1.2.3.jar;D:\Script\Maven\repository\ch\qos\logback\logback-core\1.2.3\logback-core-1.2.3.jar;D:\Script\Maven\repository\org\apache\logging\log4j\log4j-to-slf4j\2.13.3\log4j-to-slf4j-2.13.3.jar;D:\Script\Maven\repository\org\apache\logging\log4j\log4j-api\2.13.3\log4j-api-2.13.3.jar;D:\Script\Maven\repository\org\slf4j\jul-to-slf4j\1.7.30\jul-to-slf4j-1.7.30.jar;D:\Script\Maven\repository\jakarta\annotation\jakarta.annotation-api\1.3.5\jakarta.annotation-api-1.3.5.jar;D:\Script\Maven\repository\org\springframework\spring-core\5.2.12.RELEASE\spring-core-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\spring-jcl\5.2.12.RELEASE\spring-jcl-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\yaml\snakeyaml\1.26\snakeyaml-1.26.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-starter-web\2.3.7.RELEASE\spring-boot-starter-web-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-starter-json\2.3.7.RELEASE\spring-boot-starter-json-2.3.7.RELEASE.jar;D:\Script\Maven\repository\com\fasterxml\jackson\core\jackson-databind\2.11.3\jackson-databind-2.11.3.jar;D:\Script\Maven\repository\com\fasterxml\jackson\core\jackson-annotations\2.11.3\jackson-annotations-2.11.3.jar;D:\Script\Maven\repository\com\fasterxml\jackson\core\jackson-core\2.11.3\jackson-core-2.11.3.jar;D:\Script\Maven\repository\com\fasterxml\jackson\datatype\jackson-datatype-jdk8\2.11.3\jackson-datatype-jdk8-2.11.3.jar;D:\Script\Maven\repository\com\fasterxml\jackson\datatype\jackson-datatype-jsr310\2.11.3\jackson-datatype-jsr310-2.11.3.jar;D:\Script\Maven\repository\com\fasterxml\jackson\module\jackson-module-parameter-names\2.11.3\jackson-module-parameter-names-2.11.3.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-starter-tomcat\2.3.7.RELEASE\spring-boot-starter-tomcat-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\apache\tomcat\embed\tomcat-embed-core\9.0.41\tomcat-embed-core-9.0.41.jar;D:\Script\Maven\repository\org\glassfish\jakarta.el\3.0.3\jakarta.el-3.0.3.jar;D:\Script\Maven\repository\org\apache\tomcat\embed\tomcat-embed-websocket\9.0.41\tomcat-embed-websocket-9.0.41.jar;D:\Script\Maven\repository\org\springframework\spring-web\5.2.12.RELEASE\spring-web-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\spring-beans\5.2.12.RELEASE\spring-beans-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\spring-webmvc\5.2.12.RELEASE\spring-webmvc-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\spring-aop\5.2.12.RELEASE\spring-aop-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\spring-expression\5.2.12.RELEASE\spring-expression-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-starter-test\2.3.7.RELEASE\spring-boot-starter-test-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-test\2.3.7.RELEASE\spring-boot-test-2.3.7.RELEASE.jar;D:\Script\Maven\repository\org\springframework\boot\spring-boot-test-autoconfigure\2.3.7.RELEASE\spring-boot-test-autoconfigure-2.3.7.RELEASE.jar;D:\Script\Maven\repository\com\jayway\jsonpath\json-path\2.4.0\json-path-2.4.0.jar;D:\Script\Maven\repository\net\minidev\json-smart\2.3\json-smart-2.3.jar;D:\Script\Maven\repository\net\minidev\accessors-smart\1.2\accessors-smart-1.2.jar;D:\Script\Maven\repository\org\ow2\asm\asm\5.0.4\asm-5.0.4.jar;D:\Script\Maven\repository\org\slf4j\slf4j-api\1.7.30\slf4j-api-1.7.30.jar;D:\Script\Maven\repository\jakarta\xml\bind\jakarta.xml.bind-api\2.3.3\jakarta.xml.bind-api-2.3.3.jar;D:\Script\Maven\repository\jakarta\activation\jakarta.activation-api\1.2.2\jakarta.activation-api-1.2.2.jar;D:\Script\Maven\repository\org\assertj\assertj-core\3.16.1\assertj-core-3.16.1.jar;D:\Script\Maven\repository\org\hamcrest\hamcrest\2.2\hamcrest-2.2.jar;D:\Script\Maven\repository\org\junit\jupiter\junit-jupiter\5.6.3\junit-jupiter-5.6.3.jar;D:\Script\Maven\repository\org\junit\jupiter\junit-jupiter-api\5.6.3\junit-jupiter-api-5.6.3.jar;D:\Script\Maven\repository\org\apiguardian\apiguardian-api\1.1.0\apiguardian-api-1.1.0.jar;D:\Script\Maven\repository\org\opentest4j\opentest4j\1.2.0\opentest4j-1.2.0.jar;D:\Script\Maven\repository\org\junit\platform\junit-platform-commons\1.6.3\junit-platform-commons-1.6.3.jar;D:\Script\Maven\repository\org\junit\jupiter\junit-jupiter-params\5.6.3\junit-jupiter-params-5.6.3.jar;D:\Script\Maven\repository\org\junit\jupiter\junit-jupiter-engine\5.6.3\junit-jupiter-engine-5.6.3.jar;D:\Script\Maven\repository\org\junit\platform\junit-platform-engine\1.6.3\junit-platform-engine-1.6.3.jar;D:\Script\Maven\repository\org\mockito\mockito-core\3.3.3\mockito-core-3.3.3.jar;D:\Script\Maven\repository\net\bytebuddy\byte-buddy\1.10.18\byte-buddy-1.10.18.jar;D:\Script\Maven\repository\net\bytebuddy\byte-buddy-agent\1.10.18\byte-buddy-agent-1.10.18.jar;D:\Script\Maven\repository\org\objenesis\objenesis\2.6\objenesis-2.6.jar;D:\Script\Maven\repository\org\mockito\mockito-junit-jupiter\3.3.3\mockito-junit-jupiter-3.3.3.jar;D:\Script\Maven\repository\org\skyscreamer\jsonassert\1.5.0\jsonassert-1.5.0.jar;D:\Script\Maven\repository\com\vaadin\external\google\android-json\0.0.20131108.vaadin1\android-json-0.0.20131108.vaadin1.jar;D:\Script\Maven\repository\org\springframework\spring-test\5.2.12.RELEASE\spring-test-5.2.12.RELEASE.jar;D:\Script\Maven\repository\org\xmlunit\xmlunit-core\2.7.0\xmlunit-core-2.7.0.jar" com.intellij.rt.junit.JUnitStarter -ideVersion5 -junit5 com.peng.Springboot02ConfigApplicationTests,test1

20:06:54.398 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating CacheAwareContextLoaderDelegate from class [org.springframework.test.context.cache.DefaultCacheAwareContextLoaderDelegate]

20:06:54.414 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating BootstrapContext using constructor [public org.springframework.test.context.support.DefaultBootstrapContext(java.lang.Class,org.springframework.test.context.CacheAwareContextLoaderDelegate)]

20:06:54.430 [main] DEBUG org.springframework.test.context.BootstrapUtils - Instantiating TestContextBootstrapper for test class [com.peng.Springboot02ConfigApplicationTests] from class [org.springframework.boot.test.context.SpringBootTestContextBootstrapper]

20:06:54.430 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Neither @ContextConfiguration nor @ContextHierarchy found for test class [com.peng.Springboot02ConfigApplicationTests], using SpringBootContextLoader

20:06:54.445 [main] DEBUG org.springframework.test.context.support.AbstractContextLoader - Did not detect default resource location for test class [com.peng.Springboot02ConfigApplicationTests]: class path resource [com/peng/Springboot02ConfigApplicationTests-context.xml] does not exist

20:06:54.445 [main] DEBUG org.springframework.test.context.support.AbstractContextLoader - Did not detect default resource location for test class [com.peng.Springboot02ConfigApplicationTests]: class path resource [com/peng/Springboot02ConfigApplicationTestsContext.groovy] does not exist

20:06:54.445 [main] INFO org.springframework.test.context.support.AbstractContextLoader - Could not detect default resource locations for test class [com.peng.Springboot02ConfigApplicationTests]: no resource found for suffixes {-context.xml, Context.groovy}.

20:06:54.445 [main] INFO org.springframework.test.context.support.AnnotationConfigContextLoaderUtils - Could not detect default configuration classes for test class [com.peng.Springboot02ConfigApplicationTests]: Springboot02ConfigApplicationTests does not declare any static, non-private, non-final, nested classes annotated with @Configuration.

20:06:54.467 [main] DEBUG org.springframework.test.context.support.ActiveProfilesUtils - Could not find an 'annotation declaring class' for annotation type [org.springframework.test.context.ActiveProfiles] and class [com.peng.Springboot02ConfigApplicationTests]

20:06:54.514 [main] DEBUG org.springframework.context.annotation.ClassPathScanningCandidateComponentProvider - Identified candidate component class: file [D:\newProject\idea-workspace\springBoot\springboot-02-config\target\classes\com\peng\Springboot02ConfigApplication.class]

20:06:54.514 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Found @SpringBootConfiguration com.peng.Springboot02ConfigApplication for test class com.peng.Springboot02ConfigApplicationTests

20:06:54.583 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - @TestExecutionListeners is not present for class [com.peng.Springboot02ConfigApplicationTests]: using defaults.

20:06:54.583 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Loaded default TestExecutionListener class names from location [META-INF/spring.factories]: [org.springframework.boot.test.mock.mockito.MockitoTestExecutionListener, org.springframework.boot.test.mock.mockito.ResetMocksTestExecutionListener, org.springframework.boot.test.autoconfigure.restdocs.RestDocsTestExecutionListener, org.springframework.boot.test.autoconfigure.web.client.MockRestServiceServerResetTestExecutionListener, org.springframework.boot.test.autoconfigure.web.servlet.MockMvcPrintOnlyOnFailureTestExecutionListener, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverTestExecutionListener, org.springframework.boot.test.autoconfigure.webservices.client.MockWebServiceServerTestExecutionListener, org.springframework.test.context.web.ServletTestExecutionListener, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener, org.springframework.test.context.support.DependencyInjectionTestExecutionListener, org.springframework.test.context.support.DirtiesContextTestExecutionListener, org.springframework.test.context.transaction.TransactionalTestExecutionListener, org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener, org.springframework.test.context.event.EventPublishingTestExecutionListener]

20:06:54.599 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Skipping candidate TestExecutionListener [org.springframework.test.context.transaction.TransactionalTestExecutionListener] due to a missing dependency. Specify custom listener classes or make the default listener classes and their required dependencies available. Offending class: [org/springframework/transaction/interceptor/TransactionAttributeSource]

20:06:54.599 [main] DEBUG org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Skipping candidate TestExecutionListener [org.springframework.test.context.jdbc.SqlScriptsTestExecutionListener] due to a missing dependency. Specify custom listener classes or make the default listener classes and their required dependencies available. Offending class: [org/springframework/transaction/interceptor/TransactionAttribute]

20:06:54.599 [main] INFO org.springframework.boot.test.context.SpringBootTestContextBootstrapper - Using TestExecutionListeners: [org.springframework.test.context.web.ServletTestExecutionListener@5acf93bb, org.springframework.test.context.support.DirtiesContextBeforeModesTestExecutionListener@7e7be63f, org.springframework.boot.test.mock.mockito.MockitoTestExecutionListener@6cd28fa7, org.springframework.boot.test.autoconfigure.SpringBootDependencyInjectionTestExecutionListener@614ca7df, org.springframework.test.context.support.DirtiesContextTestExecutionListener@4738a206, org.springframework.test.context.event.EventPublishingTestExecutionListener@66d3eec0, org.springframework.boot.test.mock.mockito.ResetMocksTestExecutionListener@1e04fa0a, org.springframework.boot.test.autoconfigure.restdocs.RestDocsTestExecutionListener@1af2d44a, org.springframework.boot.test.autoconfigure.web.client.MockRestServiceServerResetTestExecutionListener@18d87d80, org.springframework.boot.test.autoconfigure.web.servlet.MockMvcPrintOnlyOnFailureTestExecutionListener@618425b5, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverTestExecutionListener@58695725, org.springframework.boot.test.autoconfigure.webservices.client.MockWebServiceServerTestExecutionListener@543588e6]

20:06:54.599 [main] DEBUG org.springframework.test.context.support.AbstractDirtiesContextTestExecutionListener - Before test class: context [DefaultTestContext@209da20d testClass = Springboot02ConfigApplicationTests, testInstance = [null], testMethod = [null], testException = [null], mergedContextConfiguration = [WebMergedContextConfiguration@e15b7e8 testClass = Springboot02ConfigApplicationTests, locations = '{}', classes = '{class com.peng.Springboot02ConfigApplication}', contextInitializerClasses = '[]', activeProfiles = '{}', propertySourceLocations = '{}', propertySourceProperties = '{org.springframework.boot.test.context.SpringBootTestContextBootstrapper=true}', contextCustomizers = set[org.springframework.boot.test.context.filter.ExcludeFilterContextCustomizer@d4342c2, org.springframework.boot.test.json.DuplicateJsonObjectContextCustomizerFactory$DuplicateJsonObjectContextCustomizer@56de5251, org.springframework.boot.test.mock.mockito.MockitoContextCustomizer@0, org.springframework.boot.test.web.client.TestRestTemplateContextCustomizer@6e0dec4a, org.springframework.boot.test.autoconfigure.properties.PropertyMappingContextCustomizer@0, org.springframework.boot.test.autoconfigure.web.servlet.WebDriverContextCustomizerFactory$Customizer@149e0f5d, org.springframework.boot.test.context.SpringBootTestArgs@1, org.springframework.boot.test.context.SpringBootTestWebEnvironment@71bc1ae4], resourceBasePath = 'src/main/webapp', contextLoader = 'org.springframework.boot.test.context.SpringBootContextLoader', parent = [null]], attributes = map['org.springframework.test.context.web.ServletTestExecutionListener.activateListener' -> true]], class annotated with @DirtiesContext [false] with mode [null].
20:06:54.615 [main] DEBUG org.springframework.test.context.support.TestPropertySourceUtils - Adding inlined properties to environment: {spring.jmx.enabled=false, org.springframework.boot.test.context.SpringBootTestContextBootstrapper=true}


  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.3.7.RELEASE)

2021-10-11 20:18:43.278  INFO 20452 --- [           main] c.p.Springboot02ConfigApplicationTests   : Starting Springboot02ConfigApplicationTests on peng with PID 20452 (started by peng in D:\newProject\idea-workspace\springBoot\springboot-02-config)

2021-10-11 20:18:43.278  INFO 20452 --- [           main] c.p.Springboot02ConfigApplicationTests   : No active profile set, falling back to default profiles: default

2021-10-11 20:18:43.924  INFO 20452 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'

2021-10-11 20:18:44.077  INFO 20452 --- [           main] c.p.Springboot02ConfigApplicationTests   : Started Springboot02ConfigApplicationTests in 0.995 seconds (JVM running for 1.588)

Person{name='帅比', age=18, happy=true, birth=Sat Nov 20 00:00:00 CST 1999, maps={k1=v1, k2=v2, friends={0=song, 1=hao, 2=peng}}, lists=[yanba, song, teng, lin, x], dog=Dog{name='小SB', age=8}}

2021-10-11 20:18:44.225  INFO 20452 --- [extShutdownHook] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'

```





## 7.  JSR303 校验

## 7.1  松散绑定

**配置文件和类中的属性名** ： 驼峰命名和下划线 是可以自动替换的

![image-20211012000323328](SpringBoot 学习笔记.assets/image-20211012000323328.png)

![image-20211012000428148](SpringBoot 学习笔记.assets/image-20211012000428148.png)





### 7.2

1. 注解：``@Validated``



2. 引入外部依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

3. 使用校验，大小、非空、长度

"G:\RunningCheeseChrome\App\chrome_proxy.exe"  --user-data-dir="G:\RunningCheeseChrome\Data" --profile-directory=Default --app-id=ahiigpfcghkbjfcibpojancebdfjmoop

![img](https://img2020.cnblogs.com/blog/528977/202005/528977-20200519100023944-67212265.png)



![image-20211012002352353](SpringBoot 学习笔记.assets/image-20211012002352353.png)





## 8. 多环境配置及配置文件位置

### 8.1  各配置文件路径及其优先级

 ![image-20211012131823887](SpringBoot 学习笔记.assets/image-20211012131823887.png)

```
1. file:./config/
2. file:./
3.classpath:/config/
4.classpath:/
```

在实际应用的时候，可以通过在较高优先级位置新建一个配置文件 来覆盖之前的配置。



### 8.2  多环境配置

测试和开发两个场景总会有不同的环境配置，

![image-20211012195323731](SpringBoot 学习笔记.assets/image-20211012195323731.png)

**Properties：**可以通过多配置文件来切换不同的环境（注意命名规范--==application开头==），切换通过以下语句来切换：

```properties
# springboot 的多环境配置， 可以选择激活哪一个配置文件
spring.profiles.active=test
```



#### 8.2.2  **Yaml 文件情况**

- [**SpirngBoot2.4 配置文件加载机制的变化**](https://blog.csdn.net/qq_16063307/article/details/108140237)
- [Springboot2.4 配置文件变化](https://www.cnblogs.com/javastack/p/14078993.html)

​	yaml 文件可以启用多套配置（使用 ``---`` 分隔）， springboot 2.4版本之后，``application.properties`` 和 ``application.yml`` 文件的加载方式都有所改变

​	在版本 2.4 之后， 加载 properties 和 YAML  文件时候会遵循：**在文档中声明排序靠前的属性将被靠后的属性覆盖**

```yml
test: "hello"
---
test: "Just test"
```



**PS：这点存疑**

> ​	在Springboot2.4 ， Properties 支持类似 YAML 多文档功能，多文档属性文件 使用注释（#）后跟三个（---）破折号来分隔文档 .

```properties
test=hello
#---
test=Just test
```

#### 8.2.3  特定文件激活配置

> ​	SpringBoot 2.3 前可以通过 spring.profiles 来实现，SpringBoot2.4 之后，则通过 spring.config.activate.on-profile 来配置	

```properties
test=hello
#---
spring.config.activate.on-profile=dev
test=Just test
```



#### 8.2.4  启动相对应的配置文件

​	可以通过 spring.profiles.active 属性 在 application.properties 或 application.yaml 文件的 **根配置文件** 来激活 相关配置文件

​	不允许将 ``spring.profiles.active`` 属性与 ``spring.config.activate.on-profile`` 一起使用，两者在一起会引发异常。

![image-20211012224141526](SpringBoot 学习笔记.assets/image-20211012224141526.png)



### 8.3  代码示例

```yaml
# spring.config.use-legacy-processing: true

spring.config.activate.on-profile: dev
env: dev

server:
  port: 8088


---
spring.config.activate.on-profile: test
env: test
server:
  port: 8089



---
spring.config.activate.on-profile: default
env: default
server:
  port: 8087
  
---
spring.profiles.active: dev
```



## 9.  自动配置再理解

### 9.1

取其中一个自动配置类：

![image-20211012233725658](SpringBoot 学习笔记.assets/image-20211012233725658.png)

取装配的 ``ServerProperties`` 类，结构如下：

![image-20211013000539306](SpringBoot 学习笔记.assets/image-20211013000539306.png)

**留意注解：**

``@ConfigurationProperties(prefix = "server", ignoreUnknownFields = true)``

```java
// 表示这是一个配置类
@Configuration(proxyBeanMethods = false)

// 自动配置属性： ServerProperties 此类中有哪些可以配置的属性
@EnableConfigurationProperties(ServerProperties.class)

// Spring 的底层注解： 根据不同的条件，来判断当前配置或类是否生效
@ConditionalOnWebApplication(type = ConditionalOnWebApplication.Type.SERVLET)
@ConditionalOnClass(CharacterEncodingFilter.class)
@ConditionalOnProperty(prefix = "server.servlet.encoding", value = "enabled", matchIfMissing = true)
public class HttpEncodingAutoConfiguration {

    private final Encoding properties;

    public HttpEncodingAutoConfiguration(ServerProperties properties) {
        this.properties = properties.getServlet().getEncoding();
    }
```

**重点：**注解``@EnableConfigurationProperties(ServerProperties.class)``
  在实际编程中，如果我们忘记了要配置的属性，则可以根据该注解，找到对应的配置类，查找类中有哪些属性（这些属性即是会被注入的属性）

> ​	 在我们这配置文件中配置的东西，都存在一个固有的规律：
>
> xxxAutoConfiguration （装配下一个类）→  xxxProperties（有各种属性） → 绑定了配置文件



**结论：**

1）SpringBoot 启动会加载大量的自动配置类

2）我们看我们需要的功能有没有在SpringBoot 默认写好的自动配置类当中；

3）我们再来看这个自动配置类中到底配置了哪些组件；（只要我们要用的组件存在其中，我们就不需要再手动配置了）

4）给容器中自动配置类添加组件的时候，会从 properties 类中获取某些属性。我们只需要在配置文件中制定这些属性的值即可。

xxxAutoConfiguration：**自动配置类；给容器中添加组件**

xxxProperties：**封装配置文件中相关属性**



From 弹幕：

> ​		``springboot``是通过``main``方法下的``SpringApplication.run``方法启动的,启动的时候他会调用refshContext方法,先刷新容器,然后根据解析注解或者解析配置文件的形式祖册bean,而它是通过启动类的``SpringBootApplication``注解进行开始解析的,他会根据EnableAutoConfiguration开启自动化配置,里面有个核心方法ImportSelect选择性的导入,根据l``oadFanctoryNames``根据``classpash``路径以``MATA-INF/spring.factorces``下面以什么什么``EnableAutoConfiguration``开头的  ``key``  去加载里面所有对应的自动化配置,他并不是把这一百二十多个自动化配置全部导入,在他每个自动化配置里面都有条件判断注解,先判断是否引入相互的jar包,再判断容器是否有bean再进行注入到bean容器







## 10.  Springboot Web开发

---

**思考：** Springboot 到底帮我们配置了什么？ 我们能不能进行修改？ 能修改哪些东西？ 能不能扩展？

- xxxxAutoConfiguration....  向容器中自动配置组件
- xxxxProperties： 自动配置类，装配配置文件中自定义的一些内容！



要解决的问题：

- 静态资源导入问题
- 首页
- JSP ，模板引擎 Thymeleaf
- 装配扩展 SpringMVC
- 增删改查
- 拦截器
- 国际化



### 10.1  静态资源导入探究



```java
// WebMvcAutoConfiguration.class

@Override
		public void addResourceHandlers(ResourceHandlerRegistry registry) {
			if (!this.resourceProperties.isAddMappings()) {
				logger.debug("Default resource handling disabled");
				return;
			}
			Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
			CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
			if (!registry.hasMappingForPattern("/webjars/**")) {
				customizeResourceHandlerRegistration(registry.addResourceHandler("/webjars/**")
						.addResourceLocations("classpath:/META-INF/resources/webjars/")
						.setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
			}
			String staticPathPattern = this.mvcProperties.getStaticPathPattern();
			if (!registry.hasMappingForPattern(staticPathPattern)) {
				customizeResourceHandlerRegistration(registry.addResourceHandler(staticPathPattern)
						.addResourceLocations(getResourceLocations(this.resourceProperties.getStaticLocations()))
						.setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
			}
		}
```



什么是 ``webjars``

- https://www.webjars.org/



![image-20211013132238295](SpringBoot 学习笔记.assets/image-20211013132238295.png)

加载优先级： 

定制 →  classpath:resources  →  classpath:public →  classpath:static

![image-20211025223255025](SpringBoot 学习笔记.assets/image-20211025223255025.png)









**PS：**以下这个问题好像又没遇到了，也许是我刚开始的时候有什么东西忘记配了。。

- [继承WebMvcConfigurationSupport后自动配置不生效的问题及如何配置拦截器](https://blog.csdn.net/fmwind/article/details/82832758)

![image-20211015111337741](SpringBoot 学习笔记.assets/image-20211015111337741.png)

​	该注解的意思是在项目类路径中缺少 WebMvcConfigurationSupport 类型的 Bean 时该自动配置类才会生效，

**解决办法**：

​	==所以继承 WebMvcConfigurationSupport 后再重写相应的方法==。

```java
@Configuration
public class MyWebMvc extends WebMvcConfigurationSupport {

    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/**").addResourceLocations("classpath:/static/")
                .addResourceLocations("classpath:/public/").addResourceLocations("classpath:/resources/");
        super.addResourceHandlers(registry);
    }
}

```









总结：







### 10.2  首页如何定制

![image-20211025215259277](SpringBoot 学习笔记.assets/image-20211025215259277.png)



### 10.3  thymeleaf模板引擎

> ​		模板引擎的作用就是我们来写一个页面模板，比如有些值呢，是动态的，我们写一些表达式。而这些值，从哪来呢？我们来==组装一些数据==，我们把这些数据找到。然后把这个模板和这个数据交给我们模板引擎，模板引擎按照我们这个数据帮你把这==表达式解析、填充到我们指定的位置==，然后把这个数据最终生成一个我们想要的内容给我们写出去，这就是我们这个模板引擎，不管是 JSP 还是其他模板引擎，都是这个思想。

结论：只要需要使用 thymeleaf， 只需要导入对应的依赖就可以了，我们将 html 放在我们的 ==templates== 目录下

1. 导入依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

2. 查看其自动配置源码

``ThymeleafAutoConfiguration.java`` →  ``ThymeleafProperties.java``

可知其存放地点：

![image-20211026212343636](SpringBoot 学习笔记.assets/image-20211026212343636.png)

3. 在相应的路径新建 html 文档，使用

```html
<body>
<h1>Test</h1>
<p>取变量——→</p>

<!--所有的 html 元素都可以被 thymeleaf 替换顺序 ，th:元素名-->
<p th:text="${msg}"></p>
<div><a th:href="${url}">baidu</a>
</div>

<div th:text="${msg2}"></div>
<div th:utext="${msg2}"></div>

<hr>
<div>
    <!--行内写法-->
    <h3 th:each="user:${users}">[[${user}]]</h3>
    <!--建议用这种写法-->
    <h3 th:each="user:${users}" th:text="${user}"></h3>
</div>
</body>
```

4. 代码

```java
RequestMapping("test")
    public String toText(Model model){
    model.addAttribute("msg","我是一个大可比");
    model.addAttribute("url","www.baidu.com");
    model.addAttribute("msg2","<h1>Test转义与否</h1>");
    model.addAttribute("users", Arrays.asList("帅鹏","帅坤","无敌大帅比","haha"));
    return "test";

}
```

#### 10.3.2  Thymeleaf 语法

![image-20211027231609285](SpringBoot 学习笔记.assets/image-20211027231609285.png)

```javascript
1.$符号取上下文中的变量：
<input type="text" name="userName"  th:value="${user.name}">

    
2.#符号取thymeleaf工具中的方法、文字消息表达式：
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>


3.　*{...}选择表达式一般跟在th:object后，直接选择object中的属性
<div th:object="${session.user}">
<p th:text="*{name}"/><div>
```







### 10.4  MVC 配置原理--扩展及装配

#### 10.4.1

```java
//如果， 你想DIY 一些定制化的功能，只要写这个组件，然后将它交给 Springboot ，Springboot 就会帮我们自动装配
//public interface ViewResolver   实现了视图解析器接口的类，我们就可以把它看作视图解析器
//扩展 SpringMVC ， dispatchservlet
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {
    
    @Bean
    public ViewResolver MyViewResolver(){return new MyViewResolver();}

    //自定义了一个自己的视图解析器
    public static class MyViewResolver implements ViewResolver{
        @Override
        public View resolveViewName(String viewName, Locale locale) throws Exception {
            return null;
        }
    }
}
```

![image-20211026221351392](SpringBoot 学习笔记.assets/image-20211026221351392.png)



**结论：**

​	Springboot 在自动配置很多组件的时候，会先看容器中有没有用户自己配置的（如果用户自己配置 @Bean），如果有就用用户配置的，如果没有就用自动配置的；如果有些组件可以存在多个，比如视图解析器，就将用户配置的和自己默认的**组合**起来！



#### 10.4.2 扩展

![image-20211026224200106](SpringBoot 学习笔记.assets/image-20211026224200106.png)





**总结：**

​	在 ``Springboot`` ，在非常多的 xxx  Configuration 帮助我们进行扩展配置，只要看见了这个东西，我们就要注意了。



**PS：怎么写一个启动器**

一个 Configuration 类 + 一个 Properties类， 把两个类打到一个 jar包里边，再放到 spring.boot.autoconfigure 下：



## 11 员工管理系统

### 11.1 首页配置

**注意点：** 所有页面的静态资源都需要使用 thymeleaf 接管，url： ``@{}``

![image-20211027233821377](SpringBoot 学习笔记.assets/image-20211027233821377.png)

新知识点： 配置项   ``server.servlet.context-path``

![image-20211027233930912](SpringBoot 学习笔记.assets/image-20211027233930912.png)



### 11.2  页面国际化

1. 我们需要配置 i18 文件

![image-20211028235118952](SpringBoot 学习笔记.assets/image-20211028235118952.png)

2. 我们如果需要在项目中进行==按钮自动切换==，我们需要自定义一个组件 ``LocaleResolver``

```java
public class MyLocaleResolver implements LocaleResolver {

    //解析请求
    @Override
    public Locale resolveLocale(HttpServletRequest request) {

        String language = request.getParameter("l");
        Locale locale = Locale.getDefault();  //如果没有就使用默认的
        System.out.println(getClass().getSimpleName()+"执行了一下--------------");
        //如果请求的链接携带了国际化的参数
        if (!StringUtils.isEmpty(language)){
            String[] split = language.split("_");
            //国家 地区
            locale =  new Locale(split[0], split[1]);
        }

        return locale;
    }

    @Override
    public void setLocale(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Locale locale) {

    }
}

```

![image-20211028235621826](SpringBoot 学习笔记.assets/image-20211028235621826.png)



3. 记得将自己写的组件配置到 spring 容器

```java
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {

    @Bean
    public LocaleResolver localeResolver(){
        return new MyLocaleResolver();
    }

}
```

4. 在 html 页面文件中更改 **#{}**

![image-20211124111855294](SpringBoot 学习笔记.assets/image-20211124111855294.png)



PS：

1.  这里是因为：Spring 根据方法名找到 bean 

![image-20211028205333402](SpringBoot 学习笔记.assets/image-20211028205333402.png)

2. 







### 10.3  登录功能实现

代码实现：

```java
@Controller
public class LoginController {

    @RequestMapping("/user/login")
    private String login(@RequestParam("username")String username,
                         @RequestParam("password") String password,
                         Model model, HttpSession session){
        //具体的业务
        if (!StringUtils.isEmpty(username) && password.equals("txzs")){
            System.out.println("Debug---登录成功");
            session.setAttribute("loginUser",username);
            return "redirect:/main.html";
        }else {
            model.addAttribute("msg","用户名或者密码错误");
            System.out.println("Debug---登录错误");
            return "index";
        }
    }
}
```



问题：没有样式

![image-20211029003720852](SpringBoot 学习笔记.assets/image-20211029003720852.png)

解决方法： 样式引入的时候路径没有使用对

![image-20211029003905929](SpringBoot 学习笔记.assets/image-20211029003905929.png)



### 10.4  拦截器



1. 自定义拦截器，编写逻辑

```java
public class LoginHandlerInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //登录成功之后，应该有用户的 session
        Object loginUser = request.getSession().getAttribute("loginUser");
        if (loginUser == null){
            request.setAttribute("msg","没有权限，请先登录");
            request.getRequestDispatcher("/index.html").forward(request,response);
            return false;
        }else {
            return  true;
        }

    }
}
```



2. 使其生效

```java

@Configuration
public class MyMvcConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginHandlerInterceptor())
            .addPathPatterns("/**").excludePathPatterns("/index.html","/index","/","/user/login");
    }
}
```







### 10.4 展示员工列表

1. 提取公共页面

   1. 新建一个 html, 把重复的 html  标签提取出来，新增一个 th:fragment="***" 属性，

      ![image-20211124165754055](SpringBoot 学习笔记.assets/image-20211124165754055.png)

   2. 引用上面新增的属性

      ![image-20211124165851932](SpringBoot 学习笔记.assets/image-20211124165851932.png)

   3. 如果要传递参数，可以使用（）  传参，接收判断即可
   
      ```
      <div th:replace="~{common/commons::Sidebar(active='list.html')}"></div>
      ```

   4. 列表循环展示
   
      ```html
      <div class="table-responsive">
         <table class="table table-striped table-sm">
            <thead>
               <tr>
                  <th>id</th>
                  <th>lastName</th>
                  <th>email</th>
                  <th>sex</th>
                  <th>department</th>
                  <th>birth</th>
               </tr>
            </thead>
            <tbody>
               <tr th:each="emp:${emps}">
                  <td th:text="${emp.getId()}"></td>
                  <td>[[${emp.getLastName()}]]</td>
                  <td th:text="${emp.getEmail()}"></td>
                  <td th:text="${emp.getSex()%2==0?'女':'男'}"></td>
                  <td th:text="${emp.getDepartment().getDepartmentName()}"></td>
                  <td th:text="${#dates.format(emp.getBirth(),'yyyy-MM-dd HH:mm:ss')}"></td>
                  <td>
                     <button class="btn btn-sm btn-primary">编辑</button>
                     <button class="btn btn-sm btn-danger">删除</button>
                  </td>
               </tr>
            </tbody>
         </table>
      </div>
      ```



### 10.5  增加员工显示

1. 按钮提交

![image-20211106224754247](SpringBoot 学习笔记.assets/image-20211106224754247.png)

2. 跳转到添加页面
3. 添加员工成功

4. 返回首页

```java
@GetMapping("/emps/toAdd")
public String toAdd(Model model){
    //查出所有部门并显示在前端
    Collection<Department> department = departmentDao.getDepartment();
    model.addAttribute("departs",department);
    return "emp/add";
}

@PostMapping("/emps/toAdd")
public String addEmp(Employee emps){
    //添加的操作
    System.out.println("=====>"+emps);
    employeeDao.save(emps);
    return "redirect:/emps";
}
```

![image-20211106225119051](SpringBoot 学习笔记.assets/image-20211106225119051.png)



### 10.6 修改员工信息 

1. 页面 以及 跳转的 url 和 controller

```html
<td>
   <a class="btn btn-sm btn-primary" th:href="@{emps/toUpdate/}+${emp.getId()}">编辑</a>  <!--@{emps/toUpdate/(${emp.getId()})}-->
   <a class="btn btn-sm btn-danger" th:href="@{emps/delete/}+${emp.getId()}">删除</a>
</td>
```

```java
@PostMapping("/emps/update")
public String update(Employee employee){
    //employeeDao.update(employee);
    System.out.println("=======>"+employee);
    employeeDao.save(employee);
    return "redirect:/emps";
}
```

2. **注意 隐藏域传值（传ID）**

![image-20211107154138916](SpringBoot 学习笔记.assets/image-20211107154138916.png)



### 10.7  删除、404以及注销

1. 删除，按钮跳转→url传参→写controller →重定向 list

2. 404， 在templates下新建一个 error ，然后挂一个 404 页面

![image-20211107151257453](SpringBoot 学习笔记.assets/image-20211107151257453.png)

3. 注销

   ```java
   @GetMapping("/emps/loginOut")
   public String loginOut(HttpSession session){
       session.removeAttribute("loginUser");
       //session.invalidate();
       return "redirect:/index";
   }
   ```





### 10.8 Bug

PS：

1. 没有 name 属性是无法提交的，提交不通

![image-20211105001842491](SpringBoot 学习笔记.assets/image-20211105001842491.png)

2. spring 为什么不能注入 static 变量

![image-20211106215216627](SpringBoot 学习笔记.assets/image-20211106215216627.png)

3. 特么匪夷所思的错误，自己贱呐

   我自己在存储部门的时候，那个 Map 的ID 没有对应上 部门的ID ，但是我在前端传值的时候，传的是一个部门的ID 上去的， 这时候通过这个部门的ID 就不可能在 Map 里面找到对应的部门

   ![image-20211106222652270](SpringBoot 学习笔记.assets/image-20211106222652270.png)

   前端传值：

   ![image-20211106223029651](SpringBoot 学习笔记.assets/image-20211106223029651.png)

   前端添加效果：

   ![image-20211106223146036](SpringBoot 学习笔记.assets/image-20211106223146036.png)

   后台报错：

   ![image-20211106223430028](SpringBoot 学习笔记.assets/image-20211106223430028.png)

4. **链接的形式都是 GetMapping**

5. 这次的错误是没有在controller中给 model 加入 department 的属性，导致前端 thymeleaf 模板取不到这个属性，出错![image-20211107005129122](SpringBoot 学习笔记.assets/image-20211107005129122.png)

   卧槽， 然后我把这个注释掉，我去，又特么可以了？？？？完全不知道之前为什么会出错。。咦，不过，前端什么也点不出来 

   ![image-20211107011014771](SpringBoot 学习笔记.assets/image-20211107011014771.png)

6. 思考，修改 map 中的 某个对象
   - 直接删除，然后添加，，
   - 规规矩矩的修改
   - ==map 中新增 key 相同的对象即修改这个 key==

7. 这里有个没有解决的问题：就我在修改 员工信息的时候的一个尝试：如果是删除员工然后在新增，按理说也能达到修改的效果，但是这种做法导致了修改完重定向到列表页面的时候缺失了 department 对象。

   ```java
   public void update(Employee employee){
       employees.remove(employee.getId());
       employees.put(employee.getId(), employee);
   }
   ```

   ![image-20211107144730475](SpringBoot 学习笔记.assets/image-20211107144730475.png)



## 12  聊聊如何写一个网站



### 12. 1 前端

- 模板：别人写好的，我们拿来改成自己需要的
- 框架：组件：自己手动组合拼装！ BootStrap 、LayUI 、semantic-ui
  - 栅格系统
  - 导航栏
  - 侧边栏
  - 表单



**步骤：**

```
1. 前端搞定： 页面长什么样子： 涉及哪些数据

2. 设计数据库 （数据库设计难点！！）

3. 前端让他能够自动运行，独立化工程 

4. 数据接口如何对接？ json、对象 all in one

5. 前后端联调测试
```

条件：（一个月）

1. 有一套自己熟悉的==后台模板==：工作必要！ x-admin
2. 前端界面：至少自己能够通过前端框架，组合出来一个网站页面
   - index    首页
   - about    关于
   - blog    详情页面（main）
   - post    提交页面
   - user   用户页面

3. 让这个网站能够独立运行

   ```
   用户功能
   增删改查功能
   拦截器思想
   添加分布式功能
   把项目模块化拆分
   ```

   

## 回顾

- springboot 是什么？
  - 开源的轻量级框架，一种全新的编程规范，他的产生简化了spring 的使用，其自动装配的特性简化了 spring 所需的大量配置文件，所以 springboot 是一个服务于框架的框架 
- 微服务
- 熟悉Helloworld程序
- 探究源码→ 熟悉自动装配的原理
- Springboot  的配置 → yaml
- 多文档环境切换
- 静态资源映射
- Thymeleaf    th: ***
- Springboot 如何扩展 MVC    采用 javaconfig 的形式
- 如何修改 SpringBoot 的默认配置
- CRUD
- 国际化
- 拦截器
- 定制首页、错误页



还未涉及到的东西：

- JDBC
- Mybatis   **(重点)**
- Druid   **（重点）**
- Shiro   搞安全的框架  **（重点）**
- Spring  Security  ：也是安全的框架   **（重点）**
- 异步任务 、邮件发送 、定时任务（：这个可以用Redis吗？）**（表达式）**
- Swagger
- Dubbo +  ZooKeeper



## 13  整合 JDBC 使用



### 13.1  简介

​	对于数据访问层，无论是 SQL（关系型数据库）还是NOSQL（非关系型数据库）， Springboot 底层都是采用 Spring Data 的方式进行统一处理 。

​	Spring Boot **底层**都是 采用 Spring Data 的方式进行**统一处理各种数据库**， Spring Data 也是 Spring 中与 Spring Boot 、Spring Cloud 等齐名的知名项目。



### 13.2 搭建项目

1. 在新建的时候 可以顺便勾选 Mysql Driver 、 JDBC API 等等

   ![image-20211107231100317](SpringBoot 学习笔记.assets/image-20211107231100317.png)

   ![image-20211107231116664](SpringBoot 学习笔记.assets/image-20211107231116664.png)

2. 配置

```yaml
spring:
  datasource:
    username: root
    password: txzs
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai&useSSL=false
    driver-class-name: com.mysql.cj.jdbc.Driver
```

3. 代码

```java
@RestController
public class JDBCController {

    @Autowired
    JdbcTemplate jdbcTemplate;

    //查询数据库的所有信息
    //没有实体类，数据库中 东西怎么获取 ？ 万能的　Map
    @GetMapping("/userList")
    public List<Map<String,Object>> userList(){
        String sql = "select * from mybatis.user";
        return jdbcTemplate.queryForList(sql);
    }

    @GetMapping("/addUser")
    public String addUser(){
        String sql = "insert into mybatis.user(id,name,pwd) values(7,'大傻逼','11111')";
        jdbcTemplate.update(sql);
        return "OK";
    }

    @GetMapping("/update")
    public String update(){
        String sql = "update  mybatis.user set name = '无敌大帅比' where id = 7";
        jdbcTemplate.update(sql);
        sql = "select * from mybatis.user";
        System.out.println((jdbcTemplate.queryForList(sql)));
        return "OK";
    }

    @GetMapping("/update/{id}")
    public String update1(@PathVariable("id")int id){
        String sql = "update mybatis.user set name = ? , pwd = ? where id = "+id;

        Object[] objects = new Object[2];
        objects[0] = "无敌是多么寂寞";
        objects[1] = "wwwwwww";
        jdbcTemplate.update(sql,objects);
        return "OK";
    }


    @GetMapping("/delete")
    public String delete(){
        String sql = "delete from mybatis.user where id = 7";
        jdbcTemplate.execute(sql);
        return "ok";
    }

    @GetMapping("/delete/{id}")
    public String delete1(@PathVariable("id") int id){
        String sql = "delete from mybatis.user where id =?";
        jdbcTemplate.update(sql,id);
        return "OK";
    }
}
```



有关 ``Springboot`` 包

![image-20211109233248110](SpringBoot 学习笔记.assets/image-20211109233248110.png)

![image-20211109233323655](SpringBoot 学习笔记.assets/image-20211109233323655.png)









PS：

1. JPA（持久层API） 以及JPA 的简单使用	
   - https://www.jianshu.com/p/b2baadbabc66

2. 小思考 ：``import static 包名.类名.*`` ，static 起什么作用 ？

![image-20211108001026318](SpringBoot 学习笔记.assets/image-20211108001026318.png)

​	即静态导入，相比常规的导入，多了一个 static，和末尾的 ``.*``，**意思是导入这个类里的静态成员（静态方法、静态变量）**，当然，也可以只导入某个静态方法，只要把 .* 换成静态方法名就行了。

```
1.静态导入可能会让代码更加难以阅读

2.import static和static import不能替i

3.如果同时导入的两个类中又有重命名的静态成员，会出现编译器错误。例如Integer类和Long类的MAX_VALUE。

4可以导入的静态成员包括静态对象引用、静态常量和静态方法
```



## 14  整合 Druid 数据源

### 14.1 简介

> ​	Druid 是阿里巴巴开源平台上一个 数据库连接池实现，结合了C3P0、DBCP、PROXOOL 等DB池的优点，同时加入了**日志监控。**
>
> ​	Druid 可以 很好的监控 DB 池连接和 SQL 的执行情况，天生就是针对监控而生的DB 连接池。	
>
> ​	Springboot 2.0 以上默认使用Hikari 数据源，可以说 Hikari 与 Druid 都是当前 Java Web 上最优秀的数据源。



### 14.2  编写

**重点：** 代码为什么要这么写？添加用户名和密码的配置是怎么个定义的，在哪个源码文件中可以找到呢？

```java
@Configuration
public class DruidConfig {

    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DataSource druidDataSource(){
        return new DruidDataSource();
    }

    //后台监控功能 : 需要配置web.xml， ServletRegistrationServlet
    //因为 SpringBoot 内置了 servlet 容器，所以没有 web.xml，
    // 替代方法：ServletRegistrationBean
    @Bean
    public ServletRegistrationBean StatViewServlet(){
        ServletRegistrationBean<StatViewServlet> bean = new ServletRegistrationBean<>(new StatViewServlet(), "/druid/*");

        //后台需要有人登录， 账号密码
        HashMap<String, String> initParameters = new HashMap<>();
        //增加配置
        initParameters.put("loginUsername","admin");
        initParameters.put("loginPassword","123456");

        //允许谁可以访问
        initParameters.put("allow",""); //为空代表所有人可以访问

        // 禁止谁能访问
        //initParameters.put("peng","121.4.82.98");

        bean.setInitParameters(initParameters); //设置初始化参数
        return bean;
    }
```

新增 过滤器的功能：

```java
// filter 过滤功能
public FilterRegistrationBean webStatFilter(){
    FilterRegistrationBean<Filter> bean = new FilterRegistrationBean<>();
    bean.setFilter(new WebStatFilter());
    HashMap<String, String> initParams = new HashMap<>();
    //可以过滤哪些请求呢？
    //这些东西不进行统计 以下的参数反而可以在源码中找到
    initParams.put("exclusions","*.js,*.css,/druid/*");

    return bean;

}
```



## 15  整合 Mybatis

```
1. 导入包
2. 写Mybatis配置
3. 写接口
4. 写 mapper （SQL语句）
5. service 层调 dao 层
6. controller 调用 service 层
```



1. 配置文件 

```yaml
mybatis:
  mapper-locations: classpath:mapper/userMapper.xml
  type-aliases-package: com.peng.pojo
spring:
  datasource:
    name: defaultDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai&useSSL=false
    username: HQ
    password: txzs
    type: com.zaxxer.hikari.HikariDataSource
```

2. 接口

```java
@Mapper //这个注解表示了这是一个 mybatis 的mapper 类；
@Repository
// @MapperScan("com.peng.mapper") 扫描包
public interface UserMapper {

    /*@Select("select * from mybatis.user")
    public List<User> userList();*/

    public List<User> userList();

}
```

3. mapper 的SQL 语句

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.peng.mapper.UserMapper">
    <select id="userList" resultType="User" useCache="true">
        select * from mybatis.user
    </select>

</mapper>
```

4.  

利用 SqlSession：

```java
@Component
public class UserDao {

    @Autowired
    SqlSession sqlSession;
    public List<User> userList(){

        return sqlSession.selectList("userList");
    }
    
}
```

利用　Mapper：（直接利用就可）

```java
public class UserController {

    @Autowired
    UserMapper mapper;

    @GetMapping("/userList")
    public List<?> userList(){
        List<User> objects = mapper.userList();
        System.out.println("=====>"+objects);
        return objects;
    }
}
```

5. 调用 

```
@GetMapping("/userList")
public List<?> userList(){
    List<User> objects = mapper.userList();
    //List<User> objects = userDao.userList();
    System.out.println("=====>"+objects);
    return objects;
}
```



PS:

1. 注解 **@mapper**

   ​	作用是可以给mapper接口==自动生成一个实现类==，让spring对mapper接口的bean进行管理，并且可以省略去写复杂的xml文件

2. 写了xml，使用@mapper也会走到xml文件中，但是如果xml和@select同时存在，会报错，只能使用其中一种，如果交替使用（有的用@Select，有的用xml文件）呢？==这个还没有试过==



### 15.4  BUG

1. XML 头部声明导入错误

![image-20211110230039266](SpringBoot 学习笔记.assets/image-20211110230039266.png)

正确的应该用这个，这个才是用来写映射的：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```





## 16  SpringSecurity（安全）

### 16.1  简介

- 在 web 开发中，安全第一位！ 过滤器，拦截器 
- 功能性需求： 否
- 做网站的，安全应该在什么时候考虑？→ 设计之初
  - 漏洞 → 隐私泄漏
  - 架构一旦确定 ，增加安全机制会影响大量的代码



**世面上常用的框架：**

- shiro、
- SpringSecurity

很像，除了类不一样、名字不一样。



**权限分类：**

- 功能权限
- 访问权限
- 菜单权限

如果使用 拦截器、过滤器： 需要大量的原生代码 → 冗余



**SpringSecurity：**用于 “spring 应用程序的高度可定制的身份验证和访问控制框架。

![image-20211111104757888](SpringBoot 学习笔记.assets/image-20211111104757888.png)

> ​	Spring Security is a powerful and highly customizable authentication  and access-control framework. It is the de-facto standard for securing  Spring-based applications.
>
> ​	Spring Security is a framework that focuses on providing both  authentication and authorization to Java applications. Like all Spring  projects, the real power of Spring Security is found in how easily it  can be extended to meet custom requirements

​	是针对 spring 项目的安全框架，也是 Springboot 底层安全模块默认的技术选型，他可以实现强大的Web 安全控制，对于安全控制，我们仅需要引入 spring-boot-starter-security 模块， 进行少量的配置，即可实现强大的安全管理！

​	记住几个类：

- WebSecurityConfigAdapter：自定义Security策略 （适配器模式）
  - 自定义的类会继承这个类，然后看需求重写对应的方法；
- AuthenticationManagerBuilder：自定义认证策略 （建造者模式）
- @EnableWebSecurity：开启 WebSecurity 模式

Spring Security 的两个主要目标是 **”认证“**  和 **”授权“**（访问控制）

“认证”

”授权“



###  16.2  代码 

```java
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        super.configure(http);
    }
}
```

所有的代码 ：

```java
@EnableWebSecurity
//@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    //链式编程
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        //首页所有人可以访问，但是功能页只有对应有权限的人才能访问
        //请求授权的规则
        http.authorizeRequests()
                .antMatchers("/").permitAll()
                .antMatchers("/level1/**").hasRole("vip1")
                .antMatchers("/level2/**").hasRole("vip2")
                .antMatchers("/level3/**").hasRole("vip3");

        //开启没有权限默认跳到登录页面的功能，这里可以开启登录的页面
        http.formLogin().loginPage("/toLogin");

        //开启了注销功能
        //注销完，应该跳到首页
        http.logout().logoutSuccessUrl("/index");

        //防止网站攻击 get post
        http.csrf().disable();

        //开启记住我功能  本质上就是一个 cookie，默认保存两周
        http.rememberMe().rememberMeParameter("remember");

    }

    //认证 , springboot 2.1.x 可以直接使用
    //密码编码： PassWordEncoder
    //在 SpringBoot 5.0 中新增了很多的加密方法
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                .withUser("peng").password(new BCryptPasswordEncoder().encode("txzs")).roles("vip1","vip2")
                .and()
                .withUser("root").password(new BCryptPasswordEncoder().encode("txzs")).roles("vip1","vip2","vip3")
                .and()
                .withUser("kun").password(new BCryptPasswordEncoder().encode("txzs")).roles("vip3");
    }
}

```

在完善登录后能显示已登录账号的操作：

```html
<!--登录注销-->
<div class="right menu">
    <!--未登录-->
    <!--显示登录按钮-->
    <div sec:authorize="!isAuthenticated()">
        <a class="item" th:href="@{/toLogin}">
            <i class="address card icon"></i> 登录
        </a>
    </div>

    <!--如果已登录 → 显示用户名和 注销按钮-->
    <div sec:authorize="isAuthenticated()">
        <a class="item">
            用户名：<span sec:authentication="name"></span>
            角 色：<span sec:authentication="principal.authorities"></span>
        </a>
    </div>
    <a class="item" th:href="@{/logout}">
        <i class="sign-out icon"></i> 注销
    </a>
    <!--已登录
    <a th:href="@{/usr/toUserCenter}">
        <i class="address card icon"></i> admin
    </a>
    -->
</div>
```



在针对不同账号展现不同页面的时候：

![image-20211116000422508](SpringBoot 学习笔记.assets/image-20211116000422508.png)



在自定义首页添加记住我的功能的时候： 注意这里的 name属性

![image-20211116000053393](SpringBoot 学习笔记.assets/image-20211116000053393.png)

![image-20211116000119000](SpringBoot 学习笔记.assets/image-20211116000119000.png)









### 16.3  BUG

1. 

![image-20211111231508250](SpringBoot 学习笔记.assets/image-20211111231508250.png)





## 17  Shiro

### 17.1  什么是 Shiro ？

- Apache Shiro 是一个 Java 的安全（权限）框架 
- Shiro可以非常容易的开发出足够好的应用，其不仅可以用在 JavaSE 环境，也可以用在 JavaEE 环境。
- Shiro 可以完成，认证、授权、加密、会话管理、Web集成、缓存等。



#### 17.1.1 有哪些功能

**图**

- 身份认证、登录、验证用户是不是拥有相应的身份
- 授权、即权验证，验证某个已认证的用户是否拥有某个权限，即判断用户能否进行什么操作
- Session Mannager：会话管理，即用户登录后就是第一次回话，在没有退出之前，它的所有信息都在会话中；会话可以是普通的 JavaSE 环境，也可以是Web 环境。
- Cryptography：加密，保护数据的安全性，如密码加密存储到数据库中，而不是明文存储；
- Web Support ：Web支持，可以非常容易的集成到Web 环境；
- Caching ：缓存，比如用户登录后，其用户信息，拥有的角色，权限不必每次去查看，这样可以提高效率
- Concurrency：Shiro 支持多线程应用的的并发验证，即，如在一个线程中开启另一个线程，能把权限自动的传播过去
- Testing ：提供测试支持
- Run As：允许一个用户假装为另一个用户（如果他们允许）的身份进行访问。
- Remember Me：记住我，这是非常常见的一个功能，即一次登录后，下次再来的话不用登录了。



#### 17.1.2  Shiro 架构（外部）

从外部来看 Shiro ，即从应用程序的角度来观察如何使用 Shiro 完成工作：

**图**

- Subject ：应用代码直接交互的对象是 Subject，也就是说 Shiro 的对外 核心API就是Subject，Subject 代表了当前的用户，这个用户不一定是一个具体的人，与当前应用交互的任何东西都是 Subject ，如网络爬虫，机器人等，与 Subject 的所有交互都会委托 给 SecurityManager：Subject 其实是一个门面， SecurityManageer 才是实际的执行者
- SecurityManager： 安全管理器，即所有的与安全相关的操作都会与 SecurityManager 交互，并且它管理着所有的 Subject ，可以看出它是 Shiro 的核心，它负责与 Shiro 的其他组件进行交互，它相当于 SpringMVC 的DispatcheeerServlet 的角色
- Realm： Shiro 从 Realm 获取安全数据（如用户、角色、权限），就是说SecurityManager 要验证用户身份，那么她需要从 Realm 获取相应的用户进行比较，来确定用户的身份是否合法；也需要中 Realm 得到用户相应的角色、权限，进行验证用户的操作是否能够进行，可以把 Realm 看成 DataSource



#### 17.1.3 Shiro架构 外部

图

- Subject：任何可以与应用交互的用户
- Security Manager： 相当于 SpringMVC 中的DispatcherServlet ：是Shiro  的心脏，所有具体的交互都通过 Security Manager 进行控制，它管理着所有的 Subject，且负责进行认证、授权、会话、及缓存的管理。
- Authenticator：负责 Subject认证，是一个扩展点，可以自定义实现，可以使用 认证策略（Authentication Strategy），即什么情况下算用户认证通过了？
- Realm：可以有一个或多个 的Realm ，可以认为是安全实体数据源，即用于获取安全实体的，可以用 JDBC 实现，也可以是由内存实现等等，有用户提供；所以一般在应用中都需要实现自己的 Realm
- SessionManager：管理 Session 生命周期的组件，而 Shiro 并不仅仅可以用在 Web 环境，也可以用在普通的 JavaSE 环境中
- CacheManager：缓存控制器，来管理如用户，角色，权限等缓存的；因为这些数据基本上很少改变，放到缓存中后可以提高访问的性能
- Cryptography： 密码模块， Shiro 提高了一些常见的加密组件用于密码加密，解密等



### 17.2  实践



#### 17.2.1 快速入门

```java
// 1. 获取 securityManager
DefaultSecurityManager securityManager=new DefaultSecurityManager();
IniRealm iniRealm=new IniRealm("classpath:shiro.ini");
securityManager.setRealm(iniRealm);

// 2. 获取 Subject（当前用户对象）
SecurityUtils.setSecurityManager(securityManager);
Subject currentUser = SecurityUtils.getSubject();

// 3. 通过当前用户拿到 Session
Session session = currentUser.getSession();
session.setAttribute("someKey", "天下最帅比");
String value = (String) session.getAttribute("someKey");

// 4. 获取当前用户认证
currentUser.getPrincipal();
    
// 5. 当前用户是否拥有什么角色
currentUser.hasRole("***");

// 6. 获取用户的一些权限
currentUser.isPermitted("lightsaber:wield");

// 7. 注销
currentUser.logout();

// 8. 结束
System.exit(0);
```

**一个用户对应很多角色，一个角色对应很多权限；**



#### 17.2.2  Springboot 中集成



1. 导入 jar 包

```xml
<dependencies>

    <!--
    Subject: 用户
    SecurityManager：管理所有用户
    Realm： 连接数据
    -->
    <!--导入 Shiro-->
    <dependency>
        <groupId>org.apache.shiro</groupId>
        <artifactId>shiro-spring-boot-web-starter</artifactId>
        <version>1.8.0</version>
    </dependency>

    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
    </dependency>

    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid-spring-boot-starter</artifactId>
        <version>1.2.8</version>
    </dependency>

    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.12</version>
    </dependency>

    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>2.1.4</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
        <exclusions>
            <exclusion>
                <groupId>org.junit.vintage</groupId>
                <artifactId>junit-vintage-engine</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```

2. 编写 Realm

```java
//自定义的 UserRealm
public class UserRealm extends AuthorizingRealm {

    @Autowired
    UserServiceImpl userService;
    private static final Logger log = LoggerFactory.getLogger(UserRealm.class);
    // 授权
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
        log.info("【INFO】执行了====》授权 doGetAuthorizationInfo");
        System.out.println("执行了====》授权 doGetAuthorizationInfo");
        return null;
    }

    // 认证
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
        log.info("【INFO】执行了====》认证  doGetAuthenticationInfo");

        /*String name= "root";
        String password = "txzs";*/

        UsernamePasswordToken token = (UsernamePasswordToken)authenticationToken;
        User user = userService.queryUserByName(token.getUsername());
        log.info("[INFO]==>"+user);
        // 下面这个 if 语句是无效的，因为 user 是根据 token 中的名字来取的，
        // 现在用 token 中的名字来对比 user 的名字，那一定是相同的
        /*if (!token.getUsername().equals(user.getName())){
            return null;  //抛出异常 ： UnknowAccountException

        }*/
        if (user==null) { //没有这个人
            return null;
        }

        //密码认证 ，Shiro 来做
        //这里的密码可以加密 ： MD5、 MD5 颜值加密
        return new SimpleAuthenticationInfo("",user.getPwd(),"");
    }
}
```



3. 编写 Config

```java
@Configuration
public class ShiroConfig {

    // 3.ShiroFilterFactoryBean
    // 2.DefaultWebSecurityManager
    // 1.创建 Realm 对象 ，需要自定义类

    // 1.创建 Realm 对象
    @Bean
    public UserRealm userRealm(){
        return new UserRealm();
    }

    // 2.DefaultWebSecurityManager
    @Bean(name = "defaultWebSecurityManager")
    public DefaultWebSecurityManager getDefaultWebSecurityManager(@Autowired UserRealm userRealm){
        DefaultWebSecurityManager defaultWebSecurityManager = new DefaultWebSecurityManager();
        //关联 UserRealm

        defaultWebSecurityManager.setRealm(userRealm);
        return defaultWebSecurityManager;
    }

    // 3.ShiroFilterFactoryBean
    @Bean(name = "shiroFilterFactoryBean")
    public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("defaultWebSecurityManager") DefaultWebSecurityManager defaultWebSecurityManager){
        ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
        //设置安全管理器
        bean.setSecurityManager(defaultWebSecurityManager);

        // 添加 shiro 的内置过滤器
        /*
        *  anon: 无需认证就可以访问
        *  authc: 必须认证才能访问
        *  user: 必须拥有 记住我 功能才能使用
        *  perms: 拥有对某个资源的权限才能访问
        *  role: 拥有某个角色权限才能访问
        *
        * */

        //关于 登录拦截
        Map<String, String> filterMap = new LinkedHashMap<>();
//        filterMap.put("/user/add","authc");
//        filterMap.put("/user/update","authc       filterMap.put("/user/*),"authc");;
        filterMap.put("/user/*","authc");
        bean.setFilterChainDefinitionMap(filterMap);

        //设置登录的请求
        bean.setLoginUrl("/toLogin");
        
        return bean;

    }
```

4. 编写 配置文件

```yaml
spring:
  datasource:
    username: HQ
    password: txzs
    url: jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf8&serverTimezone=Asia/Shanghai&useSSL=false
    driver-class-name: com.mysql.cj.jdbc.Driver
    type: com.alibaba.druid.pool.DruidDataSource

    #SpringBoot默认是不注入这些的，需要自己绑定
    #druid数据源专有配置
    # druid:
    initialSize: 5
    minIdle: 5
    maxActive: 20
    maxWait: 60000
    timeBetweenEvictionRunsMillis: 60000
    minEvictableIdleTimeMillis: 300000
    validationQuery: SELECT 1 FROM DUAL
    testWhileIdle: true
    testOnBorrow: false
    testOnReturn: false
    poolPreparedStatements: true

    #配置监控统计拦截的filters，stat：监控统计、log4j：日志记录、wall：防御sql注入
    #如果允许报错，java.lang.ClassNotFoundException: org.apache.Log4j.Properity
    #则导入log4j 依赖就行
    filters: stat,wall,log4j
    maxPoolPreparedStatementPerConnectionSize: 20
    useGlobalDataSourceStat: true
    connectionoProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500
```

```properties
mybatis.type-aliases-package=com.peng.pojo
mybatis.mapper-locations=classpath:mapper/*.xml
```



5. 编写Controller

```java
@Controller
public class MyController {

    private static Logger log = LoggerFactory.getLogger(MyController.class);

    @GetMapping({"/toIndex","/index","/"})
    public String index(Model model){
        model.addAttribute("msg","hello,Shiro,你是一个无敌大帅比");
        return "index";
    }

    @GetMapping("/user/add")
    public String toAdd(){
        return "user/add";
    }

    @GetMapping("/user/update")
    public String toUpdate(){
        return "user/update";
    }

    @GetMapping("toLogin")
    public String toLogin(){
        return "/login";
    }

    @RequestMapping("/login")
    public String login(String username, String password,Model model){

        //获取当前的用户
        Subject subject = SecurityUtils.getSubject();

        //封装用户的登录数据
        UsernamePasswordToken token = new UsernamePasswordToken(username, password);

        //执行登录的访问，如果没有异常，说明OK
        try {
            subject.login(token);
            return "/index";
        } catch (UnknownAccountException e) { //用户名不存在
            model.addAttribute("msg","用户名错误");
            log.info("[INFO] 用户名错误");

            log.info("[INFO] log.getName()==>"+log.getName());
            log.info("[INFO] log.getClass()==>"+log.getClass().getName());
            //System.out.println("====》用户名错误");
            return "/login";
        } catch (IncorrectCredentialsException e) {//密码错误
            model.addAttribute("msg","密码错误");
            log.info("[INFO] 密码错误");
            return "/login";
        }
    }
}
```

PS：当不指定具体的日志实现类的时候，log4j 默认使用 ``ch.qos.logback.classic.Logger`` 来实现。







#### 17.2.3 Shiro 实现登录拦截

![image-20211121005351934](SpringBoot 学习笔记.assets/image-20211121005351934.png)



#### 17.2.4  Shiro 实现用户认证











#### 17.2.5  Shiro 整合 Mybatis

1. 引入 Mybatis 启动包

![image-20211121004817767](SpringBoot 学习笔记.assets/image-20211121004817767.png)

2. 配置文件编辑数据源



3. 新建Mapper查询接口

![image-20211121004920777](SpringBoot 学习笔记.assets/image-20211121004920777.png)

4. 新建 Mapper 映射文件

![image-20211121005011039](SpringBoot 学习笔记.assets/image-20211121005011039.png)

5. Service 层引用 mapper 查询

```java
@Service
public class UserServiceImpl implements UserService{
    @Resource
    UserMapper userMapper;

    @Override
    public User queryUserByName(String name) {
        return userMapper.queryUserByName(name);
    }
}
```

6. Shiro 具体使用

![image-20211121005215901](SpringBoot 学习笔记.assets/image-20211121005215901.png)



#### 17.2.6  Shiro请求授权的实现

1. 在 ShiroConfig.java 中添加 ==哪些请求需要什么权限==的操作

![image-20211121163555626](SpringBoot 学习笔记.assets/image-20211121163555626.png)



2. 在Realm 中添加授权操作

![image-20211121164343514](SpringBoot 学习笔记.assets/image-20211121164343514.png)

关于认证的那个方法：

![image-20211121164813507](SpringBoot 学习笔记.assets/image-20211121164813507.png)

PS：注销操作

```java
@GetMapping("/logout")
public String logout(){
    Subject subject = SecurityUtils.getSubject();
    subject.logout();
    return "redirect:/index";
}
```



#### 17.2.7  Shiro 整合Thymeleaf

1. 导包

```xml
<dependency>
    <groupId>com.github.theborakompanioni</groupId>
    <artifactId>thymeleaf-extras-shiro</artifactId>
    <version>2.0.0</version>
</dependency>
```

2. HTML 页面上的使用

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org"
      xmlns:shiro="http://www.pollix.at/thymeleaf/shiro">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
<h1>首页</h1>
<p th:text="${msg}"></p>
<div shiro:hasPermission="user:add">
    <a th:href="@{/user/add}">add</a>
</div>
<div shiro:hasPermission="user:update">
    <a th:href="@{/user/update}">update</a>
</div>
<div th:if="${session.loginUser==null}">
    <a th:href="@{/toLogin}">登录</a>
</div>
<div th:if="${session.loginUser!=null}">
    <a th:href="@{/logout}">注销</a>
</div>

</body>
</html>
```

![image-20211121202017414](SpringBoot 学习笔记.assets/image-20211121202017414.png)







**注意：**

1. 在 try - catch 语句中，返回语句应该在什么位置的问题

![image-20211120171132298](SpringBoot 学习笔记.assets/image-20211120171132298.png)

==但至于为什么呢？？？？===



2.  mapper 映射文件的 namespace 配置

![image-20211120223536795](SpringBoot 学习笔记.assets/image-20211120223536795.png)



3. application.properties与application.yaml 同时存在时，两个文件都有效，但是 ``properties`` 的优先级会更高。
   - [Properties 与 Yaml 同时存在的时候 ](https://blog.csdn.net/luckyzsion/article/details/84564493)





PS：常用的图标库

- https://semantic-ui.com/
- https://www.iconfont.cn/home/index?spm=a313x.7781069.1998910419.2



----

## 思考

1. 拓展

![image-20211024234155400](SpringBoot 学习笔记.assets/image-20211024234155400.png)

2. [final 修饰基本类型值不能变，修饰引用类型地址不能变，值可以变](https://blog.csdn.net/qunqunstyle99/article/details/101014687)。
   - 本质上还是 final 修饰的对象，其地址不能变。



3. Java 中的基本类型不一定都存放在栈中，其存放位置取决于声明的位置。

   - 在方法中声明的变量，即该变量是局部变量，每当程序调用方法时，系统都会为该方法建立一个方法栈，其所在方法中声明的变量就放在方法栈中，当方法结束系统会释放方法栈，其对应在该方法中声明的变量随着栈的销毁而结束，==这也局部变量只能在方法中有效的原因。==
     - 方法中的局部变量 ，其变量名及值（变量名及值是两个概念）都是放在Java 虚拟机栈中。
     - 当声明的是引用变量时，所声明的变量（该变量实际上是在方法中存储的是**内存地址值**）是放在 Java 虚拟机的栈中，该变量所指向的对象是放在堆内存中的。

   - 在类中声明变量是成员变量（全局变量），是放在堆中的**（因为全局变量不会随着某个方法的执行结束而销毁）。**
     - 当声明的是基本类型的变量 其变量名及其值放在堆内存中的
     - 引用类型时，其声明的变量仍然会存储一个内存地址值，该内存地址值所引用的对象。引用变量名和对应的对象仍然存储在相应的堆中。



4. 

```java
public class ClassTest {

    String str = new String("peng");

    public void fun(String str){
        this.str = "shuai"; //修改的是类变量
        // str = "shuai"; // 修改的是形参
    }

    public static void main(String[] args) {
        ClassTest classTest = new ClassTest();
        classTest.fun(classTest.str);
        System.out.println(classTest.str);

    }

}
```



5. **常用的 T，E，K，V，？**  
   - https://blog.csdn.net/youanyyou/article/details/100910242

> ### **常用的 T，E，K，V，？**
>
> 本质上这些个都是通配符，没啥区别，只不过是编码时的一种约定俗成的东西。比如上述代码中的 T ，我们可以换成 A-Z 之间的任何一个 字母都可以，并不会影响程序的正常运行，但是如果换成其他的字母代替 T ，在可读性上可能会弱一些。**通常情况下，T，E，K，V，？是这样约定的：**
>
> + ？表示不确定的 java 类型
> + T (type) 表示具体的一个java类型
> + K V (key value) 分别代表java键值中的Key Value
> + E (element) 代表Element

**无界通配符：** ``？``

**上界通配符：**``< ? extends E>``

	- 表示参数化的类型可能是所指定的类型，或者是此类型的子类

**下界通配符：**``<?  super  E>``

​	- 使用 super 进行声明，表示参数化的类型可能是所指定的类型，或者是此类型的父类型，直至 Object



**？ 和  T 的区别：**

- T 是一个 ”确定的“ 类型，通常用于泛形类和泛形方法的定义， ``？`` 是一个 “不确定” 的类型， 通常用于泛型方法的调用代码 和形参， 不能用于定义类和泛型方法。

  ```java
  // 可以	
  T t = operate();	
  // 不可以	
  ？car = operate();
  ```

- **区别一：** 通过 T 来“确保” 泛型参数的一致性

  ```
  // 通过 T 来 确保 泛型参数的一致性	
  public <T extends Number> void test(List<T> dest, List<T> src)	
  //通配符是 不确定的，所以这个方法不能保证两个 List 具有相同的元素类型	
  public void test(List<? extends Number> dest, List<? extends Number> src)
  ```

  ![image-20211109235507729](SpringBoot 学习笔记.assets/image-20211109235507729.png)







## 附

1. 2021-09-26

![image-20210926221056822](C:\Users\peng\AppData\Roaming\Typora\typora-user-images\image-20210926221056822.png)



2. 莫名

![image-20211023223143212](SpringBoot 学习笔记.assets/image-20211023223143212.png)



3. 畜生

![image-20211024011528569](SpringBoot 学习笔记.assets/image-20211024011528569.png)

![image-20211024011550895](SpringBoot 学习笔记.assets/image-20211024011550895.png)



4. 

![image-20211025010401150](SpringBoot 学习笔记.assets/image-20211025010401150.png)

