---
title: "说说我的fanqiang经验"
date: "2015-02-16"
---

今天有个朋友问我，有没有什么VPN推荐啊？ 我用的是[linode](https://www.linode.com/?r=0e6ffbe8fe1ed05af48108740db6a22632325d99)+L2TP方案，于是推荐给朋友。该方案适合有一定Linux基础，也愿意折腾折腾的朋友。如果不愿意折腾，也可以选择市面上在售的各类解决方案。

# 申请linode账号

第一步，申请Linode账号，根据自己的需要选择资费方案。 [![linode1](/wp-content/uploads/2015/02/linode1.png)](https://www.linode.com/?r=0e6ffbe8fe1ed05af48108740db6a22632325d99)

第二步，根据向导一步一步注册就好，在选择机房的时候可以根据自己的需要。我选择的是东京的机房，考虑到博客的读者主要都在国内。

# 下面重要说说如何搭建自己的VPN服务器（以L2TP为例）

下面的例子用的是ubuntu 12.4服务器版本，包含客户端的配置说明

## L2TP服务安装说明

sudo apt-get install xl2tpd openswan ppp

### IPSec/Openswan

/etc/ipsec.conf文件修改如下：

config setup
    nat\_traversal=yes
    virtual\_private=%v4:10.0.0.0/8,%v4:192.168.0.0/16,%v4:172.16.0.0/12,%v4:!10.152.2.0/24
    #contains the networks that are allowed as subnet= for the remote client. In other words, the address ranges that may live behind a NAT router through which a client connects.
    oe=off
    protostack=netkey
 
conn L2TP-PSK-NAT
    rightsubnet=vhost:%priv
    also=L2TP-PSK-noNAT
 
conn L2TP-PSK-noNAT
    authby=secret
    pfs=no
    auto=add
    keyingtries=3
    rekey=no
    # Apple iOS doesn't send delete notify so we need dead peer detection
    # to detect vanishing clients
    dpddelay=30
    dpdtimeout=120
    dpdaction=clear
    # Set ikelifetime and keylife to same defaults windows has
    ikelifetime=8h
    keylife=1h
    type=transport
    # Replace IP address with your local IP (private, behind NAT IP is okay as well)
    left=x.x.x.x
    # For updated Windows 2000/XP clients,
    # to support old clients as well, use leftprotoport=17/%any
    leftprotoport=17/1701
    right=%any
    rightprotoport=17/%any
    #force all to be nat'ed. because of iOS
    forceencaps=yes

确保在ipsec.conf文件中，"config setup" 和"conn l2tp-psk" 部分左边无空格，而其他行有8个空格缩进。 文件 "/etc/ipsec.secrets"修改如下：

x.x.x.x   %any:  PSK "somegoodpassword"

把 x.x.x.x替换成你的服务器IP地址 启动IPSEC服务

/etc/init.d/ipsec start

验证IPSEC服务可用

sudo ipsec verify

期待得到如下结果

Checking your system to see if IPsec got installed and started correctly:
Version check and ipsec on-path                                 \[OK\]
Linux Openswan U2.6.28/K2.6.32-32-generic-pae (netkey)
Checking for IPsec support in kernel                            \[OK\]
NETKEY detected, testing for disabled ICMP send\_redirects       \[OK\]
NETKEY detected, testing for disabled ICMP accept\_redirects     \[OK\]
Checking that pluto is running                                  \[OK\]
Pluto listening for IKE on udp 500                              \[OK\]
Pluto listening for NAT-T on udp 4500                           \[OK\]
Checking for 'ip' command                                       \[OK\]
Checking for 'iptables' command                                 \[OK\]
Opportunistic Encryption Support                                \[DISABLED\]

如果发生错误，请自行谷歌或百度解决。 上述如果是“”失败可以不用理会。 在"/etc/init.d/" 下创建文件 "ipsec.vpn"，内容如下：

case "$1" in
  start)
echo "Starting my Ipsec VPN"
iptables  -t nat   -A POSTROUTING -o eth0 -s 10.152.2.0/24 -j MASQUERADE
echo 1 > /proc/sys/net/ipv4/ip\_forward
for each in /proc/sys/net/ipv4/conf/\*
do
    echo 0 > $each/accept\_redirects
    echo 0 > $each/send\_redirects
done
/etc/init.d/ipsec start
/etc/init.d/xl2tpd start
;;
stop)
echo "Stopping my Ipsec VPN"
iptables --table nat --flush
echo 0 > /proc/sys/net/ipv4/ip\_forward
/etc/init.d/ipsec stop
/etc/init.d/xl2tpd stop
;;
restart)
echo "Restarting my Ipsec VPN"
iptables  -t nat   -A POSTROUTING -o eth0 -s 10.152.2.0/24 -j MASQUERADE
echo 1 > /proc/sys/net/ipv4/ip\_forward
for each in /proc/sys/net/ipv4/conf/\*
do
    echo 0 > $each/accept\_redirects
    echo 0 > $each/send\_redirects
