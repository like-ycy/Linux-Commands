## 命令简介

netstat（network statistics） 是一个命令行工具，它用来显示网络连接（传入和传出），路由表和许多网络接口（网络接口控制器或软件定义的网络接口）和网络协议统计信息。也可用于查找网络中的问题，打印 Linux 中网络系统的状态信息，查看整个 Linux 系统的网络情况。

netstat 的使用平很广，包括 OS X、Linux、Solaris 和 BSD，以及基于 Windows NT 的操作系统，包括 Windows XP、Windows Vista、Windows 7/8/10。

## 语法格式

```
netstat { xxx } [ OPTIONS ]
```

## 选项说明

```
-a或--all    #显示所有的网络连接信息
-A<网络类型>  #显示该网络类型连线中的相关地址
-c或--continuous  #持续列出网络状态信息
-C或--cache  #显示路由器配置的快取信息
-e或--extend  #显示网络其他相关信息
-g或--groups  #显示多播功能群组信息
-h或--help    #打印在线帮助信息
-i或--interfaces  #显示网络界面信息表单
-l或--listening   #显示监控中的服务器的Socket
-M或--masquerade  #显示伪装的网络连线
-n或--numeric     #直接使用ip地址
-N或--netlink    #显示网络硬件外围设备的符号连接名称
-o或--timers     #显示计时器
-r或--route      #显示Routing Table
-s或--statistice   #显示所有端口的状态统计信息
-t或--tcp   #显示TCP传输协议的连接状态
-u或--udp   #显示UDP传输协议的连接状态
-v或--verbose  #显示指令执行过程信息
-V或--version  #显示版本信息
-w或--raw      #显示RAW传输协议的连线状况
-x或--unix    #此参数与"-A unix"参数结果相同
--ip或--inet  #此参数与"-A inet"参数结果 相同
```

## 应用举例

列出端口

```
##列出所有端口
[root@CentOS7-1 ~]# netstat -a
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN     
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN     
tcp        0      0 localhost:8125          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:dnp-sec         0.0.0.0:*               LISTEN     
tcp        0     52 CentOS7-1:ssh           192.168.1.93:58049      ESTABLISHED
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN     
tcp6       0      0 localhost:smtp          [::]:*                  LISTEN     
tcp6       0      0 localhost:8125          [::]:*                  LISTEN     
tcp6       0      0 [::]:dnp-sec            [::]:*                  LISTEN     
udp        0      0 localhost:8125          0.0.0.0:*                          
udp        0      0 localhost:323           0.0.0.0:*                          
udp6       0      0 localhost:8125          [::]:*                             
udp6       0      0 localhost:323           [::]:*                             
raw6       0      0 [::]:ipv6-icmp          [::]:*                  7          

#列出所有tcp端口
[root@CentOS7-1 ~]# netstat -at
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN     
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN     
tcp        0      0 localhost:8125          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:dnp-sec         0.0.0.0:*               LISTEN     
tcp        0     52 CentOS7-1:ssh           192.168.1.93:58049      ESTABLISHED
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN     
tcp6       0      0 localhost:smtp          [::]:*                  LISTEN     
tcp6       0      0 localhost:8125          [::]:*                  LISTEN     
tcp6       0      0 [::]:dnp-sec            [::]:*                  LISTEN     

#列出所有UDP端口
[root@CentOS7-1 ~]# netstat -au
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
udp        0      0 localhost:8125          0.0.0.0:*                          
udp        0      0 localhost:323           0.0.0.0:*                          
udp6       0      0 localhost:8125          [::]:*                             
udp6       0      0 localhost:323           [::]:*                  

#列出所有处于监听状态的 Sockets
netstat -l        #只显示监听端口
netstat -lt       #只列出所有监听 tcp 端口
netstat -lu       #只列出所有监听 udp 端口
netstat -lx       #只列出所有监听 UNIX 端口
 
#显示每个协议的统计信息
netstat -s    #显示所有端口的统计信息
netstat -st   #显示TCP端口的统计信息
netstat -su   #显示UDP端口的统计信息
```

显示路由表信息

```
[root@CentOS7-1 ~]# netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         gateway         0.0.0.0         UG        0 0          0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 ens33
[root@CentOS7-1 ~]# netstat -rn
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG        0 0          0 ens33
192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 ens33
```

