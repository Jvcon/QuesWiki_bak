## Setting Wifi Client on Ubuntu Server

```bash
apt-get install wireless-tools wpasupplicant
vim /etc/network/interfaces
```

```conf
auto wlp3s0b1
iface wlp3s0b1 inet dhcp
pre-up ip link set wlp3s0b1 up
pre-up iwconfig wlp3s0b1 essid ssid
wpa-ssid wct
wpa-psk wct20161002
```

```bash
ifup -v wlp3s0b1
```