---
title: SpringMVC
date: 2021-03-04 09:35:32
tags:
---

# SpringMVC简介

[官方文档](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#spring-web)
* SpringMVC是一个web框架，围绕`DispatcherServlet`设计；
* DispacherServelt的作用是将请求分发到不同的处理器。
  * DispatcherServlet是一个实际的Servlet，它继承自HttpServlet类。
* SpringMVC和许多其他的MVC框架一样，以请求为驱动，围绕一个中心servlet分派请求及提供其他功能。
* 传统MVC架构：
  ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210307210022.png)

# SpringMVC执行原理

* SpringMVC核心架构：
  ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210307210107.png)

# 快速入门

1. 建立一个web支持的项目；
2. 配置maven的资源过滤问题：
```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```
3. 导入相关依赖，主要是`spring-webmvc`
```xml
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.3</version>
    </dependency>
```
4. 配置web.xml
   * web.xml的版本要4.0及以上；
   * 在项目结构中，将maven导入的依赖，全部导入到artifacts的依赖中去。
   * 注册DispatchServlet,管理SpringMVC配置文件，设置启动级别为1，映射路径为`/`
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">

        <!-- 注册servlet -->
        <servlet>
            <servlet-name>SpringMVC</servlet-name>
            <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>、
            <!-- 通过初始化参数指定SpringMVC配置文件的位置，进行关联 -->
            <init-param>
                <param-name>contextConfigLocation</param-name>
                <param-value>classpath:springmvc-servlet.xml</param-value>
            </init-param>
            <!-- 启动顺序，数字越小，启动越早 -->
            <load-on-startup>1</load-on-startup>
        </servlet>

        <!-- 所有请求都会被springmvc拦截 -->
        <servlet-mapping>
            <servlet-name>SpringMVC</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
    </web-app>
  ```
5. 配置Springmvc-servlet.xml(web.xml关联的springmvc配置文件，放在resouce目录下)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
            https://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">


    <context:annotation-config/>
    <!--    自动扫描包，让指定包下的注解生效，由IOC容器统一管理-->
    <context:component-scan base-package="com.zestaken.controller"/>
    <!--    让springmvc不处理静态资源，如.css .js .html .mp3 .mp4-->
        <mvc:default-servlet-handler/>

    <!--    支持mvc注解驱动-->
        <mvc:annotation-driven/>

    <!--    配置视图解析器-->
        <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
            id="internalResourceViewResolver">
    <!--        前缀-->
            <property name="prefix" value="/WEB-INF/jsp/"/>
    <!--        后缀-->
            <property name="suffix" value=".jsp"/>
        </bean>
</beans>
```
   * 在视图解析器中，将所有的视图都放在**/WEB-INF/**目录下，这样可以保证视图安全，因为这个目录下的文件，客户端不能直接访问。
6. 创建controller：
```java
package com.zestaken.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/HelloController")
public class HelloController {
    
    //真实访问地址就是：项目名/HelloController/hello1
    @RequestMapping("/hello1")
    public String sayHello(Model model) {
        //向模型中添加属性msg与值，可以在jsp页面中取出并渲染
        model.addAttribute("msg", "hello, springmvc");
        //返回值代表视图：WEB-INF/jsp/hello.jsp
        return "hello";
    }
}
```
   * `@Controller`是为了让Spring IOC容器自动扫描到；
   * `@ResquestMapping`是为了映射请求路径，这里因为类与方法上都有映射，所以访问时应该是`HelloController/hello`(类上的映射可以不写)
   * 方法中声明的Model类型的参数是为了把Action中的数据带到视图层中；
   * 方法返回的结果是视图的名称hello，加上==配置文件中的前后缀==变成WEB-INF/jsp/hello.jsp
7. 创建视图层：
   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
    <h1>${msg}</h1>
    </body>
    </html>
   ```
8. 启动tomcat，访问/HelloController/hello1。
   ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210307221352.png)

