## 命令简介

passwd创建或修改用户的密码，passwd命令用于设置用户的认证信息，包括用户密码、密码过期时间等。系统管理者则能用它管理系统用户的密码。只有管理者可以指定用户名称，一般用户只能变更自己的密码。

普通用户在更改自己的密码之前，必须先输入当前密码进行验证（超级用户无需此步骤）。[一款超牛逼的 Linux 终端复用神器（附安装、使用教程）](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247503203&idx=1&sn=97c2451998647305b37b014a2823dc87&chksm=e918a87fde6f2169172d40bf1b8cfc3cca18b96799dc169fba566353e423f91a6ddd116ef15f&scene=21#wechat_redirect)

设置密码时需要符合系统对密码复杂性的要求。一般准则，密码应至少包含6个字符，包括以下每个字符中的一个或多个：[值得收藏！Linux系统常用命令速查手册](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247500085&idx=2&sn=5455a50a3ec0fc0a69a7cc910a316ebe&chksm=e918a429de6f2d3f4ba700653b387459cb16dd4bf34cd42b4b0ef53c2dd91a53ce40abf0f2a2&scene=21#wechat_redirect)

- 小写字母
- 数字0到9
- 标点符号

## 语法格式

```
passwd [选项] [username]
```

## 选项说明

```
-d  #删除密码
-f  #强迫用户下次登录时必须修改口令
-w  #口令要到期提前警告的天数
-k  #更新只能发送在过期之后
-l  #锁定账号使用
-S  #显示密码信息
-u  #启用已被停止的账户
-g  #修改群组密码
-S  #列出密码相关参数，即shadow文件内的大部分信息
-n  #后面接天数，shadow的第4字段，多久不可修改密码
-x  #后面接天数，shadow的第5字段，多久内必须要改动密码
-w  #后面接天数，shadow的第6字段，密码过期前的警告天数
-i  #后面接“日期”，shaodow的第7字段，密码失效日期
--help     #显示帮助信息
--version  #显示版本信息
--stdin    #从标准输入中读入新密码（此时可以看见设置的密码）
```

## 应用实例

修改用户密码

```
[root@mingongge ~]# passwd test  #设置test用户的密码
Enter new UNIX password:        #输入新密码，输入的密码无回显
Retype new UNIX password:       #确认密码
passwd: password updated successfully
```

显示账号密码信息

```
[root@mingongge ~]# passwd -S mingongge
mingongge P 12/25/2020 0 99999 7 -1
```

删除用户密码

```
[root@mingongge ~]# passwd -d mingongge
passwd: password expiry information changed.
```

锁定一个用户

```
[root@localhost ~]$ passwd -l mingongge     #锁定用户mingongge不能更改密码
Locking password for user mingongge.
passwd: Success                           #锁定成功
[root@localhost ~]# su mingongge    #切换到mingongge用户；
[mingongge@localhost ~]$ passwd     #来更改mingongge密码
Changing password for user mingongge.
Changing password for mingongge
(current) UNIX password:           #输入mingongge的当前密码
passwd: Authentication token manipulation error      #失败，不能更改密码
```

清除一个用户的密码

```
[root@localhost ~]$ passwd -d mingongge   #清除mingongge用户密码
Removing password for user mingongge.
passwd: Success                          #清除成功； 
[root@localhost ~]# passwd -S mingongge    #查询用户密码状态
Empty password.                          #空密码，也就是没有密码
```

注意：清除一个用户的密码之后，就代表着这个用户是没有密码了，也就是空密码可以登录。