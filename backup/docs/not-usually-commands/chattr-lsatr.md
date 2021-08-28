## 命令简介

chattr 用来改变文件（扩展）属性。通常我们叫这个属性为特殊属性。

lsattr 查看文件扩展属性。

这种特殊属性有以下8种模式：

```
a #限定文件具有某种功能。这个对于日志文件非常有作用，比如，不允许删除，只允许向里面追加内容。
b #不更新或修改文件或目录的最后存储时间
c #将文件或目录压缩后存储
d #将文件或目录排除在倾倒操作之外
i #锁定文件或目录，不被更改
s #秘密删除文件或目录
S #动态实时更新文件或目录
u #防止文件或目录被意外删除
```

如果文件或目录被配置了上述8种之一的扩展属性，通过lsattr命令可以查看到：

```
[root@centos7 testdir]# lsattr
----i----------- ./dir
#结果说明这个目录被配置扩展属性
[root@centos7 testdir]# chattr -i dir
[root@centos7 testdir]# lsattr
---------------- ./dir
```

## 语法格式

```
chattr [选项] mode file
lsattr [选项] file
```

## 选项说明

chattr选项说明

```
-R  #递归处理，将目录下的所有文件及子目录都加上此扩展属性
-v<版本编号> #设置文件或目录版本号
-V  #显示指令执行过程；
+ <属性> #添加文件或目录的某个扩展属性
- <属性> #解除文件或目录的某个扩展属性
= <属性> #指定某个扩展性至指定的文件或目录
```

lsattr选项说明

```
-E  #显示属性的当前值
-D  #显示扩展属性的名称
-R  #递归
-V  #显示版本信息
-a  #列出目录下所有文件，包括隐藏文件
#注意-E -D -R三个选项是不可以一起使用的，它们是相互排斥的。
```

## 应用举例

```
#防止误删除的作用
[root@centos7 testdir]# chattr +a test2.txt
[root@centos7 testdir]# lsattr test2.txt
-----a---------- test2.txt
#不允许直接替换，只允许追加内容
[root@centos7 testdir]# echo "12345">test2.txt
-bash: test2.txt: Operation not permitted  

#查看文件或目录有没有扩展属性
[root@centos7 testdir]# echo "12345">>test2.txt
[root@centos7 testdir]# lsattr
---------------- ./dir
---------------- ./test2.txt~
-----a---------- ./test2.txt
lsattr: Operation not supported While reading flags on ./cp
```

这两个命令在日常工作也会常用到，锁定文件，或者当文件或系统出现故障时用于排查。

```
[root@centos7 testdir]# lsattr
---------------- ./dir
---------------- ./test2.txt~
----i----------- ./test2.txt
lsattr: Operation not supported While reading flags on ./cp
[root@centos7 testdir]# echo "12345">>test2.txt
-bash: test2.txt: Permission denied
```

比如上述情况，如果此文件是一个要实时存储数据的文件，被锁定了，那么就可能会引发应用运行故障，所以，这时就可以通过lsattr命令来查看与排查。