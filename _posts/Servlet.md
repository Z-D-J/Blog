---
title: Servlet
date: 2020-10-10 07:40:40
tags:
---

# servlet简介

* Servlet：即Server Applet。
* Servlet其实就是一个遵循Servlet开发的**java类**。Servlet是由**服务器调用的，运行在服务器端**。Servlet**没有main方法**，它的创建、使用、销毁都由Servlet容器(即web服务器）进行管理（如Tomcat：提供了Servlet功能的服务器称作Servlet容器）。即虽然没有main方法，但是通过Servlet容器可以自动调用。
* servelet用来实现对服务器的动态资源的控制。
* servelet就是一个**接口**，定义了java类被浏览器访问的规则。
* 我们需要自定义一个类，这个类**实现servelet接口，复写其方法**。
* Servlet带给我们最大的作用就是能够**处理浏览器带来HTTP请求**，并**返回一个响应**给浏览器，从而实现**浏览器和服务器的交互**。servlet是作用于服务器这一端。
# 快速入门

## IDEA上配置tomcat

* 使用的ide是IDEA，需要先在IDEA上配置Tomcat。(需要IDEA的utilmate版).
  1. 点击Run---EDit Configurations...
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201010165243.jpg)
  2.点击左侧“+”号，找到Tomcat Server---Local。
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201010165641.jpg)
  3.找到tomcat存放位置并配置到idea中：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201010165926.jpg)
* IDEA会为每一个tomcat部署的项目单独建立一份配置文件
  * 查看控制台的log找到这个配置文件的存储位置：`CATALINA_BASE:     /home/zestaken/.cache/JetBrains/IntelliJIdea2020.2/tomcat/Tomcat_9_0_411_tomcat3`
* WEB-INF目录下的资源不能被浏览器直接访问。

## 编写servlet程序的步骤

1. 创建**javaEE**项目
2. 定义一个类，实现Servlet接口：`public class ServletDemo1 implements Servlet`
3. 实现接口中的抽象方法
4. 配置servlet，在web.xml中
```xml
<!-- 配置Servlet -->
<servlet>
        <servlet-name>demo1</servlet-name>
        <servlet-class>web.ServletDemo1</servlet-class>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>demo1</servlet-name>
        <url-pattern>/demo1</url-pattern>
    </servlet-mapping>
```

# 执行原理/解析过程

1. 当服务器接受到浏览器的请求后，会解析URL路径，获取访问的**Servlet**的资源路径。
2. 查找web.xml文件，是否有对应的`<url-pattern>`标签内容。
3. 如果有，则再找到对应的`<servlet-class>`全类名。
4. tomcat会将字节码文件加载进内存，并且创建其对象。
5. 调用其方法。

# 生命周期

* 方法
```java
import javax.servlet.*;
import java.io.IOException;

public class ServletDemo1 implements Servlet {
    /**
     * 初始化方法
     * 在servlet被创建时执行，只会执行一次
     * @param servletConfig
     * @throws ServletException
     */
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("init");
    }

    /**
     * 获取ServletConfig对象
     * ServletConfig：Servlet的配置对象
     * @return
     */
    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    /**
     * 提供服务的方法
     * 每一次Servlet被访问时，执行，可以执行多次（每刷新一次页面都会执行一次）
     * @param servletRequest
     * @param servletResponse
     * @throws ServletException
     * @throws IOException
     */
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("service");
    }

    /**
     * 获取Servlet的一些信息，版本，作者等。
     * @return
     */
    @Override
    public String getServletInfo() {
        return null;
    }

    /**
     * 销毁方法
     * 在服务器正常关闭时执行一次。
     */
    @Override
    public void destroy() {
        System.out.println("destroy");
    }
}
```

