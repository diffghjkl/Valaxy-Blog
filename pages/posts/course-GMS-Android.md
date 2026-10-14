---
title: Android设备上配置GMS服务（支持部分华为荣耀）
date: 2026-10-14
categories: 技术教程
tags: 
 - GMS
 - Google
 - Google Play
 - Android
excerpt_type: html
---
> 本教程仅作记录，你不需要亲自尝试其中的每一个操作。如果你不知道自己在做什么，那就不要做。

> 本文记录的内容可能仅支持部分机型，且部分内容未经验证，请谨慎参考！若设备支持通过官方渠道配置GMS，则请不要尝试本教程。

::: danger
若阅读本文并执行相关操作后出现设备损坏、隐私泄露、数据丢失等情况，则机主需要自行承担损失。
::: 

> 请注意：`HarmonyOS 4` 以上系统不存在AOSP兼容层，请使用官方提供的渠道！  

因手持设备原因，搭载 `MagicUI` & `HarmonyOS 2.0~4.3` 的手机作为本教程的重点记录部分！（不保证华为/荣耀平板通用）  

对于华为/荣耀平板设备，可尝试参考 [华为手机、平板安装microG使用Play商店和ChatGPT教程 - Alan's Blog](https://www.toalan.com/archives/71/#comment-5705)






## 前言
`GMS` 全称为 `Google Mobile Services`（即 `谷歌移动服务` ），其核心组件如下：  
- Google 服务框架（Google Services Framework）  
- Google Play 服务（Google Play services）  
- Google Play 商店（Google Play Store）  
> 以上组件通常被称为 `GMS三件套`   






## 正文
> 请先确保网络条件正常，设备可以与Google服务器通讯！  
### 原生支持 GMS 的设备
[部分机型列表 - Google Support](https://storage.googleapis.com/play_public/supported_devices.html)  
> 一般来说，这类设备GMS支持的功能相对齐全  

此类设备通常默认关闭GMS服务，需用户手动开启，部分设备需要自行安装 `Google Play 商店`   

以 `小米手机` 为例：  
1. 打开 `设置` ，搜索 `谷歌` ，启用 `谷歌基础服务`  
2. 在 `应用商店` 中安装 `Google Play 商店`  

> 在设备中开启GMS服务后，需要另行安装 `Google Play 商店` 的，可参考下面的 [#方法一](https://blog.dmoe.top/posts/course-GMS#%E6%96%B9%E6%B3%95%E4%B8%80-%E8%87%AA%E8%A1%8C%E5%AE%89%E8%A3%85gms)




### 不提供 GMS 的设备
#### 方法一：自行安装GMS
> Tips：  
> 1.本方法适用于早期设备（大致在2021年前发布的?），部分华为/荣耀机型不支持本方法  
> 2.`手动安装` 不保证GMS可用/支持服务齐全  
> 3.可先尝试使用 `第三方安装器` ，同样不保证GMS可用/支持服务齐全  

您可以自行选择以下任一方法：  

##### (1)自动安装（使用第三方安装器）
> 可能存在部分功能收费的情况  
-  [GO谷歌安装器](https://www.pgyer.com/pOEI)  
-  [SU谷歌安装器](https://www.wandoujia.com/apps/7971105)  
-  [G谷歌服务安装](https://www.wandoujia.com/apps/8436358)  
-  [HIGO谷歌安装器(支持部分华为)](https://www.wandoujia.com/apps/8124836)  
-  [OurPlay(原谷歌空间)](https://www.wandoujia.com/apps/7661165)  
-  [备用下载链接](https://github.com/sky22333/Google-Play-Store/releases)  

##### (2)手动安装
> 下载apk时请根据设备的 `Android版本` & `架构` 来选择  
###### 1.Google 服务框架（Google Services Framework）
- [APKMirror](https://www.apkmirror.com/apk/google-inc/google-services-framework/)  
- [APKPure](https://apkpure.com/cn/google-services-framework/com.google.android.gsf)  

###### 2.Google Play 服务（Google Play services）
- [APKMirror](https://www.apkmirror.com/apk/google-inc/google-play-services/)  
- [APKPure](https://apkpure.com/cn/google-play-services-app/com.google.android.gms)  

###### 3.Google Play 商店（Google Play Store）
- [APKMirror](https://www.apkmirror.com/apk/google-inc/google-play-store/)  
- [APKPure](https://apkpure.com/cn/google-play-store-2025/com.android.vending)  



#### 方法二：MicroG
> 对于 `MicroG` 作者了解的不多，本部分属于未经验证的内容，仅作简单记录，请谨慎参考！

> Tips：  
> 1.`MicroG` 不支持安装 `Google Play 商店` （可以用第三方商店代替）、不支持谷歌支付、不支持查找设备
> 2.需要设备支持 [签名伪造(Signature-Spoofing)](https://github.com/microg/GmsCore/wiki/Signature-Spoofing)  
> 3.检测设备是否支持签名伪造，可使用 [Lanchon/sigspoof-checker - Github](https://github.com/Lanchon/sigspoof-checker/releases)  

> 以下是官方的一些链接：  
> - [MicroG官网](https://microg.org/)（现已指向 https://github.com/microg/GmsCore/wiki/ ）  
> - 官方安装文档：[Installation · microg/GmsCore Wiki - Github](https://github.com/microg/GmsCore/wiki/Installation)  


##### 安装 MicroG
请按需安装以下软件：  
> 详见官方下载页：[Downloads · microg/GmsCore Wiki - Github](https://github.com/microg/GmsCore/wiki/Downloads)  
- [microG Services - Github](https://github.com/microg/GmsCore/releases/) (GmsCore) 必装  
- [microG Companion - Github](https://github.com/microg/GmsCore/releases/) (FakeStore) 必装，若已安装 `Google Play 商店` 可跳过(?)  
- [microG Services Framework Proxy - Github](https://github.com/microg/GsfProxy/releases) (GsfProxy) 可选，主要用于兼容旧版的C2DM推送接口  

> 在 `Android 7及更高版本` 中，如需定位请安装补丁或将 `microG Services` 安装为 `系统应用` （需要ROOT权限）；详见 [Installation · microg/GmsCore Wiki - Github](https://github.com/microg/GmsCore/wiki/Installation)  

然后根据软件内指引配置，并确保 `自我检查` 页的选项全部勾选

对于应用商店，可使用 [Aurora Store](https://f-droid.org/packages/com.aurora.store/) 来代替 `Google Play 商店`  



#### 方法三：虚拟机/沙盒
> 本方法受限于需安装 `第三方软件` ，支持的GMS服务可能较为齐全  

以下是几种常见的软件：  
- [VMOS](https://www.vmos.cn/)  
- [光速虚拟机](https://gsxnj.cn/)  
- [GBox](https://gboxlab.com)  
- [Gspace](https://gspaceteam.com/)  

各软件的使用方法请自行搜索！  



#### 方法四：谷歌服务助手（仅支持华为/荣耀部分机型）
> Tips：  
> 1.本部分为华为/荣耀的部分机型专属，理论上支持 `MagicUI` & `HarmonyOS2.0~4.3` 系统（不保证华为/荣耀平板通用）  
> 2.具体是否支持请根据以下内容，请执行到 [#安装谷歌服务助手](https://blog.dmoe.top/posts/course-GMS#_1-%E5%AE%89%E8%A3%85%E8%B0%B7%E6%AD%8C%E6%9C%8D%E5%8A%A1%E5%8A%A9%E6%89%8B) 部分来验证  

本方法所需文件下载：  
- [123云盘](https://1812317555.share.123pan.cn/123pan/BOa8Vv-tep39?pwd=Z1gc)（提取码：Z1gc）  


##### 0.安装前的准备
###### 1）关闭部分系统功能
悬浮导航：`设置` - `系统和更新` - `系统导航方式` - `更多` - `悬浮导航`  
增强防护：`设置` - `系统和更新` - `纯净模式`  
隐私空间：`设置` - `隐私` - `隐私空间` - `右上角`  
应用分身：`设置` - `应用和服务` - `应用分身`  
省电模式：`设置` - `电池` - `省电模式`  
> 安装GMS后以上功能均可重新使用  

###### 2）卸载Google相关应用
> 部分情况下系统中可能存在以下应用  
- Google Play商店  
- Google通讯录同步  
- Google Play服务  
- Google服务框架  
- Google账户管理程序  
- com.google.android.gms.policy_sidecar_aps  
- SharedLibrary  
- 谷歌服务助手  
- microg（只要包含这个名字的，都卸载）  


##### 1.安装谷歌服务助手
将压缩包中的 `Backup` 文件夹解压到手机根目录下的 `Huawei` 文件夹中  
通过 `设置` - `系统和更新` - `日期和时间` 修改时间为 `2019年` （需关闭 `自动设置` ）  
在 `设置` - `系统和更新` - `备份与恢复` 右上角选择 `从内部存储恢复` ，选择刚才导入的备份，密码为 `a12345678`  
> 若不存在 `从内部存储恢复` ，则需点击 `外部存储` ，应用会弹出申请权限的提示，一并允许后退出 `备份与恢复` ，然后重新打开它即可  

将系统时间的 `自动设置` 开启，打开 `谷歌服务助手` 并点击 `激活` 即可（申请的权限要全部允许；激活后不要点击开始下载，直接返回桌面即可）  
> Tips：  
> 1.若提示 `当前设备不支持` ，则说明本方法不适用该设备  
> 2.若提示 `网络连接异常` ，将 `备份与恢复` 更换成旧版本即可  


##### 2.安装GMS
将压缩包中的 `GMSAPKS` 文件夹中的文件解压出来，然后依照文件名标注的序号安装（ `7-Google Play 商店` 先不装）  
> Tips：
> 1.其中 `1-google账户管理` `5-谷歌服务框架` `6-Google Play 服务` 为必装应用，其他应用请视自身情况安装  
> 2.部分文件前标注的 `V10` / `V12` 指代 `Android 10` / `Android 12`  

##### 3.登录Google账号
通过 `设置` - `Google` 即可登录  


##### 4.禁用GSF
> 在执行本步骤前请确保符合以下情况：  
> 1.设备的 `开发者调试` - `USB调试` 已开启  
> 2.电脑端已配置好ADB环境  
> 3.设备与电脑连接时的模式为 `传输文件`  

在命令提示符（CMD）中输入以下命令，但不要回车执行  
```
adb shell pm disable-user --user 0 com.google.android.gsf
```

在设备上安装 `7-Google Play 商店` 并启动，会提示 `我们正在为您更新Google Play` ，当出现可以前往google商店的选项时，直接前往商店，跳过更新  
若 `Google Play商店` 可正常打开加载数据，则停止它的后台运行  
> 注意：在教程没有结束之前，不要通过play下载任何应用  

> 以下操作为禁用GSF并留住FCM功能

通过 https://play.google.com/store/apps/details?id=com.google.android.gms 进入 `Google Play商店` 的应用详情页  
> Tips：  
> 若不知该如何操作，可将链接放到系统自带的 `备忘录` 中并保存，当链接变为蓝色时，点击它即可  
> （若点击跳转到华为浏览器，打开 `设置` 搜索 `打开链接` - `Google Play 商店` - `未通过验证链接` - `添加` - `全选`）

点击更新（没有更新则直接禁用GSF），要注意下载的进度条，当进度条超过50%以后，立刻执行禁用命令  
命令提示符中提示执行成功后，等待 `Google Play 服务` 更新  
更新完成后，关掉 `Google Play商店` 后台，重新打开，随便下载一个应用进行测试  


##### 5.GMS的权限设置（非必须）
> 为确保谷歌服务正常运行，建议进行以下设置

在 `设置` - `应用和服务` - `应用管理` 中，将 `Google Play 服务` 权限，开启 `位置` 、 `媒体和文件` 权限（必开，其余权限请视自身情况而定）  
在 `设置` - `应用和服务` - `应用启动管理` 中，将 `Google Play 服务`、 `Google Play 商店` 设置为 `手动管理`，并将`允许自启动` `允许关联启动` `允许后台活动` 全部勾选  


##### 6.FCM的使用
###### 1）检查FCM是否开启
> 请确保设备的网络可访问Google

打开 `电话`，输入 `*#*#426#*#*` 跳转到FCM日志  
若提示 `Connected` 则表示已连接  
```
Server:Connected
Host:mtalk.google.com/28.0.0.5
Port:5228
Time Connected:00:01
```
> Tips：  
> 1.若 `Host` 和 `Port` 有数据，而 `Server` 提示 `No Connected` ，则需点击 `EVENTS` 和 `STATUS` ，如果不行请重启设备  
> 2.FCM在国内是可以直连的，若在开启代理时无法连接，可尝试关闭代理后测试  

###### 2）FCM推送通知的设置
在 `设置` - `应用和服务` - `应用启动管理` 中，找到需要FCM推送的软件，将其设置为 `手动管理`，并将`允许自启动` `允许关联启动` `允许后台活动` 全部勾选  






## 常见问题
### 无法加载登录界面  
设备连接的网络存在问题  

### 创建账号时+86手机号验证失败  
1.更换手机号  
2.IP不够干净  

### 登录提示需要另一台手机弹窗验证（没有弹窗，其他方法也无法验证）  
在其他登录过该账号的设备上，选择一个Google系应用，点击 `头像` - `管理您的谷歌账号` - `安全性` - `两步验证` - `开启两步验证` （这个页面国内手机号也可以验证）  
开启两步验证以后，进入 `备用验证码` 并生成保存  
然后重新登录，到达验证阶段时，点击 `更多方式验证` - `备用验证码`，输入刚才生成的备用验证码即可  

### 对于使用方法四的华为/荣耀设备
#### 如何升级Play服务
`Google Play商店` 默认会自动更新，无需手动更新  
`Google Play 服务` 可在 `应用管理` 中找到该应用，在应用详情页点击跳转商店页面，即可更新  

#### 安装GMS后，应用分身、悬浮框、隐私空间能否使用
可以  
> 注意：  
> 开启 `应用分身` 后，会一直弹窗“play未获得保护机制认证”，若在弹窗右下角找到2的标志，则说明是分身空间的 `Google Play 服务` 在提示，不影响使用  

若想永久关闭该提示，有以下几种方法：  
1）清理所有后台应用并断网，然后再启用 `应用分身`  
2）查看分身用户ID  
```
adb shell pm list users
```
再输入以下命令：  
（命令中的xxx需要换为你分身用户的 ID，该ID是随机的）  
```
adb shell pm disable-user --user xxx com.google.android.gsf
adb shell pm disable-user --user xxx com.google.android.gms
adb shell pm disable-user --user xxx com.android.vending
```
> `隐私空间` 同理，这两个功能本质都是多用户  

#### 安装GMS后，操作期间产生的文件如何处理
1.压缩包及其内容，可删  
2.谷歌服务助手，可删，但建议保留  
3.谷歌相关软件，不要清理缓存  


#### 关于ChatGPT
> 1.在Google Play 商店下载：https://play.google.com/store/apps/details?id=com.openai.chatgpt  
> 2.香港地区无法使用ChatGPT  
 
若打开应用后提示以下内容：
```
Something went wrong
Check that Google Play is enabled on your device and that you're using
an up-to-date version before opening the app.if the problem 
persists try reinstalling the app.
```
这时需先打开play商店再打开ChatGPT；
或者通过`设置` - `应用和服务` - `应用启动管理` - `Google Play 商店` ，将其设置为 `手动管理`，并将`允许自启动` `允许关联启动` `允许后台活动` 全部勾选  


#### 部分应用无法正常使用
> 部分软件需要更底层的谷歌服务，只能设备Root刷更底层服务

##### 因服务受限应用（目前无法解决）
- Google Pay（谷歌钱包）
- Android Auto（安卓汽车APP，有方法用，我不作解释）
- Gcam（谷歌相机）
- ......


##### 因谷歌位置服务受限应用
> 建议使用Gbox等软件
- Getir
- Tokyo 迪士尼APP
- 谷歌Earth（可解决，位置权限选择 允许本次使用）
- Tinder
- strava
- 日本环球影城（usj）
- tripadvisor
- ......






## 参考资料
- [sky22333/Google-Play-Store - Github](https://github.com/sky22333/Google-Play-Store/)  
- [2026华为鸿蒙 2.0-4.3 最新安装谷歌原生框架（不弹认证） - Alan's Blog](https://www.toalan.com/archives/184/)  
- [2026 年国产安卓手机如何开启 Google Play？其实大多数手机早就自带 GMS - 知乎](https://zhuanlan.zhihu.com/p/2014094556497463101)






## 后记
本文从内容五个月前开始整理，中间断断续续的，直至今日才写出一篇勉强算是文章的博文Orz

尽管内容上算不上合格，总感觉漏洞百出，但作为记录也算可行(?)