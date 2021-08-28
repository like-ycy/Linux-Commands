## 命令简介

find 命令在文件系统中搜索文件和目录。

find 命令用来在指定目录下查找文件，在参数之前的任何字符串都会当作是目录名。使用 find 命令时，如何不设置任何参数，则 find 命令将在当前目录下查找子目录与文件，并且将查找到的子目录和文件全部显示出来。

find 还是一个功能非常强大的用于处理 Linux 系统上文件的工具，它可以单独查找文件，也可以与其他程序（命令）结合对需要处理的文件进行操作。

## 补充说明

Linux文件类型：

```
f #普通文件
l #符号连接
d #目录
c #字符设备
b #块设备
s #套接字
p #Fifo
```

UNIX/Linux文件系统中的每个文件都有三种时间戳：

- 访问时间 （-atime/天，-amin/分钟）：用户最近一次访问时间。
- 修改时间 （-mtime/天，-mmin/分钟）：文件最后一次被修改的时间。
- 变化时间 （-ctime/天，-cmin/分钟）：文件元数据（例如权限等）

## 语法格式

```
find [目录路径] [选项] [文件名]
find [-H] [-L] [-P] [-D debugopts] [-Olevel] [path...] [expression]
```

## 选项说明

```
-amin<分钟>：#查找在指定时间内被存取过的文件或目录，单位分钟
-mmin<分钟>：#查找在指定时间内被更改过的文件或目录，单位分钟
-mtime<24小时数>：#查找在指定时间内被更改过的文件或目录，单位24小时
-atime<24小时数>：#查找在指定时间被写入过的文件或目录，单位24小时
-cmin<分钟>：#查找在指定时间之内被更改过的文件或目录
-ctime<24小时数>：#查找在指定时间之时被更改的文件或目录，单位以24小时计算
-daystart：#从今天开始计算时间
-depth：#从指定目录下最深层的子目录开始查找
-exec<执行指令>：#如果find命令返回值为True，就执行该指令
-false：#将find命令返回值都设为False
-fstype<文件系统类型>：#只查找此指定文件系统类型下的文件或目录
-gid<群组识别码>：#查找匹配此群组识别码的文件或目录
-group<群组名称>：#查找匹配此群组名称的文件或目录
-help或——help：#帮助信息
-links<连接数目>：#查找匹配指定的硬连接数目的文件或目录
-maxdepth<目录层级>：#设置查找的最大目录层级
-mindepth<目录层级>：#设置查找的最小目录层级
-name<范本样式>：#指定字符串作为寻找文件或目录的范本
-path<范本样式>：#指定字符串作为寻找目录的范本样式
-perm<权限数值>：#查找符合指定的权限数值的文件或目录
-size<文件大小>：#查找符合指定的文件大小的文件
-true： #将find命令返回值都设为True
-type<文件类型>：#只查找匹配指定的文件类型的文件
-uid<用户识别码>：#只查找匹配指定的用户识别码的文件或目录
-user<拥有者名称>：#只查找匹配指定的拥有者名称的文件或目录
-version：#显示版本信息
```

## 应用举例

当前目录搜索所有文件，文件内容包含 “192.168.1.111” 的内容

```
find . -type f -name "*" | xargs grep "192.168.1.111"
```

根据文件或者正则表达式进行匹配，查找需要的文件或目录

```
#列出当前目录及子目录下所有文件和文件夹
[root@centos7 ~]# find .
 
#在/mingongge目录下查找包含mingongge开头的文件名
[root@centos7 ~]# find /mingongge -name "mingongge*.log"
/mingongge/mingongge_errors.log
/mingongge/mingongge.log
/mingongge/mingongge_test.log
 
#当前目录及子目录下查找所有以.txt和.log结尾的文件
[root@centos7 ~]# find . \( -name "*.txt" -o -name "*.log" \) 
或
[root@centos7 ~]# find . -name "*.txt" -o -name "*.log"
 
#匹配文件路径或者文件
[root@centos7 ~]# find /usr/ -path "*txt*"
 
#基于正则表达式匹配文件路径
[root@centos7 ~]# find . -regex ".*\(\.txt\|\.log\)$"
 
#忽略大小写
[root@centos7 ~]# find . -iregex ".*\(\.txt\|\.log\)$"
```

