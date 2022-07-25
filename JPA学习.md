## JPA学习

[toc]



## 第一部分

### ORM思想

#### 建立目的

操作实体类就相当于操作数据库表

#### 两个映射关系

实体类和表的映射关系
实体类中属性和表中字段的映射关系

不再重点关注：sql语句

#### ORM框架

mybatis，hibernate

### hibernate框架介绍

Hibernate是一个开放源代码的对象关系映射框架，
		它对JDBC进行了非常轻量级的对象封装，
		它将POJO与数据库表建立映射关系，是一个全自动的orm框架

### JPA规范

Java 持久化API，是SUN公司推出的一套基于ORM的规范，内部是由一系列的接口和抽象类构成。

![1](C:\Users\Xlibi\Desktop\1.png)

### jpa基本操作-CRUD

#### 搭建环境的过程

* maven导入配置
* 配置jpa核心文件
* 编写实体类
* 完成映射关系--注解
* 保存信息到数据库

#### 完成基本CRUD

persist ： 保存
merge ： 更新
remove ： 删除
find/getRefrence ： 根据id查询

#### 常用注解

@Entity			标志实体
@Table			别名，默认为实体名

@Table(appliesTo = PPayModePromGoods.Schema.TABLE_NAME, indexes = {

  @Index(name = PPayModePromGoods.Schema.TABLE_NAME + "_x1", columnNames = {
      "owner" }) }) 

hibernate包下注解索引
@Id				必不可少 否则报错 指定主键

@GeneratedValue（strategy，generator） mysql支持identity、oracle支持sequence、auto默认自动选择、table通过表生成

@Column 标注的 columnDefinition 属性: 表示该字段在数据库中的实际类型 Date属性无法自动，String默认对应varchar

@Transient 		忽略映射	 自定义的getXX方法加上此注解  Spring环境下如果找不到对应属性会自动忽略

@Basic 		表示一个简单的属性到数据库表的字段的映射,对于没有任何标注的 getXxxx() 方法,默认即为@Basic

@Basic(fetch = FetchType.LAZY,optional = false)	懒加载、不允许为空

@Temporal(TemporalType.TIMESTAMP) 指定日期在数据库的类型 如date--年月日，timestamp年月日时分秒

@OrderBy 排序

@Enumerated(EnumType.STRING)指定枚举、varchar指定length  
number指定精度（columnDefinition = "decimal(20,10)" 或利用属性precision/scale）

@Embedded属性注解 标注对象	+@AttributeOverrides({@AttributeOverride})起别名

@Embeddable在上述标注类上 类注解 不生成表	

@Lob注解：表示属性将被持久化为Blob或者Clob类型, 具体取决于属性的类型,Java.sql.Clob, Character[],char[] 和 java.lang.String这些类型的属性都被持久化为Clob类型, 而java.sql.Blob,Byte[], byte[] 和 serializable类型则被持久化为Blob类型.

继承@MappedSuperclass注解的父类PStandardEntity（版本号@Version、时间、创建、最后修改）、PEntity(带uuid)

1.@MappedSuperclass注解使用在父类上面，是用来标识父类的作用

2.@MappedSuperclass标识的类表示其不能映射到数据库表，因为其不是一个完整的实体类，但是它所拥有的属性能够映射在     其子类对用的数据库表中

3.@MappedSuperclass标识得类不能再有@Entity或@Table注解  但是可以使用@Id 和@Column注解

#### 映射关系注解

@JoinColumn(name="CUSTOMER_ID") -----外键方

@ManyToOne(fetch=FetchType.LAZY) ------mappedby不和上面注解一起用	默认EAGER左外连接，懒加载获取时才查两次

@ManyToMany

@OneToOne

#### 实体状态

* 新建状态: 新创建的对象，尚未拥有持久性主键。 new没ID

* 游离状态：拥有持久化主键，但是没有与持久化建立上下文环境new 有ID
* 持久化状态：已经拥有持久性主键并和持久化建立了上下文环境
* 删除状态: 拥有持久化主键，已经和持久化建立上下文环境，但是从数据库中删除

#### 一对一、一对多、多对多：单向、双向

