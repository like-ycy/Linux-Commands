## 命令简介

ntpddate 命令用于使用网络计时协议（NTP）设置日期和时间。还可以用于同步时间，此命令需要具备root管理员权限才可执行。

```
[root@centos7 ~]# ntpdate
-bash: ntpdate: command not found
[root@centos7 ~]# yum install ntpdate -y
```

## 语法格式

```
ntpdate [ -b] [ -d] [ -s] [ -u] [ -aKeyid] [ -eAuthenticationDelay] [ -kKeyFile] [ -oVersion] [ -pSamples] [ -tTimeOut] Server...
```

## 选项说明

```
-aKeyid  #使用 Keyid 来认证全部数据包
-b       #通过调用 settimeofday 子例程来增加时钟的时间
-d       #指定调试方式
-eAuthenticationDelay   #指定延迟认证处理的时间秒数。
-oVersion      #指定使用的 NTP 版本实现
-pSamples      #指定从每个服务器获取的样本的数目
-s          #指定日志操作
-tTimeOut   #指定等待响应的时间
-u          #指定使用无特权的端口发送数据包
```

## 应用举例

同步时间

```
[root@centos7 ~]# date
Sun Mar 28 13:09:22 EDT 2021
[root@centos7 ~]# ntpdate 0.centos.pool.ntp.org
28 Mar 23:11:13 ntpdate[5516]: step time server 182.92.12.11 offset 36090.505486 sec
[root@centos7 ~]# date
Sun Mar 28 23:11:21 EDT 2021

[root@centos7 ~]# ntpdate 0.centos.pool.ntp.org
28 Mar 23:11:55 ntpdate[5519]: step time server 182.92.12.11 offset -0.722305 sec
[root@centos7 ~]# ntpdate asia.pool.ntp.org;hwclock -w
28 Mar 23:12:28 ntpdate[5520]: adjust time server 133.243.238.163 offset -0.013789 sec
```