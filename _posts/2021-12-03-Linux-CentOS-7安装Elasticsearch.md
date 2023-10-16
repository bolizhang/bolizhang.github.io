---
layout:     post
title:      Linux CentOS 7安装Elasticsearch
subtitle:   Elasticsearch
date:       2021-12-03
author:     LiboZhang
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - Elasticsearch
    - Elasticsearch安装
---


1.  下载并安装签名公钥
```shell
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

2. 从RPM储存库安装

* 新建并打开elasticsearch.repo文件
```shell
vi /etc/yum.repos.d/elasticsearch.repo
```

* elasticsearch.repo文件配置内容
```shell
[elasticsearch]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=0
autorefresh=1
type=rpm-md
```

* 安装
```shell
sudo yum install --enablerepo=elasticsearch elasticsearch
```

3. 修改elasticsearch.yml配置

* 打开elasticsearch.yml配置文件
```shell
vi /etc/elasticsearch/elasticsearch.yml
```

* 修改配置内容
```shell
cluster.name: my-application
node.name: node-1
network.host: 0.0.0.0
http.port: 9200
cluster.initial_master_nodes: ["node-1"]
```

4. 开机运行配置
```shell
systemctl daemon-reload
systemctl enable elasticsearch.service
```

5. 服务启动和停止
```shell
systemctl start elasticsearch.service
systemctl stop elasticsearch.service
```
