---
layout:     post
title:      Linux CentOS 7安装MySQL80
subtitle:   MySQL
date:       2021-12-01
author:     LiboZhang
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - MySQL
    - MySQL安装
---


1.  下载MySQL80
```shell
wget https://repo.mysql.com/mysql80-community-release-el7-4.noarch.rpm
```

* 如果遇到如下错误(**非必须步骤**)
```shell
wget: command not found
```

  需要执行命令先安装wget
```shell
yum -y install wget
```

  然后再下载MySQL80
```shell
wget https://repo.mysql.com/mysql80-community-release-el7-4.noarch.rpm
```


2. 安装MySQL80

* 添加MySQL80仓库
```shell
rpm -ivh mysql80-community-release-el7-4.noarch.rpm
```

* 安装MySQL80
```shell
yum install mysql-server
```

* 遇到如下提示，输入y然后回车即可
```shell
Is this ok [y/d/N]: y
```

3. 启动MySQL80服务
```shell
systemctl start mysqld
```

* 查看服务运行状态(**非必须步骤**)
```shell
systemctl status mysqld
```

4. 登录MySQL

* 登录前需要先获取安装时生成的随机密码
```shell
grep 'temporary password' /var/log/mysqld.log
```

* 登录命令
```shell
mysql -uroot -p
```

5. 退出MySQL
```shell
quit;
```

6. 修改密码

* 登录，录入随机密码
```shell
mysql -uroot -p
```

* 如果设置为简单密码，关闭密码校验规则(**非必须步骤**)
```shell
set global validate_password.policy=0;
set global validate_password.length=1;
```

* 修改密码(单引号内123456为填写新密码)
```shell
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
```

7. root账号远程登录

* 如果设置为简单密码，关闭密码校验规则(**非必须步骤**)
```shell
set global validate_password.policy=0;
set global validate_password.length=1;
```

* 授权账号远程登录
```shell
CREATE USER `root`@`%` IDENTIFIED BY 'test';
GRANT ALL ON *.* TO `root`@`%` WITH GRANT OPTION;
```


8. 添加防火墙端口号

* 添加端口号
```shell
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

* 重载防火墙立即生效
```shell
firewall-cmd --reload
```
