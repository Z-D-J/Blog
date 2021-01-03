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
## urlparttern的配置

* 一个Servlet可以定义多个访问路径，`@WebServlet({"/d4"."/dd4"})`,如果只有一个路径，则大括号可以省略。
* 路径的定义规则：
  1. `/xxx`;
  2. `/xxx/xxx`:多层路径，目录结构(不止可以写两层，可以写更多层)
  3. `*.xxx`:不管.之前写的是什么，只要最后的后缀一样即可访问。一般是`*.do`形式。
* 通配符`*`:`*`所占的位置输入任何名字都可以，但是优先级很低（即如果有那个名字的资源，则访问那个资源）。

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

# JAVAWEB的目录结构

![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009104107.png)

* bbs目录代表一个web应用
* bbs目录下的html,jsp文件可以直接被浏览器访问
* WEB-INF目录下的资源是**不能直接被浏览器访问**的
* `web.xml`文件是web程序的**主要配置文件**。
* 所有的**classes**文件都放在classes目录下
* **jar文件**放在lib目录下。

# Request对象和Resoponse对象

## 服务器与客户端交互流程

1. tomcat服务器会根据请求url中的资源路径创建对应的**实现Servlet的类的对象**;
2. tomcat**服务器**会创建**request**和**response**对象，request对象中封装请求的消息数据;
3. tomcat将request和response对象传递给**service**方法，并且调用service方法;
4. 程序员通过request对象**获取请求的消息数据**，通过response对象**设置响应的消息数据;
5. 服务器在给浏览器做出响应之前会从**response对象**中拿程序员设置的响应消息数据。

## Request对象

* 原理：
  * request对象和reponse对象是由服务器创建的;
  * request对象获取请求消息，response对象设置响应消息。
* request对象的继承体系结构：
  1. ServletRequest:最上层接口;
  2. HttpServletRequest:继承自ServletRequest的接口;
  3. org.apache.catalina.connector.RequestFacade：tomcat实现的实现了HttpServlet接口的类。
## request功能：

### 获取请求消息数据

1. 获取请求行数据：（get方式就放在doget方法中，POST方法则放在dopost方法中）
  1. **获取虚拟目录**：`/tomcat3_war_exploded`
   1. `String getContextPath();`
 1. **获取请求的URI或URL**:
      1. `String getRequestURI();`:获取URI，如：`/tomcat3_war_exploded/ServletDemo3`
      2. `String getRequestURL();`获取URL，如：`http://localhost:8080/tomcat3_war_exploded/ServletDemo3`
      3. URI和URL都是**统一资源定位符**,但是URI表示的范围比URL大。
 2. 获取Servlet路径：`/ServletDemo3`
      1. `String getServletPath();`
 3. 获取get方式请求参数：
    1. `String getQueryString();`,如：`name=%22zhangsan%22&age=13`
2. 获取请求头数据：
   1. `String getHeader(String name)`:通过请求头的名称获取请求头的数据;
   2. `Enumeration<String> getHeaderName()`:获取所有的请求头数据;
3. 获取请求体数据：
   1. 请求体：只有POST方式才有。
   2. 步骤：
      1. 获取流对象：
         1. `BufferedReader getReader();`获取字符输入流，只能操作字符数据;
         2. `ServletInputStream getInputStream()`:获取字节输入流，可以操作所有类型的数据；
      2. 从流对象中将数据拿出来

### 获取请求参数的通用方式

* 不论是get还是post方式都可以使用。（如果doget和dopost的代码完全一样的话，在doget里写`this.doPost()`即可)
1. **根据参数名称来获取参数值**:`String getParameter(String name)`，如果一个参数有多个值的话，则无法获取完。
2. 根据参数名称来获取参数值的数组：`String[] getParameterValues(String name)`;
3. 获取所有请求的参数名称：`Enumeration<String> getParameterNames()`;
4. **获取所有参数的Map集合**：`Map<String, String[]> getParameterMap()`。





