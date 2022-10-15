---
title: CloudflarePages反向代理
date: 2022-08-22 12:14:42
tags:
	- CloudflarePages
	- Cloudflare
	- 反向代理
categories: 免费资源
---
# 准备
需要的材料:
Cloudflare账户
Github/Gitlab账户
<!--more-->
# 教程
1.新建一个Github/Gitlab仓库
2.创建_worker.js文件
```
export default {
  async fetch(request, env) {
    let url = new URL(request.url);
    if (url.pathname.startsWith('/')) {
      url.hostname = '此处修改为反代的网站地址'
      let new_request = new Request(url, request);
      return fetch(new_request);
    }
    return env.ASSETS.fetch(request);
  },
};
```
3.转到CloudflarePages进行部署