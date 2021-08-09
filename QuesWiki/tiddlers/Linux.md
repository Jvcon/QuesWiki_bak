- [Applications](#applications)
    - [Audio](#audio)
    - [Chat Clients](#chat-clients)
    - [Data Backup and Recovery](#data-backup-and-recovery)
    - [Desktop Customization](#desktop-customization)
    - [Development](#development)
    - [E-Book Utilities](#e-book-utilities)
    - [Editors](#editors)
    - [Education](#education)
    - [Email Utilities](#email)
    - [File Manager](#file-manager)
    - [Games](#games)
    - [Graphics](#graphics)
    - [Internet](#internet)
    - [Office](#office)
    - [Productivity](#productivity)
    - [Proxy](#proxy)
    - [Security](#security)
    - [Sharing Files](#sharing-files)
    - [Terminal](#terminal)
    - [Utilities](#utilities)
    - [Video](#video)
    - [Others](#others)
- [Command Line Utilities](#command-line-utilities)
- [Desktop Environments](#desktop-environments)
- [Display Managers](#display-manager)
	- [Console](#console)
	- [Graphic](#graphic)
- [Window Managers](#window-managers)
	- [Compositors](#compositors)
	- [Stacking window managers](#stacking-window-managers)
	- [Tiling window managers](#tiling-window-managers)
	- [Dynamic window managers](#dynamic-window-managers)

# Awesome Linux

## 桌面与开发环境
- **显示管理器**：[lightDM](https://www.freedesktop.org/wiki/Software/LightDM/) - 简洁美观的跨桌面显示管理器。
- **窗口管理器**：[Awesome](https://awesomewm.org/) - 轻量级可定制化平铺式窗口管理器。
- **系统检测**：[Conky](https://github.com/brndnmtthws/conky) - 系统信息监测。
- **音量控制**：[volctl](https://buzz.github.io/volctl/) - 托盘栏音量控制。
- **软件启动**：[dmenu](http://tools.suckless.org/dmenu/ "简洁可定制的启动器") , [Launchy](http://www.launchy.net/ "跨平台启动软件") & [Albert](https://github.com/manuelschneid3r/albert "Alferd的fork作品")。
- **显示控制**：[caffeine]() - 保持屏幕常亮。
- **输入法**：[Fcitx](http://fcitx-im.org/) - 支持扩展rime、google、sougou。
- **Python开发**：[PyCharm](https://www.jetbrains.com/pycharm/) - 针对Python开发，具有良好用户体验的杰出IDE
- **VNC客户端**：[vncviewer](http://tigervnc.org/) - TigerVNC。
- **语法查询**：[Zeal](https://zealdocs.org/)- 拥有195种的离线语法文档
- **FTP客户端**：[FileZilla](http://filezilla-project.org/) - 强大、稳定。
- `cli` **Shell**：[zsh]() - 拥有强大的Oh my zsh，替换掉你的bash
- `cli` **Terminal**：[urxvt]() - 定制性强大的xterm代替者
	- `cli` **窗口分割**：Tmux - [参考配置1](http://blog.jobbole.com/87584/) [参考配置2](http://cenalulu.github.io/linux/tmux/) [参考配置3](http://www.cnblogs.com/bamanzi/p/tmux-mouse-tips.html)
		- Tmuxinator
		- Tmate
		- retach-to-user-namespace
	- `cli` **版本控制**：[git]() - 。
	- `cli` **主力编辑器**：[vim]() - 。
- `cli` **FTP服务器端**：[bftpd](http://bftpd.sourceforge.net/) - 小巧、易配置。
- `cli` **VNC服务器端**：[x11vnc](http://www.karlrunge.com/x11vnc/)-

## 最舒适的生产力应用
### 图形界面
* **浏览器**：[Chromium](https://www.chromium.org/) - 尽在不言中，需要安装[pepper-flash]非开源flash插件使用。[appso-chromium⇲](pages/awesome/appso-chromium.md)
- **剪贴板**：[CopyQ](http://hluk.github.io/CopyQ/) - 可跨平台同步，替代[Ditto](http://ditto-cp.sourceforge.net/)，但在易用性上仍有所欠缺。
- **密码管理**：[Keepass]() - 跨平台密码管理软件，更多客户端：[KeeWeb](https://github.com/keeweb/keeweb)，[Keepass2Android](https://apkpure.com/cn/keepass2android-password-safe/keepass2android.keepass2android)。
- **字典查询**：[Golden Dict](http://www.goldendict.org/)
- **音乐播放**：[ieaseMusic](https://github.com/trazyn/ieaseMusic) - 第三方的网易云客户端，整合了多个网络资源解决死链问题。
- **资讯阅读**：[QuiteRSS](http://quiterss.org/) - Qt/C++编写的可取代RSSOwl的跨平台RSS订阅软件。
- **邮箱**：[Nylas mail](https://github.com/nylas-mail-lives/nylas-mail) 和 [Mail Spring](http://www.getmailspring.com/) - [Nylas](https://github.com/nylas/nylas-mail)的开源续作，界面友好的邮件客户端。
- 管理与备份
	- **同步备份**：[FreeFireSync](http://www.freefilesync.org/)
	- **媒体管理**：[DataCow](http://www.datacrow.net/)
	- **书籍管理**：[Calibre](http://calibre-ebook.com/) - 电子书管理软件
	- **书籍管理**：[MComix](https://sourceforge.net/projects/mcomix/) - 为漫画压缩包设计的GTK2的图片查看器和书籍管理器
	- **文件搜索**：[FSearch](http://www.fsearch.org/) or [Catfish](http://www.twotoasts.de/index.php/catfish/) - 类似Everything的文件搜索器。
	- TC风格管理器（[Double Commander](https://doublecmd.sourceforge.io/),[Midnight Commander](http://midnight-commander.org/),[Sunflower FM](http://sunflower-fm.org)）
	- 单窗口风格管理器([Thunar](https://docs.xfce.org/xfce/thunar/start)）

- 通讯工具
	- [Franz](http://meetfranz.com/#download_all)
	- [HexChat](https://hexchat.github.io/screenshots.html) - `cli`IRC客户端
	- [iptux](https://github.com/iptux-src/iptux) - 局域网聊天软件
	- [Pidgin](http://pidgin.im/) - 多协议即时聊天客户端

- `cli` **音乐播放**：[ncmpcpp](http://rybczak.net/ncmpcpp/) - [Music Player Daemon](https://www.musicpd.org/)的客户端，[参考配置](https://github.com/Puxirepublic/dotfiles/tree/master/.ncmpcpp)。
- `cli` **视频播放**：[mpv](https://mpv.io/) - `cli`免费开源跨平台视频播放器。

- `cli` **文件管理**：Vi风格管理器（[Ranger](http://ranger.nongnu.org/),[Vifm](https://vifm.info/)） -
	- [w3m](http://w3m.sourceforge.net/) -命令行浏览器，可用于浏览图片
	- [fbpdf](http://repo.or.cz/w/fbpdf.git) - 基于MuPDF迷你pdf、djvu查看器
	- [mediainfo](https://mediaarea.net/) - 强大的视频和音频文件的编码和内容信息查看管理器
	- [jfbview](http://seasonofcode.com/pages/jfbview.html) - 基于imlib2的命令行pdf、图片查看器
	- [apvlv](http://naihe2010.github.com/apvlv/) - Vim操作的迷你PDF/DjVu/UMD/TXT查看器
	- [p7zip](http://p7zip.sourceforge.net/) - linux下的7-zip
	- [atool](http://www.nongnu.org/atool/) - 多格式支持压缩文件管理命令行
	- [pigz](http://www.zlib.net/pigz/) - 支持并行的gzip


## 文书生产环境★★★★☆
- [Dia](http://dia-installer.de/)
- [GanttProject](http://www.ganttproject.biz/)
- [Freeplane](http://freeplane.sourceforge.net/wiki/index.php/Home)
- [Transcriber](http://trans.sourceforge.net/) - 开源跨平台翻译软件
- [Libre Office](https://www.libreoffice.org/)
- [Rstudio]() - 极品支持Markdown、LaTeX的论文软件

## 媒体生产环境★★☆☆☆
- [LightScreen](https://lightscreen.com.ar/) - GUI软件，支持自动保存的简洁截图工具。
- **位图编辑**：[GIMP](http://www.gimp.org/) - 强大位图编辑软件。
- **图片管理**：[Zoomy](https://zoommyapp.com/) - 500多家版权免费图片源下载与灵感收集管理。
- **图片管理**：[Xnview MP](http://www.xnview.com/en/xnviewmp/) - 多功能看图管理软件。
- **摄影后期**：[digiKam](http://www.digikam.org/) - KDE的数码相机图片管理编辑软件。
- **摄影后期**：[darktable](http://www.darktable.org/) - RAW管理软件。
* [blender]() - 3D制作软件，小巧轻便，功能强大、启动迅速。
* **原型软件**：[pencil project]()
- **音频剪辑**：[Audacity](http://www.audacityteam.org/) - Audition的替代软件。
- `cli` [scrot]() - 最轻便命令行截图软件，主要用在命令行下，它使用 imlib2 库来抓取并保存图像。[appso-scrot⇲](pages/awesome/appso-scrot.md)
- `cli` [HandBrake](https://handbrake.fr) - 开源免费的视频格式转换软件。
	- `cli` aegisub -
	- `cli` mkvtoolnix -
	- `cli` [lightworks]()


## 工业生产环境★★★★☆
- **矢量编辑**：[Inkscape](http://inkscape.org/) - 强大矢量图片编辑软件
* [QCad](http://www.qcad.org/en/) - 2D CAD免费软件
* [solvespace](http://solvespace.com/index.pl) - 极迷你的CAD软件
* [FreeCAD](https://sourceforge.net/projects/free-cad/) - 开源的三维固体和通用设计的 CAD/CAE。
* [KiCAD](http://kicad-pcb.org/) - 开源PCB设计软件

## 网络下载环境★★★★☆
- `cli` [Aria2](https://aria2.github.io/) - 轻量化下载工具，支持http(s), FTP, BitTorrent(DHT, PEX, MSE/PE) protocols 和 Metalink，拥有JSON-RPC或XML-RPC编写的界面。
- `cli` [you-get](https://you-get.org/) 和 [youtube-dl](https://rg3.github.io/youtube-dl/) - 著名的视频网站命令行下载工具。

## 生活环境
- [at] - 自带计划任务，小巧时间命令行工具
- [Todo.txt](http://ginatrapani.github.com/todo.txt-cli/) - 跨平台简约纯文本语法型TODO清单
    - [QTodoTxt](https://github.com/mNantern/QTodoTxt) - Todo.txt的图形界面
- [Taskworrior](https://taskwarrior.org) - 可自建服务器同步
    - [Taskworrior for Android](https://bitbucket.org/kvorobyev/taskwarriorandroid/wiki/Configuration) - 安卓客户端
    - [Awesome-taskworrior](https://github.com/ValiValpas/awesome-taskwarrior) - 支持在Awesome中使用Taskworrior
- [etmtk](http://people.duke.edu/~dgraham/etmtk/) - 语法完善、自带计时的文字界面任务管理
- [Stellarium]() - 星象软件

## 系统管理
### 网络管理
* [networkmanager] - 基础网络管理包
* [network-manager-applet] - 包含nm-applet托盘插件
* [networkmanager-openvpn] - 通过NetworkManager来使用VPN
* [networkmanager-dmenu-git] - 通过dmenu来管理NetworkManager链接的脚本

### Partition
* `cli`[cfdisk] -命令行磁盘分区
* [Gparted] - GNOME的界面磁盘分区

### Mount
* [udisksvm] - u盘挂载弹出
* [ws] - 挂载windows网络服务（CIFS和VFS）
* [ldm] - 轻量级挂载磁盘

### 虚拟化工具
* [virt-manager](https://virt-manager.org/) -
* [VirtualBox](https://www.virtualbox.org/) -

