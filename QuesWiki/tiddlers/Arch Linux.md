# Installation of Archlinux

## 分区与挂载

* 分区方法
	* 可以通过PE等工具进行分区，能够自由控制分区大小
	* 使用cfdisk进行分区
* 格式化与激活swap
	* 格式化分区
             ```bash
            mkfs.ext4 /dev/sda2
            mkfs.ext4 /dev/sda3
            mkfs.ext4 /dev/sda4
            ```
	* 格式化swap分区并启用
           ```bash
            mkswap /dev/sda1
            swapon /dev/sda1
            ```
	* 挂载
            ```bash
            mount /dev/sda2 /mnt
            mkdir /mnt/boot
            mount /dev/sda3 /mnt/boot
            mkdir /mnt/home
            mount /dev/sda4 /mnt/home
            ```

 Hint: 分区视使用功能而定，下表作为参考

**For Desktop**       

| 挂载点        | 设备            | 说明               |
| ------------- | :-------------: | -----:             |
| swap          | `/dev/sda1`     | 约内存大小         |
| /boot         | `/dev/sda2`     | 200MB              |
| /             | `/dev/sda3`     | 15~20G             |
| /home         | `/dev/sda4`     | 剩余最大空间的一半 |
| /usr          | `/dev/sda5`     | 剩余最大空间的一半 |
 **For Server**

| 挂载点   | 设备        | 说明                  |
| -------- | :-----------: | --------------------: |
| swap     |`/dev/sda1`   | 约内存大小            |
| /boot    | `/dev/sda2`   | 200MB                 |
| /        | `/dev/sda3`   | 15~20G                |
| /var     | `/dev/sda4`   | 视服务器功能决定      |
| /home    | `/dev/sda5`   | 剩余最大空间的一半    |
| /usr     | `/dev/sda6`   | 剩余最大空间的一半    |

## 基础安装
1. 查看连接网络

    ```bash
    ifconfig -a
    iwconfig
    dhcpcd //启用有线网络
    rfkill liss //查看无线网卡是否被rf锁定
    rfkill list //如果有，则解除
    rfkill unblock all
    ip link set wlp21s0 up //wlp21s0网卡名称
    iwlist wlp21s0 scanning
    nano /etc/wpa_supplicant/wifi.conf
    //在wifi.conf中写入无线配置
    network={
        ssid=“无线SSID名称”
        psk=“无线密码“
        }
    wpa_supplicant -BDwext -i wlp21s0 -c /etc/wpa_supplicant/wifi.conf //启用配置文件
    dhclient wlp21s0 //激活网络服务
    ping -c 4 http://www.baidu.com //测试网络
    ```

2. 设置软件源

    ```bash
    nano /etc/pacman.d/mirrorlist

     中国国内软件源
    >Server = http://mirrors.163.com/archlinux/$repo/os/$arch
    >Server = http://mir
    rors.sohu.com/archlinux/$repo/os/$arch
    >Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
    ```

3. 安装基本系统

    ```bash
    pacstrap /mnt base base-level
    ```

4. 生成fstab

    ```bash
    genfstab -U -p /mnt >> /mnt/etc/fstab
    ```

5. 检查生成的fstab是否正确

    ```bash
    nano /mnt/etc/fstab
    ```

## 引导、账户配置
1. 切换root目录至安装电脑

    ```bash
    arch-chroot /mnt /bin/bash
    ```

2. 设置Locale

    ```bash
    nano /etc/locale.gen
    ```

    内容大致修改为
    >en_US.UTF-8 UTF-8
    >zh_CN.UTF-8 UTF-8
    >zh_TW.UTF-8 UTF-8

3. 生成locale讯息

    ```bash
    locale-gen
    ```

4. 创建locale.conf

    ```bash
    echo LANG=en_US.UTF-8 > /etc/locale.conf
    ```

5. 设置时区

    ```bash
    ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
    ```

6. 设置硬件时间

    ```bash
    hwclock --systohc --utc
    ```

7. 设置主机名

    ```bash
    echo archlinuxpc > /etc/hostname
    ```

