---
title: Microsoft免费临时远程桌面
date: 2022-08-22 14:25:12
tags:
	- Microsoft
	- 微软
	- RDP
	- VPS
	- 免费VPS
categories: 免费资源
---
Microsoft Learn提供免费的沙盒,1小时后数据自动清除,每天可以领取10个沙盒
<!--more-->
# 教程
1.打开 https://docs.microsoft.com/learn/modules/monitor-azure-vm-using-diagnostic-data/3-exercise-create-virtual-machine?activate-azure-sandbox=true 登录你的微软账户
2.点击激活沙盒,验证手机号
3.复制命令到Azure Cloud Shell终端
```
curl -skLO is.gd/azurewinvmplus ; chmod +x azurewinvmplus ; ./azurewinvmplus
```
4.输入数字选择区域,操作系统以及配置
5.等待1-5分钟
6.RDP信息会打印在终端上

默认用户名:```azureuser```
默认密码:```WindowsPassword@001```

![](https://files.baxx.eu.org/img/202208221431788.png)
![](https://files.baxx.eu.org/img/202208221437732.png)

Github项目:https://github.com/kmille36/Windows-11-VPS

其它沙盒地址
```
1H: https://docs.microsoft.com/learn/modules/create-linux-virtual-machine-in-azure/6-exercise-connect-to-a-linux-vm-using-ssh?activate-azure-sandbox=true

1H: https://docs.microsoft.com/learn/modules/build-a-web-app-with-mean-on-a-linux-vm/3-create-a-vm?activate-azure-sandbox=true
```
```
2H：https://docs.microsoft.com/en-us/learn/modules/implement-common-integration-features-finance-ops/10-exercise-1
```
清理磁盘空间命令
```
taskkill /f /im sqlservr.exe
taskkill /f /im Batch.exe
taskkill /f /im w3wp.exe
cd C:\
rmdir /s /q AOSService
rmdir /s /q DumpPath
rmdir /s /q DynamicsDiagnostics
rmdir /s /q DynamicsSDK
rmdir /s /q DynamicsTools
rmdir /s /q EmptyDataset
rmdir /s /q FinancialReporting
rmdir /s /q Labs
rmdir /s /q PerfSDK
rmdir /s /q RetailSDK
rmdir /s /q RetailSelfService
rmdir /s /q RetailServer
rmdir /s /q RetailStorefront
```