---
title: 利用Scrcpy实现Android投屏至PC
date: 2026-02-08
categories: 技术教程
tags: 
 - Scrcpy
 - ADB
 - Windows
 - Android
excerpt_type: html
---


## 准备
- 一台 `Android 5.0` 及以上的设备  
- 一台 `Windows` / `Linux` / `MacOS` 设备  
- [ADB下载 - Google开发者文档](https://developer.android.google.cn/tools/releases/platform-tools?hl=zh-cn)  
- [Genymobile/scrcpy - Github](https://github.com/Genymobile/scrcpy/releases)  

### Scrcpy的GUI版本（第三方开发）
> 以下是一些第三方开发的GUI版本（均支持 `Linux` ，`Windows` 和 `MacOS` ），您可以自行选择使用  


| 下载链接 | 帮助文档 |  
| --- | --- |  
| [viarotel-org/escrcpy - Github](https://github.com/viarotel-org/escrcpy/releases) | [escrcpy中文文档](https://viarotel.eu.org/zhHans/) |  
| [SimonAKing/scrcpy-gui - Github](https://github.com/SimonAKing/scrcpy-gui/releases) | [scrcpy-gui中文文档](https://github.com/SimonAKing/scrcpy-gui/blob/master/README.zh_CN.md) |  
| [barry-ran/QtScrcpy - Github](https://github.com/barry-ran/QtScrcpy?tab=readme-ov-file/releases) | [QtScrcpy中文文档](https://github.com/barry-ran/QtScrcpy/blob/dev/README_zh.md) |






## 正文
> 本文在Windows下进行  
### 配置ADB
> 一般情况下，GUI版的会集成ADB，可以忽略此步骤  

将下载好的ADB压缩包解压（通常解压到C盘）  

打开 `高级系统设置` ，找到 `高级` 选项卡，点击 `环境变量`  
> Tips：Win10/Win11可通过 `设置` - `系统` - `系统信息` 找到 `高级系统设置`  

在 `系统变量` / `用户变量` 中找到 `PATH` ，填写ADB所在路径  

最后在任意路径下打开CMD，输入 `adb` 命令检查是否配置成功  



### 运行Scrcpy
> 请确保手机的 `USB调试` & `USB调试授权` 设置完成  

启动 `Scrcpy` 有两种方法：  
- 直接运行 `scrcpy.exe`  
- 通过cmd启动  

更多拓展功能可前往 [官方Github仓库](https://github.com/Genymobile/scrcpy) / [Scrcpy文档](https://scrcpyapp.org/) 查看  






## 常见问题
### 提示 Could not execute "adb start-server"
完整报错为：  
```
ERROR: CreateProcessW() error 5
ERROR: Failed to execute: [C:\platform-tools\], [start-server]
ERROR: Could not execute "adb start-server"
ERROR: Could not start adb server
ERROR: Server connection failed
```
出现该问题是因为环境变量没有正确配置  

> Tips：  
> 1.请务必确保是在 `PATH` 下直接填写ADB的路径，而不是在 `系统变量` / `用户变量` 下添加 `变量名` + `变量值`  
> 2.如果您不想使用上方的方法，请在 `变量值` 填写的路径后面添加 `\adb.exe` ，但这种配置方法可能会导致部分软件无法调用ADB  






## 后记
写这篇文章是因为上方的报错居然困扰了我半个多小时（  

最后发觉是曾经配置的环境变量的问题QWQ  