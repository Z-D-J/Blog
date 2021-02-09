---
title: Mybatis
date: 2021-02-08 22:23:17
tags:
---

# Mybatis简介

* MyBatis 是一款优秀的**持久层框架**。
  * 持久化：将程序的数据永久存储到硬盘上；
  * 持久层：完成持久化工作的代码块，即三层架构中的**DAO层**。
* MyBatis 避免了几乎所有的JDBC代码和手动设置参数以及获取结果集。
* MyBatis 可以使用简单的 **XML 或注解来配置和映射原生信息**，将接口和 Java 的 POJOs(Plain Ordinary Java Object,普通的 Java对象)映射成数据库中的记录。
* Mybatis资料：
  * [官方文档](https://mybatis.org/mybatis-3/zh/index.html)
  * [下载地址](https://github.com/mybatis/mybatis-3/releases)
  * maven坐标：
```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.6</version>
</dependency>
```
* 优点：
  * 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件。
  * 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。 **sql写在xml里**，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
  * 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离。
  * 提供xml标签，支持编写动态sql。

# 快速入门

## 一：环境搭建

1. 通过maven导入三个jar包：
   1. mysql驱动包：
   2. junit包；
   3. mybatisjar包
```xml
    <dependencies>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.23</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13</version>
            <scope>test</scope>
        </dependency>>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
    </dependencies>
```

## 二：编写核心配置文件

* `mybatis-config.xml`,maven项目放在resources目录下：
```xml
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <!--配置数据源-->
            <dataSource type="POOLED">
                <!--注册驱动，同jdbc-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <!--数据库连接路径-->
                <property name="url" value="jdbc:mysql://localhost:3306/youth_study"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
    <!--每一个Mapper.xml文件都需要在这个mybatis核心配置文件中注册-->
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```

## 三：编写Mybatis工具类

 * 编写一个用来获取SQLSession实例的工具类：
```java
package com.zestaken.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class MybatisUtils {
    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
            //1.加载核心配置文件
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            //2.根据xml核心配置文件获取对应的SqlSessionFactory对象
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    //2.从SqlSessionFactory实例中获得 SqlSession 的实例。
    // SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。
    // 你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }

}
```

## 四：编写操作表的接口并实现

* 接口：T_collegeMapper
```java
package com.zestaken.dao;

import com.zestaken.Pojo.T_college;

import java.util.List;

public interface T_collegeMapper {
    List<T_college> getT_collegeList();
}
```
* 实现：Mapper.xml实现了接口实现类的功能
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace绑定一个Mapper接口-->
<mapper namespace="com.zestaken.dao.T_collegeMapper">
    <!--id是需要实现的接口中的方法名-->
    <!--resultType是返回结果的类型，如果返回的是结果集，则用resultMap-->
    <!--select是要执行sql查询语句-->
    <select id="getUserList" resultType="com.zestaken.Pojo.T_college" >
    select * from youth_study.t_college;
  </select>
</mapper>
```
* 注：Mapper.xml文件需要在mybatis-config.xml文件中注册：
```xml
    <!--每一个Mapper.xml文件都需要在这个mybatis核心配置文件中注册-->
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
```

## 五：编写junit测试类

* 编写一个可以查询表的测试类：
```java
import org.junit.Test;

import java.util.List;

public class T_collegeMapperTest {
    @Test
    public void test(){
        //1.获取SqlSession实例
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //2.获取Mapper接口的实现类
        T_collegeMapper t_collegeMapper = sqlSession.getMapper(T_collegeMapper.class);
        //3.执行sql
        List<T_college> t_collegeList = t_collegeMapper.getT_collegeList();

        for(T_college college : t_collegeList){
            System.out.println(college);
        }

        //4.释放sqlSession
        sqlSession.close();
    }
}
```

## 六：常见错误

1. Mapper.xml文件没有在mybatis-config.xml文件中注册；
2. 没有配置maven，使maven可以导入java包下的配置文件。（因为maven默认所有配置文件都是放在resources目录下的）
   * 在pom.xml中配置，使maven可以导入java包下的配置文件：
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

# Mybatis的CRUD操作

* 在mapper接口中增加对应操作的方法，在mapper.xml中增加对应的sql语句。
* **表对象中的属性，可以直接取出来**。
* **增删改操作必须提交事务才能生效**。
* 增删改操作的返回值默认为int，这个类型不需要在`resultType`中设置，如果操作成功则返回1，操作失败返回0；
* 参数可以用`#{参数名}`取出来
* 查询操作用`<select></select>`
* 添加操作用`<insert></insert>`
* 修改操作用`<update></update>`
* 删除操作用`<delete></delete>`
* 示例：
  1. mapper接口
```java

import com.zestaken.pojo.T_college;

import java.util.List;

public interface T_collegeMapper {
    //查询表中的所有值
    List<T_college> getT_collegeList();
    //根据id查询表中的值
    T_college getT_collegeByID(int id);
    //向表中插入新的数据
    int insertT_collegeList(T_college t_college);
    //修改表中某项的数据
    int updateT_collegeList(T_college t_college);
    //删除表中指定id的项
    int deleteT_collegeList(int id);

}
```
   2. mapper.xml
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace绑定一个Mapper接口-->
<mapper namespace="com.zestaken.dao.T_collegeMapper">
    <!--id是需要实现的接口中的方法名-->
    <!--resultType是返回结果的类型，如果返回的是结果集，则用resultMap-->
    <!--select是要执行sql查询语句-->
    <select id="getT_collegeList" resultType="com.zestaken.pojo.T_college" >
    select * from youth_study.t_college;
  </select>
<!--    参数用#{}取出来-->
    <select id="getT_collegeByID" parameterType="int" resultType="com.zestaken.pojo.T_college">
        select * from youth_study.t_college where id = #{id};
    </select>
    <!--表对象中的属性可以直接取出来   -->
    <insert id="insertT_collegeList" parameterType="com.zestaken.pojo.T_college" >
-- 虽然参数是表对象，但是表对象中的属性可以直接取出来，就相当于传递的参数是一系列的属性值
        insert into youth_study.t_college(id,name) values(#{id},#{name});
    </insert>

    <update id="updateT_collegeList" parameterType="com.zestaken.pojo.T_college">
        update youth_study.t_college set name=#{name} where id = #{id};
    </update>
    <delete id="deleteT_collegeList" parameterType="int">
        delete from youth_study.t_college where id = #{id};
    </delete>
</mapper>
```
  3. 测试类
```java
package com.zestaken.dao;

import com.zestaken.pojo.T_college;
import com.zestaken.utils.MybatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

public class T_collegeMapperTest {
    @Test
    public void get(){
        //1.获取SqlSession实例
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        //2.获取Mapper接口的实现类
        T_collegeMapper t_collegeMapper = sqlSession.getMapper(T_collegeMapper.class);
        //3.执行sql
        List<T_college> t_collegeList = t_collegeMapper.getT_collegeList();

        for(T_college college : t_collegeList){
            System.out.println(college);
        }

        //4.释放sqlSession
        sqlSession.close();
    }

    @Test
    public void getByID(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        T_collegeMapper mapper = sqlSession.getMapper(T_collegeMapper.class);

        T_college college = mapper.getT_collegeByID(100);
        System.out.println(college);


        sqlSession.close();
    }

    @Test
    public void insert(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        T_collegeMapper mapper = sqlSession.getMapper(T_collegeMapper.class);

        T_college t_college = new T_college();
        t_college.setId(100);
        t_college.setName("zhangjie");
        mapper.insertT_collegeList(t_college);

        //增删改操作必须提交事务才能生效
        sqlSession.commit();

        sqlSession.close();
    }

    @Test
    public void updateT_collegeList(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        T_collegeMapper mapper = sqlSession.getMapper(T_collegeMapper.class);

        T_college t_college = new T_college();
        t_college.setId(100);
        t_college.setName("zhangsi");
        mapper.updateT_collegeList(t_college);

        sqlSession.commit();

        sqlSession.close();
    }

    @Test
    public void deleteT_collegeList(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        T_collegeMapper mapper = sqlSession.getMapper(T_collegeMapper.class);

        mapper.deleteT_collegeList(100);

        sqlSession.commit();

        sqlSession.close();
    }
}
```