##### 单向

单向使用一边注解即可，无需mappby，多的一方获取少的一方默认是左外连接，区别于SpringData默认接口查询方法是懒加载

##### 双向

双向必须通过mappedBy指定关系维护端

###### 双向一对一

###### 双向一对多

###### 双向多对多

#### 二级缓存

ALL：所有的实体类都被缓存

NONE所有的实体类都不被缓存.

ENABLE_SELECTIVE：标识 @Cacheable(true) 注解的实体类将被缓存

DISABLE_SELECTIVE：缓存除标识 @Cacheable(false) 以外的所有实体类

UNSPECIFIED：默认值，JPA 产品默认值将被使用

~~~text
默认一级缓存同一个管理器内 相同sql只查一次 类比mybatis缓存同一session
开启二级缓存 不同管理器相同sql也只查一次  类比mybatis缓存不同session  前提是配置合理
~~~

#### Query接口的方法

* createQuery 全部属性、部分属性、where、orderby、groupby、外连接、子查询、多表、内建函数等 对象
*  createNamedQuery query定义在实体中 无需select 对象 
* createNativeQuery setHint 标准sql 
* createNativeQuery 带结果集参数 标准sql

#### JPA操作数据几种方式

* 继承接口默认的方式，不够通过通过Query接口自定义JPQL
* 使用JPA API 管理器操作
* 自定义JPQL语言sql的编写查删改 JPQL对实体操作不支持insert，对本地sql可以
* 自定义repository@PersistenceContext+管理器操作

#### JPQL复杂查询

查询实体类和类中的属性

类似sql查询

query对象执行jpql的对象

* 查询全部
* 分页查询
* 统计查询
* 条件查询
* 排序



## 第二部分-spring Data JPA



###  spring Data JPA 概述

![01-springDataJpa，jpa，hibernate关系](D:\My File\study\Spring Data\双元视频\day02\02-资料\01-springDataJpa，jpa，hibernate关系.png)

 

Spring Data JPA 是 Spring 基于 ORM 框架、JPA 规范的基础上封装的一套JPA应用框架，简化开发者对数据库的访问和操作。

### Spring Data JPA 特性

dao层中只需要写接口，就自动具有了增删改查、分页查询等方法

### Spring Data JPA 与 JPA和hibernate之间的关系

JPA是一套规范，内部是有接口和抽象类组成的。hibernate是一套成熟的ORM框架，而且Hibernate实现了JPA规范，hibernate为JPA的一种实现方式。

 Spring Data JPA是Spring提供的一套对JPA操作更加高级的封装，是在JPA规范下的专门用来进行数据持久化的解决方案。

### 编写符合规范的Dao层接口

* 创建一个Dao层接口，并实现**JpaRepository**和**JpaSpecificationExecutor**
* 提供相应的泛型

### 基本CRUD操作



### Spring Data JPA 实现过程

### Spring Data JPA 完整调用分析

![007](file:///C:/Users/Xlibi/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)



### Spring Data JPA 查询方式

#### 使用接口方法查询

#### 使用JPQL方式查询

**@Query**注解

**@Modifying**注解

#### 方法命名规则查询

Spring Data JPA 定义的规则，查询方法以findBy开头，涉及条件查询时，条件的属性用条件关键字连接，要注意的是：条件属性首字母需大写。框架在进行方法名解析时，会先把方法名多余的前缀截取掉，然后对剩下部分进行解析。

![image-20210825160742339](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20210825160742339.png)

具体关键字:

#### Specification动态查询

* 条件查询
* 分页查询

##### 方法及对应关系

| 方法名称                    | Sql对应关系           |
| --------------------------- | --------------------- |
| equle                       | filed =  value        |
| gt（greaterThan ）          | filed  > value        |
| lt（lessThan ）             | filed  < value        |
| ge（greaterThanOrEqualTo ） | filed  >= value       |
| le（ lessThanOrEqualTo）    | filed  <= value       |
| notEqule                    | filed  != value       |
| like                        | filed  like value     |
| notLike                     | filed  not like value |



#### 多表之间的关系和操作多表的操作步骤

#### 多表操作

