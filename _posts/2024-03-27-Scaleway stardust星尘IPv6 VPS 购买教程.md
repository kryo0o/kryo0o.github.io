---
layout: post
title: Scaleway stardust星尘IPv6 VPS 购买教程
date: 2024-03-27
categories: blog
description: Scaleway stardust星尘IPv6 VPS 购买教程。
author: 'kryo'
---
官方教程：[Scaleway CLI](https://www.scaleway.com/en/docs/compute/instances/api-cli/creating-managing-instances-with-cliv2)

建议在网页后台直接添加个SSH KEY，避免后续无法登陆。

首先获取官方文件，此处环境是在 Debian 10 X86 系统下创建，其他系统和架构可在官方 Github 处获取：[scaleway-cli/releases](https://github.com/scaleway/scaleway-cli/releases)

```bash
curl -o /usr/local/bin/scw -L "https://github.com/scaleway/scaleway-cli/releases/download/v2.16.1/scaleway-cli_2.16.1_linux_amd64"
```

```bash
chmod +x /usr/local/bin/scw
```

然后登陆并创建 stardust 服务器

```bash
scw init
```

登陆并查看账号 UUID，或者在网页中创建实例的下方查看账号 UUID。

```bash
scw instance server create type=STARDUST1-S zone=fr-par-1 image=debian_bullseye root-volume=l:10G name=Denian ip=none ipv6=true project-id=账号UUID
```

需要安装其他镜像的话把image=自行改为debian_buster，ubuntu_jammy，ubuntu_focal，centos_stream_9，centos_stream_8，centos_7.9。也可自行dd。地区zone=也可以选择荷兰nl-ams-1。
获取机器 UUID

```bash
scw instance server list
```

开机

```bash
scw instance server start 机器UUID
```

若想直接使用 root 密码登录，在网页中找到 Advanced Setting，Cloud-init 处添加下列配置，保存完成后重启服务器即可。

```yaml
users:
  - name: root
    plain_text_passwd: 'yourpasswd'
    lock_passwd: false
```

> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
