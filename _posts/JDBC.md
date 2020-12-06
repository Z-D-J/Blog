---
layout: w
title: JDBC
date: 2020-11-25 17:17:57
tags:
---

# JDBC概念

* JDBC是java database connectivity的缩写。是使用java语言来操作数据库。JDBC实现了使用统一的java代码来操作所有关系型数据库。
* JDBC是sun公司定义的操作所有关系型数据库的规则，即定义了一套接口。
* 每一个数据库厂商实现JDBC接口来操作自己的数据库。这些实现类的jar包就叫做**数据库驱动**。
* MySQL 8.0 以上版本的数据库连接有所不同：
  1. MySQL 8.0 以上版本驱动包版本 mysql-connector-java-8.0.16.jar。
  2. `com.mysql.jdbc.Driver` 更换为 `com.mysql.cj.jdbc.Driver`

# JDBC基本使用

## 1.导入驱动jar包到项目目录下

1. mysql的jar包下载:[官网](https://dev.mysql.com/downloads/connector/);下载时选择platformIndependent，选择5.xx的版本
2. 复制jar包到项目的libs目录下（也可以直接导入），右键->add as library
## 2. 注册驱动

* `  Class.forName("com.mysql.jdbc.Driver");`,会产生ClsaaNotFoundException的异常。

## 3. 获取数据库的连接对象

* `Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/youth_study", "root","root");`
  * 参数依次为连接地址，用户名，密码。
  * 连接地址中，后面是主机名：端口/数据库名

## 4.定义sql

* `String sql = "update t_branch set college_id = 2 where id = 1";`,定义一个存储sql语句的字符串。

## 5.获取执行sql语句的对象

*  `Statement  stmt = conn.createStatement();`conn是数据库的连接对象。
## 6.执行sql，接受返回结果；

* ` int count = stmt.executeUpdate(sql);`
* ` System.out.println(count);`

## 7. 释放资源

* `conn.close();`
* `stmt.close();`

```java

package com;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

/*
 * JDBC入门
 */
public class Jdbc1 {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        //获取数据库连接对象
        Connection conn = DriverManager.getConnection("jdbc:mysql://3306/youth_study", "root","root");
        //定义sql语句
        String sql = "update t_branch set college_id = 2 where id = 1";
        // 获取执行sql的对象
        Statement  stmt = conn.createStatement();
        // 执行sql
        int count = stmt.executeUpdate(sql);
        // 处理结果
        System.out.println(count);
        // 释放资源
        conn.close();
        stmt.close();
    }
}
```

# JDBC对象

## DriverManager

* 驱动管理对象
* 功能：
  1. 注册驱动
  2. 获取数据库的连接

### 注册驱动

* 告诉程序该使用哪一个数据库驱动jar包
* 方法：`static void registerDriver(Driver driver)`,注册与给定的驱动程序
* 实际使用：`Class.forName("com.mysql.jdbc.Driver");`
* 在com.mysql.jdbc.Driver的源码中存在静态代码块：
```java
Static {
      try {
        java.sql.DriverManager.registerDriver(new Driver());
      } catch (SQLException E) {
        throw new RuntimeException("Can't register driver!");
      }
}
```
* 通过导入jar包，就会自动注册驱动程序

### 获取数据库连接

* 让程序连接到具体的数据库；
* 方法：`static Connection getConnection(String url, String user, String password);`
* 参数：
  * url:指定连接数据库的路径
    * 语法：`jdbc:mysql://ip地址(域名):端口号/数据库名称`
    * 例子：`jdbc:mysql://localhost:3306/db1`
    * 特例:如果连接的是本机mysql的服务器，并且MySQL服务器的默认端口是3306，则URL可以简写为：`jdbc:mysql:///数据库名称`
  * user:用户名
  * password：用户密码

## Connection

* 数据库连接对象
* 功能：
  1. 获取执行sql的对象
  2. 管理事务

### 获取执行sql的对象

* 创建一个能够接收sql语句的对象；
* 方法：
  * `Statement createStatement();`
  * `PreparedStatement prepareStatement(String sql);`

### 管理事务

* 包含处理事务的开启，提交，回滚的方法；
* 开启事务：`void setAutoCommit(boolean autoCommit);`,调用该方法并设置参数为**false**，即可开启事务。（因为设为true则代表着着事务是自动提交，也就没有人的管理，所以也就没有开不开启事务之说）
* 提交事务：`void commit()`
* 回滚事务：`void rollback();`

## Statement

* 用于执行**静态SQL语句**并放回其生成的结果的对象。
* `boolean execute(String sql);`,可以执行任意的sql语句，不常用。
* `int executeUpdate(String sql);`:执行DML（insert， update， delete）语句，也可以执行DDL（create， alter ，drop）语句（但是这些操作一般不会使用java代码实现，所以这个方法常用于执行DML语句）。
  * 返回值：该方法的返回值是**执行该sql语句影响的行数**，通过这个返回值来判断sql语句是否执行成功（返回值>0则成功）。
* `ResultSet executeQuery(String sql);`:执行DQL（select）语句。 

## ResultSet

* 结果集对象，封装了查询的结果；
* Result对象可以想象为是一个指向查询结果表的**游标**（类似c语言的指针概念），这个“游标”开始是指向表头的。
* `boolean next() `:使游标指向下一行，并判断当前行是否有数据，如果没有则返回false。
* `getXxx(参数)`:获取某一个数据
  * Xxx；代表返回的数据类型，与要查询的数据的数据类型相匹配、如：`int getInt(), String getString()`;
  * 参数：
    1. int类型的参数：代表列的编号，从左往右数，从1开始。如：`getString(1);`表示取出当前游标所指行的第一列的数据
    2. String类型的参数：代表列的名称。如:`getDouble("balance")`表示取出当前行名为balance列的数据。
* 使用步骤：
  1. 游标向下移动一行
  2. 判断是否有数据
  3. 获取数据
  4. 如果有多行数据需要输出，则使用循环重复以上三个步骤，可以遍历整个结果集的数据。

## PreparedStatement

* 是Statement的子类，但是功能更加强大；
* SQL注入问题：在拼接sql语句时，有一些sql的特殊关键字参与字符串的拼接，会造成sql语句的含义改变，导致安全问题。
  * 示例：`String sql = "select * from user where username = '"+username+"' and password = '"+password+"'"`,其中被单双引号包裹的是传进来的字符串参数。(注意这种拼接字符串的特殊格式)。这种直接拼接参数的sql语句也叫做**静态sql语句**。
  * 如果username = "zhangsan",password = "a' or 'a' = 'a",那么拼接上参数的值后的sql语句为：`sql = "select * from user where username = '"+"zhangsan"+"' and password = '"+"a' or 'a' = 'a""'"`将双引号合并之后为:`sql = "select * from user where username = 'zhangsan' and password = 'a' or 'a' = 'a'"`,这个sql语句的含义就和我们原本的想象大不相同了。
* 解决SQL注入问题：使用PreparedStatement对象替换原来的Statement对象。
* **预编译的sql语句**：将sql语句中的参数使用占位符`?`来代替。
* ParparedStatement类型才是一般情况下通用的JDBC使用方法；
* 可以防止sql注入问题，效率更高。

### 使用步骤

1. 导入驱动jar包
2. 注册驱动
3. 获取数据库连接对象Connection
4. 定义sql语句：
   1. 需要参数的地方使用`?`来代替。如：`String sql = "select * from user where username = ? and password = ?`
5. 获取执行sql语句的PreparedStatement对象：使用Connection.prepareStatement(String sql)方法，如`PreparedStatement patmt = conn.prepareStatement(sql);`
6. 给`?`占位符赋上参数的值：
  * 方法：`setXxx(参数1，参数2)`
     * Xxx是参数的类型；
     * 参数1是int类型：是参数在sql语句中的相对位置来定的，从左往右，从1开始编号。第一个参数的参数1就是1
     * 参数2：就是具体的参数。
     * 示例：`pstmt.setString(1,username);`
     * `pstmt.setString(2, password);`
7. 执行sql，接收返回结果，**不需要传递sql语句**（与Statement不同），如：`ResultSet rs = pstmt.excuteQuery();`
8. 处理结果
9. 释放资源



# JDBC工具类

*  作用：将重复的代码封装进一个类中，简化代码的书写。
*  抽取的代码：
   *  注册驱动的代码；
      *  驱动只需注册一次，所以直接在静态代码块中实现
   *  抽取获取连接对象的代码：
      *  需求：不传递参数的同时，保证工具类的通用性。
      *  解决方法：书写`.properties`配置文件。此处是`jdbc.properties`文件.在这个文件中将获取连接对象的参数写好,之后再次使用该工具类连接不同的数据库时，只需要修改配置文件即可。
```properties
url = jdbc:mysql://localhost:3306/db3
user = root
password = root
driver = com.mysql.jdbc.Driver
```
   *  抽取释放资源的代码。
* 工具类的实现：JDBCUtils类
```java
import java.io.FileReader;
import java.io.IOException;
import java.net.URL;
import java.sql.*;
import java.util.Properties;

public class JDBCUtils {
    private static String url;
    private static String user;
    private static String password;
    private static String driver;

    /*
     * 文件的读取，只需要读取一次即可拿到这些值。使用静态代码块，只读取一次这些值
     */
    static {
        try {
            //1. 创建Properties集合类
            Properties pro = new Properties();
            //2. 获取src路径下的文件的方式:使用ClassLoader类加载器
            //获取src文件夹在计算机中的绝对路径
            ClassLoader classLoader = JDBCUtils.class.getClassLoader();
            //获取src文件夹下配置文件的url格式的路径
            URL res = classLoader.getResource("jdbc.properties");
            //将url路径转换为字符串形式
            String path = res.getPath();

            //3.加载文件
            pro.load(new FileReader(path));

            //4.获取数据，赋值
            url = pro.getProperty("url");
            user = pro.getProperty("user");
            password = pro.getProperty("password");
            driver = pro.getProperty("driver");

            //5. 注册驱动
            Class.forName(driver);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    /**
     * 获取连接
     * @return 连接对象
     */
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(url, user, password);
    }

    /**
     * 释放资源
     * @param stmt
     * @param conn
     * @param rs
     */
    public static void close(ResultSet rs, Statement stmt, Connection conn) {
        if(rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if(stmt != null) {
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        
        if(conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

    }
}
```