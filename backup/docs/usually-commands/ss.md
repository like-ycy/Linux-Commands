## 命令简介

ss 命令用于查看网络状态。ss 命令可以用来获取 socket 统计信息，它显示的信息和 netstat 命令显示的信息类似，但 ss 的优势在于它能够显示更多更详细的有关 TCP 和连接状态的信息，而且比 netstat 更快速更高效。

当服务器的 socket 连接数量变得非常大时，无论是使用 netstat 命令还是直接 cat /proc/net/tcp，执行速度都会很慢。当服务器维持的连接达到上万个的时候，使用 ss命令比netstat 更节省时间。

## 语法格式

```
ss [OPTIONS]
ss [ OPTIONS ] [ FILTER ]
```

## 选项说明

```
-h   #打印帮助信息
-V   #程序版本信息
-n   #不解析服务名称
-r   #解析主机名
-a   #显示所有套接字（sockets）
-l   #显示监听状态的套接字（sockets）
-o   #显示计时器信息
-e   #显示详细的套接字（sockets）信息
-m   #显示套接字（socket）的内存使用情况
-p   #显示使用套接字（socket）的进程
-i   #显示 TCP内部信息
-s   #显示套接字（socket）使用概况
-4   #仅显示IPv4的套接字（sockets）
-6   #仅显示IPv6的套接字（sockets）
-0   #显示 PACKET 套接字（socket）
-t   #仅显示 TCP套接字（sockets）
-u   #仅显示 UCP套接字（sockets）
-d   #仅显示 DCCP套接字（sockets）
-w   #仅显示 RAW套接字（sockets）
-x   #仅显示 Unix套接字（sockets）
-f   #显示 FAMILY类型的套接字（sockets）
-D   #将原始TCP套接字（sockets）信息转储到文件
-F   #从文件中都去过滤器信息
```

## 应用举例

显示所有TCP连接信息

```
[root@CentOS7-1 ~]# ss -t -a
State      Recv-Q Send-Q     Local Address:Port                      Peer Address:Port                
LISTEN     0      128                    *:ssh                                  *:*                    
LISTEN     0      100            127.0.0.1:smtp                                 *:*                    
LISTEN     0      128            127.0.0.1:8125                                 *:*                    
LISTEN     0      128                    *:dnp-sec                              *:*                    
ESTAB      0      0          192.168.1.100:ssh                       192.168.1.93:59231                
LISTEN     0      128                 [::]:ssh                               [::]:*                    
LISTEN     0      100                [::1]:smtp                              [::]:*                    
LISTEN     0      128                [::1]:8125                              [::]:*                    
LISTEN     0      128                 [::]:dnp-sec                           [::]:*                    
```

显示所有UDP连接信息

```
[root@CentOS7-1 ~]# ss -u -a
State      Recv-Q Send-Q     Local Address:Port                      Peer Address:Port                
UNCONN     0      0              127.0.0.1:8125                                 *:*                    
UNCONN     0      0              127.0.0.1:323                                  *:*                    
UNCONN     0      0                  [::1]:8125                              [::]:*                    
UNCONN     0      0                  [::1]:323                               [::]:*    
```

显示Sockets 摘要信息

```
[root@CentOS7-1 ~]# ss -s
Total: 569 (kernel 1020)
TCP:   9 (estab 1, closed 0, orphaned 0, synrecv 0, timewait 0/0), ports 0

Transport Total     IP        IPv6
*   1020      -         -        
RAW   1         0         1        
UDP   4         2         2        
TCP   9         5         4        
INET   14        7         7        
FRAG   0         0         0        
#显示所有状态为established的SSH连接
[root@CentOS7-1 ~]# ss -o state established '( dport = :ssh or sport = :ssh )'
Netid  Recv-Q Send-Q       Local Address:Port                        Peer Address:Port                
tcp    0      52           192.168.1.100:ssh                         192.168.1.93:59231                 timer:(on,235ms,0)

ss -o state established '( dport = :smtp or sport = :smtp )' 
#显示所有状态为established的SMTP连接

ss -o state established '( dport = :http or sport = :http )' 
#显示所有状态为Established的HTTP连接
```

ss与netstat的效率对比

```
[root@CentOS7-1 ~]# time netstat -an|awk '/^tcp/{++S[$NF]}END{for(a in S) print a,S[a]}'  
LISTEN 8
ESTABLISHED 1

real 0m0.021s
user 0m0.009s
sys 0m0.009s
[root@CentOS7-1 ~]# time ss  -tan|awk 'NR>1{++S[$1]}END{for (a in S) print a,S[a]}'
LISTEN 8
ESTAB 1

real 0m0.009s
user 0m0.007s
sys 0m0.001s
```

查看TCP或UDP连接数的脚本

```
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh
Usage: sh  ./get_tcp_or_udp-connetios.sh [closed|closing|closewait|synrecv|synsent|finwait1|finwait2|listen|established|lastack|timewait]
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh timewait
0
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh listen
8
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh established
1
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh closed
0
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh closing
0
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh closewait
0
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh synrecv
0
[root@CentOS7-1 ~]# ./get_tcp_or_udp-connetios.sh lastack
0
```

有需要此脚本的读者，可以在本公众号后台对话框回复关键字【连接数脚本】下载本脚本。