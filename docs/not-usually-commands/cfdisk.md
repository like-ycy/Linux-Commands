## 命令简介

cfdisk 命令可用于显示有关磁盘分区表的信息。它的功能与 [fdisk](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247510540&idx=6&sn=4f08021e7678cdf302fa16852118721a&chksm=e918cf10de6f460691ae5f470a666485db6414948710dddfc65ac26844741fc227d6233acb24&scene=21#wechat_redirect)相同，但它具有基于文本的“图形”界面，在操作与可视化方面更加的直观，易于使用，也非常的便捷。

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrlDB7iap74rbt5tljXbIgNosTmJ54nG5UvvlmEhNFZU8oftN8CWd1Nfw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上面就是cfdisk的图形化界面

## 语法格式

```
cfdisk [-agvz] [-c cylinders] [-h heads] [-s sectors-per-track]  [-P opt] [device]
```

## 选项说明

```
-a #使用箭头光标突出显示当前分区
-g #不要使用磁盘驱动程序给出的几何图形
-v #打印版本号和版权
-z #从零位分区表开始
-s sectors-per-track   #覆盖从BIOS读取的每个磁道的柱面数，磁头数和扇区数。
```

## 应用举例

直接输入cfdisk命令进入图形界面![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrJxmDGhVeLr9bUCvIdWfWHsq256OUK6ofaISHANsp0VfwXJLNq3iaeug/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

按上下箭头键选择磁盘名字![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrqjvUpgZyYkETx5m19ertZrLhsibR4JB2m8LVPN0M7lke3ppxFljbF3g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

查看帮助信息![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrSs37TcWPEEeyM8gPpicQlhCCN2ibHufyN08Jte97NxTP8jT2z84NmqMA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

基本的使用与fdisk一样，磁盘新建分区![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrotkiaUyCfPsSPD6piaAfSYVY8k47Wps30xibZE3jsUEibEbbFYYnaaSzCA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

选择分区类型![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFruibOgv69JgLmQoZaW5oDicmB55QHyn1zH6ScQ6fZA6OdJMUrl2e02wUQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

选择分区大小![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrpZ0jyqBSHicVdvvGEhCmp7glibKdOMpgyryAZkicIMchVmhibtF4BZxVqg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

操作写入磁盘![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpCF2icTSH7m7Y0NQwcdSYFrueal0bmWhC6rNibH0u0Q6KYPss7qZZwYIM3aBMssCLeaMBXONEF62ng/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)