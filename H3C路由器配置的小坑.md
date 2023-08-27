---
title: H3C路由器配置的小坑
date: 2022-11-09 08:09:43
tags:
---
MSR5620的端口从``g2/0/0``开始！！

一些常用指令：  
```
sysname NAME                #改名
clock datatime HH:MM:SS     #改时间
display interface brief     #查看端口
display mac-address         #查看mac转发表
int XXX                     #进入视图
ip address IP MASK          #设置ip
vlan XXX                    #创建vlanXXX
port gXXX to gXXX           #分配端口
ip route-static TARGET MASK PORT-IP #配置静态路由


#############
telnet
#############
telnet server enable                        #开启服务
set authentication password simple XXXXXX   #设置密码
user-role XXX                               #设置用户等级
(
    network-admin
    network-operator
    level-n(1~15)
)
```

小记一下防止实验课配置的时候卡壳