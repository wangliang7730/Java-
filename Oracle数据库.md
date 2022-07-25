![image-20220701152052786](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220701152052786.png)

#### 创建表空间

表空间？ORACLE数据库的逻辑单元。数据库——表空间 一个表空间可以与多个数据文件（物理结构）关联

一个数据库下可以建立多个表空间，一个表空间可以建立多个用户、一个用户下可以建立多个表。

~~~sql
create tablespace itcast 

datafile 'c:\itcast.dbf' size 100m

autoextend on 

next 10m
~~~

itcast 为表空间名称

datafile 指定表空间对应的数据文件size 后定义的是表空间的初始大小

next 后指定的是一次自动增长的大小。

autoextend on自动增长，当表空间存储都占满时，自动增长