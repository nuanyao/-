---
title: 网页秒开秘诀：网站预加载的JS脚本instantpage.js使用方法
date: 2022-08-21 20:51:51
tags: 
	- js 
	- instantpage.js 
	- html
categories: 技术教程
---
它的作用是可以预加载，用户想访问的页面，用户点击网站链接之前，他们将鼠标悬停在该链接上。当用户徘徊 65 毫秒时，当用户真正点击链接后，就会直接从缓存中读取，以此提升网站的访问速度，因此 instant.page 此时开始预加载，平均超过 300 毫秒，instant.page 是渐进式增强 ，对不支持它的浏览器没有影响。
<!--more-->
# 效果演示
经过测试，发现 instant.page 对站内访问速度的提升的确很给力。然而它只会预加载自己的站内链接，而不会预加载其他外链。

如图所示，当鼠标在左侧文章链接悬停超过 65ms 后，右侧 Network 即会对文章页面进行预加载。而悬停未超过 65ms 时，则不会进行预加载。
![](https://files.baxx.eu.org/img/202208212107707.png)
![](https://files.baxx.eu.org/img/202208212109572.gif)
# 使用方法
GitHub项目：https://github.com/instantpage/instant.page

官方使用方法，代码添加到网站的</body>标签之前

```
<script src="//instant.page/5.1.1" type="module" integrity="sha384-MWfCL6g1OTGsbSwfuMHc8+8J2u71/LA8dzlIN3ycajckxuZZmF+DNjdm7O6H3PSq"></script>
```
但是此脚本是官方的，储存在国外服务器，对国内访问不太友好，可以将该JS脚本储存到自己的服务器上，点此获取该JS脚本，然后再根据以下格式在</ body> 之前引用：

```
<script type="module" src="存放路径"></script>
```
bootcdn加速：
https://www.bootcdn.cn/instant.page/

```
<script type="module" src="https://cdn.bootcss.com/instant.page/5.1.1/instantpage.js"></script>
```
定义预加载
白名单标签属性： data-instant ，例：

```
<a href="http://www.baidu.com/" data-instant>Baidu</a>
```
黑名单标签属性： data-no-instant ，例：

```
<a href="http://www.baidu,com/" data-no-instant>百度</a>
```
全局允许：在 <body> 中添加 data-instant-allow-query-string 属性

局部允许：在使用的标签中添加 data-instant 属性（和白名单属性一样）

仅预加载部分指定链接（白名单模式）：如果只想预加载特定的链接，请在 <body> 中添加一个 data-instant-whitelist 标签，并通过向其添加 data-instant 属性来标记要预加载的链接。

# 注意
预加载可能会存在增加耗费少量 CDN 流量和PV问题，请自行对比后考虑是否使用。好了，感兴趣的可以自行测试下效果，