## 命令简介

ssh ( Secure Shell )命令是用于安全登录到远程系统的协议，它可用于在远程服务器上记录或执行命令。

ssh（SSH 客户端）是用于登录到远程计算机并在远程计算机上执行命令的程序。可以在不安全的网络中于两个不受信任的主机之间提供安全的加密通信。

## 语法格式

```
ssh [OPTIONS] [-p PORT] [USER@]HOSTNAME [COMMAND]
```

## 选项说明

```
-4 #强制ssh协议只使用IPv4地址
-6 #强制ssh协议只使用IPv6地址
-A #启用来自身份验证代理的连接转发
-a  #禁用身份验证代理连接的转发
-B bind_interface  #绑定到的地址 bind_interface在尝试连接到目标主机之前
-b bind_address    #使用 bind_address在本地计算机上作为连接的源地址
-C  #请求压缩所有数据
-c cipher_spec  #指定用于加密会话的密码规范
-D [bind_address：] 端口  #指定本地“动态”应用程序级端口转发
-E log_file   #将调试日志附加到 log_file 而非标准错误
-e escape_char  #设置带有pty的会话的转义字符（默认值：' ~'）
-F 配置文件  #指定每用户ssh的配置文件 
-f  #配置ssh在执行命令之前将请求转到后台 
-g  #允许远程主机连接到本地转发的端口
-i identity_file  #指定从这个文件中去读取用于公共密钥身份验证的标识（私有密钥）
-K  #启用基于GSSAPI的身份验证
-k  #禁用将GSSAPI凭据
-L local_socket：remote_socket  #指定将与本地（客户端）主机上给定的TCP端口或Unix套接字的连接转发到远程的给定主机和端口或Unix套接字。
-N  #禁止执行远程命令 
-p port  #指定SSH连接端口
-q  #静默模式
-s  #用于请求调用远程系统上的子系统
-T  #禁用分配伪终端
-t  #强制分配伪终端
-V  #打印SSH版本号并退出
-v  #详细模式（输出SSH连接的过程信息）
-X  #启用X11转发
-x  #禁用X11转发
-Y  #启用受信任的X11转发
-y  #指定发送日志信息 syslog（3）系统模块
```

## 应用举例

连接到远程主机

```
ssh username@remote_host

#ssh 使用特定身份（私钥）连接到远程主机
ssh -i path/to/key_file username@remote_host
```

使用特定端口连接到远程主机

```
ssh username@remote_host -p 9999
```

用SSH连接到远程服务器上再运行命令

```
ssh remote_host command
[root@centos7 ~]# ssh 192.168.1.199 ls
The authenticity of host '192.168.1.199 (192.168.1.199)' can't be established.
ECDSA key fingerprint is SHA256:mF2QLxkGH/mWhHu/NlaKOrx4nKkyVvhYV6BRPA8TdEk.
ECDSA key fingerprint is MD5:a1:91:03:6b:9a:91:f6:c3:cf:19:06:32:19:b9:85:8e.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.1.199' (ECDSA) to the list of known hosts.
root@192.168.1.199's password: 
anaconda-ks.cfg
dos_test.txt
goinception
goInception-linux-amd64-v1.2.3.tar.gz
httpd
httpd-2.4.46
httpd-2.4.46.tar.gz
mingongge.file
mingongge.z01
mingongge.z02
mingongge.zip
testdir
test.txt
```

查看一下SSH远程登录过程的详细信息

```
[root@centos7 ~]# ssh -v 192.168.1.199 -p 22
OpenSSH_7.4p1, OpenSSL 1.0.2k-fips  26 Jan 2017
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 58: Applying options for *
debug1: Connecting to 192.168.1.199 [192.168.1.199] port 22.
debug1: Connection established.
debug1: permanently_set_uid: 0/0
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_rsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_rsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_dsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_dsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_ecdsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_ecdsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_ed25519 type -1
debug1: key_load_public: No such file or directory
debug1: identity file /root/.ssh/id_ed25519-cert type -1
debug1: Enabling compatibility mode for protocol 2.0
debug1: Local version string SSH-2.0-OpenSSH_7.4
debug1: Remote protocol version 2.0, remote software version OpenSSH_7.4
debug1: match: OpenSSH_7.4 pat OpenSSH* compat 0x04000000
debug1: Authenticating to 192.168.1.199:22 as 'root'
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ecdsa-sha2-nistp256
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: curve25519-sha256 need=64 dh_need=64
debug1: kex: curve25519-sha256 need=64 dh_need=64
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: ecdsa-sha2-nistp256 SHA256:mF2QLxkGH/mWhHu/NlaKOrx4nKkyVvhYV6BRPA8TdEk
debug1: Host '192.168.1.199' is known and matches the ECDSA host key.
debug1: Found key in /root/.ssh/known_hosts:1
debug1: rekey after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey after 134217728 blocks
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<rsa-sha2-256,rsa-sha2-512>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Next authentication method: gssapi-keyex
debug1: No valid Key exchange context
debug1: Next authentication method: gssapi-with-mic
debug1: Unspecified GSS failure.  Minor code may provide more information
No Kerberos credentials available (default cache: KEYRING:persistent:0)

debug1: Unspecified GSS failure.  Minor code may provide more information
No Kerberos credentials available (default cache: KEYRING:persistent:0)

debug1: Next authentication method: publickey
debug1: Trying private key: /root/.ssh/id_rsa
debug1: Trying private key: /root/.ssh/id_dsa
debug1: Trying private key: /root/.ssh/id_ecdsa
debug1: Trying private key: /root/.ssh/id_ed25519
debug1: Next authentication method: password
root@192.168.1.199's password: 
debug1: Authentication succeeded (password).
Authenticated to 192.168.1.199 ([192.168.1.199]:22).
debug1: channel 0: new [client-session]
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: Sending environment.
debug1: Sending env LANG = en_US.UTF-8
Last login: Sun Jan 17 14:26:28 2021 from 192.168.1.93
```