显示接口列表

```
[root@CentOS7-1 ~]# netstat -i
Kernel Interface table
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
ens33            1500    48619      0      5 0          7246      0      0      0 BMRU
lo              65536     1730      0      0 0          1730      0      0      0 LRU
```

分组查看各种连接状态

```
[root@CentOS7-1 ~]# netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
LAST_ACK 5 (正在等待处理的请求数) 
SYN_RECV 3  
ESTABLISHED 10 (正常数据传输状态) 
FIN_WAIT2 5
TIME_WAIT 313 (处理完毕，等待超时结束的请求数)
```

显示连接数

```
[root@CentOS7-1 ~]# netstat -an |grep :22
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
tcp        0     52 192.168.1.100:22        192.168.1.93:58049      ESTABLISHED
tcp6       0      0 :::22 
[root@CentOS7-1 ~]# netstat -an |grep :22 |wc -l
3
```

通过端口找进程ID

```
[root@CentOS7-1 ~]# netstat -anp | grep 58049
tcp        0     52 192.168.1.100:22        192.168.1.93:58049      ESTABLISHED 1350/sshd: root@pts 
[root@CentOS7-1 ~]# netstat -anp | grep 58049 |grep ESTABLISHED
tcp        0     52 192.168.1.100:22        192.168.1.93:58049      ESTABLISHED 1350/sshd: root@pts 
[root@CentOS7-1 ~]# netstat -anp | grep 58049 |grep ESTABLISHED |awk '{print $7}'
1350/sshd:
[root@CentOS7-1 ~]# netstat -anp | grep 58049 |grep ESTABLISHED |awk '{print $7}' |cut -d/ -f1
1350
```

查看连接某个端口最多的IP地址

```
[root@CentOS7-1 ~]# netstat -ntu | grep :58049 | awk '{print $5}' | cut -d: -f1 | awk '{++ip[$1]} END {for(i in ip) print ip[i],"\t",i}' | sort -nr
1   192.168.1.93
[root@CentOS7-1 ~]# netstat -ntu | grep :22 | awk '{print $5}' | cut -d: -f1 | awk '{++ip[$1]} END {for(i in ip) print ip[i],"\t",i}' | sort -nr
1   192.168.1.93
```

显示所有端口的状态统计信息

```
[root@CentOS7-1 ~]# netstat -s
Ip:
    15146 total packets received
    0 forwarded
    0 incoming packets discarded
    15146 incoming packets delivered
    3885 requests sent out
    8 dropped because of missing route
Icmp:
    4 ICMP messages received
    0 input ICMP message failed.
    ICMP input histogram:
        destination unreachable: 4
    44 ICMP messages sent
    0 ICMP messages failed
    ICMP output histogram:
        destination unreachable: 44
IcmpMsg:
        InType3: 4
        OutType3: 44
Tcp:
    863 active connections openings
    1 passive connection openings
    858 failed connection attempts
    0 connection resets received
    1 connections established
    5021 segments received
    3772 segments send out
    0 segments retransmited
    0 bad segments received.
    858 resets sent
Udp:
    200 packets received
    44 packets to unknown port received.
    0 packet receive errors
    246 packets sent
    0 receive buffer errors
    0 send buffer errors
UdpLite:
TcpExt:
    1 TCP sockets finished time wait in fast timer
    35 delayed acks sent
    1 packets directly queued to recvmsg prequeue.
    1362 packet headers predicted
    438 acknowledgments not containing data payload received
    1160 predicted acknowledgments
    TCPRcvCoalesce: 9
    TCPOrigDataSent: 1719
IpExt:
    InBcastPkts: 10042
    InOctets: 4159848
    OutOctets: 329931
    InBcastOctets: 3778680
    InNoECTPkts: 15150
```

显示多播组信息

```
[root@CentOS7-1 ~]# netstat -g
IPv6/IPv4 Group Memberships
Interface       RefCnt Group
--------------- ------ ---------------------
lo              1      all-systems.mcast.net
ens33           1      all-systems.mcast.net
lo              1      ff02::1
lo              1      ff01::1
ens33           1      ff02::1:ff4e:26b0
ens33           1      ff02::1:ff01:b5bb
ens33           1      ff02::1
ens33           1      ff01::1
```