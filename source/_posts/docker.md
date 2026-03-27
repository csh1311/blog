---
title: docker容器代理
date: 2023-09-19 10:10:52
tags:
published: false
---

# docker

## docker设置代理

1. 进入docker容器

   ```
   docker exec -it <容器名称或容器ID> /bin/bash
   ```

2. 设置代理

   ```
   export ALL_PROXY='http://10.235.0.19:10809'
   export http_proxy='http://10.235.0.19:10809'
   export https_proxy='https://10.235.0.19:10809'
   ```
