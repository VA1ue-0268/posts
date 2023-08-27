---
title: Hyper-V安装OpenWrt多网卡eth顺序乱问题解决方法
date: 2022-12-24 23:51:49
tags:
---

[参考链接](https://forum.openwrt.org/t/how-does-openwrt-ensure-network-device-names-are-consistent/90185/6) 
使用脚本实现：按mac顺序排eth号   
配置文件放在：/etc/config/mac-static-interfaces  
```
config mac-static-interfaces
	#option eth0 "70:85:c2:8a:57:4d"
```
脚本放在/etc/init.d/：
```
#!/bin/sh /etc/rc.common

START=11

# don't run within buildroot
[ -n "${IPKG_INSTROOT}" ] && return 0

#use busybox grep as GNU grep may be set differently and break the script
grep(){
/bin/busybox 'grep' $@
}

#shutting down all interfaces, then assigning temporary name to free up interface names
#bridges and virtual interfaces are already excluded by  /sys/class/net/*/device/uevent as only physical interfaces have that
for i in $( ls /sys/class/net/*/device/uevent | awk -F'/' '{print $5}' | tr '\n' ' ' ) ;
do

	mac_address=$( grep $i /etc/config/mac-static-interfaces | awk '{print $3}' | tr -d '"' )
	if [ "$mac_address" != '' ]; then
	
		ip link set "$i" down 
		ip link set "$i" name old"$i"
		
	fi
done

for i in $( ls /sys/class/net/*/device/uevent | awk -F'/' '{print $5}' | tr '\n' ' ' ) ;
do

mac_address=$( cat /sys/class/net/$i/address  )
	interface_name=$( grep -i $mac_address /etc/config/mac-static-interfaces | awk '{print $2}' )
	if [ "$interface_name" != '' ]; then
	
		ip link set "$i" down 
		ip link set "$i" name "$interface_name"
		
	fi
done
```
**记得/etc/init.d/xxx enable**