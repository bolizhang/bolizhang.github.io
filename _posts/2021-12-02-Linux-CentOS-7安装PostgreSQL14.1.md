---
layout:     post
title:      Linux CentOS 7安装PostgreSQL14.1
subtitle:   PostgreSQL
date:       2021-12-02
author:     Zhang.Libo
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - PostgreSQL
    - PostgreSQL安装
---


1.  安装rpm文件
```shell
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

2. 安装PostgreSQL
```shell
sudo yum install -y postgresql14-server
```

3. 初始化数
```shell
sudo /usr/pgsql-14/bin/postgresql-14-setup initdb
```

4. 设备开机启动
```shell
sudo systemctl enable postgresql-14
```

5. 启动PostgreSQL服务
```shell
sudo systemctl start postgresql-14
```

6. 设置数据库密码

* 数据库安装后，默认创建账号postgres

* 使用postgres账号身份操作
```shell
su - postgres
```

* 使用postgres账号登录数据库
```shell
psql -U postgres
```

* 设置密码
```shell
alter user postgres with password '123456'
```

* 退出
```shell
\q    #退出数据库
exit  #退出postgres账号
```


7. 开启远程访问

* 对所有IP开放访问

 * 打开postgresql.conf文件
```shell
vi /var/lib/pgsql/14/data/postgresql.conf
```

  * 修改listen_address配置(对所有IP开发访问)
```shell
listen_address = '*'
```

* 增加信任连接

 * 打开pg_hba.conf文件
```shell
vi /var/lib/pgsql/14/data/pg_hba.conf
```

  * 增加新人连接配置
```shell
# IPv4 local connections:
host    all             all             0.0.0.0/0               trust
```

* 重启服务
```shell
systemctl restart postgresql-14
```


8. 添加防火墙端口号

* 添加端口号
```shell
firewall-cmd --zone=public --add-port=5432/tcp --permanent
```

* 重载防火墙立即生效
```shell
firewall-cmd --reload
```
