## 命令简介

host 命令是常用的分析域名查询工具，是一个 DNS 查找实用程序，用于查找域名的 IP 地址。 它还执行反向查找，查找与 IP 地址关联的域名。

host 命令可以用于执行 DNS 查找，将域名转换为 IP 地址，反之亦然。

```
[root@centos7 ~]# host 
-bash: host: command not found
[root@centos7 ~]# yum install -y bind-utils -y
```

## 语法格式

```
host [OPTIONS] {name} [server]
#主机(server)：指定要查询信息的主机信息。
```

## 选项说明

```
-a  #显示详细的DNS信息
-C  #查询指定主机的完整的SOA记录
-r  #在查询域名时，不使用递归的查询方式
-c<类型>  #指定查询类型
-t<类型>  #指定查询的域名信息类型
-W<时间>  #指定域名查询的最长时间
-v  #显示指令执行的详细信息
-w  #一直等待，直到域名服务器给出应答
-4  #使用IPv4
-6  #使用IPv6
```

## 应用举例

```
[root@centos7 ~]# host www.baidu.com
www.baidu.com is an alias for www.a.shifen.com.
www.a.shifen.com has address 36.152.44.95
www.a.shifen.com has address 36.152.44.96
```

显示过程详细信息

```
[root@centos7 ~]# host -a www.baidu.com
Trying "www.baidu.com"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47277
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.baidu.com.   IN ANY

;; ANSWER SECTION:
www.baidu.com.  30 IN CNAME www.a.shifen.com.

Received 58 bytes from 223.5.5.5#53 in 37 ms
```