---
title: 网心云OEC/OECT刷入Armbian
date: 2025-09-11
categories: 技术教程
tags: 
 - 网心云
 - 网心云OEC
 - 网心云OECT
 - NAS
 - Armbian
excerpt_type: html
---
> 本教程仅作记录，你不需要亲自尝试其中的每一个操作。如果你不知道自己在做什么，那就不要做。  

::: danger
若阅读本文并执行相关操作后出现设备损坏、隐私泄露、数据丢失等情况，则机主需要自行承担损失。
:::

::: warning
OEC(T)短接的失败率还是很高的，请确保你有足够的时间与耐心（运气好的话一两次就能成功）  
:::

心血来潮的买了个OECT，但是刷机耗费的时间有亿点长...  

所以需要记录一下  

OEC(T)的硬件配置：  
| 产品 | OEC | OEC-turbo |
| --- | --- | --- |
| CPU | RK3566/RK3568 | RK3566/RK3568 |
| 内存 | 2GB | 4GB |
| 系统存储 | 8GB | 8GB |
| 网络接口 | 千兆以太网接口*1 | 千兆以太网接口*1 |
| 硬盘接口 | SATA3.0接口*1；支持内置2.5寸 硬盘 | SATA3.0接口*1；支持内置2.5寸 硬盘 |
| USB | USB3.0*1 | USB3.0*1 |
| 电源 | 12V/2A 电源 | 12V/2A 电源 |
| 产品尺寸 | 145mm x 90mm x 47mm | 145mm x 90mm x 47mm |

> OEC(T)的 `2.5寸硬盘槽` 的空间有点小，装不下 `2.5寸的机械硬盘`（）






## 准备
> 本文在 Windows 下进行， MacOS 请另寻其他教程  

- `USB-A to Type-C 数据线`（ `Type-C to Type-C 数据线` 不是很推荐，但也不是不行）  

