### shiro框架

[toc]



####  shiro架构

![image-20220618200447307](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220618200447307.png)

三层：

* subject：直接交互的对象,用户。
* securitymanager：管理所有用户。
* realm：连接数据。

#### 开始

导入依赖

配置文件

helloworld

![image-20220618215559250](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220618215559250.png)

#### Spring boot集成

shiroconfiguration配置

3.shiroFilterFactoryBean：bean添加入SecurityManager，设置安全管理器。添加内置过滤器。

​	**anon**：无需认证

​	**authc**：认证访问

​	**user**：拥有记住我才可访问

​	**perms**：对某个资源的权限才可访问

​	**role**：拥有某个角色权限才可访问

2.DafultWebSecurityManager：关联Realm类

1.创建 realm 对象：自定义 Realm 类继承 AutorizingRealm 重写方法。授权（AuthorizationInfo），认证（AuthenticationInfo）两个方法。

#### 登录拦截

shiroconfiguration 中 shiroFilterFactoryBean 创建 LinkedHashMap 类型 filtemap 设置拦截类型，设置登录请求。

#### 登录认证

  Realm 类 AuthenticationInfo 方法。使用subject获取当前用户，UsernamePasswordToken 封装登陆数据，subject.login 验证token。

shiro自行密码认证

#### 整合Mybatis

加密MD5加密，MD5盐值加密

#### 请求授权

​	**anon**：无需认证

​	**authc**：认证访问

​	**user**：拥有记住我才可访问

​	**perms**：对某个资源的权限才可访问

​	**role**：拥有某个角色权限才可访问

设置未授权请求。

Realm 类 AuthorizationInfo 方法，设置SimpleAuthorizationInfo类型info对象，subject.getPrincipal 获取用户信息，根据用户添加权限。

#### 整合thymeleaf

根据权限加载前端页面

 **导入整合包**

**配置shiroDialect****：配置类中整合shiro ，thymeleaf

**前端配置shiro:hasPermission**

