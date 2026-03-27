---
title: warp
date: 2023-04-09 13:58:10
tags:
published: false
---



### 执行脚本

```
https://github.com/fscarmen/warp
//使用以下运行脚本
warp-go 运行脚本
```



```
wget -N https://raw.githubusercontent.com/fscarmen/warp/main/warp-go.sh && bash warp-go.sh
```

- 选择  非全局

  ![image-20230409140012513](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230409140012513.png)

- 免费 3

![image-20230409140043324](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230409140043324.png)

执行完毕如果没有warp-go这个命令使用以下命令

```
systemctl daemon-reload
reboot
```

配置出站规则

- 进入路径

```
/etc/v2ray-agent/xray/conf
```

- 编辑这两个文件

![image-20230409153108748](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230409153108748.png)

- 文件内容

```
nano 09_routing.json
```

![image-20230409153332716](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230409153332716.png)

```
nano 10_ipv4_outbounds.json 
```

![image-20230409153432041](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230409153432041.png)

- 如果你只有一个配置文件使用以下配置

```
{
    "outbounds":[
        {
            "tag":"INTERNET_OUT",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIP"
            }
        },
        {
            "tag":"WARP-GO_INTERFACE",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "sendThrough":"172.16.0.2"
        }
    ],
    "routing":{
        "rules":[
            {
                "type":"field",
                "outboundTag":"WARP-GO_INTERFACE",
                "domain":[
                    "geosite:google",
                    "geosite:netflix",
                    "domain:ip.sb",
                    "domain:openai.com",
                    "domain:ai.com"
                ]
            },
            {
                "type":"field",
                "outboundTag":"INTERNET_OUT",
                "network":"udp,tcp"
            }
        ]
    },
    "dns":{
        "servers":[
            "1.1.1.1",
            "1.0.0.1"
        ]
    }
}
```

重启脚本