- 驱动+刷机工具（RkDevTool_v2.84__DriverAssitant_v5.12.tar.xz）： [Github](https://github.com/ophub/kernel/releases/download/tools/RkDevTool_v2.84__DriverAssitant_v5.12.tar.xz) / [123云盘](https://www.123865.com/s/BOa8Vv-vDf7A)  
> Tips：  
> 1.`DriverAssitant` 是要安装的驱动， `RkDevTool` 是刷机工具  
> 2.上方链接存在时效性，如有需要，请前往 [Releases · ophub/kernel - Github](https://github.com/ophub/kernel/releases/) 下载最新版  
> 3.如果上方的版本不易刷入，可尝试 [DriverAssitant_v5.13 - 蓝奏云](https://diffghjkl.lanzouq.com/iIYhZ361bixi) + [RKDevTool_Release_v3.31 - 蓝奏云](https://diffghjkl.lanzouq.com/ijyV4361biyj) （经测试， `OEC-1.1` 版本可用）  

- Loader文件： 
  - 适用于 `OEC-1.1` 版本（MiniLoaderAll_oect.bin） ：[蓝奏云](https://diffghjkl.lanzouq.com/iafEY361bjwd)  
  - 适用于 `OEC L2.0` 版本（MiniLoaderAll.bin）：[Github](https://github.com/ophub/u-boot/blob/main/u-boot/rockchip/wxy-oect/MiniLoaderAll.bin) / [蓝奏云](https://diffghjkl.lanzouq.com/iD8lO361c6od)  
  - 适用于 `OEC L2.1` 版本（rk356x-MiniLoaderAll.bin）：[Github](https://github.com/ophub/u-boot/blob/main/u-boot/rockchip/wxy-oect/rk356x-MiniLoaderAll.bin) / [蓝奏云](https://diffghjkl.lanzouq.com/i31ny361c7hc)  
> Tips：  
> 1.版本需在拆机后才能看到（印在电路板上）  
> 2.不同版本的Loader之间可能不通用，请根据实际情况选择  
> 3.已知的版本有 `OEC L1.0` `OEC-1.1` `OEC L2.0` `OEC L2.1`  
> 4.上方未标注的版本，请自行寻找相应的 `Loader` 文件  

- Armbian镜像：[Release · sophub/amlogic-s9xxx-armbian - Github](https://github.com/ophub/amlogic-s9xxx-armbian/releases)  
> 若该镜像无法刷入，可尝试 [Flash_Armbian_25.05.0_rockchip_efused-wxy-oec_bookworm_6.1.99_server_2025.03.20 - 123云盘](https://www.123865.com/s/BOa8Vv-TDf7A) （经测试， `OEC 1.1` 可用）  



### Armbian命名规则
> 一般来说，以下规则仅适用于 [ophub/amlogic-s9xxx-armbian - Github](https://github.com/ophub/amlogic-s9xxx-armbian/) 仓库  

发行版（Releases）标题：  
`Armbian_<系统名称>_save_<更新日期>`  

| 系统名称 | 对应系统 |  
|---|---|
| jammy | Ubuntu 22.04.5 LTS |
| noble | Ubuntu 24.04 LTS |
| bullseye | Debian 11 |
|bookworm |	Debian 12 |
| HassIoSupervisor_bookworm |	有Home Assistant Supervised 的 Debian 12 |
| trixie | Debian 13 |


资源（Assets）名称：  
`Armbian_<版本号>_<芯片品牌>_<镜像名>_<系统名称>_<Linux内核版本>_server_<更新日期>.img.gz`  

> 对于 `网心云OECT` 来说，`wxy-oect` 适用于原版硬件；`wxy-oect-replaced`	适用于更换芯片&EMMC的  

| 芯片品牌 | 相关名称 |
| --- | --- |
| allwinner | [全志科技](https://baike.baidu.com/item/%E7%8F%A0%E6%B5%B7%E5%85%A8%E5%BF%97%E7%A7%91%E6%8A%80%E8%82%A1%E4%BB%BD%E6%9C%89%E9%99%90%E5%85%AC%E5%8F%B8/19983272) |
| amlogic | [晶晨半导体](https://baike.baidu.com/item/Amlogic/3082384) |
| rockchip | [瑞芯微电子](https://baike.baidu.com/item/%E7%91%9E%E8%8A%AF%E5%BE%AE/2133941) |






## 开始
### 拆机
> 可参考 [不到100块拥有全能NAS，保姆级低功耗家庭服务器搭建指南 - BiliBili](https://www.bilibili.com/video/BV1UAuuzyEZe/) 或 [网心云 OEC/OECT 刷armbian - Codfish Blog](https://codfish.top/posts/wxy-oect/)  

这里就不过多赘述了 ~~（绝对不是想偷懒）~~  



### 首次刷机
> 此时OEC(T)设备系统为 `原厂系统` / `昔映`  

#### 配置刷机工具
在 `DriverAssitant` 文件夹下打开 `DriverInstall.exe` （瑞芯微驱动助手） ,根据指引安装驱动  

在 `RkDevTool` 文件夹下打开 `RKDevTool.exe` （瑞芯微开发工具）  

![RkDevTool（瑞芯微开发工具）v3.31](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/B65TEU-WnOGcT4)  

如上图所示，可能需要修改第一、二项的内容：  
- `地址` 分别更改为 `0xCCCCCC` 、 `0x000000`  
- `名字` 分别更改为 `loader` 、 `system`  
- `路径` 部分要点击后方的小白块，分别更改为 `MiniLoaderAll_oect.bin` 、 `Armbian` 的所在路径  

> 若存在 `强制按地址写` ，请勾选上  



#### 短接
使用 `USB-A to Type-C 数据线` ， `Type-C端` 接入OEC(T)的Type-C接口  

![2.2.2](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/o-t7Fg3_aaprd0)  

然后找到你的设备对应的短接点（版本号所在位置如下图所示）：  
![OEC版本](https://sway.cloud.microsoft/s/4aEiTpcBD4PPvwex/images/zXPlfD5hFT-M1m)  

**OEC L1.0版本**：  
![OEC L1.0版本](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/Jx2zeR2bnaS8oQ)  

**OEC-1.1版本**：  
![OEC-1.1版本](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/7gmbRKUYrvvy0S)  

**OEC L2.0版本**：  
![OEC L2.0版本](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/jT61u2lSva4mEB)  

**OEC L2.1版本**：
> 该版本尚未找到相应资料，可尝试其他版本的短接点  

使用镊子等工具对短接点进行短接，同时 `USB-A端` 接入电脑  

直到电脑检测到设备后立即松开，并在 `RkDevTool（瑞芯微开发工具）` 中点击 `执行`  

> Tips:  
> 1.通常情况下，该方法是可行的  
> 2.若遇到短接时检测不到，松开后就检测到的情况，可选择更换短接点（或者在接入电脑后，OEC(T)设备亮灯的瞬间短接几秒，然后松开）  

等待右侧的信息输出，若提示 `下载完成` ，即刷入成功  
> Tips：  
> 1.Armbian镜像一般在5-7GB左右（应该是?），大概需要等待五分钟左右  
> 2.若不确定是否在刷入，可在 `任务管理器` 查看硬盘的读写量  

![RkDevTool（瑞芯微开发工具）v3.31](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/B65TEU-WnOGcT4)  






### 后续更换系统
> 此时OEC(T)设备系统为 `第三方系统`  

#### 配置刷机工具
在 `DriverAssitant` 文件夹下打开 `DriverInstall.exe` （瑞芯微驱动助手） ,根据指引安装驱动  

在 `RkDevTool` 文件夹下打开 `RKDevTool.exe` （瑞芯微开发工具）  

![RkDevTool（瑞芯微开发工具）v3.31](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/B65TEU-WnOGcT4)  

其中，第一项（ `0xCCCCCC` & `loader` ）不要勾选  

第二项要修改的内容：  
- `地址` 更改为 `0x000000`  
- `名字` 更改为 `system`  
- `路径` 部分要点击后方的小白块，更改为 `系统镜像` 的所在路径  

> ~~若存在 `强制按地址写` ，请勾选上~~  



#### 刷入系统镜像
使用 `USB-A to Type-C 数据线` ， `Type-C端` 接入OEC(T)的Type-C接口  

按下 `reset` 按钮，同时 `USB-A端` 接入电脑  

直到电脑检测到设备后立即松开，并在 `RkDevTool（瑞芯微开发工具）` 中点击 `执行`  

等待右侧的信息输出，若提示 `下载完成` ，即刷入成功  
> Tips：  
> 1.Armbian镜像一般在5-7GB左右（应该是?），大概需要等待五分钟左右  
> 2.若不确定是否在刷入，可在 `任务管理器` 查看硬盘的读写量  

![RkDevTool（瑞芯微开发工具）v3.31](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/B65TEU-WnOGcT4)






### 挂载硬盘
#### 第一步：临时挂载
1.显示系统中可用存储设备、磁盘分区等相关信息  
```Shell
lsblk
```
![2.3.1](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/LZ3MOZmYxh5jRZ)  
> 用的是玩客云那篇文章的截图，方便 ~~（绝对不是我想偷懒）~~  

由上图可知，我的硬盘名称是 `sda1`  

> 若硬盘是全新的，请执行 `mkfs.ext4 /dev/sda1` 命令（格式化为 ext4）进行格式化（若存在数据，可跳过此步）  


2.创建一个文件夹(挂载点)，用于挂载硬盘  
```Shell
mkdir /mnt/disk
 # 文件夹名disk可更换，依个人喜好就好~
```


3.挂载硬盘  
```Shell
mount /dev/sda1 /mnt/disk
 # 不要忘记把 sda1 & disk 换成你自己的！
```
挂载成功后一般无提示，若不确定是否挂载，可执行以下命令查看：  
```Shell
df -h
```



#### 第二步：永久挂载
> 即，设备开机时自动挂载  

1.查询硬盘uuid及文件系统  
```Shell
blkid /dev/sda1
```


2.根据硬盘信息制作出开机硬盘自动挂载命令  
```Shell
UUID=你的硬盘UUID /mnt/disk 文件系统格式 defaults,noatime,nofail 0 0

 # 例（不要忘记换成自己的）
UUID=80278b04-2d19-984c-bdce-65ab443908ab /mnt/disk ext4 defaults,noatime,nofail 0 0
```

> 一些说明：  
> - `defaults`:使用默认挂载参数（rw, suid, dev, exec, auto, nouser, async）   
>   - `rw`: 读写模式  
>   - `suid`: 允许 `SUID` 和 `SGID` 位生效  
>   - `dev`: 允许解析设备文件  
>   - `exec`: 允许执行该分区上的二进制文件  
>   - `auto`: 允许在启动时通过 `mount -a` 自动挂载  
>   - `nouser`: 只允许 root 用户挂载该文件系统  
>   - `async`: 使用异步 I/O 操作  
> - `noatime`:禁止在每次读取文件时更新其“访问时间 (atime)”元数据（减少对硬盘的写入次数）  
> - `nofail`:若该设备不存在或无法挂载，启动时系统不会报错并继续启动流程，而不是等待或进入紧急恢复模式  
> - `第一个数字 0` : 表示不使用 `dump` 这个古老的备份工具进行备份  
> - `第二个数字 0` : 表示不使用 `fsck` 工具检查文件系统的完整性（若设置为 `2` 时，则表示系统在启动时会检查这个文件系统，但优先级低于根文件系统 (根文件系统设为 `1` ) ）  


3.编辑磁盘挂载配置文件，将上一步制作出的命令添加到末行  
```Shell
# 先备份再编辑配置文件
cp /etc/fstab /etc/fstab.backup
nano /etc/fstab
```
或  
```Shell
# 先备份再编辑配置文件
cp /etc/fstab /etc/fstab.backup
vi /etc/fstab
```
> Tips:vi编辑命令使用方法  
> 1.使用键盘方向键调整光标位置  
> 2.按下Insert键(或按下 `i键` )，可以见到窗口左下角有 `Insert` 字样，表示当前为插入编辑状态  
> 3.编辑完内容后，按下`Esc键`，输入 `:wq` 再按回车可以保存并退出编辑，而输入 `:q!` 回车则取消保存  


4.测试硬盘是否挂载成功（如果报错千万不要重启，会导致进不了系统）  
```Shell
mount -a
```






## 常见问题
### 下载BOOT失败
一般多试几次就可以了  

> 若多次尝试后均未成功，可参考本文的 `#刷机` 部分  


### 测试设备失败
一般现象为在 `BOOT下载` 成功后, 执行到"测试设备"时提示 `测试设备失败`  

这说明 `BOOT` 已经写进去了并且板子也启动了, 但是从上位机去检查板子的 `USB接口` 失败了，可再多试几次  

> 但也可能是写入的 `MiniLoaderAll.bin` 不合适, 没有正常启动板子的USB口，可选择换一个 `MiniLoaderAll.bin` 试试  


### Armbian的账户密码
默认用户： `root`  
默认密码： `1234`  


### MASKROM设备 与 LOADER设备
在OEC(T)设备为 `原厂系统/昔映` 时，则会提示为 `MASKROM设备`  
在OEC(T)设备为 `第三方系统` 时，则会提示为 `LOADER设备`  



### 设备内部结构图
> 图片来自互联网  

【OEC-1.1】PCB正面：  
![【OEC-1.1】PCB正面](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/7NUjte4WTW2Caf)  

【OEC-1.1】PCB背面：  
![【OEC-1.1】PCB背面](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/qneqPMUqrNvgug)  

PCB背面：  
![PCB背面](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/WbSomNUjrFcH33)  

PCB背面 - `瑞芯微芯片RK3566`：  
![PCB背面 - 瑞芯微芯片RK3566](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/hzTFepOpesQa4m)  

PCB背面 - `瑞昱网卡芯片RTL8211F`：  
![PCB背面 - 瑞昱网卡芯片RTL8211F](https://sway-cdn.com/s/4aEiTpcBD4PPvwex/images/9q8li0STsR0z5u)  






## 参考资料
 - [Add wxy OEC-turbo by andyfanybo · Pull requests #2736 · ophub/amlogic-s9xxx-armbian - Github](https://github.com/ophub/amlogic-s9xxx-armbian/pull/2736#issuecomment-2594792433)  
 - [网心云 OEC/OECT 刷armbian - Codfish Blog](https://codfish.top/posts/wxy-oect/)  
 - [网心云 OEC/OECT 笔记(1) 拆机刷入Armbian固件 - CSDN博客](https://blog.csdn.net/michaelchain/article/details/148357445)  
 - [[重发/线刷包]适用于OEC，带VPU，灯控等的Debian Armbian - 恩山无线论坛](https://www.right.com.cn/forum/thread-8421861-1-1.html)  
 - [网心云OEC/OEC-turbo刷机各类问题汇总/下载boot失败/测试设备失败/短接的三个版本](https://www.right.com.cn/forum/thread-8441601-1-1.html)  
 - [网心云OEC/OEC-turbo刷机问题——刷机教程、救砖方法、技术要点及下载boot失败异常解决尝试 - CSDN博客](https://blog.csdn.net/John_Lenon/article/details/146461220)  
 - [OecTurbo1.0刷机Armbian错误记录和解决办法（可能你需要） - 恩山无线论坛](https://www.right.com.cn/forum/forum.php?mod=viewthread&tid=8442639)  
 - [不到100块拥有全能NAS，保姆级低功耗家庭服务器搭建指南 - BiliBili](https://www.bilibili.com/video/BV1UAuuzyEZe/)  
 - [OECTurbo 刷机短接点新方法 - 恩山无线论坛](https://www.right.com.cn/forum/thread-8445911-1-3.html)  






## 后记
总耗时两天......  

虽然内容还是不够全（参考资料和实践设备不够，悲），但总体上还算说得过去(？)  