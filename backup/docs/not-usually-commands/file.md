## 命令简介

file 命令用于查看指定文件的类型。

在Linux系统中，一切皆文件。这里就不得不提一下Linux系统中的文件类型：

```
普通文件 #属性信息表示为 - 
目录文件 #属性信息表示为 d
链接文件 #属性信息表示为 l
套接字文件 #属性信息表示为 s
字符设备文件 #属性信息表示为 b
块设备文件 #属性信息表示为 c
管道文件 #属性信息表示为 p
```

文件的属性信息在之前的文章： [每天学一个 Linux 命令（17）：chmod](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247506647&idx=3&sn=e141cc4838dd46f3f6f6bfe9a0ea862a&chksm=e918bfcbde6f36dd2be7ee6cdb118db02c4d49e4a7d5953f0c10fc9f290669f33f6e3b3dad17&scene=21#wechat_redirect) 中有介绍，文件类型信息一般都是位于文件权限信息之首的位置。

```
[root@centos7 testdir]# ll
total 0
lrwxrwxrwx 1 root root 11 Jan 15 22:50 cp -> /usr/bin/cp
drwxr-xr-x 2 root root 62 Jan  2 09:15 dir
-rw-r--r-- 1 root root  0 Jan  2 09:03 test2.txt
-rw-r--r-- 1 root root  0 Jan  2 08:57 test2.txt~
```

## 语法格式

```
file [选项] [文件名或目录名]
```

## 选项说明

```
-b：#列出结果，但不显示文件名称
-c：#详细显示指令执行过程
-L：#显示链接文件的源文件类型
-m<魔法数字文件>：#指定魔法数字文件
-v：#打印出版本信息
-z：#查看压缩文件的内容
```

## 应用举例

```
#查看文件类型
[root@centos7 testdir]# file cp
cp: symbolic link to `/usr/bin/cp`
[root@centos7 testdir]# file dir
dir: directory
[root@centos7 testdir]# file test2.txt
test2.txt: empty
[root@centos7 testdir]# file test2.txt~
test2.txt~: empty

#直接显示结果，不显示文件名
[root@centos7 testdir]# file -b dir
directory

#解读压缩文件的内容
[root@centos7 ~]# file -z httpd-2.4.46.tar.gz
httpd-2.4.46.tar.gz: POSIX tar archive (GNU) (gzip compressed data, was "httpd-2.4.46.tar", from Unix, last modified: Sat Aug  1 10:12:01 2020, max compression)
```