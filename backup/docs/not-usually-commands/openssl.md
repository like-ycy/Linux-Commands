## 命令简介

openssl 命令是强大的安全套接字层密码库。OpenSSL 是一种开源命令行工具，通常用于生成私钥，创建 CSR，安装 SSL / TLS 证书以及标识证书信息。

###### OpenSSL 运行模式

- 交互模式
- 批处理模式

直接输入 openssl 回车进入交互模式，输入带命令选项的 openssl 进入批处理模式。

```
[root@centos7 ~]# openssl
OpenSSL> version
OpenSSL 1.0.2k-fips  26 Jan 2017
```

OpenSSL 整个软件包大概可以分成三个主要的功能部分：**密码算法库、SSL 协议库以及应用程序**。

###### openssl 命令主要用途

- 创建和管理私钥，公钥和参数
- 公钥加密操作
- 创建 X.509 证书，CSR 和 CRL
- 消息摘要的计算
- 使用密码进行加密和解密
- SSL/TLS 客户端和服务器测试
- 处理 S/MIME 签名或加密的邮件
- 时间戳请求，生成和验证

## 语法格式

```
openssl command [ command_opts ] [ command_args ]
 
openssl [ list-standard-commands | list-message-digest-commands | list-cipher-commands | list-cipher-algorithms | list-message-digest-algorithms | list-public-key-algorithms]
 
openssl no-XXX [ arbitrary options ]
```

## 选项说明

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zA80Vtvztr0ReQOTDClpEeffhq8JOZia3MjDtfzfZxsAOBNedibTChkGIA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)读者可自行参考帮助文档 https://www.digicert.com/kb/ssl-support/openssl-quick-reference-guide.htm

## 应用举例

版本信息

```
[root@centos7 ~]# openssl version
OpenSSL 1.0.2k-fips  26 Jan 2017
[root@centos7 ~]# openssl version -a
OpenSSL 1.0.2k-fips  26 Jan 2017
built on: reproducible build, date unspecified
platform: linux-x86_64
options:  bn(64,64) md2(int) rc4(16x,int) des(idx,cisc,16,int) idea(int) blowfish(idx) 
compiler: gcc -I. -I.. -I../include  -fPIC -DOPENSSL_PIC -DZLIB -DOPENSSL_THREADS -D_REENTRANT -DDSO_DLFCN -DHAVE_DLFCN_H -DKRB5_MIT -m64 -DL_ENDIAN -Wall -O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches   -m64 -mtune=generic -Wa,--noexecstack -DPURIFY -DOPENSSL_IA32_SSE2 -DOPENSSL_BN_ASM_MONT -DOPENSSL_BN_ASM_MONT5 -DOPENSSL_BN_ASM_GF2m -DRC4_ASM -DSHA1_ASM -DSHA256_ASM -DSHA512_ASM -DMD5_ASM -DAES_ASM -DVPAES_ASM -DBSAES_ASM -DWHIRLPOOL_ASM -DGHASH_ASM -DECP_NISTZ256_ASM
OPENSSLDIR: "/etc/pki/tls"
engines:  rdrand dynamic 

#版本号和版本发布日期（OpenSSL 1.0.2k，2017年1月26日）
#使用库构建的选项（options）
#存储证书和私钥的目录（OPENSSLDIR）
```

生成密码功能

```
[root@centos7 ~]# openssl rand -base64 15
DYmkj+RY9QUcb4m5aoNV
[root@centos7 ~]# openssl rand -base64 10
RpyTN5W7BLznjA==
[root@centos7 ~]# openssl rand -base64 5
AeQaaBE=
```

消息摘要算法应用

```
#用SHA1算法计算文件openssl1.txt的哈西值
[root@centos7 ~]# openssl dgst -sha1 openssl1.txt
openssl1.txt: No such file or directory
[root@centos7 ~]# touch openssl1.txt
[root@centos7 ~]# openssl dgst -sha1 openssl1.txt
SHA1(openssl1.txt)= da39a3ee5e6b4b0d3255bfef95601890afd80709

#用SHA1算法计算文件openssl1.txt的哈西值，输出到文件sha1.txt
[root@centos7 ~]# openssl sha1 -out sha1.txt openssl1.txt
[root@centos7 ~]# cat sha1.txt
SHA1(openssl1.txt)= da39a3ee5e6b4b0d3255bfef95601890afd80709
```

对称加密应用

