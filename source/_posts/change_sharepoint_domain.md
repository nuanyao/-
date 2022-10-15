---
title: 修改微软全局Sharepoint二级域名前缀
date: 2022-08-24 8:46:06
tags: 
	- sharepoint
	- microsoft
	- 微软
	- 全局
categories: 技术教程
---
修改微软全局Sharepoint二级域名前缀
最近在loc上买了个E3 MSDN 25T 亚太地区的全局 （在此感谢lzw大佬，先给了管理员账号上去确认，还有记录此前在TG上交了学费）
<!--more-->
最开始E3 MSDN是通过注册链接自己注册的，所有的信息都是注册时候已经确定，买到以后，安全起见，建立新的全局管理员，再新建4个用户，分别登录onedrive，把原来的全局管理和账号都删除（25t的全局可保留一个原先已经扩容到25t的账号，如果是管理员就改成普通成员，并重置密码，因为扩容25t需要全局内有5个及以上成员，一个成员od容量使用4.5t-5t以上，工单申请扩容至25t，目前已经很难申请通过了），技术联系人修改成自己的邮箱，api删除重新申请，添加密保等操作。PS：对订阅千万、千万、千万别去操作，重要的事情说三遍！！！

通过 https://admin.microsoft.com/ 登录365管理中心 左侧标签栏里 点击全部显示 修改用户 设置 AAD等信息，买全局的也都懂，不再赘述了。

这里要说的是，你修改了组织名，在365管理中心修改了回退域（就是XXX.‎onmicrosoft.com‎)，但是在sharepoint页面（通过365管理中心 左侧全部显示 sharepoint进入，可以调整成员od默认容量至5t等）的前缀 还是原来的用户设置的前缀，这强迫症能忍？

（按照微软的说法：首次注册 Microsoft 365 时，你创建了一个 onmicrosoft.com 域。 即使你后来添加了自定义域，原始 onmicrosoft.com 域也将用于所有 SharePoint 和 OneDrive URL。）‎

据出我E3 MSDN全局的lzw大佬说这个以前都是无法修改的，但强迫症还是不死心啊，最后找到了一个最新的方法，在此分享，理论上所有全局都可以用此方法修改。

这里说的修改域名是指将 SharePoint URL 从 abc.sharepoint.com 更改为 zxc.sharepoint.com.

# 第 1 步：验证新域名
## 1.检查你想要的新域的可用性。 例如，如果希望 SharePoint 和 OneDrive URL 以 zxc.sharepoint.com 开头，在浏览器中输入 https://zxc.sharepoint.com。 如果是404页面，那么这个域名可能可用。 如果提示登录或目录中找不到用户名的消息，就要换一个。 

## 2.https://aka.ms/SPORenameAddDomain 添加新的域名（必须使用该链接转到 Azure AD 管理中心的自定义域名页面，否则添加可能不成功）

## 3.选择 添加自定义域。在“自定义域名”框中，输入完整的新“.onmicrosoft.com”域，然后选择“添加域”。（该域必须是“onmicrosoft.com”域。 例如，如果要重命名为 zxc.sharepoint.com，则输入的域应为 zxc.onmicrosoft.com）

## 4.在页面顶部的导航中，选择租户名称,返回到自定义域名页面。 确保添加的 onmicrosoft.com 域在列表中，并且状态显示为“已验证”。（值得注意的是，在365管理中心修改或者添加的回退域状态显示为“可用”而非“已验证”，如果状态不是“已验证”，则你将无法执行重命名操作，未进一步验证）

# 第 2 步：使用 Microsoft PowerShell 重命名域

## 1.必需 – 下载最新的 SharePoint Online 命令行管理程序。
https://go.microsoft.com/fwlink/p/?LinkId=255251

（如果安装过旧版就需要先卸载，mac不支持这个程序）

## 2.以全局管理员或 SharePoint 管理员身份连接到 SharePoint Online

命令为：
```
Connect-SPOService -Url https://abc-admin.sharepoint.com -Credential admin@abc.com （根据实际sharepoint网址和管理员账号修改）回车后输入密码。
```
## 3.重头戏，更改域名（必须是第一步3里面添加的已验证状态的域名前缀）

命令为：
```
Start-SPOTenantRename -DomainName “zxc” -ScheduledDateTime “2021-12-31T10:25:00” （这里的datetime必须是24小时以后最长不超过30天，可以理解为排队时间，最快也要排队24小时才开始给你更改）
```
输入命令后会有再次确认的反馈，如果没有反馈，可能是时间错误、域名未验证或者使用了旧版的软件，自行排查。

## 4.查询进度

命令为： ```Get-SPOTenantRenameStatus``` （如果有问题，就打开新的窗口再次登录）

state状态在你设定的时间到之前应该是显示Queued，在处理中是InProgress，成功就是Success。

## 5.取消重命名

命令为：```Stop-SPOTenantRename``` （必须在你设定的时间开始之前取消）

## 6.验证是否成功

从365管理中心登录sharepoint，应该就是zxc-admin.sharepoint.com了

## 7.
重命名不适用于设置了多个地理位置的组织，6个月只能重命名一次，重命名的逻辑是在原来的url上创建重定向，所以也不支持改回原来的域名，也不支持自己添加的个性域名。（经验证，输入原来的sharepoint地址会自动重定向到新的域名）


https://hostloc.com/thread-946734-1-1.html
