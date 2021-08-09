## Inbox

<<list-links "[tag[Selfhosted]]">>

## List
* DevOps
  * [Redmine](#Redmine)
  * Testlink
  * Jenkins
  * Weblate
  * Yapi
  * SVN
  * Git
  * WebDAV
  * ELK
* Virtualization
  * ProXmoX
* File Management
  * Syncthing
  * Nextcloud
  * [Samba](#Samba)
* Communication
  * Zulip
  * iRedmail & Roundcube
  * Openfire Meeting / Converse / Jitsi
* Wiki/CMS
  * TikiWiki(wiki suite)
  * Bookstack
  * ERPNext
  * [Tiddlywiki](#Tiddlywiki)
* Other
  * OctoPrint
  * RSSHub
  * Transmission
  * Taskwarrior
  * Clonezilla
  * PXE Server

# [Team Tools Topic] 如何利用开源服务组成协同办公环境

[toc]

## 需求列表

沟通部分
- [x] 对外沟通 : [E-mail](#e-mail), [企业微信](#企业微信),
- [x] 内部沟通 : [Zuplip](#zulip)

项目管理部分
- [ ] 撰写文稿 : [CUPS/SANE](#cupssane), [Onlyoffice/Collabora Online](#onlyofficecollabora-online)
- [ ] 代码开发 : Gitlab, Jenkins
- [ ] 图表绘制 :
- [ ] 文件分享 : [Nextcloud](#nextcloud), [Samba](#samba)
- [ ] 项目管理

公司管理部分
- [ ] 流程申请
- [ ] 文件签署
- [ ] 财务管理
- [ ] 物资管理
- [ ] 客户管理
- [ ] 知识管理 ： [XWiki](#xwiki), [TTRss](#tinytinyrss)
- [ ] 人力资源管理

## 工具选型

### LDAP
> 解决账户与权限问题

LDAP协议的好处就是你公司的所有员工在所有这些工具里共享同一套用户名和密码，来人的时候新增一个用户就能自动访问所有系统，走人的时候一键删除就取消了他对所有系统的访问权限。

- OpenLDAP - LDAP服务主体
    - memberOf模块 - LDAP组管理模块
- phpLDAPadmin- 管理端
- PWM - 易用的客户端，用于更改密码等基本操作

### E-mail

不建议通过自建邮箱服务器来实现邮箱收发的需求，但是可以寻求一款合适的邮箱客户端，作为统一工具，方便集成模板、签名、通讯录等相应功能。

- [Rainloop](https://github.com/RainLoop/rainloop-webmail) - Web客户端
- [Cypht](https://cypht.org/index.html) - Web邮件客户端，支持RSS订阅
- [K-9 Mail](https://f-droid.org/packages/com.fsck.k9/) -  安卓客户端

### 企业微信
> 最适合面向客户的沟通工具

企业微信与微信可以互通授权，方便客户通过普通微信添加联系人的同时，又提供在企业微信端增加许多优秀工具用于支撑客户运营；并且支持对客户资源的转移，这样很大程度能够帮助企业避免客源流失；同时与微信相对分离，员工可以较好分离生活与工作。

### Zulip
> 办公即时通讯

支持多种集成插件，并且可以按照频道进行沟通聊天。同样的竞品有Rocket.chat和Mattermost。

### Nextcloud
> 网络存储

1. 工作台
Nexcloud可以向员工提供合适的存储空间，实现文件（主要是媒体类文件）的分享和存取，承担类似Google Drive的角色，作为协同工作的工作台，通过其中的插件实现日常的文稿、表格、演示文稿、流程图的编辑撰写。
2. 插件
	- WebDav - 通过Nextcloud中原生支持的**WebDav**服务，可被不同的应用使用其共享空间；
	- Onlyoffice/Collabora Online - 文稿协同服务器，如果使用Onlyoffice需要搭配Onlyoffice的独立服务器；
	- Calendar/Mail/Contacts/Bookmark - 原生支持的协同插件；
3. 文件分享
通过[**Samba**](#samba)服务，将Nextcloud的文件目录进行共享，配置上合适的访问权限，就可以实现文件内容互通。
4. Nextcloud的扩展应用
	- [DAVx5](https://f-droid.org/en/packages/at.bitfire.davdroid/) - DAVx⁵用于解决联系人、日历的双向同步
	- [OpenTasks](https://f-droid.org/en/packages/org.dmfs.tasks/) - OpenTasks用于解决任务同步
	- [Markor](https://f-droid.org/en/packages/net.gsantner.markor/) - Markor用于解决便签同步
	- [Floccus](https://github.com/marcelklehr/floccus) - 用于解决书签同步

### Samba

> 文件服务扩充

### CUPS/SANE
> 打印机/扫描服务

- [CUPS](https://www.cups.org/) - CUPS is the standards-based, open source printing system
- [Sane](http://www.sane-project.org/)
    - [swingsane](http://swingsane.com/) - A powerful, cross platform, open source Java front-end for using Scanner Access Now Easy (SANE) back-ends. 
    - [phpSane](https://github.com/gawindx/phpSane) - phpSANE is a web-based frontend for SANE written in HTML/PHP
    - [SaneTwain](https://sanetwain.ozuzo.net/) - A Fronet-end for Windows

### Onlyoffice/Collabora Online

### XWiki

### TinyTinyRSS


## 搭建环境对比

|项目|MySQL |MariaDB|PostgreSQL|
|---|---|---|---|
|Nextcloud|✔|✔|✔|
|Zulip|✔|✘|✔|
|XWiki|✔|✘|✔|
|TikiWiki|✔|✔|✘|

## Reference

- [Opensource Builders](https://opensource.builders/)
- [Teams Tools](https://teams.tools/)