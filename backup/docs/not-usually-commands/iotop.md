## 命令简介

iotop 命令用来查看磁盘 I/O 使用状况的工具。iotop 具有与 top 相似的 UI界面，其展示的包括 PID、用户、I/O、进程等相关信息。

```
[root@centos7 ~]# iotop
-bash: iotop: command not found
[root@centos7 ~]# yum install iotop -y
```

## 语法格式

```
iotop [OPTIONS]
```

## 选项说明

```
-o  #只显示有io操作的进程
-b  #批量显示，无交互，主要用作记录到文件
-n NUM   #显示NUM次，主要用于非交互式模式
-d SEC   #间隔SEC秒显示一次
-p PID   #监控的进程pid
-u USER  #监控的进程用户
```

iotop 快捷键

```
左右箭头  #改变排序方式，默认是按IO排序
r  #改变排序顺序
o  #只显示有IO输出的进程
p  #进程/线程的显示方式的切换
a  #显示累积使用量
q  #退出
```

## 应用举例

```
[root@centos7 ~]# iotop
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPprOgoqjcg8PbItFPgrE550yZFU0rmLxVxbVTUofFuibw0gB0BlGRKZzcJ7en2ic3C54v9Dp8nNC9dw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

更多参数使用有兴趣的读者可以自已操作查看。