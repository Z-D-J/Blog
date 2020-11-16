---
title: Mysql
date: 2020-10-23 12:09:42
tags:
---

# 数据库简介

* 特点：
  1.  持久化保存数据；
  2.  可以实现结构化查询，方便管理。
* DB:数据库（database），存储数据的仓库，保存了有组织的数据。
* DBMS:数据库管理系统。数据库是通过DBMS来创建和管理的容器。常见数据库管理系统：MYSQL，Oracle，DB2,SqlServer。
* SQL：结构化查询语言（StructureQuery Language），专门用来与数据库通信。几乎所有DBMS都支持SQL。
* 数据存储数据：
  1.  将数据存入表中，表再放入库中。一个数据库中可以有多个表，每个表有一个名字，表名具有唯一性。
  2.  表具有一些特性，这些特性定义了数据在表中如何存储，类似java中的“类”。
  3.  表由列组成，这些列也称为**字段**，每一列类似java中的属性。
  4.  表中的数据是按行存储的，每一行类似java中的对象。

# MySQL的安装

* MySQL的特点：
  1.  开放源代码；
  2.  性能高
  3.  容易安装和使用。
* DBMS的分类：
  1.  基于共享文件系统的（如：Access）
  2.  基于客户机-服务器的DBMS（如；MySQL，oracle，sqlsever）。
* MySQL下载安装：
  1.  社区版（免费）
  2.  企业版（收费）
  3.  下载地址：https://dev.mysql.com/downloads/installer/
  4.  跟随安装指导进行配置。

# MySQL服务的启动

1. 搜索服务，点击打开；
2. 在cmd输入`services.msc`启动；
3. 在管理员cmd输入`net start <本机mysql的名字>`或者`net stop <本机mysql的名字>`启动或者关闭。

# MySQL的登录

* 登录本地用户：`mysql -uroot -proot`，-u后面接的是用户名，-p后面接的是root用户的密码。`mysql -uroot -p`,会在之后输入密码。
* 登录远程用户：`mysql -h127.0.0.1 -p` -h后面接的是连接目标的ip。
* 登录：`mysql --host=IP --user=用户名 --passward=连接目标的密码`

# MySQL的目录结构

1.MySQL的安装目录：
  1.  bin：二进制可执行文件，包括很多命令的执行程序。
  2.  data：存放mysql的日志文件，数据文件等。
  3.  include：放置.h头文件；
  4.  lib：所需的jar包；
  5.  share：错误信息存放
2.MySQL的数据目录：（在c盘下的programdata下）
  1.  数据库及其中的数据；
  2.  my.ini是MySQL的配置文件。

# SQLyog图形化界面

* 可以使用sql语句控制，也可以直接使用鼠标控制。

# SQL语句

## SQL的简介

* SQL：结构化查询语言（StructureQuery Language），专门用来与数据库通信。几乎所有DBMS都支持SQL。可以用来操作所有的关系型数据库。

## SQL的通用语法

* SQL可以单行或者多行书写，以分号结尾。
* 使用空格和缩进来规范格式。
* Mysql的SQL语句不区分大小写。，关键字建议使用大写。
* 注释：
  1.  单行注释：`-- `或者`# `之后写注释内容。（--注释符后面有空格。#可以没有空格，是MySQL特有的。）

## SQL的分类

* DDL（data definition language）：操作数据库和表；
* DML（Data Manipulation Language）；增删改表中的数据。
* DQL（Data Query Language）:查询表中的数据。
* DCL（Data control Language）:数据控制语言，控制访问权限和安全级别等。

## DDL

### 操作数据库（CRUD）

1. C（creat）:创建；
   1. 创建数据库：`creat database 数据库名称;`
   2. 判断数据库不存在，再创建：`creat database if not exists 数据库名称;`
   3. 创建数据库，并指定字符集：`creat database 数据库名称 character set 字符集名;`
2. R（Retrieve）：查询；
   1. 查询已经存在的数据库：`show databases;`
   2. 查看某个数据库的字符集：`show creat database 数据库名称;`(同时也是查询数据库的创建语句)
