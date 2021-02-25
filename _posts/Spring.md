---
title: Spring
date: 2021-02-10 08:30:49
tags:
---
# Spring简介

* 历史：
  1. 2002年，首次推出Spring框架的雏形：interface21框架
  2. 2004年3月24日，基于interface21框架，发布了Spring框架的1.0版本（本次学习使用的是Spring5）
  3. Spring Framework的创始人：Rod Johnson
* Spring理念：使现有技术更加容易使用，本身整合了现有的很多技术框架。
* SSH:struct2+Spring+Hibernate
* SSM:SpringMVC+Spring+Mybatis
* [官方文档](https://spring.io/projects/spring-framework)
* [官网下载地址](https://repo.spring.io/realse/org/springframework/spring)
* [github地址](https://github.com/spring-projects/spring-framework)
* maven坐标：
```xml
<!-- 安装这个包，会自动添加其它依赖的包-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.3</version>
</dependency>

<!-- 和mybatis整合需要的包 -->
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.3</version>
</dependency>
```
* Spring优点：
  1.  是一个开源的免费的框架；
  2.  轻量级，非入侵式框架；
  3.  **控制反转（IOC）**
  4.  **面向切面编程（AOP）**
  5.  支持事务的处理
  6. 支持框架整合
* 缺点：配置繁琐

* Spring的组成：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210210093918.jpg)

* Spring的拓展：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210210094952.jpg)
  * SpringBoot：
    * 一个快速开发的脚手架；
    * 基于SpringBoot可以快速开发单个的微服务；
    * 约定大于配置
  * SpringCloud:
    * SpringClod是基于SpringBoot实现的。
  * 学习SpringBoot的前提是Spring及SpringMVC

# IOC

## IOC原型

* 普通接口实现：
```java
package com.zestaken.service;

import com.zestaken.dao.UserDao;
import com.zestaken.dao.UserDaoImpl;

//在service层调用Dao层的方法进行业务操作
public class UserServiceImpl implements UserService{
    //直接在编写程序时写好UserDao属性
    private UserDao userDao = new UserDaoImpl();

    @Override
    public void getUsers() {
        userDao.getUsers();
    }
}
```
* IOC注入思想实现：
```java
package com.zestaken.service;

import com.zestaken.dao.UserDao;

public class UserServiceImpl implements UserService{
    //编写程序将UserDao对象设置为从外界获取注入的值，而不是直接由程序员设置
    private UserDao userDao;

    //注入UserDao的值
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void getUsers() {
        userDao.getUsers();
    }
}
```
* 用普通的方法实现，每一次新增UserDao接口的实现类，都需要修改UserService实现类的代码。
* 普通实现方法:程序是**主动创建对象**，控制权在程序员的手上。
* IOC思想实现：使用set注入后，程序**不再具有主动性**，而是被动接受传递的对象。
* 优点：程序员不用再去管理对象的创建了，系统的耦合性大大降低。

## IOC本质

* 控制反转（Inversion Of Control），是一种设计思想，DI（Dependency Injection，依赖注入）是实现IOC的一种方式。
* 未使用IOC思想的面向对象编程中，对象的创建和对象间的依赖关系，完全硬编码在程序中，**对象的创建由程序自己控制**，使用IOC思想后，**对象的创建转移给第三方**，控制反转即**获得依赖对象的方式反转了**。
* 控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式；
* 在Spring中实现IOC的是**IOC容器**，其**实现方法是DI（依赖注入）**。
  
## Spring的IOC实现

1. 书写接口实现类：
```java
//Dao层实现
package com.zestaken.dao;

public class UserDaoImpl implements UserDao{
    @Override
    public void getUsers() {
        System.out.println("sql查询");
    }
}
//Service层实现
package com.zestaken.service;

import com.zestaken.dao.UserDao;

public class UserServiceImpl implements UserService{
    private UserDao userDao ;

    //注入UserDao的值
    //使用Spring管理的类的属性，必须由set方法设定
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void getUsers() {
        userDao.getUsers();
    }
}
```
2. 将实现类用xml的方式交给Spring管理
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

<!--    在Spring中使用bean来创建对象，-->
<!--    id是该类生成的对象名，class是完全限定类名-->
    <bean id="userDaoImpl" class="com.zestaken.dao.UserDaoImpl"/>
    <bean id="userServiceImpl" class="com.zestaken.service.UserServiceImpl">
<!--        name指定需要赋值的属性 ref指定传递的对象-->
        <property name="userDao" ref="userDaoImpl"/>
    </bean>

</beans>
```
3. 测试：
```java
package com.zestaken.service;

import org.junit.jupiter.api.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ServiceTest {
    @Test
    public void userServiceImplTest(){
        //获取Spring的上下文对象,参数是配置文件名
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //现在所有的对象都交由Spring管理了，要想使用对象，只需要从Spring中取出即可（Spring中这些对象叫做bean）
        UserServiceImpl userServiceImpl = (UserServiceImpl) context.getBean("userServiceImpl");
        //获取出对象之后，即可正常使用
        userServiceImpl.getUsers();
    }
}
```
* 控制：传统的程序的对象是由程序本身控制创建的，使用Spring的对象是由Spring来创建的；
* 反转：程序本身不创建对象，而变成**被动的接收对象**。
* IOC即对象由Spring来创建，管理和装配。我们只需要修改相应的配置文件，例如此处由xml文件配置，则修改xml文件即可修改程序实现。

## Spring中IOC创建对象的方式

1. 通过类的无参构造方法类构造对象，默认使用这种。
2. 使用有参的构造方法构造：
    1. 下标赋值：
    ```xml
    <bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg index="0" value="7500000"/>
    <constructor-arg index="1" value="42"/>
    </bean>
    ```
   2. 类型赋值：
   ```xml
   <bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg type="int" value="7500000"/>
    <constructor-arg type="java.lang.String" value="42"/>
   </bean>
   ```
   3. 参数名赋值(常用)：
   ```xml
   <bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg name="years" value="7500000"/>
    <constructor-arg name="ultimateAnswer" value="42"/>
   </bean>
   ```

# Spring配置

## alias(别名)

* 如果配置了别名，我们也可以使用别名来获取到这个对象：
```xml
    <alias name="userDaoImpl" alias="userDaoImpl2"/>
```
## Bean配置

* id:bean的唯一标识符，相当于对象名；
* class：bean对象所对应的类的完全限定类名
* name：也是别名，而且那么可以同时取多个别名，并且别名之间可以用空格，`,`,`;`等来分隔
* 示例：
```xml
 <bean id="userDaoImpl" class="com.zestaken.dao.UserDaoImpl" name="zhangjie lisi,zestaken;zhangsan"/>
```

## import配置

* 一般用于团队开发使用，可以将多个配置文件导入到一个配置文件从而合并为一个配置文件:
```xml
<import resource="bean1.xml"/>
<import resource="bean2.xml"/>
<import resource="bean3.xml"/>
```

# 依赖注入(DI)

## 一：构造器注入

* 构造器注入即有参数的构造方法来构造对象，在构造时将对象属性初始化。
* 三种方式：
    1. 下标赋值：
    ```xml
    <bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg index="0" value="7500000"/>
    <constructor-arg index="1" value="42"/>
    </bean>
    ```
   2. 类型赋值：
   ```xml
   <bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg type="int" value="7500000"/>
    <constructor-arg type="java.lang.String" value="42"/>
   </bean>
   ```
   3. 参数名赋值(常用)：
   ```xml
   <bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg name="years" value="7500000"/>
    <constructor-arg name="ultimateAnswer" value="42"/>
   </bean>
   ```

## 二:setter方法注入

* 依赖：bean对象的创建依赖于容器；
* 注入:bean对象中的所有属性由容器来注入。
* 使用这种方式注入的属性，必须全部使用setter方法来设置属性。
* 不同类型的属性的注入方式不同：
  1. 基本类型以及String类型的注入：通过`value`来实现
    ```xml
    <property name="name" value="zhangjie"/>
    ```
   2. bean类型注入（即属性类型是类类型，且这个类的实现对象必须在Spring中注册）：使用`ref`:
   ```xml
   <bean id="address" class="com.zestaken.pojo.Address"/>
   <bean id="person" class="com.zestaken.pojo.Person">
        <property name="address" ref="address"/>
   </bean>
   ```
   3. 数组，list集合 map集合,set集合类型的注入，需要使用专门的标签：
   ```xml
       <!-- 数组 -->
           <property name="books">
            <array>
                <value>红楼梦</value>
                <value>西游记</value>
            </array>
        </property>
        <!--list集合  -->
        <property name="hobbys">
            <list>
                <value>写代码</value>
                <value>看书</value>
            </list>
        </property>
        <!--map集合  -->
        <property name="card">
            <map>
                <entry key="身份证" value="123435"/>
                <entry key="银行卡" value="2340273"/>
            </map>
        </property>
    <!--set集合  -->
        <property name="games">
            <set>
                <value>lol</value>
                <value>csgo</value>
                <value>overwatch</value>
            </set>
        </property>
    ```
    4. Properties类型的注入：
    ```xml
        <property name="properties">
            <props>
                <prop key="username">zhangjie</prop>
                <prop key="password">12435325</prop>
            </props>
        </property>
    ```
    5. 赋值为null的注入：
    ```xml
        <property name="girlfriend">
            <null/>
        </property>
    ```

## 三：c命名空间注入

* 对应构造器注入的方式，c命名空间相当于constructor-arg标签，所以必须有有参数的构造方法才能使用这种方式。
* 使用c命名空间，必须先导入对应的xml约束：
```xml
 xmlns:c="http://www.springframework.org/schema/c"
```
* 示例；
```xml
 <!-- c-namespace declaration with argument names -->
    <bean id="beanOne" class="x.y.ThingOne" c:thingTwo-ref="beanTwo"
        c:thingThree-ref="beanThree" c:email="something@somewhere.com"/>
```

## 四：p命名空间注入

* 对应setter的注入方式，p命名空间相当于property标签，所以必须有setter方法才能使用这种方法。
* 使用p命名空间，也必须先导入相应的xml约束：
```xml
xmlns:p="http://www.springframework.org/schema/p"
```
* 示例：
```xml
    <bean name="p-namespace" class="com.example.ExampleBean"
        p:email="someone@somewhere.com"/>
```

# Bean的作用域

1. 单例模式:从一个bean中无论获取多少次获取的都是同一个对象。
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210220100546.jpg)
    * 单例模式是bean的默认作用域，也可以显式设置：
    ```xml
    <bean id="accountService" class="com.something.DefaultAccountService"/>

    <!-- the following is equivalent, though redundant (singleton scope is the default) -->
    <bean id="accountService" class="com.something.DefaultAccountService" scope="singleton"/>
    ```
2. 原型模式：每次从bean中获取的对象都是新的对象。
   ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210220100858.jpg)
   * 设置原型模式：
    ```xml
    <bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
    ```
3. Request
4. Session
5. Application
6. WebSocket （后面的四个都是在web开发中使用的）

# Bean的自动装配

* 自动装配：Spring会在上下文中自动寻找，并**自动给bean装配属性**。
* Spring中的三种装配方式：
  1. 在xml中显式的配置
  2. 在java中显式的配置
  3. 隐式的自动装配bean
* 自动装配的两种方式：
  1. byName：会自动在容器上下文中寻找id属性值和自己对象的set方法后面的名称相同的bean。
     1. 使用byName需要保证所有bean的id唯一，并且这个bean的id值需要和自动注入的属性的对应的set方法值一致。
     2. 示例：
   ```xml
       <bean id="userServiceImpl" class="com.zestaken.service.UserServiceImpl" autowire="byName">
        <!--        name指定需要赋值的属性 ref指定传递的对象-->
        <!--        <property name="userDao" ref="userDaoImpl"/> -->
       </bean>
    ```
  2. byType:会自动在容器上下文中寻找和自己对象的类型相同的bean。
    1. 使用byType需要保证所有bean的class唯一，并且这个bean需要和自动注入的属性的类型一致。
    2. 示例：
    ```xml
        <bean id="userServiceImpl" class="com.zestaken.service.UserServiceImpl" autowire="byType">
        <!--        name指定需要赋值的属性 ref指定传递的对象-->
        <!--        <property name="userDao" ref="userDaoImpl"/> -->
        </bean>
    ```

# Spring注解开发

* **开启注解**：
    * 扫描包中的注解：如扫描`@Component`注解`<context:component-scan base-package="com.zestaken"/>`
    * 配置注解的支持：`<context:annotation-config/>`
* xml与注解优缺点：
    * xml更加万能，维护更加方便；
    * 注解需要能够修改类中的代码，维护相对困难；
* xml与注解配合使用：
    * xml用来管理bean；
    * 注解只负责属性注入，即`@Value`。

## 注解注册bean

* `@Component`注解：
    * 组件注解，==放在类上==,说明这个类被Spring管理了，即==注册lbean==；
    * 自动注入的bean对象名是==类名的首字母小写==形成的。
    * 等价于`<bean id="userDaoImpl" class="com.zestaken.dao.UserDaoImpl" />`
* `@Component`为mvc模式形成的衍生注解,这些==注解功能完全相同==，只是为了更好的区分架构层而使用：
    * dao层:`@Repository`
    * service层：`@Service`
    * controller层：`@Controller`

## 注解注入属性

* `@Value("属性值")`注解：
    * 在基本类型以及字符串类型对象上使用，为创建的对象的的对应属性赋值。
    * 等价于`<property name="name" value="zestaken"/>`

## 注解配置作用域

* `@Scope("作用域")`注解：
    * 用于配置bean对象的作用域，如：`@Scope("prototype")`
 
## 注解实现自动装配

* 注解使用配置：
    1. 导入约束：
        * `xmlns:context="http://www.springframework.org/schema/context"`
        * ` http://www.springframework.org/schema/context`
        * `https://www.springframework.org/schema/context/spring-context.xsd"`
    2.配置注解的支持：`<context:annotation-config/>`
    3. 示例：
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            https://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            https://www.springframework.org/schema/context/spring-context.xsd">

        <context:annotation-config/>

    </beans>
    ```
* `@Autowired`注解：
    * 使用该注解在类中需要导入包:`import org.springframework.beans.factory.annotation.Autowired;`
        * 这个包需要在maven中配置导入。
    * 直接在==属性==上使用即可，也可以在set方法上使用。
    * 使用这个注解，可以==不用编写属性对应的set方法==。前提是要被装配的属性在Spring容器中存在。
    * 配置注解`@Autowired(required = false)`可以使属性可以为空，默认不能。与注解`@Nullable`作用相同。
    * `@Autowird`注解：会自动根据该属性的==类型或者名字==来自动装配;
        * 可以配合使用`@Qualifier(value = "属性名")`来限定根据bean id的名字来装配。
    * 示例：
    ```java
    package com.zestaken.service;

    import com.zestaken.dao.UserDao;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.beans.factory.annotation.Qualifier;

    public class UserServiceImpl implements UserService{
        @Autowired
        @Qualifier(value = "userDaoImpl")
        private UserDao userDao ;

        //注入UserDao的值
        //使用Spring管理的类的属性，必须由set方法设定
        public void setUserDao(UserDao userDao) {
            this.userDao = userDao;
        }

        @Override
        public void getUsers() {
            userDao.getUsers();
        }
    }
    ```
* `@Resource`注解：
    * `@Resource`注解是java==原生==的，无需导入包；
    * `@Resource`相当于拥有`@Autowired`和`@Qualifier`两个注解的功能。
    * 直接使用该注解，和`@Autowired`一样；
    * 该注解可以设置参数，限定查找的bean id属性名，如：`@Resource(name = "userDaoImpl")`.




