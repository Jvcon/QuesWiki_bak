<<dbadge "Windows" 7,8,10 success>>

以Total Commander为骨干，所构建的管理、查看一站式管理文件系统。

同类型解决方案:[以Q-Dir为骨干构建的File Commander in Q-Dir]()

## 安装激活Totalcmd
官方网站:[ghisler.com](http://www.ghisler.com) | 插件网站:[totalcmd.net](http://totalcmd.net/) | [下载链接](http://totalcommander.ch/win/tcmd900ax32_64.exe)

Step1. 多语言环境安装totalcmd；

Step2. 将密钥文件wincmd.key复制到Totalcmd根目录，完成激活，[TC Patch in Mega]()；

## Lister Plugins
{{uLister}}
{{sLister}}
{{vLister}}

- [VisDirSzie](http://totalcmd.net/plugring/visdirsize.html) | ~~[DirsizeCalc](http://lefteous.totalcmd.net/tc/dirsizecalc_eng.htm)~~ - 以图标方式查看文件夹大小
- [tLister](https://totalcmd.net/plugring/tlister.html) - 让TC内置Lister支持多标签页查看
- [CudaLister](http://totalcmd.net/plugring/CudaLister.html) - 满足基本的文本语法高亮查看，适配SynWrite的[语法高亮规则](https://sourceforge.net/projects/synwrite-addons/files/Lexers/)
- [IniED](http://totalcmd.net/plugring/inied.html) -  <kbd>.ini</kbd>查看和编辑
- [uLister](https://totalcmd.net/plugring/oilister.html) with [Oracle Viewer Technology](http://www.oracle.com/technetwork/middleware/content-management/downloads/oit-dl-otn-097435.html) - 基于Oracle的查看器库，对大部分文件的查看支持，尤其是MS-Office等系列文件的预览
- [multilister](https://totalcmd.net/plugring/filter.html) with [Configuration tool](https://totalcmd.net/plugring/filter_cfg.html)
- [AKFont](http://totalcmd.net/plugring/akfont.html) - <kbd>.ttf</kbd> <kbd>.otf</kbd> <kbd>.ttc</kbd>字体文件查看，可以对预览内容进行自定义
- [iclview](http://totalcmd.net/plugring/iclview.html) - <kbd>.ico</kbd> <kbd>.icl</kbd> <kbd>.exe</kbd> <kbd>.dll</kbd> <kbd>.scr</kbd> <kbd>.ocx</kbd> <kbd>.bpl</kbd> <kbd>.cpl</kbd> <kbd>.acm</kbd>，实现对图标导出、增删、 重命名和排序
- [Imagine](http://totalcmd.net/plugring/imagine.html) - 类Xnview的图片管理器，快速查看下都能进行比较丰富的图片操作，若使用XnView作为主力图片管理其可以选择：[PhotoViewer](http://totalcmd.net/plugring/photoviewer.html)自带一些滤镜特效，没有文件管理功能模块
- [ruDWGPreviewNew](http://totalcmd.net/plugring/rudwgpreviewnew.html)
- [Solidwork Preview](http://totalcmd.net/plugring/solidworkswlx.html)
- [anyTag](http://totalcmd.net/plugring/anytag.html)
- [Mmedia](http://totalcmd.net/plugring/mmedia.html)
- [SWFView](http://totalcmd.net/plugring/swfview.html)
- [TorrentLister](http://totalcmd.net/plugring/TorrentLister.html)

  **wincmd.ini**
  ```
  0=%COMMANDER_PATH%\plugins\wlx\VisualDirSize\visualdirsize.wlx
  1=%COMMANDER_PATH%\plugins\wlx\tlister\tlister.wlx
  1_detect="MULTIMEDIA"
  2=%COMMANDER_PATH%\plugins\wlx\CudaLister\cudalister.wlx
  3=%COMMANDER_PATH%\plugins\wlx\slister\slister.wlx
  3_detect="MULTIMEDIA& (EXT="PDF" | EXT="DJVU" | EXT="DJV"| EXT="XPS" | EXT="CBZ" | EXT="CBR" )"
  4=%COMMANDER_PATH%\Plugins\Wlx\IniEd\IniEd.wlx
  4_detect="EXT="INI"|EXT="INF"|EXT="REG"|EXT="URL""
  5=%COMMANDER_PATH%\plugins\wlx\ulister\ulister.wlx
  6=%COMMANDER_PATH%\Plugins\wlx\PDFFilter\filter.wlx
  7=%COMMANDER_PATH%\Plugins\Wlx\AKFont\AKFont.wlx
  7_detect="FORCE | EXT="TTF" | EXT="PFM" | EXT="OTF" | EXT="TTC" | EXT="FON" | EXT="PFB""
  8=%COMMANDER_PATH%\Plugins\Wlx\ICLview\ICLview.wlx
  8_detect="MULTIMEDIA & (ext="DLL" | ext="EXE" | ext="ICL" | ext="ICL32" | ext="ICO" | size=0 | force)"
  9=%COMMANDER_PATH%\Plugins\Wlx\Imagine\Imagine.wlx
  9_detect="MULTIMEDIA"
  10=D:\totalcmd\plugins\wlx\ruDWGPreviewNew\ruDWGPreviewNew.wlx
  10_detect="ext="DWG""
  11=D:\totalcmd\plugins\wlx\SLDPreview\sldpreview.wlx
  11_detect="EXT="SLDASM"|EXT="SLDDRW"|EXT="SLDPRT"|EXT="ASMDOT"|EXT="DRWDOT"|EXT="PRTDOT"|EXT="SLDFLP"|EXT="SLDDRT"|EXT="ASM"|EXT="DRW"|EXT="PRT""
  12=D:\totalcmd\plugins\wlx\wlx_anytag\anytag.wlx
  13=%COMMANDER_PATH%\Plugins\Wlx\MMedia\MMedia.wlx
  13_detect="MULTIMEDIA"
  14=%COMMANDER_PATH%\Plugins\Wlx\SWFView\SWFView.wlx
  14_detect="MULTIMEDIA & EXT="SWF" | (([0]="F" & [1]="W" & [2]="S")|([0]="C" & [1]="W" & [2]="S") & FORCE)"
  15=%COMMANDER_PATH%\PLUGINS\wlx\TorrentLister\TorrentLister.wlx
  15_detect="EXT="TORRENT""
  ```

  **整合至Universal Viewer Pro**：在Universal Viewer中配置插件，通过Total Commander的配置导入插件即可

## 搜索

### 搜索 by Everything
  **wincmd.ini**
  ```
  [Configuration]
  Everything=%COMMANDER_PATH%\Tools\Everything\Everything.exe -startup
  EverythingForSize=1
  UseEverything=1
  ```

### 搜索 by tcmatch
[QuickSearch eXtended](http://cid-f8c4901fa2fb692e.skydrive.live.com/self.aspx/TC/QuickSearch%20eXtended/QuickSearch%20eXtended.zip) - 通过输入首字母完成快速搜索

  **wincmd.ini**
  ```
  [Configuration]
  AltSearch=3
  QuickSearchMatchBeginning=1
  QuickSearchExactMatch=0
  ```

### 搜索 by WDX
- [Tempus](http://totalcmd.net/plugring/Tempus.html)
- [ShellDetails](http://lefteous.totalcmd.net/tc/docs/shelldetails/readme.htm)
- [TextSearch](http://totalcmd.net/plugring/TextSearch.html)
- [xPDFSearch](http://lefteous.totalcmd.net/tc/xpdfsearch_eng.htm)
- [ImageMetaData](http://totalcmd.net/plugring/iptcwdx.html)
- [WDXTagLib](https://github.com/murzz/wdxtaglib/releases/tag/v1.1.4)
- [eBookInfo WDX](http://totalcmd.net/plugring/eBookInfoWdx.html)
- [Torrent WDX](http://totalcmd.net/plugring/Torrent_wdx.html)
- [Apk-viewer](http://totalcmd.net/plugring/APK-wdx.html) with [Android Asset Packaging Tool](https://github.com/eladkarako/aapt-pre-build-binary)

## 转换与解压缩 by WCX

压缩镜像
- [WinRar](https://www.rarlab.com/download.htm) - 更新内置的rar.exe，授权密钥Rarreg.key，[TCrar in Mega]()
- [Total7zip](http://totalcmd.net/plugring/Total7zip.html) with [7 zip](http://www.7-zip.org/) | [7zip ZStandard](https://github.com/mcmilk/7-Zip-zstd/releases) - 日常使用的压缩插件,支持多种压缩格式，下载7-zip-zstd里面的Totalcmd.zip，更新内置的7zip压缩调用的dll（Totalcmd根目录下），可以支持ZStandard协议
- [TotalISO](http://totalcmd.net/plugring/totaliso.html) with [mkisofs.exe in cdrtools](http://smithii.com/files/cdrtools-latest.zip) - 光盘映像的制作与解压
- [Resource Extractor](http://totalcmd.net/plugring/resextract.html) with [ResourceHacker](http://www.angusj.com/resourcehacker/) - 程序解包

多媒体
- [Audio Converter](http://totalcmd.net/plugring/wcx_plugin_BitRate_Converter_0.html) - 音频转换
- [Graphic Converter 1.6 Beta](http://totalcmd.net/plugring/graphicconverter.html) - 图像格式转换和压缩大小，替代Graphics Converter和TotalRSZ
- [iclread](http://totalcmd.net/plugring/iclread.html) - 图标操作

文件/文件夹
- [DiskDir Extended](http://www.totalcmd.net/plugring/diskdir_extended.html) -
- [Checksum](http://totalcmd.net/plugring/checksum.html) - 生成MD5验证文件

  **wincmd.ini**
  ```
  [Packer]
  LastUsedPacker=10000
  ZIPlikeDirectory=1
  InternalUnarj=1
  ARJlongnames=0
  InternalUnlzh=1
  InternalUnrar=1
  InternalUnace=1
  LinuxCompatible=1
  ARJ=arj.exe
  LHA=lha.exe
  RAR=%COMMANDER_PATH%\plugins\wcx\WinRAR\Rar.exe
  UC2=uc.exe
  ACE=winace.exe

  [PackerPlugins]
  tio=23,%COMMANDER_PATH%\plugins\wcx\TotalISO\TotalISO.wcx
  7z=735,%COMMANDER_PATH%\plugins\wcx\Total7zip\Total7zip.wcx
  icl=15,%COMMANDER_PATH%\plugins\wcx\ICLRead\ICLRead.wcx
  icl32=15,%COMMANDER_PATH%\plugins\wcx\ICLRead\ICLRead.wcx
  lst=31,%COMMANDER_PATH%\plugins\wcx\DiskDirExtended\DiskDirExtended.wcx
  audioconverter=21,%COMMANDER_PATH%\plugins\wcx\audioconverter\audioconverter.wcx
  GraphConv=263,%COMMANDER_PATH%\plugins\wcx\GraphicConverter\GraphicConverter.wcx
  pe_res_dummy=479,%COMMANDER_PATH%\plugins\wcx\ResExtract\ResExtract.wcx
  md5=21,%COMMANDER_PATH%\PLUGINS\wcx\Checksum\checksum.wcx
  ```

## 设备文件管理 by WFX
- [sftp4tc](https://totalcmd.net/plugring/sftp4tc.html) - SFTP base on PuTTY
- [VirtualDisk](http://totalcmd.net/plugring/virtdisk.html) - 提供HDD、FDD、CD/DVD三种模式，支持挂载iso、bin、img等格式
- [VirtualPanel](http://totalcmd.net/plugring/virtualpanel.html)
- [Android ADB](http://totalcmd.net/plugring/android_adb.html)

  **wincmd.ini**
  ```
  [FileSystemPlugins]
  Secure FTP Connections=%COMMANDER_PATH%\plugins\wfx\sftp4tc\plugin_sftp.wfx
  Virtual Disks=%COMMANDER_PATH%\plugins\wfx\VirtualDisk\VirtualDisk.wfx
  VirtualPanel=%COMMANDER_PATH%\plugins\wfx\VirtualPanel\VirtualPanel.wfx
  ADB=%COMMANDER_PATH%\plugins\wfx\ADB\ADBPlugin.wfx
  ```

## 新建、命名、比较、分割、合并、编辑
- [Notepad++](https://notepad-plus-plus.org/zh/) - Windows最强最快文本编辑器
- [TC_extdir](http://totalcmd.net/plugring/tc_extdir.html) - 新建文件夹
- [NewFiles](http://totalcmd.net/plugring/newfiles.html) - 新建文件
- [ReDate](http://totalcmd.net/plugring/redate_addon2.html) - 更新文件时间
- [DiffMerge](http://sourcegear.com/diffmerge/downloads.php) - 支持三方文件比较，跨平台

## 工具箱
- [TotalUpdater](http://totalcmd.net/plugring/totalupdater.html) - TC插件升级管理器
- [UltraTCEditors](http://totalcmd.net/plugring/ultra_tc_editors.html) - TC编辑器
