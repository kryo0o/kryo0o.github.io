---
layout: post
title: ServerStatus中文版
date: 2023-12-27
categories: blog
description: ServerStatus中文版
author: 'kryo'
---

部署：
【服务端】：

Docker:

```bash
wget --no-check-certificate -qO ~/serverstatus-config.json https://raw.githubusercontent.com/cppla/ServerStatus/master/server/config.json && mkdir ~/serverstatus-monthtraffic
```

```bash
docker run -d --restart=always --name=serverstatus -v ~/serverstatus-config.json:/ServerStatus/server/config.json -v ~/serverstatus-monthtraffic:/usr/share/nginx/html/json -p 80:80 -p 35601:35601 cppla/serverstatus:latest
```

【客户端】：

```bash
wget --no-check-certificate -qO client-linux.py 'https://raw.githubusercontent.com/cppla/ServerStatus/master/clients/client-linux.py' && nohup python3 client-linux.py SERVER={$SERVER} USER={$USER} PASSWORD={$PASSWORD} >/dev/null 2>&1 &
```

```bash
wget --no-check-certificate -qO client-linux.py 'https://raw.githubusercontent.com/cppla/ServerStatus/master/clients/client-linux.py' && nohup python3 client-linux.py SERVER=45.79.67.132 USER=s04  >/dev/null 2>&1 &
```

【客户端配置】

客户端有两个版本，client-linux为普通linux，client-psutil为跨平台版，普通版不成功，换成跨平台版即可。

一、client-linux 版配置：
1. `nano client-linux.py`，修改 SERVER 地址，username 帐号，password 密码
2. `python3 client-linux.py` 运行即可

二、client-psutil 版配置：
1. 安装 psutil 跨平台依赖库

Debian/Ubuntu

```bash
apt -y install python3-pip && pip3 install psutil
```

Centos/Redhat

```bash
yum -y install python3-pip gcc python3-devel && pip3 install psutil
```

2. 修改 SERVER 地址，username 帐号，password 密码

```bash
nano client-psutil.py
```

3. `python3 client-psutil.py` 运行即可

服务器和客户端自行加入开机启动，或进程守护，或后台方式运行。
例如：

```bash
nohup python3 client-linux.py &
```

> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
