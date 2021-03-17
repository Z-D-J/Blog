---
title: Spring Boot
date: 2020-09-20 15:29:43
tags:
---

# SpringBoot简介

[官方文档](https://spring.io/projects/spring-boot#learn)

* Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。
* SpringBoot所具备的特征有：
（1）可以创建独立的Spring应用程序，并且基于其Maven或Gradle插件，可以创建可执行的JARs和WARs；
（2）内嵌Tomcat或Jetty等Servlet容器；
（3）提供自动配置的“starter”项目对象模型（POMS）以简化Maven配置；
（4）尽可能自动配置Spring容器；
（5）提供准备好的特性，如指标、健康检查和外部化配置；
（6）绝对没有代码生成，不需要XML配置。
* 微服务（或微服务架构）是一种云原生架构方法，其中单个应用程序由许多松散耦合且可独立部署的较小组件或服务组成。这些服务通常有自己的堆栈，包括数据库和数据模型；
通过REST API，事件流和消息代理的组合相互通信；
* 它们是按业务能力组织的，分隔服务的线通常称为有界上下文。
* 尽管有关微服务的许多讨论都围绕体系结构定义和特征展开，但它们的价值可以通过相当简单的业务和组织收益更普遍地理解：
* 可以更轻松地更新代码。
* 团队可以为不同的组件使用不同的堆栈。
* 组件可以彼此独立地进行缩放，从而减少了因必须缩放整个应用程序而产生的浪费和成本，因为单个功能可能面临过多的负载。

# 快速入门

* 可以在[官网](https://start.spring.io/)直接配置下载入门项目。
* 也可以在idea中通过spring initializer快速创建springboot项目。
* ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314111338.png)
* 默认项目结构如下图：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314111453.png)
  * 可以删除不必要的文件，如.mvn,.gitignore等。
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314112222.png)
* 项目结构解释：
  * `SpringbootApplicaton.java`（项目名+Application.java）:是整个SpringBoot项目的主入口，不能删也不能改。
  * `application.properties`是SpringBoot的配置文件（一般会用.yml文件）。
  * test包下默认有一个测试类：`SpringbootApplicationTests.java`，即在主入口名后加上Tests。
  * 项目的代码**放在Application的同级目录中，在此例中，所有业务代码都应放在`com.zestaken.springboot`包下**。（可以在这个包下再建包）
  * 编写controller层代码，在页面上显示hello：
  ```java
  package com.zestaken.springboot.controller;


    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class HelloController {

        @RequestMapping("/hello")
        public String hello() {
            return "hello springboot!";
        }
    }
    ```
    * 无需编写视图层，便能直接将结果显示到页面上：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314113132.png)
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314113033.png)
* pom.xml配置解释：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
<!--    有一个父项目 继承spring-boot-starter-parent的依赖管理，控制版本与打包等内容-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.3</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.zestaken</groupId>
    <artifactId>springboot</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springboot</name>
    <description>Demo project for Spring Boot</description>

<!--    java版本-->
    <properties>
        <java.version>1.8</java.version>
    </properties>


    <dependencies>

<!--        web依赖-->
<!--        所有springboot的依赖都是使用spring-boot-starter开头的-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

<!--        单元测试依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
<!--            打jar包的插件-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```
 
* 修改项目的端口号，在application.properties中添加如下配置：
  ```properties
  # 更改项目的端口号为8081（默认为8080）
  server.port = 8081
  ```
    
* 修改背景图片：使用在线工具生成banner.txt 放到application.properties的同级目录下：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210315182722.png)

# Springboot自动装配原理

## 配置解析

* `spring-boot-dependencies`:核心依赖，在父工程（`spring-boot-starter-parent`）中;
  * 作用：配置了springboot依赖的版本仓库，使我们在写或者引入springboot依赖的时候不用写版本号；
* `spring-boot-starter`:启动器
```xml
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter</artifactId>
<version>2.4.3</version>
</dependency>
```
  * 配置了SpringBoot的启动场景，比如spring-boot-starter-web就会帮我们导入web环境的所有的依赖。
  * SpringBoot会将所有的**功能场景，都变成一个个的启动器**。
  * 需要使用什么功能，只需要找到对应的启动器。
  * [启动器介绍文档](https://docs.spring.io/spring-boot/docs/2.4.3/reference/html/using-spring-boot.html#using-boot-starter)

## 主程序

* 本例中中主程序是SpringbootApplication(项目名+Application):
```java
package com.zestaken.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;


