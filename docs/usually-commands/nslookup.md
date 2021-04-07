## 命令简介

nslookup（name server lookup）命令用于查询域名 DNS 信息的工具。nslookup 有两种工作模式，即“交互模式”和“非交互模式”。

```
[root@CentOS7-1 ~]# nslookup
-bash: nslookup: command not found
[root@CentOS7-1 ~]# yum install -y bind-utils
```

## 语法格式

```
nslookup [-option] [name | -] [server]
```

## 选项说明

```
-query=TYPE      #设置查询类型
-timeout=NUMBER  #设置等待响应的超时时间，单位秒
-sil             #不显示任何警告信息。
```

还有一些交互的命令，有兴趣的读者可以查看帮助信息阅读。![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPp03cvks6ldZUKY33Gp5A09loJiblicdtrrTHStrDqBumYAl5Z4VfjkXJkLTnjT1qU5edA5UbiaNuwXQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 应用举例

实例

```
非交互式模式
[root@CentOS7-1 ~]# nslookup www.baidu.com
Server:  223.5.5.5
Address: 223.5.5.5#53

Non-authoritative answer:
www.baidu.com canonical name = www.a.shifen.com.
Name: www.a.shifen.com
Address: 36.152.44.96
Name: www.a.shifen.com
Address: 36.152.44.95

#交互式模式
[root@CentOS7-1 ~]# nslookup
> baidu.com
Server:  223.5.5.5
Address: 223.5.5.5#53

Non-authoritative answer:
Name: baidu.com
Address: 39.156.69.79
Name: baidu.com
Address: 220.181.38.148
> 163.com
Server:  223.5.5.5
Address: 223.5.5.5#53

Non-authoritative answer:
Name: 163.com
Address: 123.58.180.7
Name: 163.com
Address: 123.58.180.8
```

google.com 相关的信息

```
#在您的 DNS 中查询与域名 google.com 相关的所有可用信息。
[root@CentOS7-1 ~]# nslookup -type=any google.com
Server:  223.5.5.5
Address: 223.5.5.5#53

Non-authoritative answer:
Name: google.com
Address: 93.46.8.90
google.com nameserver = ns1.google.com.
google.com nameserver = ns2.google.com.
google.com nameserver = ns4.google.com.
google.com nameserver = ns3.google.com.

Authoritative answers can be found from:

#在您的 DNS 中查询与域名 google.com 相关邮件交换服务器的信息
[root@CentOS7-1 ~]# nslookup -type=mx google.com
Server:  223.5.5.5
Address: 223.5.5.5#53

Non-authoritative answer:
google.com mail exchanger = 10 aspmx.l.google.com.
google.com mail exchanger = 50 alt4.aspmx.l.google.com.
google.com mail exchanger = 20 alt1.aspmx.l.google.com.
google.com mail exchanger = 30 alt2.aspmx.l.google.com.
google.com mail exchanger = 40 alt3.aspmx.l.google.com.

Authoritative answers can be found from:
```

反向查找一个地址(文中地址作了处理哈)

```
[root@CentOS7-1 ~]# nslookup 200.208.150.3
 
Server:         103.240.22.111
Address:        103.240.22.111#53
 
Non-authoritative answer:
3.150.208.200.in-addr.arpa      name = 200.208.150.3.xmission.com.
 
Authoritative answers can be found from:
150.208.200.in-addr.arpa        nameserver = ns1.xmission.com.
150.208.200.in-addr.arpa        nameserver = ns2.xmission.com.
150.208.200.in-addr.arpa        nameserver = ns.xmission.com.
```