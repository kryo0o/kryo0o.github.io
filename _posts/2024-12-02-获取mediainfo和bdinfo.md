---
layout: post
title: 获取mediainfo和bdinfo
date: 2024-12-02
categories: blog
tags: [pt]
description: 获取mediainfo和bdinfo。
author: 'kryo'
---

`Debian`安装 `apt install mediainfo mediainfo-gui`

使用示例`mediainfo <path_to_media_file>`

例子：`mediainfo xxx.mkv`

bdinfo 

两种方法

1、`https://github.com/zoffline/BDInfoCLI-ng`的方法，推荐直接docker运行获取，bdinfo获取在原盘目录下

`docker run --rm -it -v <BD_PATH>:/mnt/bd zoffline/bdinfocli-ng /mnt/bd`

2、`https://github.com/Aniverse/bluray`这个脚本可以截图

运行`bash <(wget -qO- https://git.io/bluray) -u`，`bluray`



> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