8. 并在/etc/hosts添加同样的主机名

    ```bash
    nano /etc/hosts
    ```
    内容大致修改为
    ><ip-address> <hostname.domain.org> <hostname>
    >127.0.0.1 localhost.localdomain localhost archlinuxpc
    >::1 localhost.localdomain localhost archlinuxpc

9. 设置自动连接有线网络

    ```bash
    systemctl start dhcpcd
    systemctl enable dhcpcd
    ```

10. 设置Root密码

    ```bash
    passwd
    ```

11. 安装GRUB

    ```bash
    pacman -S grub os-prober
    grub-install --target=i386-pc --recheck /dev/sda
    grub-mkconfig -o /boot/grub/grub.cfg
    ```

12. 卸载分区并重启机器

    ```bash
    exit # 退回安装环境
    umount -R /mnt/boot
    umount -R /mnt/boot
    umount -R /mnt #卸载前面所有挂载的分区
    reboot
    ```

Note! 重启之前请移除安装盘

## 基础部署
1.  添加用户和设置密码
    ```bash
    useradd -m -g users -s /bin/bash 用户名
    passwd 用户名
    ```
2. 添加archlinuxcn的源
    ```bash
    sudo gedit /etc/pacman.conf
    ```
    pacman.conf末尾处添加
    > [archlinuxcn]
    > SigLevel = Optional TrustAll
    > Server = http://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch

3. 更新系统
    ```bash
    pacman -Syu
    ```
4. 检查一下Locale和时间设置

5. 安装X.org
X.Org 是 X Window System 的开源实现。如果我们要在 Arch Linux 中运行图形化的程序，那么 X.Org 的安装是必不可少的，该指令将为你安装 X.Org 所必需的包，包括 X.Org 服务器、工具、字体、键盘驱动、鼠标驱动、显卡驱动等等。
    ```bash
    pacman -S xorg
    pacman -S xorg-server xorg-server-utils xorg-xinit
    ```
6. 生成 xorg.conf 配置文件
    ```bash
    xorgconfig
    ```
7. 编辑 xorg.conf 配置文件
    直接由工具所生成的 xorg.conf 配置文件并不能满足实际情况的需要。因此，我们还有必要对该文件进行适当的编辑。
    Module 部分：定义默认载入的模块。比如，要载入 GLX 模块：
    ```bash
    Load "glx" //可以去掉下列内容前面的注释符 #
    ```
    Files 部分：你应当开启默认的字体搜索路径。
    InputDevice 部分：可以让你配置鼠标、键盘等。
    Monitor 部分：对显示器进行配置，注意输入正确的水平和垂直刷新率。必要时可以查阅显示器说明手册。
    Device 部分：配置显卡，NVIDIA 显卡用户可以加上以下选项，从而去掉 NVIDIA 烦人的标志。
    ```bash
    Option "NoLogo" "true"
    ```
    Screen 部分：设置显示器的色深和屏幕分辨率。
8. 安装声卡驱动
    ```bash
    pacman -S alsa-utils
    ```
9. 安装显卡驱动
    ```bash
    pacman -Ss xf86-video #模糊搜索驱动
    pacman -S xf86-video-intel        # Intel
    pacman -S xf86-video-ati        # Ati
    pcaman -S xf86-video-vesa # 虚拟机
    pacman -S xf86-video-vmware #VMWare虚拟机
    pacman -S xf86-video-nouveau #NVIDIA
    pacman -S nouveau-dri #NVIDIA
    pacman -S nvidia #NVIDIA新版驱动
    pacman -S nvidia-96xx
    pacman -S nvidia-71xx #NVIDIA旧版驱动
    ```

Note!如果要备份此系统则不得安装显卡驱动

10. 安装archlinuxcn-keyring，这个是提供校验软件包的密钥的。
    ```bash
    sudo pacman -S archlinuxcn-keyring
    ```
11. 安装yaourt
    ```bash
    pacman -S yaourt
    ```