3. U（Update）：修改；
   1. 修改数据库的字符集：`alter database 数据库名称 character set 字符集名称;`
4. D(Delete):删除；
   1. 删除数据库：`drop database 数据库名称;`。
   2. 判断数据库存在，再删除：`drop database if exists 数据库名称;`
5. 使用数据库。
   1. 查询当前正在使用的数据库名称:`select database();`
   2. 使用数据库：`use 数据库名称;`

### 操作表（CRUD）


1. C（creat）:创建；
   1. 创建语法:`creat table 表名（列名1， 数据类型1， 列名2 数据类型2， ... 列名n 数据类型n）;`**创建表时，至少有一个列，否则创建会直接失败**
   2. 复制：`creat table 表名（即将创建） like 表名（被复制的）`
2. R（Retrieve）：查询；
   1. 查询数据库中所有表的名称：`show tables;`
   2. 查询表结构：`desc 表名;`
3. U（Update）：修改；
   1. 修改表名：`alter table 表名 rename to 新表名;`
   2. 修改表的字符集：`alter table 表名 character set 字符集名称;`
   3. 添加一列：`alter table 表名 add 列名 数据类型;`
   4. 修改列名称 类型：`alter table 表名 modify 列名 新数据类型;`（仅修改列的数据类型）或者`alter table 表名 change 列名 新列名 新数据类型;`
   5. 删除列：`alter table 表名 drop 列名;`
4. D(Delete):删除；
   1. 删除数据库中的表;·drop table 表名;`
   2. 判断表存在后再修改:`drop table if exists 表名;`

### 数据类型

* int： 整数类型；
* double：浮点数类型，double（5, 2）表示总共有5位数，其中小数点后有两位。
* date:日期，只包含年月日，yyyy-mm-dd;
* datetime:日期，包含年月日时分秒，yyyy-mm-dd HH:mm:ss;
* timestamp:时间戳类型，包含年月日时分秒（同datetime），但是如果不给这个字段赋值或者赋值为null，则默认使用当前的系统时间来自动赋值。
* varchar：字符串类型，varchar（20），表示字符串的最多有20个字符。**必须在varchar后面接上（数字），否则就是语法错误。**

## DML

1. 添加数据：
   1. 添加语法：`insert into 表名 （列名1， 列名2，... ，列名n）value（值1，值2，...,值n）;`
      1. 列名和值要一一对应；
      2. 如果表名后不给列名，在提供和列数相同个数值的前提下，会默认依次给所有列添加值，否则会报错。
2.删除数据：
   1.  删除语法：`delete from where 条件；`如果没有加条件，就会删除表中所有的数据。示例：`delete from where id=1;`
   2.  删除表，然后再创建一个一模一样的空表：`truncate table 表名;`
3.修改数据：
   1.  修改语法：`update 表名 set 列名1 = 值1，列名2 =值2 ... where 条件;`,示例：`update stu set age = 19， score = 12 where id = 1;`。如果不加任何条件则会将表中所有的数据全部修改。

## DQL

1.排序查询：
   1.  排序基础语法：`order by 子句`
   2.  `order by 排序字段1 排序方式1, 排序字段2 排序方式2, ... 排序字段n 排序方式n;`
   3.  示例：`select * from stu order by id desc;`
   4.  位于后面的排序字段的优先级较低，则当当前面的条件值一样时，才会去判断之后的条件来排序。
   5.  排序方式：
       1.  ASC：升序排列，如果不指定排序方式，默认升序；
       2.  DESC：降序排列；
2.聚合函数：将一列数据作为一个整体，进行**纵向**的计算。聚合函数会默认排除为null的项。
   1.count：计算个数；
       * 示例:`select count(列名) from 表名;`,会忽略为null的项。
       * `select count(ifnull(列名，0)) from 表名;`，会将值为null的项的值转为0，再计数。
       * `select count(*) from 表名;`,会综合所有列来计数（除非有一行都为null）
   2.max：计算最大值；
   3.min;计算最小值；
   4.sum：求和；
   5.avg：计算平均值。  
   * 适用于count的特殊方法也会适用于其他函数（除了`*`）
3.分组查询
   1. 语法：`group by 分组字段`，可以增加条件：`where 条件 group by 分组字段;`（分组前进行限定，如果不满足条件，则不参与分组。where后不可以跟聚合函数进行判断）或者`group by 分组字段 having 条件
   2. 示例：`select sex avg(math), count(id) from student group by sex;`,有条件：`select sex from student where math>70 group by sex;`(math>70 才能有被分组的资格)，`select sex feom student group by sex having count(id) > 2;`(id的个数要大于2，才会参与分组)。
   3. 分组后查询的字段：只能是被查询的字段，或者是聚合函数。
