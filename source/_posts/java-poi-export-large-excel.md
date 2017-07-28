title: Java使用POI导出excel大文件
date: 2017-7-28
tags:
- POI
- excel导出
-----

## 介绍

Apache POI 是一个Java API 用于读写微软Excel文件。这个库提供了如下接口，使用于不同的情况：
- HSSF ， 用于读写XLS文件
- XSSF ，用于读写XLSX文件
- SXSSF ，用于读写数据量大的XLSX文件

本文介绍第3种情况：使用SXSSF导出数据大的XLSX文件。

## SXSSF, Streaming Usermodel API (SXSSF 接口)

`package: org.apache.poi.xssf.streaming`

SXSSF接口区别于XSSF，在于：
- 使用了滑动窗口机制，有限的访问文件中的行。访问过的行就不能再访问，因为它们被写入到磁盘中了。
- XSSF 则可以访问excel文件中的行
- SXSSF会生成临时文件，且必须明显调用dispose方法来清除