@SpringBootApplication //标注这个这个类是一个springboot的应用
public class SpringbootApplication {

    public static void main(String[] args) {
        //将SpringBoot应用启动
        SpringApplication.run(SpringbootApplication.class, args);
    }

}
```
* `@SpringBootApplication`注解：这个注解是一个组合注解，其中包含的比较重要的注解如下
  *  `@SpringBootConfiguration`:springboot的配置注解，这个注解也是一个组合注解，包含的比较重要的注解如下：
     *  `@Configuration`：spring的配置注解，这个注解也是一个组合注解，包含的比较重要的注解如下：
        *  `@Component`:spring的组件注解。
     * 从根本来说，这个主程序也是**spring的一个组件**。
* `@EnableAutoConfiguration`:springboot自动配置注解，这个注解也是一个组合注解，包含的比较重要的注解如下：
  * `@AutoConfigurationPackage`:自动配置包注解，这个注解也是一个组合注解，包含的比较重要的注解如下：
    * `@Import({Registrar.class})`自动配置包的注册
  * `@Import({AutoConfigurationImportSelector.class})`:自动配置导入选择器，这个注解也是一个组合注解，包含的比较重要的注解如下：

# 主程序

* 实现的工作：
  1. 推断应用的类型是普通的项目还是web项目；
  2. 查找并加载所有可用的**初始化器**，设置到initializers属性中；
  3. 找出所有的应用程序监听器，设置到listeners属性中；
  4. 推断并设置main方法的定义类，找到运行的主类。

# SpringBoot配置

* SpringBoot使用一个全局的配置文件，配置文件的名称是固定的为`application`,但是可以使用两种格式：
  * `application.properties`:
    * 语法结构：`key = value`
  * `application.yml`:
    * 语法结构：`key : (此处有空格) value`
* 配置文件的作用：修改SpringBoot的自动配置的默认值。

## yaml

* YAML 是 "YAML Ain't a Markup Language"（YAML 不是一种标记语言）的递归缩写。
* YAML 的语法和其他高级语言类似，并且可以简单表达清单、散列表，标量等数据形态。它使用**空白符号缩进**和大量依赖外观的特色，特别适合用来表达或编辑数据结构、各种配置文件、倾印调试内容、文件大纲（例如：许多电子邮件标题格式和YAML非常接近）。
* **YAML 的配置文件后缀为 .yml或者.yaml**，如：`application.yml`或者`application.yaml`，官方推荐使用`.yaml`
* yaml的特点：
  * 大小写敏感
  * 使用缩进表示层级关系 
  * 缩进不允许使用tab，只允许空格
  * 缩进的空格数不重要，只要相同层级的元素左对齐即可
  * `#`表示注释。
* YAML 支持以下几种数据类型：
  * 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
  * 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
  * 纯量（scalars）：单个的、不可再分的值
* 纯量（普通的数据）：
  * `name: zestaken`
* 对象:
  * 空格缩进存对象：
  ```yml
  # 包含name和age属性值的student对象。
  studen:
   name: zestaken
   age: 19
  ```
  * 行内使用花括号：
  ```yml
  # 还是student对象
  student: {name: zestaken, age: 19}
  ```
  * 利用yaml可以存储对象的特点，可以用于给**对象赋值**。
* 数组：
  * 使用空格缩进和`-`:
  ```yml
  # 包含三个元素的pets数组
  pets:
   - cat
   - dog
   - pig
  ```
  * 行内使用中括号：
  ```yml
  pets: [cat, dog, pig]
  ```
###  使用yaml给对象赋值：

