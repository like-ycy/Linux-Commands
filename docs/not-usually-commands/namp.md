## 命令简介

nmap（Network Mapper - 网络映射器）命令用于网络探测和安全审核，是网络探索工具和端口扫描程序。namp 它可以扫描单主机，也可以快速扫描大型网络结构。

nmap 输出信息是你所扫描目标的列表，且每个目标都有详细的信息展示，具体的展示信息取决于所使用的选项。该信息中的关键是“有趣的端口表”。该表列出了端口号和协议，服务名称以及状态。状态为打开，已过滤，已关闭或未过滤。

```
[root@CentOS7-1 ~]# nmap --help
-bash: nmap: command not found
[root@CentOS7-1 ~]# yum install nmap -y
```

## 语法格式

```
nmap [Scan Type...] [Options] {target specification}
```

## 选项说明

```
-O   #激活探测操作
-P0  #只进行扫描，不ping主机
-PT  #是同TCP的ping
-sV  #显示服务版本信息
-sP  #ping扫描，仅发现目标主机是否存活
-ps  #发送同步（SYN）报文
-PU  #发送udp ping
-PE  #强制执行直接的ICMPping
-PB  #默认模式
-6   #使用IPv6地址
-v   #详细信息
-d   #增加调试信息地输出
-A   #使用所有高级扫描选项
--resume  #恢复（继续上次）中止的扫描
-P  #指定要扫描的端口，可以是一个端口，用逗号隔开多个端口，使用“-”表示端口范围
-e  #在多网络接口Linux系统中，指定扫描使用的网络接口
-g  #将指定的端口作为源端口进行扫描
--ttl   #指定发送的扫描报文的生存期
--packet-trace  #显示扫描过程中收发报文统计
--scanflags     #设置在扫描报文中的TCP标志
--send-eth/--send-ip  #使用原始以太网发送/构造指定IP发送
```

## 应用举例

典型的扫描

```
[root@CentOS7-1 ~]# nmap -A  www.baidu.com

Starting Nmap 6.40 ( http://nmap.org ) at 2021-03-13 04:30 EST
Nmap scan report for www.baidu.com (36.152.44.95)
Host is up (0.012s latency).
Other addresses for www.baidu.com (not scanned): 36.152.44.96
Not shown: 998 filtered ports
PORT    STATE SERVICE        VERSION
80/tcp  open  http-proxy     sslstrip
|_http-methods: No Allow or Public header in OPTIONS response (status code 302)
| http-robots.txt: 10 disallowed entries 
| /baidu /s? /ulink? /link? /home/news/data/ /bh /shifen/ 
|_/homepage/ /cpro /
|_http-title: \xE7\x99\xBE\xE5\xBA\xA6\xE4\xB8\x80\xE4\xB8\x8B\xEF\xBC\x8C\xE4\xBD\xA0\xE5\xB0\xB1\xE7\x9F\xA5\xE9\x81\x93
443/tcp open  ssl/http-proxy sslstrip
|_http-methods: No Allow or Public header in OPTIONS response (status code 302)
| http-robots.txt: 10 disallowed entries 
| /baidu /s? /ulink? /link? /home/news/data/ /bh /shifen/ 
|_/homepage/ /cpro /
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=baidu.com/organizationName=Beijing Baidu Netcom Science Technology Co., Ltd/stateOrProvinceName=beijing/countryName=CN
| Not valid before: 2020-04-02T06:04:58+00:00
|_Not valid after:  2021-07-26T04:31:02+00:00
|_ssl-date: 2021-03-16T03:14:21+00:00; +2d17h43m18s from local time.
| tls-nextprotoneg: 
|_  http/1.1
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: specialized|switch
Running (JUST GUESSING): AVtech embedded (88%), HP embedded (86%)
OS CPE: cpe:/h:hp:procurve_switch_4000m
Aggressive OS guesses: AVtech Room Alert 26W environmental monitor (88%), HP 4000M ProCurve switch (J4121A) (86%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 10 hops

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   0.97 ms  192.168.1.1
2   4.96 ms  100.106.0.1
3   ... 9
10  15.25 ms 36.152.44.95

OS and Service detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.64 seconds
```

TCP 端口扫描

```
[root@CentOS7-1 ~]# nmap -sT 192.168.1.100

Starting Nmap 6.40 ( http://nmap.org ) at 2021-03-13 04:32 EST
Nmap scan report for 192.168.1.100
Host is up (0.00037s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
```

扫描1-65535

