---
title: 使用Vercel反代网站
date: 2022-08-24 13:22:35
tags:
	- Vercel
	- 反向代理
	- CDN
	- 反代
categories: 技术教程
---
使用Vercel反代网站，加速网站访问
<!--more-->
# 准备
一个[Vercel](https://vercel.com)账户
安装好[NodeJS](https://nodejs.org/zh-cn/)环境

# 安装Vercel CLI
```
npm i -g vercel
```

# 登录Vercel
```
vercel login
```

# 创建 xxx.json 文件(文件名随意)
```
{
  "version": 2,
  "routes": [
      {"src": "/(.*)","dest": "http://example.com/$1"}
  ]
}
```
将上面的```http://example.com/```改为你想要反代的URL

# 部署
```
vercel -A xxx.json --prod
```