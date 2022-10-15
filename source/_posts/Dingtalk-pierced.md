---
title: Dingtalk-pierced--钉钉提供的免费内网穿透工具
date: 2022-08-24 12:03:07
tags:
	- 内网穿透
	- DingTalk
	- 钉钉
categories: 免费资源
---
鉴于很多开发者在临时体验开发时往往没有公网域名或者公网IP，本工具提供了一个公网代理服务，目的是方便开发测试。
本工具当前不保证多个开发者随意设置相同的子域名导致的冲突以及通道稳定性，因此正式应用、正式环境必须是真实的公网IP或者域名，正式应用上线绝对不能使用本工具。
<!--more-->
Github地址:https://github.com/open-dingtalk/pierced
# 使用方法
## 下载
从Github上下载适合系统的程序和ding.cfg
WindowsX64:
https://github.com/open-dingtalk/pierced/tree/master/windows_64
Linux(AMD64):
https://github.com/open-dingtalk/pierced/tree/master/linux
Linux(Arm):
https://github.com/open-dingtalk/pierced/tree/master/linux_arm
MacX64
https://github.com/open-dingtalk/pierced/tree/master/mac_64

## HTTP 穿透
### Windows:
打开cmd 定位到程序目录
```
ding -config=./ding.cfg -subdomain=域名前缀 端口
```

### Linux:
定位到程序目录
```
chmod +x ding
./ding -config=./ding.cfg -subdomain=域名前缀 端口
```
如需后台运行:
```
screen -S ding
./ding -config=./ding.cfg -subdomain=域名前缀 端口
Ctrl A+D 退出
```
### Mac:
定位到程序目录
```
chmod 777 ./ding
./ding -config=./ding.cfg -subdomain=域名前缀 端口
```
### 命令参数说明
|参数	|说明|
|---|---|
|config|内网穿透的配置文件，按命令照示例固定为钉钉提供的./ding.cfg，无需修改。|
|subdomain|您需要使用的域名前缀，该前缀将会匹配到“vaiwan.com”前面，例如你的 subdomain 是 abcde，启动工具后会将 abcde.vaiwan.com 映射到本地。|
|端口	|您需要代理的本地服务 http-server 端口，例如你本地端口为 8080 等。|

## 数据库穿透
### Windows
```
ding -config=./ding.cfg -proto=tcp start ssh
```
### Linux
```
chmod +x ding
./ding -config=./ding.cfg -proto=tcp start ssh
```
### Mac
```
chmod 777 ding
./ding -config=./ding.cfg -proto=tcp start ssh
```
### 命令参数说明
|参数	|说明|
|---|---|
|config|内网穿透的配置文件，按命令照示例固定为钉钉提供的./ding.cfg，无需修改。|
|proto|启动的是 TCP 协议穿透。|

详见[官方文档](https://github.com/open-dingtalk/pierced/blob/master/README.md)