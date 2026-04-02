---
title: docker-django
date: 2022-11-21 23:18:56
tags:
published: false
---


<!-- # docker部署 Django -->

## 配置

1. 在根目录创建Dockerfile

   ```
   FROM python:3
   ENV PYTHONUNBUFFERED 1
   WORKDIR /code/djangoblog/
   
   
   #RUN  apt-get install ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime \
   ADD requirements.txt requirements.txt
   RUN pip install --upgrade pip  && \
           pip install -Ur requirements.txt  && \
           pip install gunicorn[gevent] && \
           pip cache purge
   
   EXPOSE 8099
   ADD . .
   RUN chmod +x bin/docker_start.sh
   ENTRYPOINT ["bin/docker_start.sh"]
   ```

2. 创建需要的依赖的配置文件

   ```
   使用命令行创建
   pip freeze > requirements.txt 
   pip install -Ur requirements.txt
   ```

   

3. 创建在运行脚本

   ```
   #!/usr/bin/env bash
   python manage.py runserver 0.0.0.0:8099
   ```

## 打包成docker镜像

```
 docker build -t houses:v0.1 . 
```

## 推送和拉取到docker Hub

```
 //设置标签
 docker tag houses:v0.1 shanhui/houses:tagname
 //推送到docker Hub
 docker push shanhui/houses:tagname
 
 //拉取
 docker pull shanhui/houses:houses
```

## docker运行Django

```
docker run -d  -p 8099:8099 3a16afa66aab[images]
```



## 删除容器

![image-20221120200528932](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221120200528932.png)

```
docker image rmi shanhui/houses:tagname

如果还有容器运行会报
Error response from daemon: conflict: unable to remove repository reference "shanhui/houses:tagname" (must force) - container 44d9766d8fd6 is using its referenced image 2b18f4236f3e

解决办法
 如果还有请反复执行
 docker stop 44d9766d8fd6
 docker rm 44d9766d8fd6
 docker image rmi shanhui/houses:tagname
```

<!-- <style>
  /* 设置整个页面的字体 */
  html, body, .markdown-body {
    font-family: KaiTi,"Microsoft YaHei",Georgia, sans, serif;
    font-size: 20px;
  }

  /* 只设置 markdown 字体 */
  .markdown-body {
    font-family: KaiTi,"Microsoft YaHei",Georgia, sans, serif;
    font-size: 80px;
  } -->
<!-- </style> -->
