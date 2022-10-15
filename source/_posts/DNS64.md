---
title: 免费NAT64 DNS64服务
date: 2022-08-23 09:33:18
tags:
	- DNS64
categories: 免费资源
---
免费NAT64 DNS64服务
<!--more-->
芬兰 https://www.trex.fi/2011/dns64.html
```
echo -e "nameserver 2001:67c:2b0::4\nnameserver 2001:67c:2b0::6" > /etc/resolv.conf
```
德国 https://nat64.net/
```
echo -e "nameserver 2a01:4f8:c2c:123f::1\nnameserver 2a00:1098:2c::1\nnameserver 2a01:4f9:c010:3f02::1" > /etc/resolv.conf
```

|提供商|国家/城市|DNS64服务|NAT64前缀|
|---|---|---|---|
|Kasper Dupont|芬兰/赫尔辛基|2a01:4f9:c010:3f02::1|2a01:4f9:c010:3f02:64::/96|
|Trex|芬兰/坦佩雷|2001:67c:2b0::4|2001:67c:2b0:db32::/96|
|Trex|芬兰/坦佩雷|2001:67c:2b0::6|2001:67c:2b0:db32:0:1::/96|
|level66.network|德国/美因河畔法兰克福|2a09:11c0:f1:bbf0::70|2a09:11c0:f1:be00::/96|
|Kasper Dupont|德国/纽伦堡|2a01:4f8:c2c:123f::1|2a01:4f8:c2c:123f:64::/96|
|go6Labs|斯洛文尼亚|2001:67c:27e4:15::6411|2001:67c:27e4:642::/96|
|go6Labs|斯洛文尼亚|2001:67c:27e4::64|2001:67c:27e4:64::/96|
|go6Labs|斯洛文尼亚|2001:67c:27e4:15::64|2001:67c:27e4:1064::/96|
|go6Labs|斯洛文尼亚|2001:67c:27e4::60|2001:67c:27e4:11::/96|
|Kasper Dupont|荷兰/阿姆斯特丹|2a00:1098:2b::1|2a00:1098:2b::/96|
|Tuxis|荷兰/中部|2a03:7900:2:0:31:3:104:161|2a03:7900:6446::/96|
|Kasper Dupont|英国/伦敦|2a00:1098:2c::1|2a00:1098:2c::/96|
