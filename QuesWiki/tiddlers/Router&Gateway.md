# 路由器与网管安装手册

## 基础联网功能

### DHCP联网

```
cat /etc/network/interfaces


```

### PPoE联网

编辑拨号配置文件`/etc/ppp`，也可以执行下面命令输入账号密码即可拨号上网

```
sudo pppoeconf
```


#### 单线程多拨

略

## 配置网桥

使用10.0.0.1/24作为内网ip，enp1s0作为外部网络（WAN）接口，其余接口作为局域网（LAN）接口

```
cat /etc/netplan/*.yaml
```

```
network:
    renderer: networkd
    ethernets:
        enp1s0:
          dhcp4: no
        enp2s0:
          dhcp4: no
        enp3s0:
          dhcp4: no
        enp4s0:
          dhcp4: no
        enp5s0:
          dhcp4: no
        enp6s0:
          dhcp4: no
    bridges:
      br0:
        addresses: [10.0.0.1/24,'ipv6全球路由前缀/64']
        dhcp4: no
        dhcp6: no
        accept-ra: no
        interfaces:
          - enp6s0
          - enp5s0
          - enp4s0
          - enp3s0
          - enp2s0
    version: 2
```

## ipv4/ipv6转发

```
sudo vim /etc/sysctl.conf
net.ipv4.ip_forward=1
net.ipv6.conf.all.forwarding=1
sudo sysctl -p
```

## Reference
[使用Ubuntu 18.04打造超级家庭网关](https://www.johnrosen1.com/ubuntu-router/)
[Linux 软路由单线多拨](https://www.zfl9.com/multi-wan-router.html)