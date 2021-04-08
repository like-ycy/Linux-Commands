## 命令简介

touch 命令用来创建新的空文件。touch命令也可以用来修改文件时间戳。如果该文件不存在，则创建具有该名称的空文件。

**与文件关联的时间戳**

```
Access time        #上次读取文件的时间，简称atime
Modification time  #最后一次修改文件的内容，简称mtime
Change time        #上次更改文件的元数据（称为“状态”）。状态信息包括文件的权限及其时间戳。每当文件发生任何事件时，其状态的至少一个元素都会更改，并且其ctime将设置为当前系统时间。简称ctime
```

atime和mtime是文件状态元数据的一部分。因此，当更改文件的atime（-a）或mtime（-m）时，其ctime会自动设置为当前时间。**无法手动设置 ctime**。

## 命令语法

```
touch [选项] [文件名]
touch [option] [filename]
```

## 选项说明

```
-a：或--time=atime或--time=access或--time=use  #只更改读取时间
-c：或--no-create  #不建立任何文件
-d：<时间日期> #更改文件的修改时间，使用指定的日期时间，而非现在的时间
-h,--no-dereference #如果file是符号链接并且指定了此选项，则touch将修改符号链接的时间戳，而不是其引用的文件。 如果未指定此选项，则在进行修改之前触摸将取消引用符号链接。此选项意味着-c：如果文件不存在，则不会创建任何内容。
-f：#此参数将忽略不予处理，仅负责解决BSD版本touch指令的兼容性问题；
-m：或--time=mtime或--time=modify  #只更该变动时间；
-r：<参考文件或目录>  #把指定文件或目录的日期时间，统统设成和参考文件或目录的日期时间相同；
-t：<日期时间>  #使用指定的日期时间，而非现在的时间；
--help：       #在线帮助；
--version：    #显示版本信息。
```

## 应用举例

创建新文件

```
[root@centos7 testdir]# touch testfile
[root@centos7 testdir]# ls -l
total 0
-rw-r--r-- 1 root root 0 Jan  2 07:55 testfile
```

如果创建文件时，此文件存在，则会修改这个文件的其访问，修改和更改时间（atime，mtime和ctime）设置为当前系统时间。

```
[root@centos7 testdir]# date
Sat Jan  2 07:57:00 EST 2021
[root@centos7 testdir]# touch testfile
[root@centos7 testdir]# ls -l
total 0
-rw-r--r-- 1 root root 0 Jan  2 07:57 testfile
```

修改文件的atime与mtime

```
[root@centos7 testdir]# touch -d "25 Feb" testfile
[root@centos7 testdir]# ls -l
total 0
-rw-r--r-- 1 root root 0 Feb 25  2021 testfile
```

复制文件访问时间，把另一个文件的访问时间直接赋予到新创建的文件上

```
[root@centos7 testdir]# touch -r testfile filetest
[root@centos7 testdir]# ls -l
total 0
-rw-r--r-- 1 root root 0 Feb 25  2021 filetest
-rw-r--r-- 1 root root 0 Feb 25  2021 testfile
```

touch命令和mkdir命令功能相同，都是用来创建文件或目录所用，touch命令的功能稍多一些，也都是Linux上的基础必备命令。