* 生命周期
  1. 被创建：执行init方法，只执行一次,一般用于**加载资源**.
     1. Servlet被创建的时间
        1. 默认情况下，第一次被访问时（即在浏览器中访问该页面时），Servlet被创建
        2. 可以在web.xml配置执行Servlet的创建时间：
            * 在`<servlet>`标签下配置
              1. 第一次被访问时创建:`<load-on-startup>`的值为负数
              2. 在服务器启动时创建：`<load-on-startup>`的值为0或者正数。
     2. Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例的
        1. 多个用户同时访问时，可能存在线程安全问题。
        2. 解决：尽量不再在Servlet中定义成员变量，即使定义了，也不要修改它。
  2. 提供服务：执行service方法，可执行多次
     1. 每次被访问Servlet时，Service方法都会被调用一次。
  3. 被销毁：执行destroy方法，只执行一次
     1. Servlet被销毁时执行。
     2. 服务器关闭时，Servlet被销毁
     3. 只有服务器正常关闭时，才会执行destroy方法
     4. destroy方法在Servlet被销毁之前执行，一般用于**释放资源**。

# 注解配置

* Servlet3.0之后，**支持注解配置，可以不用写web.xml了。
* 步骤：
  1. 创建JavaEE项目，选择Servlet的版本3.0以上，**可以不创建web.xml**(也可以创建，因为注解配置会覆盖web.xml的配置)
  2. 定义一个类，实现Servlet接口;
  3. 复写方法;
  4. 在类上使用`@WebServlet`注解，进行配置：
     1. `@WebServlet(loadOnStartup="资源路径名")`与`@WebServlet(value="资源路径名")`与`@WebServlet("资源路径名")`等效。
* `@WebServlet`注解的具体内容：
```java
package javax.servlet.annotation;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface WebServlet {
    String name() default "";

    String[] value() default {};

    String[] urlPatterns() default {};

    int loadOnStartup() default -1;

    WebInitParam[] initParams() default {};

    boolean asyncSupported() default false;

    String smallIcon() default "";

    String largeIcon() default "";

    String description() default "";

    String displayName() default "";
}
```

# Servlet的体系结构

* Servlet接口：最上层。
* GenericServlet:实现了Servlet接口的**抽象类**,处于第二层。
  * 将Servlet接口中的其他的方法都做了默认空实现，只将service()方法作为抽象。
  * 将来定义Servlet的类时，可以继承GenericServlet，实现**service()方法即可**。（但是不常用）
* HttpServlet：继承自GenricServlet的**抽象类**,处于第三层。
  * 所有方法都没有要求实现。
  * 对http协议的一种封装，简化操作。
  * 使用：
    * 定义类继承HttpServlet
    * 复写doGet()/doPost()等方法。

# HTTP协议

## HTTP协议的概念

* 超文本传输协议（HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准。它是TCP/IP协议的一个应用层协议简单来说，HTTP协议就是客户端和服务器交互的一种通迅的格式。

## HTTP1.0和HTTP1.1

* HTTP1.0协议中，客户端与web服务器建立连接后，只能获得**一个web资源**【短连接，获取资源后就断开连接】
* HTTP1.1协议，允许客户端与web服务器建立连接后，在一个连接上获取**多个web资源**【保持连接】

## HTTP请求

* 浏览器向服务器请求某个web资源时，称之为浏览器向服务器发送了一个http请求。一个完整http请求应该包含三个部分：
  1.  请求行【描述客户端的请求方式、请求的资源名称，以及使用的HTTP协议版本号】
  2. 多个消息头【描述客户端请求哪台主机，以及客户端的一些环境信息等】
  3. 一个空行

### 请求行

* 请求行：`GET /java.html HTTP/1.1`。请求行中的GET称之为请求方式，之后跟请求的路径，最后是请求协议版本。请求方式有：POST,GET,HEAD,OPTIONS,DELETE,TRACE,PUT。
* 常用的请求方式有：POST,GET
  * 一般来说，当我们点击超链接，通过地址栏访问都是get请求方式。通过表单提交的数据一般是post方式。
  * 可以简单理解GET方式用来**查询数据**,POST方式用来**提交数据**，get的提交速度比post**快**。
  * GET方式：在URL地址后附带的参数是有限制的，其**数据容量通常不能超过1K**。
  * POST方式：可以在请求的实体内容中向服务器**发送数据，传送的数据量无限制**。

