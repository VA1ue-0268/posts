---
title: RStdio中文路径问题
date: 2022-11-20 21:31:17
tags:
---

```
Warning message:
In normalizePath(path.expand(path),winslash, mustWork):  
  path[1]="C:/Users/xxx/OneDrive/??": 文件名、目录名或卷标语法不正确。
```

### 解决方法：
主要是R_USER这个变量出了问题。  
在windows系统变量中添加一个新的R_USER变量即可解决问题。

### 无效方法：
包括但不限于

1. 进入library->base->R，使用记事本打开Rprofile加入Sys.setenv(R_USER="D:/R/")

2. 使用.libPaths(“C:/Program Files/R/R-3.3.1/library”)

3. Rprofile.site加入S
.libPaths(c("D:/Rlibrary", .libPaths()))
