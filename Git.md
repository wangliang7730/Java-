# Git

### 原理

git是一套内容寻址的文件系统，存储key-value键值对，根据key值来查找value------指针

### 三个对象

commit对象，tree对象和blob对象

#### commit

commit对象则记录了每次提交到本地仓库的文件快照

多次提交，形成链表



#### tree

tree对象则记录了文件快照中各个目录和文件的结构关系，它指向被跟踪的快照

类似于树

#### blob

blob对象对应的就是文件快照中那些发生变化的文件内容

### 提交流程

![img](https://img-blog.csdn.net/20140417113336421)

#### 补充

git status

git log

