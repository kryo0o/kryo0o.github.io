---
layout: post
title: 获取mediainfo和bdinfo
date: 2024-12-02
categories: blog
description: 获取mediainfo和bdinfo。
author: 'kryo'
---

Debian 安装

```bash
apt install mediainfo mediainfo-gui
```

使用示例

```bash
mediainfo <path_to_media_file>
```

bdinfo 两种方法

1、[BDInfoCLI-ng](https://github.com/zoffline/BDInfoCLI-ng) 的方法，推荐直接 docker 运行获取，bdinfo 获取在原盘目录下

```bash
docker run --rm -it -v <BD_PATH>:/mnt/bd zoffline/bdinfocli-ng /mnt/bd
```

2、[Aniverse/bluray](https://github.com/Aniverse/bluray)，这个脚本可以截图

```bash
bash <(wget -qO- https://git.io/bluray) -u
```

```bash
bluray
```

> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
