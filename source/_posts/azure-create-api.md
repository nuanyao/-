---
title: Azure云创建API
date: 2022-08-26 17:51:38
tags:
    - azure
categories: 技术教程
---
Azure云创建API
<!--more-->
# 安装Azure Cli
官网教程：
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

# 登录Azure
```
az login
```

# 创建API访问权限
```
az ad sp create-for-rbac --name api
```
保存参数