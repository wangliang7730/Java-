## Docker

[toc]

### docker安装

1.运行以下命令，安装Docker存储驱动的依赖包

~~~
dnf install -y device-mapper-persistent-data lvm2
~~~

2.运行以下命令，添加稳定的Docker软件源。

~~~
dnf config-manager --add-repo=https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
~~~

3.运行以下命令，查看已添加的Docker软件源。

~~~
dnf list docker-ce
~~~

正确的返回示例如下。

~~~
docker-ce.x86_64        3:19.03.13-3.el7        docker-ce-stable
~~~

4.运行以下命令安装Docker

~~~
dnf install -y docker-ce --nobest
~~~

5.运行以下命令启动Docker。

~~~
systemctl start docker
~~~

6.查看Docker运行状态

~~~
systemctl status docker
~~~

7.查看Docker版本信息

~~~
docker version
~~~

**错误1*

安装Docker出现 package docker-ce-3:19.03.13-3.el7.x86_64 requires containerd.io ＞= 1.2.2-3

解决：centos8默认使用podman代替docker，所以需要containerd.io.
安装co

~~~
yum install https://download.docker.com/linux/fedora/30/x86_64/stable/Packages/containerd.io-1.2.6-3.3.fc30.x86_64.rpm
~~~

安装docker报错：错误：事务检查错误

安装docker会与podman有冲突，这个在上面的大段错误信息中也有描述到。

通过rpm -q podman命令查看本地环境中的podman信息

~~~
[root@wuwl ~]# rpm -q podman
~~~

卸载podman，dnf remove podman

~~~
[root@wuwl ~]# dnf remove podman
~~~

重新安装docker

**DevOps=文化+过程+工具**

### 基本概念

镜像(Image)

容器(Container)

仓库(Repository)

### 容器技术简介

old项目部署：部署慢，成本高，资源浪费，难于迁移和扩展，限定硬件厂商

解决----虚拟化技术

![image-20220726141443850](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220726141443850.png)

一个物理机可以部署多个app，每个app单独VM里

资源池

易扩展

容易云化

容器：开发运维之间桥梁。对软件机器依赖的标准化打包，应用之间相互隔离。

容器和虚拟机的区别

![image-20220726145059739](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220726145059739.png)

### Docker的架构和底层技术

提供一个开发，打包，运行app平台，app与底层infrastructure隔离开来

![image-20220726165929281](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220726165929281.png)

#### Docker Engine

后台进程（dockerd）

REST API Server

CLI接口(docker)

![image-20220726170247005](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220726170247005.png)

#### 底层技术支持

Namespaces：做隔离id，net，ipc，mnt，uts

Control group：做资源限制

Union file systems：Container和image的分层

#### 镜像(Image)

文件和meta data的集合

分层的，每一层可以添加，删除

不同的image共享layer

Lmage本身是read-only的

##### Image获取

* Build from Dockerfile

![image-20220727132847498](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727132847498.png)

![image-20220727132857212](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727132857212.png)

* Pull from Registry

![image-20220727133143796](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727133143796.png)

~~~
docker pull xxx：xx
~~~



#### 容器(Container)

通过Image创建

在Image layer之上建立container layer(可读写)

类比：类和实例

Image负责app存储和分发，container负责运行

~~~
docker container ls
docker container ls -a
docker run xxx
docker run -it xxx
docker rm
docker rmi
docker ps
~~~

~~~
docker container commit 简写 docker commit
~~~

~~~
docker image build简写
docker build
~~~

##### Dockerfile语法

* FROM

FROM scratch

FROM centos

* LABEL

![image-20220727145543622](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727145543622.png)

RUN

![image-20220727145601954](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727145601954.png)

WROKDIR

![image-20220727145701834](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727145701834.png)

ADD和COPY

![image-20220727145842536](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727145842536.png)

![image-20220727150006351](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727150006351.png)

ENV

![image-20220727150037505](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727150037505.png)

尽量使用ENV增加可维护性

VOLUME and EXPOSE

CMD and EXTRYPOINT

![image-20220727150706697](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727150706697.png)

##### shell和Exec格式

![image-20220727152426955](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727152426955.png)

![image-20220727152639447](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727152639447.png)

##### CMD

![image-20220727170452746](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727170452746.png)

##### ENTRYPOINT

![image-20220727170629640](C:\Users\Xlibi\AppData\Roaming\Typora\typora-user-images\image-20220727170629640.png)