4.分页查询
   1. 分页语法：`limit 分页索引，每页显示的条数`（limit是mysql的方言）
   2. 分页索引的计算：开始的索引 - （当前的页码 -1）* 每页的条数。
   3. 示例：`select * from stu limit 0,3;`(第一页)， `selct  * from stu limit 3,3;`(第二页)

### DQL查询表中的数据

* 查询所有数据：`select * from 表名`(将表中的所有数据查询出来)
* 总语法：`select 字段列表 from 表名列表 where 条件列表 group by 分组字段 having 分组之后的条件限定 order by 排序子句 limit 分页限定`

#### 基础数据查询

* 查询指定列：`select 列名1，列名2 from 表名`.示例：
```sql
select 
      name , -- 姓名
      age，  -- 年龄
from
      student; --学生表
```
* 去除重复的结果集显示某列的内容:`select distinct 需去重的列名1，需去重的列名2 from 表名`（必须去重的所有的列的数据完全一样才会去掉）
* 计算列的的结果再显示：`select 列名1， 列名2，列名1 + 列名2 form 表明;`(如果某一列的数据为null，则计算结果都为null)
  * 一般可以使用四则运算进行运算（只有数值型计算）。
  * ifnull函数：`ifnull(表达式1，表达式2);`表达式1：需要判断是否为null的字段；表达式2；被查询字段为null后替代的值。
* 给列起别名：` select 列名1 as 别名1 form 表名`或者省略as`select 列名1 别名1 form 表名`(列名和别名之间用空格)

#### 条件查询

* where子句后跟条件；
* 运算符：
  * `>, <, >= , <=, =(没有==，=就是等于) , !=, <>(也是不等号）`
  * `between...and...(在两者之间，包含边界0`
  * 逻辑运算符：`and(与&&相同),or(与||相同)，not(与!相同)`
  * `in(数据1，数据2，数据3，...)`数据等于数据1，或者数据2，或者数据3都可以。
  * `is null, is not null`null值不能被直接查询，只能使用这两个特殊语句判断。
  * `like`:模糊查询
    * 占位符:
      * `_`：单个任意字符；
      * `%`:多个任意字符；
    * 示例：
      * `select name from stu where name like '马%';`(name中第一个字是马)
      * `select name from stu where name like '_化_`（name中第二个字是化）
      * `select naem from stu where name like '%德%'(name中含马)
      * `select name from stu where name like '___'`(name为三个字)

## 约束

### 约束概念

* 约束：对表中的数据进行限定，从而保证数据的正确性，有效性和完整性。
* 约束的分类：
  1. 主键约束：primary key
  2. 非空约束：not null
  3. 唯一约束：unique
  4. 外键约束：foreign key

### 非空约束 NOT NULL

* 在创建表时添加约束：
  * 示例：
  ```sql
   CREATE TABLE stu1(
   id INT,
   NAME VARCHAR(20) NOT NULL -- name必须为非空，才能加入表中
   );
   ```
* 创建表完成后添加或删除约束：
  * 示例：
  ```sql
  ALTER TABLE stu1 MODIFY NAME VARCHAR(20); -- 将原来有约束的name改为没有not null的
  ALTER TABLE stu1 MODIFY NAME VARCHAR(20) NOT NULL; -- 给name添加not null约束
  ```

### 唯一约束 UNIQUE

* 创建表时添加约束：
  * 示例：
  ```sql
   CREATE TABLE stu1(
   id INT,
   NAME VARCHAR(20) UNIQUE -- name必须为是唯一没有重复的，才能加入表中
   );
