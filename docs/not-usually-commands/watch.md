## 命令简介

watch 命令用于周期性的执行给定的命令，并将命令的输出以全屏方式显示。

watch 是一个非常实用的命令，基本所有的 Linux 发行版都带有这个小工具，watch 可以帮你监测一个命令的运行结果，无需你手动去重复运行某一个命令。

## 语法格式

```
watch [options] command
```

## 选项说明

```
-c, --color        #解释 ANSI 颜色和样式序列
-n 或--interval    #指定间隔的时间
-d 或--differences #会高亮显示变化的区域
-t 或-no-title     #关闭watch命令在顶部的时间间隔
-h, --help         #查看帮助文档
 -v, --version     #查看版本信息并退出
```

## 应用举例

间隔一秒高亮显示网络链接数的变化情况

```
[root@centos7 ~]# watch -n 1 -d netstat -ant
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)重复执行Uptime命令（默认是间隔2s）

```
[root@centos7 ~]# watch uptime
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

间隔10s打印一次系统平均负载信息

```
[root@centos7 ~]# watch -n 10 'cat /proc/loadavg'
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoMIfWb7sfk8zKYUwX8rM2EiaajEiaSy1Mp1O2YCKHEQcayBZF22lbyQFrhSwk0u4RKn5ckwv3LXRmQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

监控文件的变化

```
[root@centos7 download]# watch -d 'ls -l|grep mingongge'

[root@centos7 ~]# echo "122222333333333333333333333333323" > ./download/mingongge
[root@centos7 ~]# echo "333333333323" > ./download/mingongge
[root@centos7 ~]# echo "33399999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999923" > ./download/mingongge
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoMIfWb7sfk8zKYUwX8rM2Es7jc9kdsb90weu7RNJzNIVfcvdeVuiazq1lRKp2Olxq5opj80bAq1Pg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoMIfWb7sfk8zKYUwX8rM2ExNoq8srpSOBtQI8y2cbJG7HxcRqs4sgfvoHWXBzz4qMYBBcg7DVKCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoMIfWb7sfk8zKYUwX8rM2EaXxXadiclKnCY2zqbe9ibqRLunxPOiaBf29kfhSwU7wbobLzCiaC7VFHFQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)监测磁盘inode和block数目变化情况

```
[root@centos7 ~]# watch -n 1 "df -i;df" 
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPoMIfWb7sfk8zKYUwX8rM2EropiafglQLbPbxTORwYYs2PrKYlcm2WGG2XcA4Hv28npyibv5VEJRXnQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)