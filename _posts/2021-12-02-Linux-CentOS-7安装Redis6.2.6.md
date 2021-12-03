---
layout:     post
title:      Linux CentOS 7安装Redis6.2.6
subtitle:   Redis
date:       2021-12-02
author:     ZhangLibo
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - Redis
    - Redis安装
---


1.  下载Redis6.2.6
```shell
wget https://download.redis.io/releases/redis-6.2.6.tar.gz
```

* 如果遇到如下错误(**非必须步骤**)
```shell
wget: command not found
```

  需要执行命令先安装wget
```shell
yum -y install wget
```

  然后再下载Redis6.2.6
```shell
wget https://download.redis.io/releases/redis-6.2.6.tar.gz
```


2. 解压
```shell
cd /usr/local
tar xzf redis-6.2.6.tar.gz
```

3. 安装
```shell
cd redis-6.2.6
make
```

* 如果遇到如下错误提示
```shell
/bin/sh: cc: command not found
```

  * 安装gcc
```shell
yum install -y gcc
```

  * 重新执行make安装
```shell
make distclean && make
```

4. 修改配置

* 打开配置文件
```shell
vi /usr/local/redis-6.2.6/redis.conf
```

* 更新配置
```shell
protected-mode no #关闭保护模式
daemonize yes #守护进程模式开启
#bind 127.0.0.1 #注释配置后开启远程访问
port 6379 # 端口
requirepass 123456 #密码
```

5. 启动服务
```shell
/usr/local/redis-6.2.6/src/redis-server /usr/local/redis-6.2.6/redis.conf
```

6. 连接测试
```shell
/usr/local/redis-6.2.6/src/redis-cli -h 127.0.0.1 -p 6379 -a 123456
```

7. 停止服务
```shell
/usr/local/redis-6.2.6/src/redis-cli -p 6379 -a 123456 shutdown
```

8. 开机运行

* 新建文件redis.service
```shell
vi /lib/systemd/system/redis.service
```

* 写入配置
```shell
[Unit]
Description=The redis-server Process Manager
Documentation=https://redis.io/
After=network.target
[Service]
Type=forking
ExecStart=/usr/local/redis-6.2.6/src/redis-server /usr/local/redis-6.2.6/redis.conf
ExecStop=/usr/local/redis-6.2.6/src/redis-cli -h 127.0.0.1 -p 6379 -a 123456
[Install]
WantedBy=multi-user.target
```

* redis.service文件授权
```shell
systemctl daemon-reexec
```

* 开运运行设置
```shell
systemctl enable redis.service
```


9. 添加防火墙端口号

* 添加端口号
```shell
firewall-cmd --zone=public --add-port=6379/tcp --permanent
```

* 重载防火墙立即生效
```shell
firewall-cmd --reload
```