* 创建表完成后添加或者删除约束：
   * 示例：
   ```sql
   ALTER TABLE stu1 DROP INDEX NAME VARCHAR(20); -- 删除创建表时的唯一约束（使用DROP INDEX 而不是MODIFY）
   ALTER TABLE stu1 MODIFY NAME VARCHAR(20) UNIQUE; -- 添加唯一约束，仍然使用MODIFY
   ```
* MySQL中多个null不认为是重复的

### 主键约束：PRIMARY KEY

* 主键约束：非空且唯一，一张表中只能有一个字段为主键，主键就是表中记录的唯一标识。
* 创建时添加主键，示例：
```sql
create table stu (
   id int primary key, -- 给id添加主键约束
   name varchar(20)
)
```
* 删除主键约束，示例：
```sql
alter table stu1  drop primary key;
```
   * 因为一个表中的主键是唯一的，所以无需指定特定的列。
* 创建完表之后，添加主键，示例：
```sql
alter table stu1 modify id int primary key;
```
* **自动增长**：
  * 如果某一列是数值类型的，使用auto_increment可以完成值的自动增长。一般和主键联合在一起使用。
  * 创建表时添加主键约束，并且实现主键的自增长，示例：
  ```sql
  create table stu1 (
     id int primary key auto_increment, -- 给id添加主键约束，并自动增长。
     name varchar(20)
  );
  ```
* 使用自动增长：
```sql
insert into stu1 values(null, 'name1'); -- 每次执行此操作，如果不指定id的值，就会自动根据上一行的数据加一来作为本行的id值
```
* 删除自动增长：
```sql
alter table stu1 modify id int; -- 能够去除自动增长，但是不能这样删除主键
```
* 创建完表后添加自动增长：
```sql
alter table stu modify id int auto_increment;
```

### 外键约束：FOREIGN KEY

* 联系两个表某些列，之后关联的两列的删除添加操作都是相互制约的,从而保证数据的正确性。
* 创建表时添加外键：
```sql
create table 表名 (
   ...
   外键列(和其它表有关系的列)
   constanit  外键名称 foreign key (外键列的名称) references 主表名称(主表的列（一般为主键列）名称)
)

示例：

creat table department (
   id int primary key,
   name varchar(20)
)

create table empolyee (
   id int primary key,
   dep_id int -- 外键对应主表的主键（外键列）
   constraint emp_dept_fk foreign key (dep_id) references department(id)
)
```
* 删除外键：
```sql
alter table employee drop foreign key emp_dept_key;
```
* 创建表之后添加外键：
```sql
alter table employee add constraint emp_dept_fk foreign key (dep_id) references department(id);
```
* **级联操作**:修改有外键连接的两个表的列中的数据，操作会自动同步给关联的另一个列。
  * 添加级联操作语法：
  ```sql
  ALTER TABLE 表名 ADD CONSTRAINT 外键名称 
         FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON UPDATE CASCADE ON DELTE CASCADE;
   ```
   * 级联更新：ON UPDATE CASADE;
   * 级联删除：ON DELTE CASCADE;

# 数据库的设计

## 多表关系

1. 一对一关系（使用较少）
   1. 如：人与身份证
   2. 实现：一对一关系实现，可以在任意一方添加**唯一外键**指向另一方的主键。可以直接合成一张表。
2. 一对多关系
   1. 如：部门和员工
   2. 实现：在“多”的一方建立外键，指向“一”的一方的主键。
3. 多对多关系：
   1. 如：课程与学生
   2. 实现：多对多关系需要借助**中间表**，中间表至少包含两个字段，这两个字段（这两个字段是**联合**的）作为第三张表的外键，分别指向两张表的主键。

## 数据库设计的范式

* 范式概念：设计数据库时需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求。
  * 设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。（前三种足矣。）
