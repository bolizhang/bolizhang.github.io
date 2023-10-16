---
layout:     post
title:      Linux CentOS 7安装MongoDB 5.0.4
subtitle:   Mongo
date:       2021-12-02
author:     Zhang.Libo
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - Mongo
    - Mongo安装
---


1.  下载MongoDB5.0.4
```shell
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/5.0/x86_64/RPMS/mongodb-org-server-5.0.4-1.el7.x86_64.rpm
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/5.0/x86_64/RPMS/mongodb-org-shell-5.0.4-1.el7.x86_64.rpm
```

* 如果遇到如下错误(**非必须步骤**)
```shell
wget: command not found
```

  需要执行命令先安装wget
```shell
yum -y install wget
```

  然后再下载MongoDB5.0.4
```shell
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/5.0/x86_64/RPMS/mongodb-org-server-5.0.4-1.el7.x86_64.rpm
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/5.0/x86_64/RPMS/mongodb-org-shell-5.0.4-1.el7.x86_64.rpm
```


2. 安装MongoDB
```shell
rpm -ivh mongodb-org-server-5.0.4-1.el7.x86_64.rpm
rpm -ivh mongodb-org-shell-5.0.4-1.el7.x86_64.rpm
```

3. 启动MongoDB服务
```shell
systemctl start mongod
```

4. 设置账号密码

* 开启认证
```shell
/usr/bin/mongod --auth
```

* 连接
```shell
mongo --port 27017
```

* 进入Mongo命令行后操作，切换admin库，创建账号
```shell
use admin
db.createUser({user:"admin",pwd:"password",roles:["root"]})
```

* 进入Mongo命令行后操作，认证登录
```shell
db.auth("admin", "password")
```

5. 开启远程访问

* 打开mongod.conf文件
```shell
vim /etc/mongod.conf
```

* 修改bindIp配置后保存
```shell
bindIp = 0.0.0.0
```

* 重启Mongo服务
```shell
systemctl restart mongod
```

* 重启Mongo服务时遇到mongodb-27017.sock文件未授权错误，删除文件再重启服务(**非必须步骤**)
```shell
rm -rf /tmp/mongodb-27017.sock
```


6. 添加防火墙端口号

* 添加端口号
```shell
firewall-cmd --zone=public --add-port=27017/tcp --permanent
```

* 重载防火墙立即生效
```shell
firewall-cmd --reload
```
