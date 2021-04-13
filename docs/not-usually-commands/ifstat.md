## 命令简介

ifstat 命令用于统计网络接口流量状态，能比较简单看网络流量。ifstat 可以整齐地打印出网络接口统计信息，还可以用来禁用指定的网络接口。

## 语法格式

```
ifstat [OPTIONS]
```

## 选项说明

```
-a  #监测能检测到的所有网络接口的状态信息
-z  #隐藏流量是无的接口
-h  #显示帮助信息
-j  #用JSON格式输出信息
-n  #关闭显示周期性出现的头部信息
-t  #在每一行的开头加一个时间戳
-T  #报告所有监测接口的全部带宽
-w  #用指定的列宽
-W  #如果内容比终端窗口的宽度还要宽就自动换行
-S  #在同一行保持状态更新（不滚动不换行）
-q  #安静模式
-v  #显示版本信息
-d  #指定一个驱动来收集状态信息
```

## 应用举例

常见应用

```
[root@centos7 ~]# ifstat
#kernel
Interface        RX Pkts/Rate    TX Pkts/Rate    RX Data/Rate    TX Data/Rate  
                 RX Errs/Drop    TX Errs/Drop    RX Over/Rate    TX Coll/Rate  
lo                 40261 0         40261 0         2014K 0         2014K 0      
                       0 0             0 0             0 0             0 0      
ens33             385230 0        283301 0        44144K 0        77585K 0      
                       0 14            0 0             0 0             0 0    
```

监控指定接口

```
[root@centos7 ~]# ifstat   ens33
#kernel
Interface        RX Pkts/Rate    TX Pkts/Rate    RX Data/Rate    TX Data/Rate  
                 RX Errs/Drop    TX Errs/Drop    RX Over/Rate    TX Coll/Rate  
ens33                118 0            44 0          8712 0          5414 0      
                       0 0             0 0             0 0             0 0   
```