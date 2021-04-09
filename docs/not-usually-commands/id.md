## 命令简介

id 命令用于查看用户的 UID\GID 及所属的用户组等信息。

需要注意的就是：UID在系统中是唯一的，也是用户的身份标识，但GID可以对应多个UID(简单理解就是一个用户可以加入多个用户组)。

## 语法格式

```
id [OPTIONS][用户名称]
```

## 选项说明

```
-g  #显示用户所属群组的ID
-G   #显示用户所属附加群组的ID
-n  #显示用户，所属群组或附加群组的名称
-r  #显示实际ID
-u  #显示用户ID
-Z   #仅打印当前用户的安全上下文
-help   #打印帮助信息
-version      #打印版本信息
```

## 应用举例

```
[root@centos7 ~]# id
uid=0(root) gid=0(root) groups=0(root)
#root 的 UID = 0，GID = 0

[root@centos7 ~]# id -a
uid=0(root) gid=0(root) groups=0(root)
[root@centos7 ~]# id -g
0
[root@centos7 ~]# id -G
0
[root@centos7 ~]# id mingongge
uid=1000(mingongge) gid=1000(mingongge) groups=1000(mingongge)
```