```
#给文件openssl1.txt用base64编码，输出到文件jiami.txt
[root@centos7 ~]# cat openssl1.txt 
openssl
[root@centos7 ~]# openssl base64 -in openssl1.txt -out jiami.txt
[root@centos7 ~]# cat jiami.txt 
b3BlbnNzbAo=
```

DSA 应用

```
#生成1024位DSA参数集，并输出到文件jm.pem
[root@centos7 ~]# openssl dsaparam -out jm.pem 1024
Generating DSA parameters, 1024 bit long prime
This could take some time
........+...........+..................+.....+..............+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*
.+...+..........+......+.....+..+......+.........+.........+.................+............+...........+..................+...........+........+............+....+.+......+....+...............................+.................+.................+.+......+.......+..........+........+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*
[root@centos7 ~]# cat jm.pem 
-----BEGIN DSA PARAMETERS-----
MIIBHgKBgQCR+2rHHnotQERnaw1i3PaeeGyhZHP7Mjih9RAnNRv3oe+HO2AgiLgr
vWLbT/oRNZhdnvuW8u8b1dmm9xPwwAfkNt0cPyH+28HNJ6ImoO9qQCBVlgPnwmah
WPtA9TXIw7kJVOCUImKKXkbQvKOvlXsTgFHhhQ9GAt9gbHxmWVhqjwIVANzDXsuC
hXZDNAR6O0Dke4p/4H1XAoGAHzT3cByKaD0IN0zCXA0yXMNlyDtE8w7dlv37LcaR
7u0ZV1r4zof/g7Pf+GCHbkVUVPzTrrlkn1Wfqtl2QsmT73jMBwPl+z3Oj7DyFb8J
Nm66epCO1uLaXoIubTZa4QFCuuTarWouizo4qDYQg/vYRDBQK8N5nIh8Wfnte9gq
zTY=
-----END DSA PARAMETERS-----
```

RSA 应用

```
#产生1024位RSA私匙，用3DES加密它，口令为mingongge，输出到文件rsa.pem
[root@centos7 ~]# openssl genrsa -out rsa.pem -passout pass:mingongge -des3 1024
Generating RSA private key, 1024 bit long modulus
....................++++++
...............++++++
e is 65537 (0x10001)
[root@centos7 ~]# cat rsa.pem 
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: DES-EDE3-CBC,34B51F9BE30A3448

uvI8+9g2NGBS+t6VoxUW9JvjiSSnXAHVgJXFsiPtQRIQq3tUEv48QVXOXrLMSTei
DOmScLCrU0X+il+Kl2HtTEqmqzxmP+HlbiahSMthTbXUEcqSnKt/80UxzsKFWsag
lYj5yl+skQoMYLHt0JSc2MlWA6tAHPdEb4/BoEN0zerhgVcXDlLeFXm7ni1tUmVj
mbHmM1TV03kxxzd8KQhFsQkwT/aDtm143rxVrD3NpSS4eXbzm8D4B2A3L0DMaUzk
cAql+iggvH4vS3BCKOX6h5Zr9Vyo4CGjvYSyvkASbc+fVKgvmPM9KP0+hedUH2Hc
55K1ND5S0TWa2qFWk511tKbpBT9RM5P7ipcnr3tyya/RSpVZT7EpEUm+EokOrvHg
SY6AgPSojYdDL3/WrQvJAkMQmuckpEW1lNYGSgFsQmRN8gFb8LXhr+uUf8psT3D9
+Cvo5ynkocW1P1sHpJHuA7WtW7SaRbBGwEoPKjzAfKaV41oz9Sknn1PE5LXpvtIA
zn/vVbKVQvD3ho2I2RuX5vtI7Jvy/TeKDOO9fAuNKqlR7/MmqE7OiKZovuh2xHRk
3d3qif8uH6dCe7l6rElqgONNkYYJ/dBgJ+ZV15ahJFNK10JoBqFgF9dj+vFumWGt
7FuN2kk7Qe1YSn13ZZ7M10EWDPxaMXSnjynazC8MLnokRwf1SwqsZW250J9/dbvt
BEE00IQWC+RmaRgJV+H+3gvCHyMZBRGaxUKiOftrM9Ir3w28wk2jwgSm6v6p/WUg
4JUMPAqjft82lv+MwfKn4OHnuIyfgrZGB6+oR52BToQ=
-----END RSA PRIVATE KEY-----
```