12. 修改makepkg在root下运行
    ```bash
    nano /usr/bin/makepkg
    ```
    Add asroot to OPT_LONG. Just search for “OPT_LONG”.
    ```
    OPT_LONG=('allsource' 'check' 'clean' 'cleanbuild' 'config:' 'force' 'geninteg'
    'help' 'holdver' 'ignorearch' 'install' 'key:' 'log' 'noarchive' 'nobuild'
    'nocolor' 'nocheck' 'nodeps' 'noextract' 'noprepare' 'nosign' 'pkg:' 'repackage'
    'rmdeps' 'sign' 'skipchecksums' 'skipinteg' 'skippgpcheck' 'source' 'syncdeps'
    'verifysource' 'version' 'asroot')
    ```
    Remove EUID check. Just search for "EUID",注释掉以下代码段.
    ```
    if (( ! INFAKEROOT )); then
    if (( EUID == 0 )); then
    error "$(gettext "Running %s as root is not allowed as it can cause permanent,\n\catastrophic damage to your system.")" "makepkg"
    exit 1 # $E_USER_ABORT
    fi
    fi
    ```

## 安装软件
### 基层软件的安装
显示管理器：lightdm lightdm-gtk-greeter
窗口管理器与桌面：awesome feh dmenu
输入法：fcitx-im fcitx-configtool fcitx-rime
字体：ttf-dejavu wqy-microhei wqy—zenhei
终端：lxterminal/urxvt
网络管理器：networkmanager network-manager-applet
压缩软件：p7zip atool unrar unzip tar
传输软件：openssh git wget uget curl
### 其他软件
leafpad vim ranger spacefm python
## 配置启动
* 自启动服务
    ```bash
    systemctl enable NetworkManager
    systemctl enable lightdm
    ```
* 配置.xprofile及.xinitrc
    * 链接文件
    ln -s ~/.xinitrc ~/.xprofile
    * 配置输入法
    ```bash
    nano ~/.xprofile
    ```
    内容大致修改为：
    export XIM=fcitx
    export XMODIFIERS="@im=fcitx"
    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    export XIM_PROGRAM=fcitx
    fcitx &
    * 启动某软件
    exec nm-applet

## 自动挂载分区

*在mnt下新建文件夹用于加载win下的c、d、e、f、g盘与U盘。
```bash
mkdir /mnt/c
mkdir /mnt/d
mkdir /mnt/e
mkdir /mnt/f
mkdir /mnt/g
mkdir /mnt/u
```

* 查看每个盘的编号与磁盘格式
```bash
fdisk -l
```

**实例**：sda7与sda8，也就是f盘与g盘，是ntfs格式

```
磁盘 /dev/sda：320.1 GB, 320072933376 字节，625142448 个扇区
Units = 扇区 of 1 * 512 = 512 bytes
扇区大小(逻辑/物理)：512 字节 / 512 字节
I/O 大小(最小/最佳)：512 字节 / 512 字节
磁盘标签类型：dos
磁盘标识符：0x06e858c3
设备 Boot Start End Blocks Id System
/dev/sda1 * 63 45560339 22780138+ c W95 FAT32 (LBA)
/dev/sda2 45560340 625142447 289791054 f W95 Ext'd (LBA)
/dev/sda5 45560403 125435519 39937558+ b W95 FAT32
/dev/sda6 125435583 205310699 39937558+ b W95 FAT32
/dev/sda7 205310763 543221909 168955573+ 7 HPFS/NTFS/exFAT
/dev/sda8 543221973 592380809 24579418+ 7 HPFS/NTFS/exFAT
/dev/sda9 * 592380873 592557524 88326 83 Linux
/dev/sda10 592557588 608381549 7911981 83 Linux
/dev/sda11 608381613 622840049 7229218+ 83 Linux
/dev/sda12 622840113 625142447 1151167+ 82 Linux swap / Solaris
```

下面编辑加载列表，并让其支持中文显示

```bash
vi /etc/fstab
```

```
/dev/sda1 /mnt/c vfat user,rw,iocharset=utf8,umask=000 0 0
/dev/sda5 /mnt/d vfat user,rw,iocharset=utf8,umask=000 0 0
/dev/sda6 /mnt/e vfat user,rw,iocharset=utf8,umask=000 0 0
/dev/sda7 /mnt/f ntfs user,rw,umask=000 0 0
/dev/sda8 /mnt/g ntfs user,rw,umask=000 0 0
```