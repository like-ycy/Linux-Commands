## 命令简介

ifconfig 命令用于查看、配置、启用或禁用网络接口和显示 Linux 系统网卡的网络参数。

## 语法格式

```
ifconfig [-v] [-a] [-s] [interface]
ifconfig [-v] interface [aftype] options | address ...
```

## 选项说明

```
add<地址>  #配置网络设备IPv6的ip地址
del<地址>  #删除网络设备IPv6的IP地址
up    #启动指定的网络设备
down  #关闭指定的网络设备
<hw<网络设备类型><硬件地址>  #配置网络设备的类型与硬件地址
io_addr<I/O地址>    #配置网络设备的I/O地址
irq<IRQ地址>        #配置网络设备的IRQ
media<网络媒介类型>   #配置网络设备的媒介类型
mem_start<内存地址>  #配置网络设备在主内存所占用的起始地址
metric<数目>   #指定在计算数据包的转送次数时，所要加上的数目
mtu<字节>      #配置网络设备的MTU
netmask<子网掩码>    #配置网络设备的子网掩码
tunnel<地址>        #建立IPv4与IPv6之间的隧道通信地址
-broadcast<地址>    #将要送往指定地址的数据包当成广播数据包来处理
-pointopoint<地址>  #与指定地址的网络设备建立直接连线，此模式具有保密功能
-promisc  #关闭或启动指定网络设备的promiscuous模式
IP地址     #配置网络设备的IP地址
网络设备    #配置网络设备的名称
```

## 应用举例

显示网络设备信息（激活状态的）

```
[root@CentOS7-1 ~]# ifconfig
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 2409:8a31:918:be20:1a76:7add:7b4e:26b0  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::c8e8:4d2:1b01:b5bb  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:25:62:6f  txqueuelen 1000  (Ethernet)
        RX packets 835899  bytes 1208840751 (1.1 GiB)
        RX errors 0  dropped 2  overruns 0  frame 0
        TX packets 317633  bytes 81085908 (77.3 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 1730  bytes 89964 (87.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1730  bytes 89964 (87.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
#enss33 表示第一块网卡, inet addr这块网卡的IP地址，在centOS 7系统以前的版本中，eth0表示第一块网卡。
#lo（loopback） 是表示主机的回坏地址
```

启动关闭指定网卡：

```
ifconfig ens33 up    #启动网卡
ifconfig ens33 down  #关闭网卡
#使用ssh登陆linux服务器操作要小心，关闭了就不能开启了，除非你有多网卡，否则你将无法通过ssh远程登录到此主机。
```

为网卡配置和删除IPv6地址

```
ifconfig ens33 add 75eg:2650:800:35cv::2/64    #配置IPv6地址
ifconfig ens33 del 75eg:2650:800:35cv::2/64    #删除IPv6地址
```

用 ifconfig 修改 MAC 地址：

```
ifconfig ens33 hw ether 35:78:9E:AF:YH:JK
```

配置 IP 地址：

```
[root@CentOS7-1 ~]# ifconfig ens33:1 192.168.1.200
[root@CentOS7-1 ~]# ifconfig ens33:1
ens33:1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.200  netmask 255.255.255.0  broadcast 192.168.1.255
        ether 00:0c:29:25:62:6f  txqueuelen 1000  (Ethernet)
[root@CentOS7-1 ~]# ifconfig ens33:1 192.168.1.200 netmask 255.255.255.0
[root@CentOS7-1 ~]# ifconfig ens33:1 192.168.1.200 netmask 255.255.255.0 broadcast 192.168.1.255
[root@CentOS7-1 ~]# ifconfig ens33:1
ens33:1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.200  netmask 255.255.255.0  broadcast 192.168.1.255
        ether 00:0c:29:25:62:6f  txqueuelen 1000  (Ethernet)
```

启用和关闭 arp 协议

```
[root@CentOS7-1 ~]# ifconfig ens33 arp    #开启网卡ens33的arp协议
[root@CentOS7-1 ~]# ifconfig ens33 -arp   #关闭网卡ens33的arp协议
```

停用网络接口 wlan0。

```
[root@CentOS7-1 ~]# ifconfig wlan0 down
```

将网络接口 wlan1 配置为使用静态 IP 地址 172.16.1.99

```
[root@CentOS7-1 ~]# ifconfig wlan1 172.16.1.99 netmask 255.255.255.0
```

设置最大传输单元：

```
[root@CentOS7-1 ~]# ifconfig ens33 mtu 1000   #设置能通过的最大数据包大小为 1000 bytes
```