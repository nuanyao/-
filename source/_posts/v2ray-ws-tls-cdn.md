---
title: 搭建v2ray+ws+tls+cdn教程
date: 2022-08-23 13:44:15
tags:
	- v2ray
	- websocket
	- cloudflare
	- fq
	- 代理
categories: 技术教程
---
搭建v2ray+ws+tls+cdn教程
<!--more-->
1.安装unzip
```
apt install unzip
```

新建文件夹/root/v2，并移动过去。后面所有操作都在这里进行。
```
mkdir -p /root/v2
cd /root/v2
```

2.下载caddy和v2ray。默认下载的是Linux amd64位版本。
Caddy官网:https://caddyserver.com/download
V2ray Github仓库:https://github.com/v2fly/v2ray-core
```
wget -O caddy --no-check-certificate "https://onedrive.baxx.eu.org/api/raw/?path=/caddy_linux_amd64" 
wget --no-check-certificate "https://github.com/v2fly/v2ray-core/releases/download/v4.45.2/v2ray-linux-64.zip" && unzip -o v2ray-linux-64.zip v2ray v2ctl geosite.dat geoip.dat && rm v2ray-linux-64.zip
chmod +x caddy v2ray v2ctl
```

3.新建文件：Caddyfile
```
http://example.com {
    reverse_proxy /hello 127.0.0.1:10000 {
      header_up -Origin
    }
}
```
Cloudflare的加密模式要选择Flexible

4.新建文件：config.json。这是v2ray的配置文件。
VMESS:
```
{
    "log": {
        "loglevel": "info"
    },
    "inbounds": [
        {
            "protocol": "vmess",
            "port": 10000,
            "listen": "127.0.0.1",
            "settings": {
                "clients": [
                    {
                        "alterId": 0,
                        "id": "d80d1881-a00f-7153-1740-0ccff5b916ca"
                    }
                ]
            },
            "streamSettings": {
                "network": "ws",
                "wsSettings": {
                    "path": "/hello"
                }
            }
        }
    ],
    "outbounds": [
        {
            "tag": "direct",
            "protocol": "freedom"
        }
    ]
}
```
VLESS:
```
{
  "inbounds": [
    {
      "port": 10000,
      "listen":"127.0.0.1",
      "protocol": "vless",
      "settings": {
        "decryption": "none",
        "clients": [
          {
            "id": "d80d1881-a00f-7153-1740-0ccff5b916ca",
            "level": 0
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
        "path": "/hello"
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```
d80d1881-a00f-7153-1740-0ccff5b916ca为UUID
/hello为路径
如果没有UUID，执行./v2ctl uuid，会随机输出一个。

5.后台运行
Caddy:
```
./caddy start
```
V2ray:
```
screen -S v2ray
./v2ray
Ctrl A+D 退出
```
如果没有screen要先安装:
```
apt install screen
```

当前目录除了以下文件，其他都可以删除。
```
v2ray v2ctl geosite.dat geoip.dat caddy Caddyfile config.json
```

6.客户端下载
v2rayN：https://github.com/2dust/v2rayN/releases
v2rayNG：https://github.com/2dust/v2rayNG/releases