---
title: 使用dex2oat编译优化app
date: 2023-08-29 11:18:25
tags:
---

**使用到的命令：**
```
cmd package compile -m <编译选项> <其余参数> <应用包名>
```
### **1、编译选项：**

**interpret-only**：不编译，仅靠解释运行应用，效率很低，占用空间最小；

**space**：仅编译一小部分函数，其余不编译，占用空间较小；

**balanced**：在占用空间与运行效率上做一平衡；

**speed-profile**：将配置文件中标明的函数编译一遍，这些函数可能是热点函数，为部分编译，频繁使用的功能运行效率会变高，不常使用的效率便会很低；

**speed**：将程序中所有函数都编译一遍，效率和占用空间均较高；

**everything**：译所有代码，效率最高，能耗较低，占用空间最高。

手机存储空间比较大建议speed或者everything模式，手机内存小就space模式。

### **2、其他参数：**

-f :强制编译，无论应用是否曾被编译，均会被重新编译。

-a :编译全部。

比如：

使用everything模式重新编译全部app。编译时间长。
```
cmd package compile -m everything -f -a
```
使用speed模式编译telegram
```
cmd package compile -m speed -f com.telegram.messenger
```
### **3、获取app包名**
可以使用app，或者查看：/data/system/packages.list。

有root或者使用adb，也可以无需root权限，无需adb，但是终端不能用termux。可以使用script manager，或者terminal。

如果编译app后出现了什么问题，清理缓存，或者卸载重装，即可恢复。如果是系统应用，使用speed模式编译模式出问题，就可以使用interpret-only模式编译回去。

更新app之后，需要重新编译app。