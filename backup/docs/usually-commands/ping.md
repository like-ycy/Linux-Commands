## 命令简介

ping 命令用于测试主机之间网络的连通性。

ping 是一种向网络上的另一台计算机发送网络数据并从其接收网络数据的简单方法。它通常用于测试与另一个系统是否可以通过网络访问，如果可以，则需要花费多少时间来交换该数据。

## 语法格式

```
ping [options] destination
ping -6 [options] destination
```

## 选项说明

```
-c<完成次数>  #指定要求回应的次数
-f  #最大极限检测
-i<间隔秒数>  #指定收发信息的间隔时间
-n  #只输出数值
-p<范本样式>  #设置填满数据包的范本样式
-q  #不输出执行过程信息，开头和结尾的相关信息除外
-r  #忽略普通的 Routing Table，直接将数据包送到远端主机上
-R  #记录路由过程
-s<数据包大小>  #设置数据包的大小
-t<存活数值>   #设置存活数值TTL的大小
-v   #详细输出执行过程信息
```

## 应用举例

常见举例

```
[root@centos7 ~]# ping www.baidu.com
PING www.a.shifen.com (36.152.44.95) 56(84) bytes of data.
64 bytes from 36.152.44.95 (36.152.44.95): icmp_seq=1 ttl=56 time=10.5 ms
64 bytes from 36.152.44.95 (36.152.44.95): icmp_seq=2 ttl=56 time=11.8 ms
64 bytes from 36.152.44.95 (36.152.44.95): icmp_seq=3 ttl=56 time=10.7 ms
^C
--- www.a.shifen.com ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6095ms
rtt min/avg/max/mdev = 10.588/11.512/12.007/0.546 ms

[root@centos7 ~]# ping -n www.baidu.com
PING www.a.shifen.com (36.152.44.96) 56(84) bytes of data.
64 bytes from 36.152.44.96: icmp_seq=1 ttl=56 time=13.6 ms
64 bytes from 36.152.44.96: icmp_seq=2 ttl=56 time=14.0 ms
^C
--- www.a.shifen.com ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5032ms
rtt min/avg/max/mdev = 13.616/14.373/14.933/0.442 ms
```

只进行2次Ping操作

```
[root@centos7 ~]# ping -c 2 www.baidu.com
PING www.a.shifen.com (36.152.44.96) 56(84) bytes of data.
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=1 ttl=56 time=14.0 ms
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=2 ttl=56 time=14.4 ms

--- www.a.shifen.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1013ms
rtt min/avg/max/mdev = 14.086/14.257/14.428/0.171 ms
```

极限 PING 测试

```
[root@centos7 ~]# ping -c 10 -f www.baidu.com
PING www.a.shifen.com (36.152.44.96) 56(84) bytes of data.
  
--- www.a.shifen.com ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 110ms
rtt min/avg/max/mdev = 13.368/13.587/13.871/0.142 ms, pipe 2, ipg/ewma 12.279/13.609 ms
```