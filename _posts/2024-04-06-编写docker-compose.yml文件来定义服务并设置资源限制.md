---
layout: post
title: 编写docker-compose.yml文件来定义服务并设置资源限制 
date: 2024-3-27
categories: blog
description: 编写docker-compose.yml文件来定义服务并设置资源限制
author: 'kryo'
---

编写 `docker-compose.yml` 文件来定义服务并设置资源限制

```
services:
  my_service:
    image: some/image
    deploy:
      resources:
        limits:
          cpus: '0.5' # 最多使用50%的CPU资源
          memory: 512M # 限制内存最大为512MB
        reservations:
          cpus: '0.25' # 确保至少有25%的CPU资源可用
          memory: 256M # 至少预留256MB内存给该容器
    # 其他服务配置...
```

请注意，在 `docker-compose` v3 及以上版本中，为了应用这些资源限制，您可能需要在 Swarm 模式下部署服务。如果仅在单机环境或非 Swarm 模式下运行，直接在服务配置中设置资源限制可能不会生效。在这种情况下，可以直接在服务容器级别设置资源限制，如下所示：

```
services:
  my_service:
    image: some/image
    container_name: my_container
    mem_limit: 512M # 单纯设置内存限制，适用于非Swarm模式部署
    mem_reservation: 256M # 设置内存预留量，同样适用于非Swarm模式
    cpu_shares: 512 # 在非Swarm模式下设置相对CPU权重（不是严格的CPU限制）
    # （严格CPU核心数限制在非Swarm模式下难以实现，需借助其他手段如使用约束或使用较新版本的Docker）
```

`cpu_shares` 是一个相对权重值，而不是绝对的CPU使用率百分比。要实现更精确的CPU限制，尤其是硬性限制，通常需要在Swarm模式下部署或者在较新的Docker版本中使用类似 `cpus:` 的配置。

另外，对于IO资源限制，Docker本身提供了一定程度的IO带宽限制，但在 `docker-compose.yml` 文件中并不直接支持。在较新的Docker版本中，可能需要通过额外的存储驱动器选项或Linux的 blkio cgroup 来间接控制容器的IO资源。
> 如有任何知识产权、版权问题或理论错误，还请指正。
>
> 转载请注明原作者及以上信息。
