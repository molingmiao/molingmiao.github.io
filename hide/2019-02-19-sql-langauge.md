---
layout: post
title:  "SQL基础语句"
categories: SQL
tags: SQL
author: MLM
---

完整的创建数据库例子：

>create database db_test default character set utf8 collate utf8_general_ci;

>use db_test; 

>CREATE TABLE tb_user(

>id INT(10) NOT NULL AUTO_INCREMENT COMMENT"主键",

>name VARCHAR(20) NOT NULL COMMENT"姓名",

>age INT(3) DEFAULT 0,

>PRIMARY KEY(id)

>) COMMENT"用户表";

 

 

 

 

 

其他有关命令：
1,启动和关闭数据库

>net start mysql 

>net stop mysql 

所以命令必须是一行的第一个，并且以分号结尾：

All text commands must be first on line and end with ";" 

 

2,根据用户名密码，登录数据库

>mysql -uroot -p; 

如果数据库没有密码则使用

>mysql -uroot; 

 

3,查看在当前服务器中有多少个数据库

>show databases; 

 

4,删除某个数据库

>drop database databaseName; 

>commit; 

 

5,创建数据库

>CREATE DATABASE db_name DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

更改数据库的字符编码

ALTER DATABASE db_name DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

 

6,选择使用某个数据库

>use databaseName; 

 

7,查看数据库中有多少的表

 >show tables; 

 

8,创建表

>create table tableName( 

 id int(10) NOT NULL AUTO_INCREMENT,PRIMARY KEY(id),

name varchar(20)

); 

 

9,显示本数据库的所有表

>show tables;

 

10,显示某一个表

>show create table tableName;

 

11,显示表结构

>describe tableName;   (或者简写: desc tableName;)

 

12,向表中加入数据并查看

>insert into tableName(id,name...) values('1','admin',...); 

>select * from tableName; 

 

13,导入.sql文件(文件所在路径是F:\file.sql 

>source F:/file.sql; 

 

14,删除表

>drop table tableName; 

 

15,删除表中的所有数据，但是表结构依然存在

>delete from tableName; 

 

16,更新表中的数据,如果没有where，则将影响所有的记录

>update tableName set name='administrator' where id='1'; 

  

17,查看服务器版本和当前日期

>select version(),current_date; 

>select version(); 

 >select now(); 

 

18,把mysql作为一个简单的计算器

select pi(); 

>select pi()*10; 

 

19,查看用户

>select user(); 

 

20,使用load 

>load data local infile filePath into table tableName; 

 

 

一、连接MYSQL

格式: mysql -h主机地址-u用户名-p用户密码

 

1、例1:

连接到本机上的MYSQL

 

首先在打开DOS窗口，

然后进入目录mysqlbin，

再键入命令mysql -uroot -p，

回车后提示你输密码，如果刚安装好MYSQL，超级用户root是没有密码的，故直接回车即可进入到MYSQL中了，MYSQL的提示符是:mysql> 

 

2、例2:

连接到远程主机上的MYSQL。假设远程主机的IP为:110.110.110.110，用户名为root,密码为

abcd123。则键入以下命令: 

mysql -h110.110.110.110 -uroot -pabcd123 

(注:u与root可以不用加空格，其它也一样) 

 

3、退出MYSQL命令: exit (回车) 

 

 

二、修改密码。

 格式:mysqladmin -u用户名-p旧密码password 新密码

 

 1、例1:给root加个密码ab12。首先在DOS下进入目录mysqlbin，然后键入以下命令

 mysqladmin -uroot -password ab12 

 注:

因为开始时root没有密码，所以-p旧密码一项就可以省略了。

 

2、例2:再将root的密码改为djg345。

 mysqladmin -uroot -pab12 password djg345 

 

 

 

三、增加新用户。

(注意:

和上面不同，下面的因为是MYSQL环境中的命令，所以后面都带一个分号作为命令结束符) 

 

格式:grant select on 数据库.* to 用户名@登录主机identified by \"密码\" 

 

例1、增加一个用户test1密码为abc，让他可以在任何主机上登录，并对所有数据库有查

询、插入、修改、删除的权限。首先用以root用户连入MYSQL，然后键入以下命令: 

grant select,insert,update,delete on *.* to test1@\"%\" Identified by \"abc\"; 

 

 

 

但

例1增加的用户是十分危险的，你想如某个人知道test1的密码，那么他就可以在internet

上的任何一台电脑上登录你的mysql数据库并对你的数据可以为所欲为了，解决办法见例2。

 

例2、

增加一个用户test2密码为abc,让他只可以在localhost上登录，并可以对数据库mydb进行查询、插入、修改、删除的操作(localhost指本地主机，即MYSQL数据库所在的那台主机)

，这样用户即使用知道test2的密码，他也无法从internet上直接访问数据库，只能通过MYSQL主机上的web页来访问了。

grant select,insert,update,delete on mydb.* to test2@localhost identified by \"abc\"; 

 

 如果你不想test2有密码，可以再打一个命令将密码消掉。

grant select,insert,update,delete on mydb.* to test2@localhost identified by \"\"; 

 

 

在上篇我们讲了登录、增加用户、密码更改等问题。下篇我们来看看MYSQL中有关数据库方面的操作。

注意:

你必须首先登录到MYSQL中，以下操作都是在MYSQL的提示符下

 

 

 

alter命令

alter add命令用来增加表的字段。
alter add命令格式：alter table 表名 add字段 类型 其他;
例如，在表MyClass中添加了一个字段passtest，类型为int(4)，默认值为0：
   mysql> alter table MyClass add passtest int(4) default '0';

添加两个字段：   mysql> alter table Person add age int,add address varchar(11); 

删除两个字段：   mysql> alter table Person drop column age,drop column address;

修改字段的注释:  mysql> ALTER TABLE `student` MODIFY COLUMN `id` COMMENT '学号';

 

1) 加索引
   mysql> alter table 表名 add index 索引名 (字段名1[，字段名2 …]);
