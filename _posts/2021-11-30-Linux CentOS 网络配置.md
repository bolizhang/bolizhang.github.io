# 自动获取IP地址网络设置

1.  进入ifcfg-ens33配置文件
```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

2. ifcfg-ens33文件内容
```
#网卡类型(Ethernet:以太网)  
TYPE=Ethernet  
#代理方式(none:关闭状态)  
PROXY_METHOD=none  
#只是浏览器(no:否)  
BROWSER_ONLY=no  
#引导协议(dhcp:动态获取IP;static:静态IP;none:不指定,不指定容易出现各种各样的网络受限)  
BOOTPROTO=dhcp  
#默认路由(yes:是)  
DEFROUTE=yes  
#是否开启IPV4致命错误检测(no:否)  
IPV4_FAILURE_FATAL=no  
#IPV6是否自动初始化(yes:是,现在还未用到IPV6,不会有任何影响)  
IPV6INIT=yes  
#IPV6是否自动配置(yes:是)  
IPV6_AUTOCONF=yes  
#IPV6是否可以为默认路由(yes:是)  
IPV6_DEFROUTE=yes  
#是否开启IPV6致命错误检测(no:否)  
IPV6_FAILURE_FATAL=no  
#IPV6地址生成模型  
IPV6_ADDR_GEN_MODE=stable-privacy  
#网卡物理设备名称  
NAME=ens33  
#通用唯一识别码,每一个网卡都会有,不能重复  
UUID=a8a20814-3813-4dcf-bec0-df39618b08cf  
#网卡设备名称,必须和**NAME**值一样  
DEVICE=ens33  
#是否开机启动(yes:是)  
ONBOOT=<span style="color:red">yes</span>
```

3. 重启网卡  
```
systemctl restart network
```


# 静态IP地址网络设置

1.  进入ifcfg-ens33配置文件
```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

2. ifcfg-ens33文件内容
```
#网卡类型(Ethernet:以太网)  
TYPE=Ethernet  
#代理方式(none:关闭状态)  
PROXY_METHOD=none  
#只是浏览器(no:否)  
BROWSER_ONLY=no  
#引导协议(dhcp:动态获取IP;static:静态IP;none:不指定,不指定容易出现各种各样的网络受限)  
BOOTPROTO=dhcp  
#默认路由(yes:是)  
DEFROUTE=yes  
#是否开启IPV4致命错误检测(no:否)  
IPV4_FAILURE_FATAL=no  
#IPV6是否自动初始化(yes:是,现在还未用到IPV6,不会有任何影响)  
IPV6INIT=yes  
#IPV6是否自动配置(yes:是)  
IPV6_AUTOCONF=yes  
#IPV6是否可以为默认路由(yes:是)  
IPV6_DEFROUTE=yes  
#是否开启IPV6致命错误检测(no:否)  
IPV6_FAILURE_FATAL=no  
#IPV6地址生成模型  
IPV6_ADDR_GEN_MODE=stable-privacy  
#网卡物理设备名称  
NAME=ens33  
#通用唯一识别码,每一个网卡都会有,不能重复  
UUID=a8a20814-3813-4dcf-bec0-df39618b08cf  
#网卡设备名称,必须和**NAME**值一样  
DEVICE=ens33  
#是否开机启动(yes:是)  
ONBOOT=<span style="color:red">yes</span>  
#本机IP  
<span style="color:red">IPADDR=192.168.137.129</span>  
#子网掩码  
<span style="color:red">NETMASK=255.255.255.0</span>  
#默认网关  
<span style="color:red">GATEWAY=192.168.137.2</span>  
#DNS1  
<span style="color:red">DNS1=8.8.8.8</span>  
#DNS2  
<span style="color:red">DNS2=114.114.114.114</span>
```

3. 重启网卡  
```
systemctl restart network
```
