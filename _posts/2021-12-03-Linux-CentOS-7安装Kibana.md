---
layout:     post
title:      Linux CentOS 7安装Kibana
subtitle:   Kibana
date:       2021-12-03
author:     ZhangLibo
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - Kibana
    - Kibana安装
---


1.  下载并安装签名公钥
```shell
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

2. 从RPM储存库安装

* 新建并打开kibana.repo文件
```shell
vi /etc/yum.repos.d/kibana.repo
```

* kibana.repo文件配置内容
```shell
[kibana-7.x]
name=Kibana repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

* 安装
```shell
sudo yum install kibana
```

3. 修改kibana.yml配置

* kibana.yml配置文件
```shell
vi /etc/kibana/kibana.yml
```

* 修改配置内容
```shell
server.port: 5601
server.host: "0.0.0.0"
server.publicBaseUrl: "http://192.168.107.130:5601"
elasticsearch.hosts: ["http://localhost:9200"]
i18n.locale: "zh-CN"
```

4. 开机运行配置
```shell
systemctl daemon-reload
systemctl enable kibana.service
```

5. 服务启动和停止
```shell
systemctl start kibana.service
systemctl stop kibana.service
```
