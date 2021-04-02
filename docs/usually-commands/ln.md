## 命令简介

ln 命令用于创建（软/硬）链接文件。

在linux系统中，有两种链接类型：硬链接与软件，默认创建的就是硬链接，创建软链接需要-s选项来配合完成。

**硬链接文件**是指通过索引节点来进行链接，在Linux系统中多个文件同时指向同一个索引节点，这种情况下的文件被称为硬链接文件。

**软链接文件**也称做符号链接（同Windows系统中快捷方式）。实际上它是一个文本文件，文本文件里存储着指向源文件链接的位置信息。

## 命令格式

```
ln [选项] [链接文件名]
ln [OPTION] [LINKNAME]
```

## 选项说明

```
-b #创建备份文件
-f #强行删除任何已存在的目标文件
-i #覆盖现有文件前先询问用户
-s #给一个文件创建软链接
-v #打印每个链接文件的名称
--help     #打印帮助信息后退出
--version  #打印版本信息后退出
```

## 应用举例

```
#在当前目录中创建硬链接
[root@centos7 testdir]# ln test2.txt test3
[root@centos7 testdir]# ls -li test*
50342754 -rw-r--r-- 2 root root 6 Jan 16 02:47 test2.txt
50342754 -rw-r--r-- 2 root root 6 Jan 16 02:47 test3
#从结果可以看出硬链接文件与源文件的inode号一样

#在当前目录中创建软链接
[root@centos7 testdir]# ln -s test2.txt test4
[root@centos7 testdir]# ls -li test*
50342754 -rw-r--r-- 2 root root 6 Jan 16 02:47 test2.txt
50342754 -rw-r--r-- 2 root root 6 Jan 16 02:47 test3
50342753 lrwxrwxrwx 1 root root 9 Jan 16 03:57 test4 -> test2.txt
#从结果可以看出，软链接与源文件的inode号不一样

#创建源文件test2.txt的软件链接文件名为test3，如果test3存，则将其改名为test3~
[root@centos7 testdir]# ln -s -b test2.txt test3
[root@centos7 testdir]# ls -li test*
50342754 -rw-r--r-- 2 root root 6 Jan 16 02:47 test2.txt
50342767 lrwxrwxrwx 1 root root 9 Jan 16 04:06 test3 -> test2.txt
50342754 -rw-r--r-- 2 root root 6 Jan 16 02:47 test3~
50342753 lrwxrwxrwx 1 root root 9 Jan 16 03:57 test4 -> test2.txt
```

基础入门必备命令之一，非常简单易学，掌握这些就够了。