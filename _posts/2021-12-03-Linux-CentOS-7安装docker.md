---
layout:     post
title:      Linux CentOS 7安装docker
subtitle:   Docker
date:       2021-12-03
author:     ZhangLibo
header-img:
catalog: 	 true
tags:
    - Linux
    - CentOS
    - CentOS 7
    - Docker
    - Docker安装
---


1.  卸载旧版本
```shell
sudo yum remove docker \
                 docker-client \
                 docker-client-latest \
                 docker-common \
                 docker-latest \
                 docker-latest-logrotate \
                 docker-logrotate \
                 docker-engine
```

2. 设置储存库
```shell
sudo yum install -y yum-utils
sudo yum-config-manager \
          --add-repo \
          https://download.docker.com/linux/centos/docker-ce.repo
```

3. 安装 Docker 引擎
```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

4. 启动 Docker
```shell
sudo systemctl start docker
```

5. 开机运行
```shell
sudo systemctl enable docker.service
```

6. 远程访问配置

* 打开配置文件docker.service
```shell
vi /usr/lib/systemd/system/docker.service
```

* 更新配置
```shell
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375
```

* 重载配置
```shell
sudo systemctl daemon-reload
```

* 重新启动Docker
```shell
sudo systemctl restart docker.service
```

7. 添加防火墙端口号

* 添加端口号
```shell
firewall-cmd --zone=public --add-port=2375/tcp --permanent
```

* 重载防火墙立即生效
```shell
firewall-cmd --reload
```

8. Portainer管理工具搭建

* 下载镜像
```shell
docker pull docker.io/portainer/portainer
```

* 运行镜像
```shell
docker run -d -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name prtainer-test docker.io/portainer/portainer
```
