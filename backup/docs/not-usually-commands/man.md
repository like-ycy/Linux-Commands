## 命令简介

man 命令用于查看、显示 Linux 中命令的帮助信息，显示的帮助信息，可上下滚动，搜索特定文本的出现以及其他有用的功能。

man 命令是 Linux 系统下的帮助命令，通过 man 命令可以查看 Linux 系统中的命令帮助、配置文件帮助和编程帮助等信息,并且格式化显示出来所有的信息。

## 命令语法

```
man [选项] [命令]
```

## 选项说明

man命令常用参数

```
-a    #显示所有匹配项
-d   #显示man查照手册文件时候，搜索路径信息,不显示手册页内容
-D   #同-d,显示手册页内容
-f   #同命令whatis ，将在whatis数据库查找以关键字开同的帮助索引信息
-h   #显示帮助信息
-k   #同命令apropos 将搜索whatis数据库，模糊查找关键字
-S list #指定搜索的领域及顺序 如：-S 1:1p httpd 将搜索man1然后 man1p目录
-t   #使用troff 命令格式化输出手册页 默认：groff输出格式页
-w   #不带搜索title 打印manpath变量 带title关键字 打印找到手册文件路径,默认搜索一个文件后停止
-W   #同-w
```

man命令其它参数

```
-c #显示使用 cat 命令的手册信息
-C #指定man 命令搜索配置文件 默认是man.config
-K #搜索一个字符串在所有手册页中,速度很慢
-M #指定搜索手册的路径
-P pro #使用程序pro显示手册页面，默认是less
-B pro #使用pro程序显示HTML手册页，默认是less
-H pro #使用pro程序读取HTML手册，用txt格式显示，默认是cat
-p str #指定通过groff格式化手册之前，先通过其它程序格式化手册
```

## 应用举例

显示帮助文件的路径

```
[root@centos7 ~]# man -w cd
/usr/share/man/man1/builtins.1.gz
[root@centos7 ~]# man -w ls
/usr/share/man/man1/ls.1.gz
[root@centos7 ~]# man -w chmod
/usr/share/man/man1/chmod.1.gz

#显示所有帮助文件的路径
[root@centos7 ~]# man -aw passwd
/usr/share/man/man1/passwd.1.gz
/usr/share/man/man1/sslpasswd.1ssl.gz
```

显示man执行过程搜索查找方法，以及查询手册通过怎么样格式化语句显示

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoIuAMbWL6yYo6nazmsCRlWvwI6z7QkSeiaDOQib5vaiczqbBiaEP0l356v0FllTIWL38DLRSMibnyFl9g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

显示man命令查找手册的路径

```
[root@centos7 ~]# man -w
/usr/local/share/man:/usr/share/man
```

显示某个命令的帮助信息![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoIuAMbWL6yYo6nazmsCRlWicj0nIJWx7JJKfPAwfHWfQTrMINStoYVTk89GojjJSq0TpY2BKz9tWg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)所以，man命令对于任何一个学习Linux命令的人来说绝对是一个神器，也是必不可少的工具，大家一定要掌握并且能熟练运用它。