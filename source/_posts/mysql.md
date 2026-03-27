---
title: mysql5.7-deploy
date: 2023-07-01 15:36:15
tags:
published: false
---


## 使用RPM安装MySQL 存储库

```
rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```

## 使用yum命令安装软件包

```
yum install mysql-server
```

### 问题

​		在这里会出现系统已经安装了与MySQL 5.7存储库关联的GPG密钥，但密钥不匹配正在尝试安装的软件包

![image-20230701160233875](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230701160233875.png)

### 解决办法：

#### 	解决办法一：

1. 清除YUM缓存：执行以下命令以清除YUM缓存并尝试重新安装

   ```
   yum clean all
   ```

2. 更新密钥：执行以下命令来更新存储库的GPG密钥：

   ```
   rpm --import https://dev.mysql.com/doc/mysql-repo-extractor/KEY
   ```

#### 解决办法二

1. 使用以下网站下载GPG密钥

   ```
   https://repo.mysql.com/
   ```

   ![image-20230701155413611](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230701155413611.png)

2. 密钥

   ```
   -----BEGIN PGP PUBLIC KEY BLOCK-----
   
   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
   =Xqbo
   -----END PGP PUBLIC KEY BLOCK-----
   ```

3. 在centos7路径下 

   ```
   cd /etc/pki/rpm-gpg/
   ```

4. 创建一个文件,将上面的密钥全部粘贴，

   ```
   vim RPM-GPG-KEY-mysql
   ```

5. 重新运行以下命令

   ```
   yum install mysql-server
   ```

## 启动和查看mysql

```
systemctl start mysqld
systemctl status mysqld
```

## 查看mysql初始密码

```
grep 'temporary password' /var/log/mysqld.log
```

![image-20230701160617413](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230701160617413.png)

## 加强MySQL的安全性

```
mysql_secure_installation
```

1. 输入root用户密码

   ![image-20230701160809142](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230701160809142.png)

2. 输入新密码，

   ![image-20230701161032743](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230701161032743.png)

3. 输入完后

   设置完新密码后，会直接进入安装配置环节。或是按 CTRL+C 终止上次操作再重新执 行，不要选择修改密码即可。 在进行 MySQL 数据库初始化过程中会出现以下交互确认信息： 

   ①Change the password for root ? ((Press y|Y for Yes, any other key for No) 表示是否更改 root 用户密码，如果已经修改密码为 Password123$，则直接回车；如果密 码没有修改，可以点 y 在键盘输入 y 和回车。 

   ②Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) 表示是否使用设定的密码继续，在键盘输入 y 和回车。

    ③Remove anonymous users? (Press y|Y for Yes, any other key for No) 表示是否删除匿名用户，在键盘输入 y 和回车。 

   ④Disallow root login remotely? (Press y|Y for Yes, any other key for No) 表示是否拒绝 root 用户远程登录，在键盘输入 n 和回车，表示允许 root 用户远程登录。 

   ⑤Remove test database and access to it? (Press y|Y for Yes, any other key for No) 表示是否删除测试数据库，在键盘输入 y 和回车。test 库在 MySQL 中特殊存在，一般部署 完 mysql 后应当删除该库，并规定不能创建以 test 和 test_字符开头的数据库。因为在 my sql 中，test 库对任意用户都有管理员权限，会造成安全问题。 

   ⑥Reload privilege tables now? (Press y|Y for Yes, any other key for No) 表示是否重新加载授权表，在键盘输入 y 和回车。

## 进入mysql

```
mysql -uroot -p
```

## 将数据库的编码全部改成utf-8

1. 编辑文件

   ```
   vim /etc/my.cnf
   ```

2. 添加以下内容

   ```
   character_set_server=utf8
   ```

3. 重启mysql

   ```
   systemctl restart mysqld
   ```

4. 使用以下命令查看

   ```
   show variables like 'character%';
   ```

   ![image-20230701162733347](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20230701162733347.png)

## 修改数据库密码

1. 使用以下密码修改

   ```
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'Password23_';
   ```

2. 刷新数据库趣权限

   ```
   flush privileges;
   ```

## 设置数据库远程权限

1. 使用以下命令开启远程访问权限

   ```
   grant all privileges on *.* to 'root'@'%'identified by 'Password123_' with grant option;
   ```

2. 刷新数据库权限

   ```
   flush privileges;
   ```

   
