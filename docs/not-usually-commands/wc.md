## 命令简介

wc 命令用来统计文件中的行数、单词数或字节数，然后将结果输出在终端上。我们可以使用 wc 命令来计算文件的Byte数、字数或是列数。

## 语法格式

```
wc [选项] [文件]
wc [OPTION] [FILE]
```

## 选项说明

```
-c #统计字节数
-l #统计行数
-m #统计字符数
-w #统计字数
-L #显示最长行的长度
-help     #显示帮助信息
--version #显示版本信息
```

## 应用举例

查看文件的字节数、字数、行数

```
[root@centos7 ~]# wc test.txt 
  6  34 140 test.txt
[root@centos7 ~]# wc mingongge.file 
0 0 0 mingongge.file
[root@centos7 ~]# wc -L test.txt 
29 test.txt
[root@centos7 ~]# wc -m test.txt 
140 test.txt
[root@centos7 ~]# wc -l test.txt 
6 test.txt
[root@centos7 ~]# wc -c test.txt 
140 test.txt
```

统计当前目录下的所有文件行数及总计行数

```
[root@centos7 ~]# wc -l *
      48 anaconda-ks.cfg
wc: goinception: Is a directory
       0 goinception
   45222 goInception-linux-amd64-v1.2.3.tar.gz
wc: httpd-2.4.46: Is a directory
       0 httpd-2.4.46
   36246 httpd-2.4.46.tar.gz
       0 mingongge.file
wc: testdir: Is a directory
       0 testdir
       6 test.txt
   81522 total
```

配合命令输出结果来统计

```
[root@centos7 ~]# ls -l |wc -l
9
[root@centos7 ~]# ls -l
total 21888
-rw-------.  1 root root     1320 Aug 20 10:39 anaconda-ks.cfg
drwxr-xr-x   3 root root       39 Aug 30 03:48 goinception
-rw-r--r--   1 root root 13034487 Aug 30 03:42 goInception-linux-amd64-v1.2.3.tar.gz
drwxr-sr-x  11 root   40     4096 Dec 24 22:35 httpd-2.4.46
-rw-r--r--   1 root root  9363314 Aug  5 07:32 httpd-2.4.46.tar.gz
-rw-r--r--   1 root root        0 Jan  2 08:43 mingongge.file
drwxr-xr-x   3 root root      210 Jan 16 10:19 testdir
-rw-r--r--   1 root root      140 Jan 16 10:30 test.txt
```