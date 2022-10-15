---
title: 定制自己的宝塔安装脚本
date: 2022-08-26 12:22:13
tags:
    - baota
    - bt
categories: 技术教程
---
定制自己的宝塔安装脚本
<!--more-->
```
installpanel_version=7.7.0 #版本
installpanel_admin_path_pl=False #取消入口限制
installpanel_port=18888 #面板端口

#正常安装官方最新版
curl -sSO http://download.bt.cn/install/install_panel.sh && bash install_panel.sh

#切换成自己想要的版本
curl -sL http://download.bt.cn/install/update6.sh|sed "s/version=.*/version=${installpanel_version}/g"|bash

#取消入口限制
if [[ "${installpanel_admin_path_pl}" == "False" ]];then
bt 11
fi

#改端口
if [[ "${installpanel_port}" ]];then
bt 8 <<EOF
$installpanel_port
EOF
fi

#安装软件(自己定制)
#installpanel_soft=True
if [[ "${installpanel_soft}" == "True" ]];then
dir=/www/server/panel/install
if [[ -f $dir/install_soft.sh ]];then
cd $dir
#以下是极速安装Nginx1.20 PHP7.4 Mysql5.7
bash $dir/install_soft.sh 1 install nginx 1.20
bash $dir/install_soft.sh 1 install php 7.4
bash $dir/install_soft.sh 1 install mysql 5.7
else
echo "没找到$dir/install_soft.sh，是不是没安装宝塔或者有其他错误"
fi
fi

bt default
```
宝塔历史版本：
```
http://download.bt.cn/install/update/LinuxPanel-1.0.3.zip
http://download.bt.cn/install/update/LinuxPanel-1.0.4.zip
http://download.bt.cn/install/update/LinuxPanel-1.0.5.zip
http://download.bt.cn/install/update/LinuxPanel-1.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.0.2.zip
http://download.bt.cn/install/update/LinuxPanel-3.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.2.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.3.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.4.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.5.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.7.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.7.1.zip
http://download.bt.cn/install/update/LinuxPanel-3.8.0.zip
http://download.bt.cn/install/update/LinuxPanel-3.9.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.0.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.0.1.zip
http://download.bt.cn/install/update/LinuxPanel-4.0.2.zip
http://download.bt.cn/install/update/LinuxPanel-4.0.3.zip
http://download.bt.cn/install/update/LinuxPanel-4.0.4.zip
http://download.bt.cn/install/update/LinuxPanel-4.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.2.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.2.1.zip
http://download.bt.cn/install/update/LinuxPanel-4.3.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.4.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.4.1.zip
http://download.bt.cn/install/update/LinuxPanel-4.5.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.5.1.zip
http://download.bt.cn/install/update/LinuxPanel-4.6.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.7.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.7.1.zip
http://download.bt.cn/install/update/LinuxPanel-4.8.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.8.1.zip
http://download.bt.cn/install/update/LinuxPanel-4.8.2.zip
http://download.bt.cn/install/update/LinuxPanel-4.8.3.zip
http://download.bt.cn/install/update/LinuxPanel-4.9.0.zip
http://download.bt.cn/install/update/LinuxPanel-4.9.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.0.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.0.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.0.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.1.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.1.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.1.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.2.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.2.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.2.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.2.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.2.4.zip
http://download.bt.cn/install/update/LinuxPanel-5.2.5.zip
http://download.bt.cn/install/update/LinuxPanel-5.3.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.3.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.3.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.3.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.3.4.zip
http://download.bt.cn/install/update/LinuxPanel-5.4.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.4.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.4.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.4.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.4.4.zip
http://download.bt.cn/install/update/LinuxPanel-5.5.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.5.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.5.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.5.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.5.4.zip
http://download.bt.cn/install/update/LinuxPanel-5.5.5.zip
http://download.bt.cn/install/update/LinuxPanel-5.6.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.6.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.6.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.6.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.6.4.zip
http://download.bt.cn/install/update/LinuxPanel-5.7.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.7.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.7.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.7.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.5.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.6.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.7.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.8.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.9.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.0.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.1.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.2.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.3.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.4.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.5.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.6.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.7.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.8.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.9.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.2.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.3.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.4.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.5.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.6.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.7.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.8.zip
http://download.bt.cn/install/update/LinuxPanel-6.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.1.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.1.2.zip
http://download.bt.cn/install/update/LinuxPanel-6.2.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.2.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.3.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.4.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.4.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.5.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.5.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.6.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.6.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.6.6.zip
http://download.bt.cn/install/update/LinuxPanel-6.7.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.2.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.3.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.4.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.5.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.6.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.7.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.8.zip
http://download.bt.cn/install/update/LinuxPanel-6.8.9.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.0.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.1.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.2.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.3.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.4.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.5.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.6.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.7.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.8.zip
http://download.bt.cn/install/update/LinuxPanel-6.9.9.zip
http://download.bt.cn/install/update/LinuxPanel-7.0.1.zip
http://download.bt.cn/install/update/LinuxPanel-7.0.2.zip
http://download.bt.cn/install/update/LinuxPanel-7.0.3.zip
http://download.bt.cn/install/update/LinuxPanel-7.1.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.1.1.zip
http://download.bt.cn/install/update/LinuxPanel-7.2.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.3.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.2.zip  (安全漏洞)
http://download.bt.cn/install/update/LinuxPanel-7.4.3.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.5.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.6.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.7.zip
http://download.bt.cn/install/update/LinuxPanel-7.4.8.zip
http://download.bt.cn/install/update/LinuxPanel-7.5.1.zip
http://download.bt.cn/install/update/LinuxPanel-7.5.2.zip
http://download.bt.cn/install/update/LinuxPanel-7.6.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.7.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.8.0.zip
http://download.bt.cn/install/update/LinuxPanel-7.9.1.zip
http://download.bt.cn/install/update/LinuxPanel-7.9.2.zip
http://download.bt.cn/install/update/LinuxPanel-7.9.3.zip
```

```
http://download.bt.cn/install/update/LinuxPanel-5.8.8_pro.zip
http://download.bt.cn/install/update/LinuxPanel-5.8.9_pro.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.0_pro.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.1_pro.zip
http://download.bt.cn/install/update/LinuxPanel-5.9.2_pro.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.1_pro.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.2_pro.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.3_pro.zip
http://download.bt.cn/install/update/LinuxPanel-6.0.4_pro.zip
```
https://hostloc.com/thread-958289-1-1.html