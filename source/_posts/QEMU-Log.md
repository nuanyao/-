---
title: QEMU记录
date: 2022-10-15 12:06:59
tags:
	- QEMU
categories: 技术教程
---
QEMU记录
<!--more-->
# 新建空白镜像
```
qemu-img create -f qcow2 /root/w.qcow2 5G
```
# 启动
```
qemu-system-x86_64 -m 512 -boot c -hda /root/windowsxp.qcow2 -net nic,model=rtl8139 -net user -soundhw ac97 -vga cirrus -vnc :1 -net user,hostfwd=tcp::3389-:3389 -localtime
```
