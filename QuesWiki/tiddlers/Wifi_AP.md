Setting of wifi ap

# Setting of wifi in ap-mode on Ubuntu Server

安装网卡驱动

```bash
# 查看USB网卡设备，找出对应型号
& lsusb
# 查看网卡信息
& ifconfig -a
# 开启或关闭网卡
ifconfig wlan0 up
ifconfig wlan0 down
```

```bash
& git clone https://github.com/quickreflex/rtl8188eus
& cd rtl8188eus
& make all
& make install
```

配置wlan0

```bash
& vim /etc/network/interfaces

allow-hotplug wlx14cf92b424d5
iface wlx14cf92b424d5  inet static
address 192.168.3.1
netmask 255.255.255.0
```

修改ipv4内部转发

```bash
& vim /etc/sysctl.conf

net.ipv4.ip_forward = 1  # 把0改成1
```

修改防火墙规则

```bash
#清空规则
iptables -F
iptables -t nat -nL
#在filter表中添加一条FORWARD规则
iptables -A FORWARD --in-interface wlx14cf92b424d5 -j ACCEPT
iptables -nL
#在nat表中添加一条POSTROUTING路由规则
iptables --table nat -A POSTROUTING --out-interface eth0 -j MASQUERADE
iptables -t nat -nL
```

保存防火墙规则

```bash
iptables-save > /etc/iptables-rules
ip6tables-save > /etc/ip6tables-rules
```

恢复防火墙规则

```bash
iptables-restore < /etc/iptables-rules
ip6tables-restore < /etc/ip6tables-rules
```

配置Hostapd

```bash
& vim /etc/hostapd/hostapd.conf

#配置详情如下
interface=wlx14cf92b424d5
driver=nl80211
ssid=XXXXXXXX
hw_mode=g
channel=11
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=********
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

hostapd开机启动

```bash
& vim /etc/default/hostapd

#把 #DAEMON_CONF="" 改为 DAEMON_CONF="/etc/hostapd/hostapd.conf"
DAEMON_CONF="/etc/hostapd/hostapd.conf"

& vim/etc/init.d/hostapd

#指定配置文件DAEMON_CONF=/etc/default/hostapd
DAEMON_CONF=/etc/default/hostapd

#启动hostapd
& /etc/init.d/hostapd start

#设置自启动
& update-rc.d hostapd enable
```

配置udhcpd

```bash
& vim /etc/udhcpd.conf

# The start and end of the IP lease block

start   192.168.3.20    #default: 192.168.0.20
end 192.168.3.254   #default: 192.168.0.254


# The interface that udhcpd will use

interface   wlx14cf92b424d5 #default: eth0

# Setting of DHCP
opt dns 8.8.8.8 114.114.114.114
option  subnet  255.255.255.0
opt router  192.168.3.1
opt wins    192.168.3.10
option  dns 129.219.13.81   # appened to above DNS servers for a total of 3
option  domain  local
option  lease   864000  # 10 days of seconds

```

udhcpd开启启动

```bash
& vim /etc/default/udhcpd

DHCPD_ENABLED="yes"

& update-rc.d udhcpd enable
```