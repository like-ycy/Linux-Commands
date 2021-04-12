## 命令简介

route 命令用于显示和设置linux系统的路由表（静态路由表）。

route 命令用来显示并设置 Linux 内核中的网络路由表，route 命令设置的路由主要是静态路由。在 Linux、BSD 和其他类似 Unix 的系统上，route 命令用于查看和更改内核路由表。在不同的系统上，命令语法不同。

## 语法格式

```
route [-CFvnee]
route [-v] [-A family] add [-net|-host] target [netmask Nm] [gw Gw] 
      [metric N] i [mss M] [window W] [irtt m] [reject] [mod] [dyn] 
      [reinstate] [[dev] If]
route [-v] [-A family] del [-net|-host] target [gw Gw] [netmask Nm] 
      [metric N] [[dev] If]
route [-V] [--version] [-h] [--help]
```

## 选项说明

```
-A  #指定地址类型
-C  #打印将Linux核心的路由缓存
-v  #输出详细信息
-n  #不执行DNS反向查找，直接显示数字形式的IP地址
-e  #netstat格式显示路由表
-net  #到一个网络的路由表
-host  #到一个主机的路由表

Add  #增加指定的路由记录
Del  #删除指定的路由记录
Target  #目的网络或目的主机
gw  #设置默认网关
mss  #设置TCP的最大区块长度（MSS），单位MB
window  #指定通过路由表的TCP连接的TCP窗口大小
dev  #路由记录所表示的网络接口
```

## 应用举例

显示当前系统的路由表

```
[root@CentOS7-1 ~]# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         gateway         0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
```

其中 Flags 为路由标志，标记当前网络节点的状态，Flags 标志说明如下：

```
U  #Up 表示此路由当前为启动状态
H  #Host 表示此网关为一主机
G  #Gateway 表示此网关为一路由器
R  #Reinstate Route 使用动态路由重新初始化的路由
D  #Dynamically 此路由是动态性地写入
M  #Modified 此路由是由路由守护程序或导向器动态修改
!  #表示此路由当前为关闭状态
```

添加网关/设置网关

```
[root@CentOS7-1 ~]# route add -net 192.168.2.0 netmask 255.255.255.0 dev ens33
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
192.168.2.0     0.0.0.0         255.255.255.0   U     0      0        0 ens33
#增加一条到达192.168.2.0子网的路由。
```

屏蔽一条路由

```
[root@CentOS7-1 ~]# route add -net 192.168.3.0 netmask 255.255.255.0 reject
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
192.168.2.0     0.0.0.0         255.255.255.0   U     0      0        0 ens33
192.168.3.0     -               255.255.255.0   !     0      -        0 -   
#增加一条屏蔽的路由，目的地址为192.168.3.0子网将被拒绝。
```

删除路由记录

```
[root@CentOS7-1 ~]# route del -net 192.168.2.0 netmask 255.255.255.0
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
192.168.3.0     -               255.255.255.0   !     0      -        0 -
[root@CentOS7-1 ~]# route del -net 192.168.3.0 netmask 255.255.255.0 reject
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
```

删除和添加设置默认网关

```
[root@CentOS7-1 ~]# route add default gw 192.168.1.1
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    0      0        0 ens33
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
[root@CentOS7-1 ~]# route del default gw 192.168.1.1
[root@CentOS7-1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33
```