* Yaml注入配置文件@ConfigurationProperties
1. 在springboot项目中的resources目录下新建一个文件 application.yml
2. 编写一个实体类 Dog
```java
@Component//注册bean到容器中 
public class Dog {

    private String name;
    private Integer age;
     //有参无参构造、get、set方法、toString()方法 
}
```
`3. 思考，我们原来是如何给bean注入属性值的！ @Value，给狗狗类测试一下：
```java
@Component 
//注册bean 
public class Dog {    
	@Value("阿黄")    
	private String name;    
	@Value("18")    
	private Integer age; 
}
```
4. 在SpringBoot的测试类下注入狗狗输出一下；
```java
@SpringBootTest 
class DemoApplicationTests {
    @Autowired //将狗狗自动注入进来    
    Dog dog;
    @Test    
    public void contextLoads() {        
    System.out.println(dog); //打印看下狗狗对象    
}
```
  * 结果成功输出，@Value注入成功，这是我们原来的办法
5. 我们再编写一个复杂一点的实体类：Person 类
```java
@Component
public class Person {
    private String name;
    private Integer age;
    private Boolean happy;
    private Date birth;
    private Map<String, Object> map;
    private List<Object> list;
    private Dog dog;
```
6. 我们来使用yaml配置的方式进行注入，大家写的时候注意区别和优势，我们编写一个yaml配置
```yml
Person:
  name: zyx${random.uuid} #随机uuid
  age: ${random.int} #随机int
  happy: true
  birth: 1992/10/07
  map: {k1: v1,k2: v2}
  list:
    - 唱歌
    - 跳舞
    - 表演
  dog:
    name: haha
    age: 3
```
7、我们刚才已经把person这个对象的所有值都写好了，我们现在来注入到我们的类中！\
```java
 //@ConfigurationProperties作用： 将配置文件中配置的每一个属性的值，映射到这个组件中；告诉SpringBoot将本类中的所有属性和配置文件中相关的配置进行绑定
//参数 prefix = “person” : 将配置文件中的person下面的所有属性一一对应 
@Component
@ConfigurationProperties(prefix = "person")
public class Person {
    private String name;
    private Integer age;
    private Boolean happy;
    private Date birth;
    private Map<String, Object> map;
    private List<Object> list;
    private Dog dog;
```
8、IDEA 提示，springboot配置注解处理器没有找到，让我们看文档，我们可以查看文档，找到一个依赖
![](https://gitee.com/zhangjie0524/picgo/raw/master/20210317182009.png)
```xml
<!-- 导入配置文件处理器，配置文件进行绑定就会有提示，需要重启 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```
9、确认以上配置都OK之后，我们去测试类中测试一下
```java
@SpringBootTest
class Springboot01PropertyApplicationTests {

    @Autowired
    private Person person;//将person自动注入进来
    @Test
    void contextLoads() {

        System.out.println(person); //打印person信息 
    }

}
```
* 结果：所有值全部注入成功！

## JSR-303校验

* JSR-303 是 JAVA EE 6 中的一项子规范，叫做 Bean Validation。
* Bean Validation 为 JavaBean 验证定义了相应的元数据模型和 API。缺省的元数据是 Java Annotations，通过使用 XML 可以对原有的元数据信息进行覆盖和扩展。在应用程序中，通过使用 Bean Validation 或是你自己定义的 constraint，例如 @NotNull, @Max, @ZipCode， 就可以确保数据模型（JavaBean）的正确性。constraint 可以附加到字段，getter 方法，类或者接口上面。对于一些特定的需求，用户可以很容易的开发定制化的 constraint。Bean Validation 是一个运行时的数据验证框架，在验证之后验证的错误信息会被马上返回。
* Bean Validation 规范内嵌的约束注解：
![](https://gitee.com/zhangjie0524/picgo/raw/master/20210317183152.png)
* SpringBoot使用：
  1. 引入依赖
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

   2. 给参数对象添加校验注解
```java
@Data
public class User {
    
    private Integer id;
    @NotBlank(message = "用户名不能为空")
    private String username;
    @Pattern(regexp = "^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{8,16}$", message = "密码必须为8~16个字母和数字组合")
    private String password;
    @Email
    private String email;
    private Integer gender;

}
```
   3. Controller 中需要校验的参数Bean前添加 @Valid 开启校验功能，紧跟在校验的Bean后添加一个BindingResult，BindingResult封装了前面Bean的校验结果。
```java
@RestController
@RequestMapping("/user")
public class UserController {

    @PostMapping("")
    public Result save (@Valid User user , BindingResult bindingResult)  {
        if (bindingResult.hasErrors()) {
            Map<String , String> map = new HashMap<>();
            bindingResult.getFieldErrors().forEach( (item) -> {
                String message = item.getDefaultMessage();
                String field = item.getField();
                map.put( field , message );
            } );
            return Result.build( 400 , "非法参数 !" , map);
        }
        return Result.ok();
    }
}
```

