---
title: ubuntu 下 nginx pcre库的安装
date: 2022-11-06 10:27:15
tags:
---

（其实得看编译时的环境）  

安装  
`apt-get install libpcre3 libpcre3-dev`

搜索  
`find / -name "libpcre.so.*"`

链接  
`ln -s 找到的位置 /lib/libpcre.so.1`
