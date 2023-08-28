---
title: Homeassistant相关
date: 2023-08-27 13:52:04
tags:
---

**Ubuntu安装**
```
sudo BYPASS_OS_CHECK=true dpkg -i --ignore-depends=systemd-resolved homeassistant-supervised.deb
```

**米家空调伴侣2**  
```
service: 
    xiaomi_miot.send_command
data:
    entity_id: climate.lumi_mcn02_xxxx
    method: set_tar_temp
    params: [23]
```