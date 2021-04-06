## 命令简介

which 命令用于查找并显示指定的命令的绝对路径信息，按环境变量PATH路径查找。使用 which 命令，也可以看到某个系统命令是否存在。

## 语法格式

```
which [options] [--] programname [...]
```

## 选项说明

```
-a  #打印每个匹配文件名的所有匹配路径名
-V  #打印版本信息
```

## which 退出状态

```
0 #找到了所有文件名，所有文件都是可执行的
1 #找不到一个或多个文件名，或者文件名不可执行
2 #指定的选项无效
```

## 应用举例

显示命令的完整路径

```
[root@centos7 ~]# which which
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
 /usr/bin/alias
 /usr/bin/which
[root@centos7 ~]# which ls
alias ls='ls --color=auto'
 /usr/bin/ls
[root@centos7 ~]# which pwd
/usr/bin/pwd
[root@centos7 ~]# which rz
/usr/bin/rz
[root@centos7 ~]# which ifconfig
/usr/sbin/ifconfig
```