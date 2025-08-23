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
> 本教程仅作记录，你不需要亲自尝试其中的每一个操作。如果你不知道自己在做什么，那就不要做。  
::: danger
若阅读本文并执行相关操作后出现设备损坏、隐私泄露、数据丢失等情况，则机主需要自行承担损失。
:::

近几年一直在使用MuMu模拟器，但直到近期我才开始研究该如何优化它（  

若存在问题，可在评论区指出~

<!-- more -->







## 准备
- [MuMu模拟器安装包](https://mumu.163.com/)（若已安装，请根据您的实际情况酌情卸载）  
> Tips:  
> 1.MuMu模拟器(国内版)V5前的最后一个版本应该是 `V4.1.33(3741)` ：https://mumu.nie.netease.com/api/v1/release/downloader/NEMUX?channel=V4.1.33.3741  
> 2.国际版-MuMu模拟器(MuMuPlayer)：https://www.mumuplayer.com/

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
> Tips:  
> 1.修改 `system.vdi` 文件会在 `新建虚拟机` 时生效（一般来说，这也会在 `当前虚拟机` 内生效 ）  
> 2.通过 `ROOT` 权限修改将仅在 `当前虚拟机` 内生效  
> 3.需获取ROOT权限时，可考虑使用 `Kitsune Mask`  

#### V5及以上版本
##### 方法一
在 `DiskGenius`(专业版) 内点击 `磁盘`-`打开虚拟磁盘文件`  
Tab栏选择 MuMu模拟器根目录下 `.\nx_device\12.0\vms\MuMuPlayer-12.0-base` 的 `system.vdi` 文件   
编辑 `逻辑分区` 中的 `build.prop` 文件，在文件末尾新增一行：  
```File-build.prop
ro.build.version.overseas=true
```  
> 即设置为海外版(无桌面/搜索栏的广告) 

##### 方法二
在虚拟机的设备设置中启用 `ROOT` & `可写系统盘`  
获取Root权限后，编辑 `/system/build.prop` 文件  
在文件末尾新增一行：  
```File-build.prop
ro.build.version.overseas=true
```   
> 即设置为海外版(无桌面/搜索栏的广告)  


#### V5以下版本
> V5替换桌面APK似乎只能屏蔽搜索框广告（所以V5部分就没写这个）  
##### 方法一
在 `DiskGenius`(专业版) 内点击 `磁盘`-`打开虚拟磁盘文件`  
Tab栏选择 MuMu模拟器根目录下 `.\vms\MuMuPlayer-12.0-base\system.vdi` 的 `system.vdi` 文件   
将 [Mumu Launcher(Nebula版桌面)](https://diffghjkl.lanzouq.com/iHt2T346y95c) 名称更改为 `com.mumu.launcher_new.apk`   
并替换 `逻辑分区`-`priv-app/com.mumu.launcher_new` 文件夹的 `com.mumu.launcher_new.apk` 文件  
 
##### 方法二
> 推荐使用 [MT文件管理器](https://mt2.cn/)  

在虚拟机的设备设置中启用 `ROOT` & `可写系统盘`  
获取Root权限后，进入 `/system/priv-app` 文件夹  
将 [Mumu Launcher(Nebula版桌面)](https://diffghjkl.lanzouq.com/iHt2T346y95c) 名称更改为 `com.mumu.launcher_new.apk`   
并替换 `/system/priv-app/com.mumu.launcher_new` 文件夹中的 `com.mumu.launcher_new.apk` 文件  
> 或者使用 `授权ROOT权限后的MT文件管理器` 直接安装 `替换的apk`  

然后删除原桌面APP的数据，即可实现替换操作  
若操作后不生效（如提示桌面已停止运行），请通过ADB执行下方命令：  
> MuMu模拟器V5以下版本的ADB连接地址为 `127.0.0.1:7555`  
```Shell
adb install -r -d "替换的桌面apk所在路径\com.mumu.launcher_new.apk"
```
> 或者直接在 `授权ROOT权限后的MT文件管理器` 中再次执行 `替换的apk` 安装操作  






## 参考资料
- [MuMu12开屏广告与桌面广告的简单解决办法 - Bilibili](https://www.bilibili.com/opus/830791956620640309)
- [MuMu模拟器12精简优化系统去广告及修改WebView实现 - 潘钜森 - 博客园](https://www.cnblogs.com/geoisam/p/18808872)
- [【汇总】mumu模拟器历史版本 下载器、安装包历史版本官方下载 - 悟透的杂货铺 - 博客园](https://www.cnblogs.com/wutou/p/18165628)






## 后记
~~虽然耗时有点长，但我觉得这就是在水文章（~~  

2025/08/23补：修正了部分存在错误的内容  
> 同时我要收回之前水文章的话...为了保证内容正确，耗费的时间更长了啊啊啊——  