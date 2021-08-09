# Samba 

```
& apt install samba
& groupadd testgroup #新建testgroup
& useradd -G testgroup user1 #新建user1并添加至testgroup
& gpasswd -a user1 testgroup #将user1添加至testgroup
& gpasswd -d user1 testgroup #将user1从testgroup移除
& pdbedit -a username    #新建Samba账户
& pdbedit -x username    #删除Samba账户
& pdbedit -v username    #显示账户详细信息
& pdbedit -L             #列出Samba用户列表，读取passdb.tdb数据库文件
& pdbedit -Lv            #列出Samba用户列表详细信息
& cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
& vim /etc/samba/smb.conf
```

smb.conf 配置注释

```
[global]
    ##识别信息##
    workgroup = WORKGROUP
    server string = %h server (Samba, Ubuntu)
    dns proxy = no
    ##日志设置##
    log file = /var/log/samba/log.%m
    max log size = 1000
    syslog = 0
    panic action = /usr/share/samba/panic-action %d
    ##验证权限##
    server role = standalone server
    security = user
    passdb backend = tdbsam
    obey pam restrictions = yes
    unix password sync = yes
    passwd program = /usr/bin/passwd %u
    passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
    pam password change = yes
    map to guest = bad user
    ##杂项##
    usershare allow guests = yes
[homes]
    comment = Home Directories
    valid users = %S
    browseable = no
    writable = yes
    create mode = 0775
    directory mode = 0775
[Share]
    comment =   #注释
    path =  #路径
    public = #是否可以看到该目录
    readonly =  #仅可读
    writable =  #可写
    browseable = #可网络发现该目录
    create mask =  0755 #文件权限
    directory mask =   0755 #文件夹权限
    valid users = @group1,user1  #可使用者
    invalid users = @group2,user2 #不可使用者
    force user =    #强制转换使用者身份
    force group =   #强者转换使用组身份
```