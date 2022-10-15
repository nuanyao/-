---
title: Onedrive-Vercel-index部署
date: 2022-08-22 12:54:50
tags:
	- onedrive
	- Onedrive-Vercel-index
	- Onedrive牵引
categories: 技术教程
---
Onedrive-vercel-index是一个界面美丽的OneDrive 公共目录列表,使用 Onedrive-vercel-index 可以展示、共享、预览和下载OneDrive中的文件
<!--more-->
# 演示
https://drive.swo.moe/
![](https://files.baxx.eu.org/img/202208221301497.png)

# 文档
https://ovi.swo.moe/docs/getting-started

# 部署教程
1.Fork https://github.com/spencerwooo/onedrive-vercel-index 到你的Github
2.更改 config/site.config.js 中的 userPrincipleName 为你的Microsoft账户邮箱地址
3.更改 config/site.config.js 中的 baseDirectory 为想要共享的Onedrive文件夹
4.根据情况修改 config/api.config.js (可选)
5.导入到Vercel并添加[Upstash](https://vercel.com/integrations/upstash)数据库
6.重新部署