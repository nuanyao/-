---
title: E5SubBot-微软E5开发者订阅TG自动续期Bot部署教程
date: 2022-08-23 08:49:05
tags:
	- E5SubBot
	- 微软
	- Microsoft
	- E5
	- E5续期
categories: 技术教程
---
E5SubBot是一款通过调用Outlook ReadMail API,实现E5开发者订阅续期的Telegram机器人
<!--more-->
## 演示
[@E5Sub_bot](https://t.me/E5Sub_bot)

## 原理

E5订阅为开发者订阅，只要调用相关API就有可能续期

调用 [Outlook ReadMail API](https://docs.microsoft.com/zh-cn/graph/api/user-list-messages?view=graph-rest-1.0&tabs=http)
实现玄学的续订方式，不保证续订效果。

## 使用方法

1. 在机器人对话框输入 **/bind**
2. 注册应用，使用E5主账号或同域账号登录，跳转页面获得client_secret。**点击回到快速启动**,获得client_id
3. 复制client_secret和client_id，以 `client_id client_secret`格式回复
4. 获得授权链接，使用E5主账号或同域账号登录
5. 授权后会跳转至`http://localhost/e5sub……`  (会提示网页错误，复制链接即可)
6. 复制整个浏览框内容，在机器人对话框回复 `链接+空格+别名(用于管理账户)`
   例如：`http://localhost/e5sub/?code=abcd MyE5`，等待机器人绑定后即完成

## 自行部署

首先你得有一个Telegram账户
进入Telegram 直接搜索```@BotFather```
![](https://files.baxx.eu.org/img/202208221453616.png)
点击Start
![](https://files.baxx.eu.org/img/202208221456724.png)
输入/newbot,按照提示一步步操作即可,保存Token

### Docker(推荐)

`Docker` 部署使用 `sqlite` 作为数据库

支持 `amd64` `386` `arm64` `arm/v6` `arm/v7` 架构

```shell
#启动，你可以设置自己想要的时区
docker run --name e5sub -e TZ="Asia/Shanghai" --restart=always -d iyear/e5subbot:latest
#查看log
docker logs -f e5sub
#设置配置文件
docker cp PATH/TO/config.yml e5sub:/config.yml
docker restart e5sub
#导入数据库
docker cp PATH/TO/DATA.db e5sub:/data.db
docker restart e5sub
#备份数据库
docker cp e5sub:/data.db .
#备份配置文件
docker cp e5sub:/config.yml .
```

### 二进制文件

在 [Releases](https://github.com/iyear/E5SubBot/releases) 页面下载对应系统的二进制文件，上传至服务器

Windows: 启动 `E5SubBot.exe`

Linux:

```bash
screen -S e5sub
chmod +x E5SubBot
./E5SubBot
(Ctrl A+D)
```

### 编译

下载源码，安装GO环境

```shell
git clone https://github.com/iyear/E5SubBot.git && cd E5SubBot && go build
```

## 部署配置

在同目录下创建`config.yml`，编码为`UTF-8`

配置模板:

```yaml
bot_token: YOUR_BOT_TOKEN
# socks5: 127.0.0.1:1080
bindmax: 999
goroutine: 20
admin: 111,222,333
errlimit: 999
notice: |-
   aaa
   bbb
   ccc
cron: "1 */1 * * *"
db: sqlite
table: users
# mysql:
#    host: 127.0.0.1
#    port: 3306
#    user: root
#    password: pwd
#    database: e5sub
sqlite:
   db: data.db
```

`bindmax`,`notice`,`admin`,`goroutine`,`errlimit`可热更新，直接更新`config.yml`保存即可

|  配置项   | 说明  |默认值|
|  ----  | ----  | ---- |
| bot_token  | 更换为自己的`BotToken` | -|
| socks5  | `Socks5`代理,不需要删去即可.例如:`127.0.0.1:1080` |-|
|notice|公告.合并至`/help`|-|
|admin|管理员`tgid`，前往 https://t.me/userinfobot 获取，用`,`隔开;管理员权限: 手动调用任务，获得任务总反馈|-|
|goroutine|并发数，不要过大|10|
|errlimit|单账户最大出错次数，满后自动解绑单账户并发送通知，不限制错误次数将值改为负数`(-1)`即可;bot重启后会清零所有错误次数|5|
|cron|API调用频率，使用cron表达式|-|
|bindmax|最大可绑定数|5|
|db|`mysql` 或 `sqlite` ，表示使用的数据库类型，并设置对应的配置|-|
|table|数据表名(旧版本升级请设置table为 `users`，否则读不到数据表)|-|
|mysql|`mysql` 配置，请提前创建数据库|-|
|sqlite|`sqlite` 配置|-|

### 命令

```
/my 查看已绑定账户信息  
/bind  绑定新账户  
/unbind 解绑账户  
/export 导出账户信息(JSON格式) 
/help 帮助  
/task 手动执行一次任务(Bot管理员)  
/log 获取最近日志文件(Bot管理员)  
```

## 注意事项

> 更新时间与北京时间不符
更改服务器时区为`Asia/Shanghai`，然后使用`/task`手动执行一次任务刷新时间

> 绑定格式错误
不要带"+"号

> 错误:Can't create more than max_prepared_stmt_count statements (current value: 16382)
没有关闭`db`导致触发`mysql`并发上限，请更新至`v0.1.9`

> 长时间运行崩溃
疑似内存泄露，尚未解决，请自行采用守护进程运行或定时重启`Bot`

> 无法通过Bot创建应用程序
https://t.me/e5subbot/5201

Github仓库地址:https://github.com/iyear/E5SubBot/