### 请求头

* Accept: text/html,image/* 【浏览器告诉服务器，它支持的数据类型】
* Accept-Charset: ISO-8859-1 【浏览器告诉服务器，它支持哪种字符集】
* Accept-Encoding: gzip,compress 【浏览器告诉服务器，它支持的压缩格式】
* Accept-Language: en-us,zh-cn 【浏览器告诉服务器，它的语言环境】
* Host: www.it315.org:80【浏览器告诉服务器，它想访问哪台主机】
* If-Modified-Since: Tue, 11 Jul 2000 18:23:51 GMT【浏览器告诉服务器，缓存数据的时间】
* Referer: http://www.it315.org/index.jsp【浏览器告诉服务器，客户机是从那个页面来的---反盗链】
* 8.User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)【浏览器告诉服务器，浏览器的内核是什么】
* Cookie【浏览器告诉服务器，带来的Cookie是什么】
* Connection: close/Keep-Alive 【浏览器告诉服务器，请求完后是断开链接还是保持链接】
* Date: Tue, 11 Jul 2000 18:23:51 GMT【浏览器告诉服务器，请求的时间】

## HTTP响应

* 一个HTTP响应代表着服务器向浏览器回送数据。一个完整的HTTP响应应该包含四个部分:
  1. 一个状态行【用于描述服务器对请求的处理结果。】
  2. 多个消息头【用于描述服务器的基本信息，以及数据的描述，服务器通过这些数据的描述信息，可以通知客户端如何处理等一会儿它回送的数据】
  3. 一个空行
  4. 实体内容【服务器向客户端回送的数据】

### 状态行

* 格式： HTTP版本号　状态码　原因叙述
* 状态行：HTTP/1.1 200 OK
* 状态码用于表示服务器对请求的处理结果，它是一个三位的十进制数。响应状态码分为5类:
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201010121055.png)

### 响应头

* Location: http://www.it315.org/index.jsp 【服务器告诉浏览器要跳转到哪个页面】
* Server:apache tomcat【服务器告诉浏览器，服务器的型号是什么】
* Content-Encoding: gzip 【服务器告诉浏览器数据压缩的格式】
* Content-Length: 80 【服务器告诉浏览器回送数据的长度】
* Content-Language: zh-cn 【服务器告诉浏览器，服务器的语言环境】
* Content-Type: text/html; charset=GB2312 【服务器告诉浏览器，回送数据的类型】
* Last-Modified: Tue, 11 Jul 2000 18:23:51 GMT【服务器告诉浏览器该资源上次更新时间】
* Refresh: 1;url=http://www.it315.org【服务器告诉浏览器要定时刷新】
* Content-Disposition: attachment; filename=aaa.zip【服务器告诉浏览器以下载方式打开数据】
* Transfer-Encoding: chunked 【服务器告诉浏览器数据以分块方式回送】
* Set-Cookie:SS=Q0=5Lb_nQ; path=/search【服务器告诉浏览器要保存Cookie】
* Expires: -1【服务器告诉浏览器不要设置缓存】
* Cache-Control: no-cache 【服务器告诉浏览器不要设置缓存】
* Pragma: no-cache 【服务器告诉浏览器不要设置缓存】
* Connection: close/Keep-Alive 【服务器告诉浏览器连接方式】
* Date: Tue, 11 Jul 2000 18:23:51 GMT【服务器告诉浏览器回送数据的时间】



# JAVAWEB的目录结构

![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009104107.png)

* bbs目录代表一个web应用
* bbs目录下的html,jsp文件可以直接被浏览器访问
* WEB-INF目录下的资源是**不能直接被浏览器访问**的
* `web.xml`文件是web程序的**主要配置文件**。
* 所有的**classes**文件都放在classes目录下
* **jar文件**放在lib目录下。





