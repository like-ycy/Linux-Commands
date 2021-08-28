## 命令简介

su 命令用于切换当前用户身份到其他用户身份。

sudo 命令用于切换用户执行权限，这个命令可使其它非 root 用户具有 root 权限。默认情况下，sudo 要求用户使用密码进行身份验证，这是用户密码，不是 root 密码。

## 语法格式

```
su [ options ] [ username ]
sudo [ options ] [ command ]
```

## 选项说明

su 命令选项

```
-c<指令>  #执行完指定的指令后，即恢复原来的身份
-f  #使shell不用去读取启动文件
-l  #切换身份时，同时变更工作目录
-m  #切换身份时，不变更环境变量
-s  #指定要执行的shell
--help     #打印帮助信息
--version  #打印版本信息
```

sudo 命令选项

```
-b  #在后台执行指令
-h  #打印帮助信息
-H  #将HOME环境变量设为新身份的HOME环境变量
-k  #结束密码的有效期限，也就是下次再执行sudo时便需要输入密码
-l  #列出目前用户可执行与无法执行的指令
-s<shell>  #执行指定的shell
-u<用户>   #以指定的用户作为新的身份
-v  #延长密码有效期限5分钟
-V  #打印版本信息
```

## 应用举例

```
#切换用户到 mingongge
[root@centos7 ~]# su - mingongge
Last login: Sun Jan 17 08:08:46 EST 2021 on pts/0

#切换到root用户后执行pwd命令后再切换至原用户
[mingongge@centos7 ~]$ su -c pwd root
Password: 
/home/mingongge
[mingongge@centos7 ~]$ sudo -i
[sudo] password for mingongge: 
mingongge is not in the sudoers file.  This incident will be reported.
#普通用户如果没有在/etc/sudoers文件里配置相关的信息，则无法执行sudo这个命令
[mingongge@centos7 ~]$ sudo -l
[sudo] password for mingongge: 
Sorry, user mingongge may not run sudo on centos7.
```

用户需要执行 sudo 命令时就需要在/etc/sudoers配置文件中配置，然后直接使用sudo + 需要执行的命令 这种组合来让自己具有管理员权限。