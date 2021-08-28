## 命令简介

chkconfig 命令用于管理Linux系统开机启动项

## 语法格式

```
chkconfig [options] 
```

## 选项说明

```
--add   #增加所指定的系统服务
--del  #删除所指定的系统服务
--level<等级代号>  #指定读系统服务要在哪一个执行等级中开启或关毕
```

缺省的运行级，RHS用到的级别如下：

- 0：关机
- 1：单用户模式
- 2：无网络支持的多用户模式
- 3：有网络支持的多用户模式
- 4：保留，未使用
- 5：有网络支持有X-Window支持的多用户模式
- 6：重新引导系统，即重启

运行级文件

每个被chkconfig管理的服务需要在对应的init.d下的脚本加上两行或者更多行的注释。第一行告诉chkconfig缺省启动的运行级以及启动和停止的优先级。如果某服务缺省不在任何运行级启动，那么使用-代替运行级。第二行对服务进行描述，可以用\跨行注释。

```
# chkconfig: 2345 10 90
# description: Activates/Deactivates all network interfaces configured to \
#       start at boot time.
```

## 应用举例

列出所有系统的服务

```
[root@centos7 ~]# chkconfig --list

Note: This output shows SysV services only and does not include native
      systemd services. SysV configuration data might be overridden by native
      systemd configuration.

      If you want to list systemd services use 'systemctl list-unit-files'.
      To see services enabled on particular target use
      'systemctl list-dependencies [target]'.

netconsole      0:off 1:off 2:off 3:off 4:off 5:off 6:off
network         0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

其它实例

```
[root@centos7 ~]# chkconfig --add httpd        #增加httpd服务
[root@centos7 ~]# chkconfig --del httpd        #删除httpd服务
[root@centos7 ~]# chkconfig --level httpd 2345 on    #设置httpd在运行级别为2、3、4、5的情况下都是on（开启）的状态
[root@centos7 ~]# chkconfig --list httpd       #列出httpd服务设置情况
[root@centos7 ~]# chkconfig --level 35 httpd on #设定httpd在等级3和5为开机运行服务
[root@centos7 ~]# chkconfig httpd on    #设定httpd在各等级为on
 
[root@centos7 ~]# chkconfig –level redis 2345 on #把redis在运行级别为2、3、4、5的情况下都是on（开启）的状态
```

注意：增加一个服务时，这个服务启动脚本必须存放在 /etc/init.d/目录下。