find 否定参数用法举例

```
#找出/mingongge下不是以.log结尾的文件
[root@centos7 ~]# find /mingongge ! -name "*.log"
```

基于目录深度搜索

```
#向下最大深度限制为5
[root@centos7 ~]# find . -maxdepth 5 -type f
 
#搜索出深度距离当前目录至少3个子目录的所有文件
[root@centos7 ~]# find . -mindepth 3 -type f
```

根据文件时间戳进行查找

```
#查找最近10天内被访问过的所有文件
[root@centos7 ~]# find . -type f -atime -10
 
#查找超过10天内被访问过的所有文件
[root@centos7 ~]# find . -type f -atime +10
 
#查找访问时间超过20分钟的所有文件
[root@centos7 ~]# find . -type f -amin +20
 
#找出比mingongge修改时间更长的所有文件
[root@centos7 ~]# find . -type f -newer mingongge
```

删除查找到的匹配文件

```
#删除当前目录下所有.txt文件
[root@centos7 ~]# find . -type f -name "*.txt" -delete
```

根据文件权限/所有权进行匹配：

```
#当前目录下找出权限为777的文件
[root@centos7 ~]# find . -type f -perm 777#找出当前目录下所有者是mingongge的所有文件
[root@centos7 ~]# find . -type f -user mingongge
 
#找出当前目录下用户组为mingongge的所有文件
[root@centos7 ~]# find . -type f -group mingongge #找出当前目录下权限不是644的.log文件
[root@centos7 ~]# find . -type f -name "*.log" ! -perm 644
```

find 和 -exec 选项结合使用

```
#找出当前目录下所有者为root的文件，并把所有者更改为mingongge这个用户
[root@centos7 ~]# find .-type f -user root -exec chown mingongge {} \;
 
#找出当前用户家目录下所有的.log文件并执行删除动作
[root@centos7 ~]# find $HOME/. -name "*.log" -exec rm {} \;
 
#查找当前目录下所有.log文件并将他们拼接起来然后写入到mingongge.txt这个文件中
[root@centos7 ~]# find . -type f -name "*.log" -exec cat {} \;> /mingongge.txt
 
#查找出10天前的.log文件，然后全部移动到mingongge目录下
[root@centos7 ~]# find . -type f -mtime +10 -name "*.log" -exec cp {} mingongge \;
 
#找出当前目录下所有.log文件，然后以“File:文件名”的格式打印输出到屏幕上
[root@centos7 ~]# find . -type f -name "*.log" -exec printf "File: %s\n" {} \;
```

根据文件大小来查找目标文件

```
#查找当前目录下文件大小超过500M的文件
[root@centos7 ~]# find . -type f -size +500M     
./mingongge/backup_file.tar.gz
./mingongge/upload.tar.gz
 
#查找当前目录超过500M的文件，并打印出文件的详细属性信息
[root@centos7 ~]# find . -type f -size +800M  -print0 | xargs -0 ls -l         
-rw-r--r-- 1 root root  4250099200 Apr 15  2019 ./mingongge/backup_file.tar.gz
-rw-r--r-- 1 root root 6832225765 Oct 14 12:57 ./mingongge/upload.tar.gz
 
#查找当前目录超过500M的文件，并打印出文件的具体大小
[root@centos7 ~]# find . -type f -size +500M  -print0 | xargs -0 du -h|sort -nr
6.8G    ./mingongge/upload.tar.gz
4G     ./mingongge/backup_file.tar.gz
```

查找系统中前5的大文件

```
# find / -type f -print0 | xargs -0 du -h | sort -rh | head -n 5
1.1G    /download/ubuntu-17.04-desktop-amd64.iso
377M    /download/app_backup.tar.gz
100M    /usr/lib/x86_64-linux-gnu/libOxideQtCore.so.0
93M /usr/lib/firefox/libxul.so
84M /var/lib/snapd/snaps/core_3604.snap
```

方法有很多种，都需要与其它命令配合使用，才能查找出来。

find 命令在文件查找及其它的应用方面具有强大的功能，学习系统命令，find 命令是需要重点掌握的，不管是平时的学习，还是日后工作中，这个命令都有着非常重要的作用。