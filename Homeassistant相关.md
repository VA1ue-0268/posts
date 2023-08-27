---
title: Homeassistant相关
date: 2023-08-27 13:52:04
tags:
---

**米家空调伴侣2**  
```
service: 
    xiaomi_miot.send_command
data:
    entity_id: climate.lumi_mcn02_xxxx
    method: set_tar_temp
    params: [23]
```