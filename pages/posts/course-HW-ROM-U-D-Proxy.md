---
title: 华为/荣耀系统升降级（使用HiSuite Proxy）
date: 2026-02-21
categories: 技术教程
tags: 
 - HarmonyOS
 - EMUI
 - MagicUI
excerpt_type: html
---
> 本教程仅作记录，你不需要亲自尝试其中的每一个操作。如果你不知道自己在做什么，那就不要做。

> 本文记录的系统升降级可能仅支持部分机型；若设备支持通过官方渠道执行系统升降级，则请不要尝试本教程。

::: danger
若阅读本文并执行相关操作后出现设备损坏、隐私泄露、数据丢失等情况，则机主需要自行承担损失。
::: 






## 前言
> 因近期暂无时间进行升降级操作，故本文内容未经实践确认，可能存在错误，还请根据实际情况操作！  

本文记录的案例为从 `HarmonyOS` 降级到 `EMUI` / `MagicUI`  

> 在 `EMUI` / `MagicUI` 的设备上升降级（如升级到HarmonyOS）应该也是可以的






## 准备
- `HiSuite Proxy`（代理工具）  
  - [Github](https://github.com/ProfessorJTJ/HISuite-Proxy/releases)  
  - [蓝奏云](https://diffghjkl.lanzouq.com/b0kot5c9a)（密码:eh1y）  
  - [123云盘](https://www.123865.com/s/BOa8Vv-w3B7A)

- `HiSuite_11.0.0.610_OVE`（华为手机助手海外版，不支持 `WLAN连接` ）
  > 部分机型可能不兼容此版本，请根据实际情况下载使用
  - [Github](https://github.com/ProfessorJTJ/HISuite-Proxy/releases/download/3.0/HiSuite_11.0.0.610_OVE.exe)  
  - [蓝奏云](https://diffghjkl.lanzouq.com/b0kot5cbc)（密码:6wcm）  
  - [123云盘](https://www.123865.com/s/BOa8Vv-g3B7A)







## 正文
### 配置 HiSuite Proxy
> 请先确保 `HiSuite` 已安装  
#### 安装
运行 `HiSuite Proxy.exe` ，点击 `SETUP`  
![HiSuite Proxy](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/rrYr_UBYqKcI0_)  

等待弹出的窗口中输出 `Checks Finished, You can proceed to installation now!`  
> 可能会存在报错，请自行检查  
```
 [12:53:11]: Join The Telegram Group for Volunteered Support
 [12:53:11]: https://t.me/firmfinder
 [12:53:12]: 
 [12:53:12]: Checking if HISuite is Installed...
 [12:53:13]: HiSuite Exists, Proceeding...
 [12:53:13]: Closing HISuite....
 [12:53:15]: Checking HISuite Version...
 [12:53:16]: HiSuite Version 11 Is Installed, Proceeding....
 [12:53:17]: Patching HISuite Files....
 [12:53:17]: Patch succeeded, Proceeding....
 [12:53:18]: Checking HISuite Proxy Settings...
 [12:53:18]: Proxy Settings Are Already Set, Proceeding...
 [12:53:19]: Checking Hosts File For Redundant Entries....
 [12:53:19]: Hosts File Is Already Neat, Proceeding...
 [12:53:20]: Checking Connection To HISuite Proxy....
 [12:53:21]: HISuite Proxy Is On And Working.
 [12:53:21]: 
 [12:53:22]: Checks Finished, You can proceed to installation now!
```
![HiSuite Proxy的SetUP窗口](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/JOvR_zG87OPhgU?quality=320&allowAnimation=false)  



#### 获取设备信息
运行 `HiSuite` ，根据软件指引连接设备

设备连接成功后， `HiSuite Proxy` 会在右侧弹出窗口，将会显示设备的 `Phone Model（手机型号）` 、 `Phone Region（手机地区）` 等信息  
![HiSuite Proxy](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/Q8GKpKbVScwvfl)

在手机端的拨号界面输入 `*#*#2846579#*#*` 打开 `ProjectMenu（工程菜单）`   

在 `2.Veneer Informations（单板信息查询）` - `1.Version Info（版本信息）` 下找到：  
- `Base Software Version（基础包版本号）`  
- `Cust Software Version（定制包版本号）`  
- `Preload Software Version（预装包版本号）`  
![版本信息](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/pJfoav01pmlO_J)  
![Version Info](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/RQegFIGutrGyax)  

> 部分系统（如 `HarmonyOS` ）可能需要 `关于手机` - `版本号` 中括号内的信息（如 `C00E205` ），以此来判断应刷入哪个系统包  



#### 添加 ROM
访问 [Firm Finder](https://professorjtj.github.io/) 或 [Firm Finder v2.0](https://professorjtj.github.io/) 网站：
- `Phone Model` 处填入 `手机型号`  
- `Vendor/Country (hw-eu)` 处填入 `手机地区`  
  > 例：中国大陆地区（全网通）需填入 `all-cn`  
- `Target Version` 处填入需要的 `系统版本号`  
![Firm Finder](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/OmTUXVYza7YXyx)

找到需要的ROM后，点击 `View Rom` - `Add Rom` ，此时浏览器左下角应提示 `ROM successfully added.`  
![Firm Finder](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/UzEYdvT-D_L3og)



### 刷入 ROM
运行 `HiSuite` ，根据软件提示连接设备，点击 `Update（系统更新）` ，检查弹出的窗口中显示的系统是否正确
![HiSuite_OVE](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/wi4OE7iQgE1Bes)









## 参考资料
- [Complete Guide V2.0 · ProfessorJTJ/HISuite-Proxy Wiki - Github](https://github.com/ProfessorJTJ/HISuite-Proxy/wiki/Complete-Guide-V2.0)  
- [华为降级工具适用于所有系统 - 吾爱破解 - 52pojie.cn](https://www.52pojie.cn/thread-1421908-1-1.html)  
- [荣耀20Pro手机系统降级教程（拍照负优化解决方案）其它华为/荣耀手机降级方法 - 知乎](https://zhuanlan.zhihu.com/p/336116925)  
- [HiSuite Proxy V3使用教程 - 知乎](https://zhuanlan.zhihu.com/p/587582306)  
- [华为手机使用HiSuite升级和降级刷机方法_hisuite proxy - CSDN博客](https://blog.csdn.net/qq_44709006/article/details/122948566)  






## 后记
暂时先记录这些吧，欢迎各位在评论区指出本文存在的问题~  
