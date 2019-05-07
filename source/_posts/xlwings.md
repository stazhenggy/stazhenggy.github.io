---
title: xlwings
date: 2019-03-22 19:21:00
tags: excel 
categories: python
---
python加持excel, 速度起飞。

<!--more-->

# 背景

开始之前, 回忆一下使用`Excel`的场景。

+ 同时打开多个`Excel`文件，多个workbook，每个 workbook 又可以用多个 sheet；且需要在多个 sheet workbook Excel 窗口之间切换
+ 对一个或多个单元格进行增删改查，设置格式，合并分拆等操作

以上场景，需要不停地来回切换，且不同的对象可能需要重复的却又不同的操作，手动工作量大。 `xlwings` 用于解决以上各种切换和操作，提高效率。

# 使用说明

基于`BSD-licensed`的Python第三方模块，可以很方便的和Excel交互，它有以下优点：

+ 语法接近 `VBA`

+ 可以用`Python`代码取代`VBA`编写宏

+ `windows`中可以用`Python`写`Excel`用户自定义函数

+ 全功能支持`Numpy`,`Pandas`,`matplotlib`等库

# 示例
## 如何执行xlwings编写的自定义函数

+ 将xxxx.xlsx文件另存为 hong.xlsm 文件
+ 确保hong.py  与 hong.xlsm是在同一个文件夹下
+ 确保hong.xlsm文件的VBA是引用xlwings的，如下图
+ 导入自定义函数，点击“xlwings”栏目的“Import Functions”按钮，如下图
+ 可以像调用系统自带函数一样，使用自定义开发的函数，如下图：

