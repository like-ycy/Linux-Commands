## 命令简介

telnet 命令用于使用 TELNET 协议与另一个主机进行交互通信。可以对另一主机进行远程登录、管理操作，同样也可以通过telnet来确认远程主机的某个端口是否开放？也是日常网络故障排错的重要一部分。

## 语法格式

```
telnet [OPTIONS] [host [port]
[host]远程主机 #指定要登录进行管理的远程主机；
[port]端口    #指定TELNET协议使用的端口号。
```

## 选项说明

```
-4  #强制IPv4地址解析
-6  #强制进行IPv6地址解析
-a  #尝试自动登录远端主机系统
-b<主机别名>  #使用指定远端主机名称
-c  #不读取用户专属目录里的.telnetrc文件
-d  #启动排错模式
-e<脱离字符>  #设置脱离字符
-E  #滤除脱离字符
-K  #不自动登录远端主机
-l<用户名称>  #指定要登录远端主机的用户名称
-L  #允许输出8位字符资料
-n<记录文件>  #指定文件记录相关信息
-x  #假设主机有支持数据加密的功能就用它
-X<认证形态>  #关闭指定的认证形态
```

## telnet 服务配置

telnet 服务配置如下：

```
#通常参数配置，如下：
service telnet
{
    disable = no #启用
    flags = REUSE #socket可重用
    socket_type = stream #连接方式为TCP
    wait = no #为每个请求启动一个进程
    user = root #启动服务的用户为root
    server = /usr/sbin/in.telnetd #要激活的进程
    log_on_failure += USERID #登录失败时记录登录用户名
}
 
#配置允许登录的客户端列表
only_from = 10.0.0.2 #只允许10.0.0.2登录
 
#配置禁止登录的客户端列表
no_access = 10.0.0.{2,3,4}  #禁止10.08.0.2、10.0.0.3、10.0.0.4登录
 
#设置开放时段
access_times = 9:00-12:00 13:00-17:00 # 每天只有这两个时段开放服务

#配置用户只从某个地址登录telnet服务
bind = 10.0.0.2
```

## 应用举例

尝试打开与远程主机 baidu.com 的连接

```
[root@centos7 ~]# telnet www.baidu.com
Trying 36.152.44.96...
```

尝试使用登录名 mingongge 在端口 9999 上打开到远程主机 mingongget.com 的连接。如果连接成功，将会提示输入 mingongge 的密码

```
[root@centos7 ~]# telnet -l mingongge mingongge.com 9999
Trying 104.164.133.141...
```

查看某个端口是否开放

```
[root@centos7 ~]# telnet 127.0.0.1 22
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
SSH-2.0-OpenSSH_7.4
#出现上述信息则说明22端口已开放

#出现如下提示则说明相应的端口没有开放
[root@centos7 ~]# telnet 127.0.0.1 80
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
[root@centos7 ~]# telnet 127.0.0.1 9999
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
```