* 范式分类：
  1. 第一范式（1NF）：每一列都是不可分割的原子数据项。（数据库中创建表的基本要求）
     1. 存在严重的数据冗余问题
     2. 数据添加存在问题
     3. 数据删除存在问题**
  2. 第二范式（2NF）：在1NF的基础上，非码属性必须完全依赖于候选码（在1NF的基础上消除了非主属性对主码的**部分依赖**，解决了数据冗余问题）
     1. 概念：
        1. 函数依赖：A->B，如果通过A属性（属性组）的值，可以确定唯一B属性的值，则称B依赖于A
        2. 完全函数依赖：A->B,如果A是一个属性组，则B的值的确定需要依赖于A属性组中所有的属性值
        3. 部分函数依赖：A->B,如果A是一个属性组，则B属性值的确定只需要依赖于A属性组中某一些属性值即可。
        4. 传递函数依赖：A->B, B->C,如果通过A属性（属性值）的值，可以唯一确定B属性的值，在通过B属性（属性组）的值可以确定唯一的C属性的值，则称C传递函数依赖于A.
        5. 码：如果在一张表中，如果一个属性或者属性组，被其它所有属性完全依赖，则称这个属性（属性组）为该表的码。
        6. 主属性：码属性组中的所有属性。
        7. 非主属性：除了码属性组的属性。
  3. 第三范式（3NF）：在2NF的基础上，任何非主属性不依赖于其它非主属性（在2NF的基础上消除传递依赖，解决了数据添加和删除存在的问题）

# 数据库的备份和还原

* 语法：`mysqldump -u用户名 -p密码 数据库名称 > 备份保存的路径`（保存到以.sql结尾的文件）
* 还原：
    1. 登录数据库；`mysql -u用户名 -p密码;`
    2. 创建一个新数据库；`create database 新数据库名;`
    3. 使用数据库:`use 数据库名;`
    4. 执行备份的文件:`source 文件路径;`

# 多表查询

## 多表查询的基本概念

* 查询基本语法：
```sql
select
   列名列表
from
   表的列表（可以写多个表）
where
   ...(条件)
```
* 示例：`select * from table1, table2;`。不加任何条件查询多个表的结果是：所有表的组合（两个表时是笛卡尔积）。

## 多表查询的分类

1. 内连接查询
2. 外连接查询
3. 子查询

### 内连接查询

1. 隐式内连接：使用where条件来消除多个表组合后的无用信息。
```sql
select 
      * 
from 
      table1, table2 
where 
      table1.`id1` = `table.id2`; -- 组合后不满足的这个条件的行都会被去掉


select 
      table1.name, table2.name -- 要查询两个表里的同名列，需要在列名前面加上表名的限定。
from 
      table1, table2 
where       
      table1.`id1` = table2.`id2`; 


select 
      t1.name, t2.name 
from 
      table1 t1, table2 t2 -- 通过取别名来简化对表名的书写。
where 
      t1.`id1` = t2.`id2`; 
```

2. 显式内连接：
   * 语法：`select 字段列表 from 表名1 inner join 表名2 on 条件;`
   * 同样支持对表取别名来简化书写
```sql
select
      * 
from
      table1
inner join
      table2  -- 两个表是分开放的
on 
      table1.`id1` = table2.`id2`;


select
      * 
from
      table1 t1
join              -- inner可以省略
      table2 t2
on 
      t1.`id1` = t2.`id2`;
```

### 外连接查询

1. 左外连接：
   * 语法：`select 字段列表 from 表1 left outer join 表2 on 条件;`(outer同样是可以省略的)
   * 查询的是左表所有数据以及左表和右表数据交集部分。from后面的是左表，join后面是右表。
2. 右外连接：
   * 语法：`select 字段列表 from 表1 right outer join 表2 on 条件;`(outer同样是可以省略的)
   * 查询的是右表所有数据以及左表和右表数据交集部分。from后面的是左表，join后面是右表。

### 子查询

* 查询中嵌套查询，嵌套的查询称为子查询。
* 示例：
```sql
# 查询工资最高的员工的信息需完成两步操作：一：查询最高的工资；二：查询最高工资对应的员工信息
select
      * 
from 
      table1 -- 外层查询整个表的员工信息
where 
      table1.`salary` = (select max(salary) from table1); -- 嵌套一个子查询语句在条件里，完成最高工资的限定
```

