---
title: 论如何优化MuMu模拟器的使用体验
date: 2025-08-22
categories: 技术教程
tags: 
 - MuMu模拟器
 - 安卓模拟器
 - 软件优化
excerpt_type: html
---
近几年一直在使用MuMu模拟器，但到近期我才开始研究该如何优化它（  

若存在问题，可在评论区指出~

<!-- more -->






## 准备
- [MuMu模拟器安装包](https://mumu.163.com/)（若已安装，请根据您的实际情况酌情卸载）  
> Tips:  
> 1.MuMu模拟器V5前的最后一个版本为 `V4.1.31.3724` ：https://mumu.nie.netease.com/api/v1/release/downloader/NEMUX?channel=V4.1.31.3724  
> 2.MuMu模拟器国际版：https://www.mumuplayer.com/

- [DiskGenius专业版](https://diffghjkl.lanzouq.com/ih6NA346yf8b)（可选）   
> 推荐使用V6版本，V5版本似乎打不开 `system.vdi` 文件  

- [Mumu Launcher(Nebula版桌面)](https://diffghjkl.lanzouq.com/iHt2T346y95c) （可选）






## 开始
> 本篇内容以MuMu模拟器V5.0及以上版本为例，V5以下版本请查看 `Tips` 的补充部分  

### 屏蔽开屏广告&消息中心
在 `Windows资源管理器` 的地址栏中输入 `%APPDATA%\Netease\MuMuPlayer\data` 并回车  
> Tips:  
> 1.完整路径为 `C:\Users\用户名\AppData\Roaming\Netease\MuMuPlayer\data`  
> 2.v5以下版本请将上方路径中的 `MuMuPlayer` 修改为 `MuMuPlayer-12.0` 

删除 `startupImage`(开屏广告) 文件夹，并使用同名的空文件替换  
> 其他方法：  
> 1.删除 `startupImage` 文件夹后新建同名文件夹并将文件夹权限改为只读  
> 2.替换 `startupImage` 文件夹里的 `imageManager.json`  
> 3.将 `imageManager.json` 文件权限设置为只读  
> 4.修改host文件内的 `mumu.nie.netease.com` 的IP  

删除 `msgCenter`(消息中心) 文件夹，并使用同名的空文件替换/新建同名文件夹并将文件夹权限改为只读



### 屏蔽模拟器内的桌面广告
在 `DiskGenius`(专业版) 内点击 `磁盘`-`打开虚拟磁盘文件`  

Tab栏选择 MuMu模拟器根目录下 `.\nx_device\12.0\vms\MuMuPlayer-12.0-base` 的 `system.vdi` 文件   
> V5以下版本请选择 `.\vms\MuMuPlayer-12.0-base\system.vdi` 


> 注意：方法一、二可在 `新建虚拟机` 时生效，方法三仅在 `当前虚拟机` 内生效  
#### 方法一
编辑 `逻辑分区` 中的 `build.prop` 文件，在文件末尾新增一行：  
```Code
ro.build.version.overseas=true
```  
> 即设置为海外版(无桌面/搜索栏的广告)  


#### 方法二（仅适用于V5以下版本）
> V5使用该方法似乎只能屏蔽搜索框广告~~（所以这部分就没写V5的教程） ~~

将 [Mumu Launcher(Nebula版桌面)](https://diffghjkl.lanzouq.com/iHt2T346y95c) 名称更改为 `com.mumu.launcher_new.apk`   
并替换 `逻辑分区`-`priv-app/com.mumu.launcher_new` 文件夹的 `com.mumu.launcher_new.apk` 文件  


#### 方法三
在虚拟机的设备设置中启用 `ROOT` & `可写系统盘`  

> 下方选项任选其一即可  
##### (选择1)替换桌面apk（仅适用于V5以下版本）
获取Root权限后，进入 `/system/priv-app` 文件夹  
将 [Mumu Launcher(Nebula版桌面)](https://diffghjkl.lanzouq.com/iHt2T346y95c) 名称更改为 `com.mumu.launcher_new.apk`   
并替换 `/system/priv-app/com.mumu.launcher_new` 文件夹中的 `com.mumu.launcher_new.apk` 文件   

##### (选择2)修改系统构建属性(build.prop)
获取Root权限后，编辑 `/system/build.prop` 文件  
在文件末尾新增一行：  
```Code
ro.build.version.overseas=true
```   
> 即设置为海外版(无桌面/搜索栏的广告)  






## 参考资料
- [MuMu12开屏广告与桌面广告的简单解决办法 - Bilibili](https://www.bilibili.com/opus/830791956620640309)
- [MuMu模拟器12精简优化系统去广告及修改WebView实现 - 潘钜森 - 博客园](https://www.cnblogs.com/geoisam/p/18808872)






## 后记
虽然耗时有点长，但我觉得这就是在水文章（