## 命令简介

mkdir 命令用于创建新目录。创建目录时，如果目录名前没有指定路径，那么就直接在当前工作目录下创建新的目录。如指定了路径，那么就会在这个指定的目录下创建一个新目录。

创建目录是需要注意，你所创建的目录名与当前目录下的文件名没有重名，如果有重名，系统会出现如下的提示，无法创建成功。

```
[root@centos7 test]# ls -l
total 0
-rw-r--r-- 1 root root 0 Jan  2 07:06 test
[root@centos7 test]# mkdir test
mkdir: cannot create directory ‘test’: File exists
```

## 命令语法

```
mkdir [选项] [目录名]
mkdir [option] [directory]
```

## 选项说明

```
-m，--mode=模式 #设定权限<模式>（类似 chmod）
-p，--parents #可以是一个路径名称，递归创建目录，可以创建目录路径不存在的目录，即一次可以建立多个目录;
-v，--verbose #显示创建目录的创建过程信息
--help #显示帮助信息并退出
--version #输出版本信息并退出
```

## 应用举例

创建新目录（一个目录）

```
[root@centos7 ~]# mkdir testdir
[root@centos7 ~]# ls -l
total 21884
-rw-------.  1 root root     1320 Aug 20 10:39 anaconda-ks.cfg
drwxr-xr-x   2 root root        6 Jan  2 07:12 testdir
```

一次创建多个目录

```
[root@centos7 ~]# cd testdir
[root@centos7 testdir]# ls
[root@centos7 testdir]# mkdir test1 test2 test3 test4
[root@centos7 testdir]# ls
test1  test2  test3  test4

[root@centos7 testdir]# mkdir -p test6/{1..5}
[root@centos7 testdir]# tree test6
test6
├── 1
├── 2
├── 3
├── 4
└── 5

5 directories, 0 files
```

递归创建目录，当上一级目录不存在时，需要使用递归参数

```
[root@centos7 testdir]# mkdir test5/test
mkdir: cannot create directory ‘test5/test’: No such file or directory
[root@centos7 testdir]# mkdir -p test5/test
[root@centos7 testdir]# tree
.
├── test1
├── test2
├── test3
├── test4
└── test5
    └── test

6 directories, 0 files
```

创建目录时，并配置其权限

```
#创建的新目录，默认权限是755
[root@centos7 test5]# ll
total 0
drwxr-xr-x 2 root root 6 Jan  2 07:16 test
[root@centos7 test5]# mkdir -m 777 test1
[root@centos7 test5]# ll
total 0
drwxr-xr-x 2 root root 6 Jan  2 07:16 test
drwxrwxrwx 2 root root 6 Jan  2 07:38 test1
```

mkidr命令在日常的使用过程，基本上都是创建目录，没有其它常用的用途。所以，这个命令掌握起来也比较简单，易学、易上手。