## 命令简介

umask 命令用于显示或设置权限掩码。系统默认的权限掩码是0022。

```
[root@centos7 ~]# umask
0022
```

所以，系统默认创建目录与文件的权限如下

```
目录权限=0777-0022=0755(rwxr-xr-x)
文件权限=0666-0022=0644(rwr--r--)
[root@centos7 ~]# touch A
[root@centos7 ~]# mkdir B
[root@centos7 ~]# ls -l A
-rw-r--r-- 1 root root 0 Mar 24 21:13 A
[root@centos7 ~]# ls -ld B
drwxr-xr-x 2 root root 6 Mar 24 21:14 B
```

## 语法格式

```
umask [OPTIONS]
```

## 选项说明

```
-P  #输出的权限掩码可以直接作为指令来执行
-S  #以符号方式来输出权限掩码
[权限掩码]  #设置权限掩码
```

## 应用举例

常用就是设置掩码

```
[root@centos7 ~]# umask 0033
[root@centos7 ~]# umask
0033
```

修改完成后，按照规则，创建文件与目录的默认权限会是以下权限值

- 目录权限=0777-0033=0744
- 文件权限=0666-0033=0633

下面开始验证

```
[root@centos7 ~]# touch C
[root@centos7 ~]# mkdir D
[root@centos7 ~]# ls -l C
-rw-r--r-- 1 root root 0 Mar 24 21:23 C
[root@centos7 ~]# ls -ld D
drwxr--r-- 2 root root 6 Mar 24 21:23 D
#通过验证可以发现，目录的默认权限rwx=7 r=4 r=4 与预期值一样
#不过文件的权限好像与预期值不太一样，rw=6 r=4 r=4 ,所以，这里有一个结论，当umask设置的掩码值为奇数时，文件的默认权限会在得到结果值里有奇数位的值上再加上1（0633-063（3+1）3（3+1）），所以我们看到的文件的权限是0644。
```

继续验证上面的结论

```
[root@centos7 testdir]# umask 0023
[root@centos7 testdir]# umask
0023
#修改后文件与目录的默认权限应该是  
目录权限=0777-0023=0754 
文件权限=0666-0023=0643

#接下来创建用于验证的文件a与目录b
[root@centos7 testdir]# touch a
[root@centos7 testdir]# mkdir b
[root@centos7 testdir]# ls -l a
-rw-r--r-- 1 root root 0 Mar 24 21:33 a  #-rw-r--r-- 0644（3+1）
[root@centos7 testdir]# ls -ld b
drwxr-xr-- 2 root root 6 Mar 24 21:33 b  #rwxr-xr--  0754
#结果表明上述的结论是正确的
```

不过民工哥还是在这给大家提个建议：**不建议修改系统默认的umask值（掩码权限）**，系统的设置肯定是有一定的原则的。