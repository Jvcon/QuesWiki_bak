# plink

ssh服务器
```
plink -v -ssh -2 -p 22 rott@192.168.2.1 -pw 密码
```
翻墙重连
```
@echo off
:relink
echo y|plink -N -D 10.10.1.10:1080 国外ssh.vicp.cc -i .\ssh\openxxx.ppk
goto relink
```