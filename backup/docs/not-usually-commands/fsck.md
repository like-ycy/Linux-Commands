## 命令简介

fsck 命令用于检查并修复Linux文件系统。

fsck 用于对“文件系统一致性检查”。在大多数系统上，如果检测到某些情况，fsck 将在引导时运行。通常，这些条件是：

- 文件系统被标记为“dirty” –--其写入状态与计划写入的数据不一致
- 文件系统已挂载了一定次数而未检查

无论文件系统类型如何，fsck通常具有三种操作模式：

- 检查错误，并交互提示用户决定如何解决单个问题
- 检查错误，并尝试自动修复任何错误
- 检查错误，不尝试修复它们，而是在标准输出上显示错误

## 语法格式

```
fsck [-lsAVRTMNP] [-C [fd]] [-t fstype] [filesys...]
     [--] [fs-specific-options]
```

## 选项说明

```
-a  #自动修复文件系统，不进行提示
-A  #按/etc/fstab文件配置的内容，检查文件内所列的全部文件系统
-N  #不执行指令，仅列出实际执行会进行的动作
-P  #当搭配"-A"参数使用时，则会同时检查所有的文件系统
-r  #采用互动模式，在执行修复时询问问题，让用户得以确认并决定处理方式
-R  #当搭配"-A"参数使用时，则会略过/目录的文件系统不予检查
-s  #依序执行检查作业，而非同时执行
-t<文件系统类型>  #指定要检查的文件系统类型
-T  #执行fsck指令时，不显示标题信息
-V  #显示指令执行过程
```

## 应用举例

```
[root@centos7 ~]# fsck /dev/sda1
fsck from util-linux 2.23.2
If you wish to check the consistency of an XFS filesystem or
repair a damaged filesystem, see xfs_repair(8).
[root@centos7 ~]# fsck
fsck from util-linux 2.23.2
```

执行检查，只输出错误信息不作任何修复动作

```
[root@centos7 ~]# fsck -n /dev/sda1
fsck from util-linux 2.23.2
If you wish to check the consistency of an XFS filesystem or
repair a damaged filesystem, see xfs_repair(8).
```

fsck返回的代码是一个唯一数字,，其中意思如下：

```
0  #无错误
1  #已纠正文件系统错误
2  #应重新启动系统
4  #未纠正文件系统错误
8  #操作错误
16   #使用或语法错误
32   #用户请求取消Fsck
128  #共享库错误
```