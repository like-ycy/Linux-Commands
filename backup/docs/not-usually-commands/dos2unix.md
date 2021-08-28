## 命令简介

dos2unix 命令用于将纯文本文件从 DOS 或 Mac 格式转换为 Unix。DOS 下的文本文件是以 \r\n 作为换行符，而 Unix 下的文本文件是以 \n 作为换行符。

默认系统是没有安装这个命令，需要用户自行安装：

```
[root@centos7 ~]# dos2unix test.txt 
-bash: dos2unix: command not found
 
#CentOS/RHEL 安装
[root@centos7 ~]# yum install -y dos2unix

#Debian/Ubuntu 安装
[root@centos7 ~]# apt-get install dos2unix
```

## 语法格式

```
dos2unix [选项] [文件]
dos2unix [OPTION] [FILE]
```

## 选项说明

```
-k  #输出文件的日期不变
-q  #安静模式
-V  #查看版本
-c  #转换模式，模式有：ASCII, 7bit, ISO, Mac, 默认是：ASCII。
-o  #写入到源文件
-n  #写入到新文件
```

## 应用举例

最简单的用法

```
[root@centos7 ~]# dos2unix test.txt 
dos2unix: converting file test.txt to Unix format ...
```

一次转换多个文件（注：也可以加上 -o 参数，也可以不加，效果一样）

```
[root@centos7 ~]# dos2unix test.txt mingongge.file 
dos2unix: converting file test.txt to Unix format ...
dos2unix: converting file mingongge.file to Unix format ...
[root@centos7 ~]# dos2unix -o test.txt mingongge.file 
dos2unix: converting file test.txt to Unix format ...
dos2unix: converting file mingongge.file to Unix format ...
```

转换时保持源文件不变（默认是直接修改源文件），可以使用 -n 参数

```
[root@centos7 ~]# ll test.txt 
-rw-r--r-- 1 root root 140 Jan 16 11:32 test.txt
[root@centos7 ~]# dos2unix -n test.txt dos_test.txt
dos2unix: converting file test.txt to file dos_test.txt in Unix format ...
[root@centos7 ~]# ll test.txt 
-rw-r--r-- 1 root root 140 Jan 16 11:32 test.txt
[root@centos7 ~]# ll dos_test.txt 
-rw-r--r-- 1 root root 140 Jan 16 11:34 dos_test.txt
```

如果要保持文件时间戳不变，加上 -k 参数

```
[root@centos7 ~]# ll
total 21892
-rw-r--r--   1 root root      140 Jan 16 11:34 dos_test.txt
-rw-r--r--   1 root root        0 Jan 16 11:32 mingongge.file
drwxr-xr-x   3 root root      210 Jan 16 10:19 testdir
-rw-r--r--   1 root root      140 Jan 16 11:32 test.txt
[root@centos7 ~]# dos2unix dos_test.txt
dos2unix: converting file dos_test.txt to Unix format ...
[root@centos7 ~]# ll
total 21892
-rw-r--r--   1 root root      140 Jan 16 11:36 dos_test.txt
-rw-r--r--   1 root root        0 Jan 16 11:32 mingongge.file
drwxr-xr-x   3 root root      210 Jan 16 10:19 testdir
-rw-r--r--   1 root root      140 Jan 16 11:32 test.txt
#可以看出默认是改变了文件的时间戳信息

[root@centos7 ~]# dos2unix -k test.txt
dos2unix: converting file test.txt to Unix format ...
[root@centos7 ~]# dos2unix -k dos_test.txt mingongge.file
dos2unix: converting file dos_test.txt to Unix format ...
dos2unix: converting file mingongge.file to Unix format ...
[root@centos7 ~]# ll
total 21892
-rw-r--r--   1 root root      140 Jan 16 11:36 dos_test.txt
-rw-r--r--   1 root root        0 Jan 16 11:32 mingongge.file
drwxr-xr-x   3 root root      210 Jan 16 10:19 testdir
-rw-r--r--   1 root root      140 Jan 16 11:32 test.txt
```