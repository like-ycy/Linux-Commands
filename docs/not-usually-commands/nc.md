## 命令简介

nc 命令是一款功能强大的网络工具。它是一个端口扫描工具，也是一款安全工具，还能是一款监测工具，甚至可以做为一个简单的 TCP 代理。

## 语法格式

```
nc [-hlnruz][-g<网关...>][-G<指向器数目>][-i<延迟秒数>][-o<输出文件>][-p<通信端口>]
[-s<来源位址>][-v...][-w<超时秒数>][主机名称][通信端口...]
```

## 选项说明

```
-g<网关>      #设置路由器跃程通信网关，最大可设置8个。
-G<指向器数目> #设置来源路由指向器，其数值为4的倍数
-i<延迟秒数>  #设置时间间隔，以便传送信息及扫描通信端口
-o<输出文件>  #指定输出保存到文件中
-p<通信端口>  #设置本地主机使用的通信端口
-s<来源位址>  #设置本地主机送出数据包的IP地址
-w<超时秒数>  #设置等待连线的时间
-l  #使用监听模式
-n  #使用IP地址
-r  #乱数指定本地与远端主机的通信端口
-u  #使用UDP传输协议
-v  #显示指令执行过程中的详细信息
-z  #使用0输入/输出模式
-h  #打印帮助信息
```

## 应用举例

扫描端口

```
[root@centos7 ~]# nc -c -z -w4 192.168.1.199 1-65535
Ncat: Connection refused.
```

这里有一个坑，在CentOS7.X 中使用yum install -y nc安装的nc实际安装的是nmap-ncat（ncat命令）,但ncat这个命令没有端口扫描功能，但为何在系统中又可以使用nc命令呢，如下：

```
[root@centos7 ~]# which nc
/usr/bin/nc
[root@centos7 ~]# ls -l /usr/bin/nc
lrwxrwxrwx 1 root root 22 Aug 20  2020 /usr/bin/nc -> /etc/alternatives/nmap
[root@centos7 ~]# ll /etc/alternatives/nmap 
lrwxrwxrwx 1 root root 13 Aug 20  2020 /etc/alternatives/nmap -> /usr/bin/ncat
[root@centos7 ~]# ll /usr/bin/ncat 
-rwxr-xr-x 1 root root 380184 Aug  8  2019 /usr/bin/ncat
```

所以，当你在系统中执行nc命令时，实际执行的是ncat命令，解决文案如下：下载 nc软件包（https://sourceforge.net/projects/netcat/files/netcat/0.7.1/），上传解压并编译安装（你会发现网上好多的教程全是没有验证这个坑的）

```
[root@centos7 ~]# tar zxf netcat-0.7.1.tar.gz
[root@centos7 ~]# cd netcat-0.7.1
[root@centos7 ~]# ./configure
[root@centos7 ~]# make && make install
[root@centos7 ~]# echo $?
[root@centos7 ~]# 0
[root@centos7 ~]# which netcat
/usr/local/bin/netcat
[root@centos7 ~]# ln -s /usr/local/bin/netcat /usr/bin/nc

[root@centos7 ~]# nc --help
GNU netcat 0.7.1, a rewrite of the famous networking tool.
Basic usages:
connect to somewhere:  nc [options] hostname port [port] ...
listen for inbound:    nc -l -p port [options] [hostname] [port] ...
tunnel to somewhere:   nc -L hostname:port -p port [options]

Mandatory arguments to long options are mandatory for short options too.
Options:
  -c, --close                close connection on EOF from stdin
  -e, --exec=PROGRAM         program to exec after connect
  -g, --gateway=LIST         source-routing hop point[s], up to 8
  -G, --pointer=NUM          source-routing pointer: 4, 8, 12, ...
  -h, --help                 display this help and exit
  -i, --interval=SECS        delay interval for lines sent, ports scanned
  -l, --listen               listen mode, for inbound connects
  -L, --tunnel=ADDRESS:PORT  forward local port to remote address
  -n, --dont-resolve         numeric-only IP addresses, no DNS
  -o, --output=FILE          output hexdump traffic to FILE (implies -x)
  -p, --local-port=NUM       local port number
  -r, --randomize            randomize local and remote ports
  -s, --source=ADDRESS       local source address (ip or hostname)
  -t, --tcp                  TCP mode (default)
  -T, --telnet               answer using TELNET negotiation
  -u, --udp                  UDP mode
  -v, --verbose              verbose (use twice to be more verbose)
  -V, --version              output version information and exit
  -x, --hexdump              hexdump incoming and outgoing traffic
  -w, --wait=SECS            timeout for connects and final net reads
  -z, --zero                 zero-I/O mode (used for scanning)

Remote port number can also be specified as range.  Example: '1-1024'
```

扫描端口（指定范围）

```
[root@centos7 ~]# nc -v -z -w2 192.168.1.100 1-65535
192.168.1.100 22 (ssh) open
192.168.1.100 19999 (dnp-sec) open
```

指定端口扫描

```
[root@centos7 ~]# nc -nvv 192.168.1.100 22
192.168.1.100 22 (ssh) open
SSH-2.0-OpenSSH_7.4

Protocol mismatch.
Total received bytes: 40
Total sent bytes: 1
```

查看从服务器到目标地址的出站端口是否被防火墙阻断

```
[root@centos7 ~]# nc -vz www.baidu.com 443 -w2
www.baidu.com [36.152.44.96] 443 (https) open
[root@centos7 ~]# 
[root@centos7 ~]# nc -vz www.baidu.com 80 -w2
www.baidu.com [36.152.44.96] 80 (http) open
```