#### 子查询的不同结果

* 子查询结果是**单行单列**的：
  * 子查询结果可以作为条件，使用判断运算符去判断,如：
  ```sql
  table1.`salary` = (select max(salary) from table1);
  ```
* 子查询结果是**多行单列**的：
  * 子查询可以作为条件，使用运算符`in`（是否在这个集合中）去判断，如：
  ```sql
  table.`id` in (select id from table1 where name = '1' or name = '2');
  ```
* 子查询的结果是**多行多列**的：
  * 子查询可以作为一张虚拟表，参与查询，如：
  ```sql
  # 查询员工的入职日期是`2011-11-11`日之后的员工信息和部门信息
  
  -- 子查询方式
   select
         *
   from 
         dept t1,(select * from emp where emp.`join_date` > '2011-11-11') t2   -- 子查询结果作为一张表参与查询
   where
         t1.id = t2.dept_id;

   -- 普通内连接
   select
         * 
   from
         emp t1, dept t2
   where
         t1.`dept_id` = t2.`id` and t1.`join_date` > '2011-11-11';
   ```

# 事务

## 事务的基本介绍

* 事务概念：如果一个包含多个步骤的业务操作，被事务管理，那么这些操作**要么同时成功，要么同时失败**。
* 基本操作；
  1. 开启事务：start transaction；
  2. 回滚：rollback；
  3. 提交：commit。
* 示例：
```sql
# 实现张三给李四的账户上转去500：1.张三的账户减五百 2.李四的账户加500 （如果这两步中有任何一步出错了的话，事务管理机制保证账户信息不被修改）
start transaction; -- 开启事务

update account set money = money - 500 where name = 'zhangsan'; -- 张三的账户减500

update account set money = money +500 where name = 'lisi'; -- 李四的账户加500

-- 如果两步执行完没有异常，则提交，提交后的数据库改变才真正生效
commit;
-- 如果执行出错，则回滚，数据库的状态维持启动事务时的状态
rollback;
```
* 在MySQL中，事务是默认自动提交的
  * 自动提交：
    * 一条DML（增删改）语句会自动提交一次事务
  * 手动提交：
    * 需要先开启事务，再提交
  * 修改事务的默认提交方式：
    * 查看默认提交方式：`select @@autocommit;`,结果为1代表自动提交
    * 设置默认提交方式：`set @@autocommit = 0;`，改为0代表手动提交
* 在oracle中，事务是默认手动提交的。

## 事务的四大特征

1. 原子性：是不可分割的最小单位，要么同时成功，要么同时失败。
2. 持久性：事务一旦提交或者回滚后，数据库会持久化地保存数据。
3. 隔离性：多个事务之间相互独立。
4. 一致性：事务操作前后，数据总量不变。（即如果事务执行到中途出错了，则整个数据库都回滚到事务开始前的状态。）

## 事务的隔离级别

* 概念：理论上多个事务之间是隔离的，相互独立。如果多个事务操作同一批数据，那么这些事务之间就不是隔离的了，会引发一些问题，设置不同的隔离级别来解决这些问题。
* 存在的问题：
  1. 脏读：一个事务，读取到了另一个事务中**没有提交**的数据。
  2. 不可重复读（虚读）：在同一个事务中，两次读到的数据不一样。(原因可能是其它事务在两次查询之间的时间修改了数据库)
  3. 幻读：一个事务操作（DML）数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改。
* 隔离级别：隔离级别从小到大安全性越来越高，但是效率越来越低。
  1. read uncommited：读未提交
     1. 产生的问题：脏读，不可重复读，幻读。
  2. read commited:读已提交（oracle默认）
     1. 产生的问题：不可重复读，幻读
  3. repeatable read：可重复读（MySQL默认）
     1. 产生的问题：幻读
  4. serializable：串行化（一个事务在操作一个表时，其它事务是不可以操作这个表，类似给这个表“加锁”）
     1. 可以解决所有问题。
* 数据库查询隔离级别：`select @@tx_isolation;`
* 数据库设置隔离级别：`set global transaction isolation level 级别字符串;`