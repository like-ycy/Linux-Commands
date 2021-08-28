## 命令简介

pwd (print working directory)显示用户当前工作目录的绝对路径。

pwd 命令将当前用户的工作目录的全路径名称（从根目录）以绝对路径的方式标准输出在屏幕上。

## 语法格式

```
tree [选项] [.....]
pwd  [OPTION]...
```

## 选项说明

```
-P  #打印当前目录的完整路径信息
--help  #显示帮助信息
--version #显示版本信息
```

## 应用举例

```
#打印当前工作目录路径
[root@centos7 dir]# pwd
/root/testdir/dir
#下面就是有链接文件
[root@centos7 var]# ll mail
lrwxrwxrwx. 1 root root 10 Aug 20 10:31 mail -> spool/mail
[root@centos7 mail]# pwd
/var/mail
[root@centos7 mail]# pwd -P
/var/spool/mail
```

pwd命令非常简单，基本上只会用到打印当前工作目录的功能，所以掌握起来很容易，同cd/ls/shutdown等一些命令一样，属于入门的最基础命令。