done
/etc/init.d/ipsec restart
/etc/init.d/xl2tpd restart
 
;;
  \*)
 echo "Usage: /etc/init.d/ipsec.vpn  {start|stop|restart}"
 exit 1
  ;;
esac

上面这段配置的是防火墙跳转，如果你用的内部IP地址池不是10.152.2/24网段，请自行修改。 设置执行权限

sudo chmod 755 ipsec.vpn

禁用ipsec默认初始脚本

#update-rc.d -f ipsec remove

用上述刚才写的脚本替换默认脚本

#update-rc.d ipsec.vpn defaults

### L2TP

/etc/xl2tpd/xl2tpd.conf文件内容如下：

\[global\]
ipsec saref = no
 
\[lns default\]
ip range = 10.152.2.2-10.152.2.254
local ip = 10.152.2.1
require chap = yes
refuse pap = yes
require authentication = yes
ppp debug = yes
pppoptfile = /etc/ppp/options.xl2tpd
length bit = yes

1\. ip range = 给客户端分配的IP地址池 2. local ip = VPN服务器IP地址。注意要在上述"ip range"范围外。 3. refuse pap = refure pap 认证 4. ppp debug = 测试的时候设置为yes 选择一个严格的认证字符串。密码应该是16位长或更长。没有最小长度要求。密码存在文件/etc/xl2tpd/l2tp-secrets中

\* \* exampleforchallengestring

在文件/etc/ppp/options.xl2tpd中

refuse-mschap-v2
refuse-mschap
ms-dns 8.8.8.8
ms-dns 8.8.4.4
asyncmap 0
auth
crtscts
idle 1800
mtu 1200
mru 1200
lock
hide-password
local
#debug
name l2tpd
proxyarp
lcp-echo-interval 30
lcp-echo-failure 4

上述一般无需修改。

### 添加用户

修改文件 /etc/ppp/chap-secrets 如下：

client server secret IP
user1 l2tpd chooseagoodpassword \*
user2 \* chooseagoodpassword \*

1\. client = 用户名 2. server = 在ppp.options文件中定义的xl2tpd的名字 3. secret = 用户密码 4. IP Address = 设置为\*允许用户从任何地方登陆 注意：这里可以添加多个用户

### 跳转

修改文件 /etc/sysctl.conf 如下：

net.ipv4.ip\_forward=1

加载文件/etc/sysctl.conf 的新配置项

sysctl -p

### 启动VPN

sudo /etc/init.d/ipsec.vpn restart
sudo /etc/init.d/xl2tpd restart

## 用iOS设备连接VPN

1\. 设置 > 通用> 网络> VPN > 添加VPN配置 > L2TP 2. VPN 描述> VPN的名字 3. Set VPN server > VPN服务器的地址(x.x.x.x) 4. 账号> PPP 用户名 5. 密码 > 用户密码somegoodpassword 6. L2TP密码 > L2TP密码exampleforchallengestring 7. 用PPP的方式连接 username/password (user1 chooseagoodpassword)

## 用安卓设备连接VPN

1\. 设置 > 无线网络 > VPN 设置> 添加VPN > 添加L2TP/IPSec PSK VPN > 2. VPN 名字/ 描述> VPN名字 3. Set VPN server > VPN服务器的地址(x.x.x.x) 4. IPSec 密码 > somegoodpassword 5. 启用L2TP secret > 是 6. 设置L2TP Secret > 密码exampleforchallengestring 7. 用PPP的用户名和密码连接(user1 chooseagoodpassword)

参考文档：[https://help.ubuntu.com/community/L2TPServer](https://help.ubuntu.com/community/L2TPServer) 如果您想购买linode VPS，感谢使用我的推荐链接！

[linode购买链接](https://www.linode.com/?r=0e6ffbe8fe1ed05af48108740db6a22632325d99)