```
[root@CentOS7-1 ~]# nmap -p 1-65535 -T4 -A -v 192.168.1.100

Starting Nmap 6.40 ( http://nmap.org ) at 2021-03-13 04:33 EST
NSE: Loaded 110 scripts for scanning.
NSE: Script Pre-scanning.
Initiating Parallel DNS resolution of 1 host. at 04:33
Completed Parallel DNS resolution of 1 host. at 04:33, 0.00s elapsed
Initiating SYN Stealth Scan at 04:33
Scanning 192.168.1.100 [65535 ports]
Discovered open port 22/tcp on 192.168.1.100
Discovered open port 19999/tcp on 192.168.1.100
Completed SYN Stealth Scan at 04:33, 6.82s elapsed (65535 total ports)
Initiating Service scan at 04:33
Scanning 2 services on 192.168.1.100
Completed Service scan at 04:33, 19.10s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 192.168.1.100
NSE: Script scanning 192.168.1.100.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.14s elapsed
Nmap scan report for 192.168.1.100
Host is up (0.000032s latency).
Not shown: 65533 closed ports
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 2048 37:71:8e:4a:db:cc:ac:29:f2:a2:20:93:23:8c:f6:e8 (RSA)
|_256 cc:4b:7d:b6:59:0f:77:83:a9:a5:32:70:4e:87:0d:41 (ECDSA)
19999/tcp open  unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at http://www.insecure.org/cgi-bin/servicefp-submit.cgi :
SF-Port19999-TCP:V=6.40%I=7%D=3/13%Time=604C86FA%P=x86_64-redhat-linux-gnu
SF:%r(GenericLines,190,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nConnection:\
SF:x20close\r\nServer:\x20NetData\x20Embedded\x20HTTP\x20Server\x20v1\.29\
SF:.3\r\nAccess-Control-Allow-Origin:\x20\*\r\nAccess-Control-Allow-Creden
SF:tials:\x20true\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nDate
SF::\x20Sat,\x2013\x20Mar\x202021\x2009:33:46\x20GMT\r\nCache-Control:\x20
SF:no-cache,\x20no-store,\x20must-revalidate\r\nPragma:\x20no-cache\r\nExp
SF:ires:\x20Sat,\x2013\x20Mar\x202021\x2009:33:47\x20GMT\r\nContent-Length
SF::\x2027\r\n\r\nI\x20don't\x20understand\x20you\.\.\.\r\n")%r(GetRequest
SF:,5580,"HTTP/1\.1\x20200\x20OK\r\nConnection:\x20close\r\nServer:\x20Net
SF:Data\x20Embedded\x20HTTP\x20Server\x20v1\.29\.3\r\nAccess-Control-Allow
SF:-Origin:\x20\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nContent-
SF:Type:\x20text/html;\x20charset=utf-8\r\nDate:\x20Tue,\x2009\x20Feb\x202
SF:021\x2010:11:54\x20GMT\r\nCache-Control:\x20public\r\nExpires:\x20Sun,\
SF:x2014\x20Mar\x202021\x2009:33:46\x20GMT\r\nContent-Length:\x2085228\r\n
SF:\r\n<!doctype\x20html><html\x20lang=\"en\"><head><title>netdata\x20dash
SF:board</title><meta\x20name=\"application-name\"\x20content=\"netdata\">
SF:<meta\x20http-equiv=\"Content-Type\"\x20content=\"text/html;\x20charset
SF:=utf-8\"/><meta\x20charset=\"utf-8\"><meta\x20http-equiv=\"X-UA-Compati
SF:ble\"\x20content=\"IE=edge,chrome=1\"><meta\x20name=\"viewport\"\x20con
SF:tent=\"width=device-width,initial-scale=1\"><meta\x20name=\"apple-mobil
SF:e-web-app-capable\"\x20content=\"yes\"><meta\x20name=\"apple-mobile-web
SF:-app-status-bar-style\"\x20content=\"black-translucent\"><meta\x20name=
SF:\"author\"\x20content=\"costa@tsaousis\.gr\"><link\x20rel=\"icon\"\x20h
SF:ref=\"data:image/x-icon;base64,iVBORw0KGgoAAA")%r(HTTPOptions,1C7,"HTTP
SF:/1\.1\x20200\x20OK\r\nConnection:\x20close\r\nServer:\x20NetData\x20Emb
SF:edded\x20HTTP\x20Server\x20v1\.29\.3\r\nAccess-Control-Allow-Origin:\x2
SF:0\*\r\nAccess-Control-Allow-Credentials:\x20true\r\nContent-Type:\x20te
SF:xt/plain;\x20charset=utf-8\r\nDate:\x20Sat,\x2013\x20Mar\x202021\x2009:
SF:33:47\x20GMT\r\nAccess-Control-Allow-Methods:\x20GET,\x20OPTIONS\r\nAcc
SF:ess-Control-Allow-Headers:\x20accept,\x20x-requested-with,\x20origin,\x
SF:20content-type,\x20cookie,\x20pragma,\x20cache-control,\x20x-auth-token
SF:\r\nAccess-Control-Max-Age:\x201209600\r\nContent-Length:\x202\r\n\r\nO
SF:K");
Device type: general purpose
Running: Linux 3.X
OS CPE: cpe:/o:linux:linux_kernel:3
OS details: Linux 3.7 - 3.9
Uptime guess: 0.241 days (since Fri Mar 12 22:47:04 2021)
Network Distance: 0 hops
TCP Sequence Prediction: Difficulty=261 (Good luck!)
IP ID Sequence Generation: All zeros

NSE: Script Post-scanning.
Initiating NSE at 04:34
Completed NSE at 04:34, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.46 seconds
           Raw packets sent: 65647 (2.891MB) | Rcvd: 131302 (5.519MB)
```

UDP 端口扫描

```
[root@CentOS7-1 ~]# nmap -sU 192.168.1.100

Starting Nmap 6.40 ( http://nmap.org ) at 2021-03-13 04:34 EST
Nmap scan report for 192.168.1.100
Host is up (0.0000040s latency).
All 1000 scanned ports on 192.168.1.100 are closed

Nmap done: 1 IP address (1 host up) scanned in 1.65 seconds
```