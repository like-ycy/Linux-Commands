## 命令简介

iptraf 命令是基于 ncurses 的 IP LAN 监视器，它生成各种网络统计信息，包括 TCP 信息、UDP 计数、ICMP 和 OSPF 信息，以太网负载信息，节点统计信息，IP 校验和错误等。

```
[root@centos7 ~]# iptraf
-bash: iptraf: command not found
[root@centos7 ~]# yum install iptraf -y
```

iptraf 命令是一款交互式、色彩鲜艳的 IP 局域网监控工具。它可以显示每个连接以及主机之间传输的数据量。

若在 CentOS Linux 中，其采用的版本是 IPTraf 的衍生版本 iptraf-ng(没有iptrsf这个命令)。

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAILibaVZICOw2azszqAJTQ1u4t6ke0adOflEu1ZNtichpdz1o6Wg1tuCg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 语法格式

```
iptraf { [ -f ] [ -q ] [ { -i iface | -g | -d iface | -s iface | -z iface | -l iface } [ -t timeout ] [ -B [ -L logfile ] ] ] | [ -h ] }
```

## 选项说明

```
-d  #允许您立即启动指定接口上的详细信息（iface）
-z  #显示指定接口上的数据包计数大小
-i  #立即在指定接口启动IP流量监视器
-u  #允许使用不受支持的接口作为以太网设备
-g  #立即启动常规接口统计
```

## 应用举例

先看一个动图展示

![图片](https://mmbiz.qpic.cn/mmbiz_gif/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAJooFbUYPux0O0Drwg3SsOf5Yh5KicgoL0vicz0AwWqbCykzMvRuPAGIA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)



![图片](https://mmbiz.qpic.cn/mmbiz_gif/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAW3D3Fib5mKY9Kq3qQx7pmvGhfSCiahCbKVibWOQ1MhHiaibETSZibNqplWBA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)

立即启动指定接口上的详细信息

```
[root@centos7 ~]# iptraf-ng -d ens33
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAnBRg7D5untKDdLwAFiby1k1HHxBMQLwkwIoQm2I5Z0viajBrn568NGbA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)查看数据包大小

```
[root@centos7 ~]# iptraf-ng -z ens33
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAapnL0qG0sCOv7mYxqJIcmiaoibbD0SicaNoJcnZEegF5hXIqPBmuKJGEA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)以上都是用的截图方式展示，其实实际使用过程中都是动态更新的。