例子： mysql> alter table employee add index emp_name (name);
2) 加主关键字的索引
    mysql> alter table 表名 add primary key (字段名);
例子： mysql> alter table employee add primary key(id);
3) 加唯一限制条件的索引
   mysql> alter table 表名 add unique 索引名 (字段名);
例子： mysql> alter table employee add unique emp_name2(cardnumber);
4) 删除某个索引
   mysql> alter table 表名 drop index 索引名;
例子： mysql>alter table employee drop index emp_name;
5) 增加字段
    mysql> ALTER TABLE table_name ADD field_name field_type;
6) 修改原字段名称及类型
    mysql> ALTER TABLE table_name CHANGE old_field_name new_field_name field_type;
7) 删除字段
    MySQL ALTER TABLE table_name DROP field_name;

 

 

MySQL添加用户、删除用户与授权

MySql中添加用户,新建数据库,用户授权,删除用户,修改密码(注意每行后边都跟个;表示一个命令语句结束):

1.新建用户

　　1.1 登录MYSQL：

　　@>mysql -u root -p

　　@>密码

　　1.2 创建用户：

　　mysql> insert into mysql.user(Host,User,Password) values("localhost","test",password("1234"));

　　这样就创建了一个名为：test 密码为：1234 的用户。

　　注意：此处的"localhost"，是指该用户只能在本地登录，不能在另外一台机器上远程登录。如果想远程登录的话，将"localhost"改为"%"，表示在任何一台电脑上都可以登录。也可以指定某台机器可以远程登录。

　　1.3 然后登录一下：

　　mysql>exit;

　　@>mysql -u test -p

　　@>输入密码

　　mysql>登录成功

 

2.为用户授权

　　授权格式：grant 权限 on 数据库.* to 用户名@登录主机 identified by "密码";　

　　2.1 登录MYSQL（有ROOT权限），这里以ROOT身份登录：

　　@>mysql -u root -p

　　@>密码

　　2.2 首先为用户创建一个数据库(testDB)：

　　mysql>create database testDB;

　　2.3 授权test用户拥有testDB数据库的所有权限（某个数据库的所有权限）：

　　 mysql>grant all privileges on testDB.* to test@localhost identified by '1234';

 　　mysql>flush privileges;//刷新系统权限表

　　格式：grant 权限 on 数据库.* to 用户名@登录主机 identified by "密码";　

　　2.4 如果想指定部分权限给一用户，可以这样来写:

　　mysql>grant select,update on testDB.* to test@localhost identified by '1234';

　　mysql>flush privileges; //刷新系统权限表

　　2.5 授权test用户拥有所有数据库的某些权限： 　 

　　mysql>grant select,delete,update,create,drop on *.* to test@"%" identified by "1234";

     //test用户对所有数据库都有select,delete,update,create,drop 权限。

　 //@"%" 表示对所有非本地主机授权，不包括localhost。（localhost地址设为127.0.0.1，如果设为真实的本地地址，不知道是否可以，没有验证。）

　//对localhost授权：加上一句grant all privileges on testDB.* to test@localhost identified by '1234';即可。

 

3. 删除用户

 　　@>mysql -u root -p

　　@>密码

 　　mysql>Delete FROM user Where User='test' and Host='localhost';

 　　mysql>flush privileges;

 　　mysql>drop database testDB; //删除用户的数据库

删除账户及权限：>drop user 用户名@'%';

　　　　　　　　>drop user 用户名@ localhost; 

 

4. 修改指定用户密码

  　　@>mysql -u root -p

  　　@>密码

  　　mysql>update mysql.user set password=password('新密码') where User="test" and Host="localhost";

  　　mysql>flush privileges;

 

5. 列出所有数据库

　　mysql>show database;

 

6. 切换数据库

　　mysql>use '数据库名';

 

7. 列出所有表

　　mysql>show tables;

 

8. 显示数据表结构

　　mysql>describe 表名;

 

9. 删除数据库和数据表

　　mysql>drop database 数据库名;

　　mysql>drop table 数据表名;