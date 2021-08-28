## 命令简介

hostname 命令用于显示或设置系统主机名。

在使用 hostname 命令设置主机名后，系统并不会永久保存新的主机名，重新启动机器之后还是原来的主机名。如果需要永久修改主机名，需要同时修改 /etc/hosts 和 /etc/sysconfig/network 的相关内容。

## 语法格式

```
hostname [-v] [-b|--boot] [-F|--file file name] [hostname]
```

## 选项说明

```
-v  #详细信息模式
-a  #显示主机别名
-d  #显示DNS域名
-f  #显示FQDN名称
-i  #显示主机的ip地址
-s  #显示短主机名称，在第一个点处截断
-y  #显示NIS域名
```

## 应用举例

```
[root@centos7 ~]# hostname
centos7
[root@centos7 ~]# hostname CentOS7
[root@centos7 ~]# hostname
CentOS7
```

临时生效，重启后失效。