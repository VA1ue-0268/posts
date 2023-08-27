---
title: VSCode配置C++环境的小坑
date: 2022-11-04 11:30:17
tags:
---

使用 **mingw64** 作为 VSCode 编译器的时候，要将 `mingw64\bin\libstdc++-6.dll` 放到工作目录才能显示输出，否则无法显示输出。（不配置launch.json的时候调试却没这个问题）  

引用自定义头文件时需要引用.c/.cpp文件，不然就报未定义（怪）