---
title: Filter
date: 2021-01-20 21:48:09
tags:
---
# Filter概述

* web中的过滤器：当访问服务器的资源时，过滤器可以将每次请求拦截下来，完成一些特殊的功能;
* 作用：
  * 一般用于完成**通用的操作**,如：登录验证，统一编码处理，敏感字符过滤。

# Filter快速入门

* 步骤：
  1. 定义一个类，实现接口Filter,注意这个Filter接口是java.servlet包下的（因为java.util包下也有Filter接口）;
  2. 复写方法，（主要起作用的方法是doFilter)
  3. 配置拦截路径：
     1. 在web.xml文件中去配置;
     2. 用注解`@WebFilter`注解，如：`@WebFilter("/demo1")`代表访问/demo1目录下的资源的时候执行拦截。
* 示例：
```java

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;

@WebFilter("/*")
public class FilterDemo1 implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("I'm Filter!");

        chain.doFilter(request, response);
    }

    @Override
    public void destroy() {
        
    }
}
```

# web.xml配置方式

* 配置filter;
* 配置filter的拦截路径。
* 示例：
```xml
<filter>
    <filter-name>过滤器的名字</filter-name>
    <filter-class>过滤器的完全限定类名</filter-class>
</filter>

<filter-mapping>
    <filter-name>过滤器的名字</filter-name>
    <url-pattern>拦截的路径</url-pattern>
</filer-mapping>
```