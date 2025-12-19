---
layout: post
title: ServerStatus中文版
date: 2022-12-27
categories: blog
description: ServerStatus中文版
author: 'kryo'
---

部署：
【服务端】：

`Docker`:     

`wget --no-check-certificate -qO ~/serverstatus-config.json https://raw.githubusercontent.com/cppla/ServerStatus/master/server/config.json && mkdir ~/serverstatus-monthtraffic    `
`docker run -d --restart=always --name=serverstatus -v ~/serverstatus-config.json:/ServerStatus/server/config.json -v ~/serverstatus-monthtraffic:/usr/share/nginx/html/json -p 80:80 -p 35601:35601 cppla/serverstatus:latest     `

`Docker-compose(推荐)`: docker-compose up -d`

【客户端】：

`wget --no-check-certificate -qO client-linux.py 'https://raw.githubusercontent.com/cppla/ServerStatus/master/clients/client-linux.py' && nohup python3 client-linux.py SERVER={$SERVER} USER={$USER} PASSWORD={$PASSWORD} >/dev/null 2>&1 &`

`wget --no-check-certificate -qO client-linux.py 'https://raw.githubusercontent.com/cppla/ServerStatus/master/clients/client-linux.py' && nohup python3 client-linux.py SERVER=45.79.67.132 USER=s04  >/dev/null 2>&1 &`
【客户端配置】

客户端有两个版本，client-linux为普通linux，client-psutil为跨平台版，普通版不成功，换成跨平台版即可。

一、client-linux版配置：
1、`nano client-linux.py`, 修改SERVER地址，username帐号， password密码
2、`python3 client-linux.py `运行即可。

二、client-psutil版配置:
1、安装psutil跨平台依赖库

`Debian/Ubuntu`: `apt -y install python3-pip && pip3 install psutil`   
`Centos/Redhat`: `yum -y install python3-pip gcc python3-devel && pip3 install psutil`      
`Windows`: `https://pypi.org/project/psutil/ `

2、`nano client-psutil.py`, 修改SERVER地址，username帐号， password密码
3、`python3 client-psutil.py `运行即可。

服务器和客户端自行加入开机启动，或进程守护，或后台方式运行。 例如: `nohup python3 client-linux.py &`

> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
