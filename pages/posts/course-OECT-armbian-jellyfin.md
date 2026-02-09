---
title: 网心云OECT（RK3566）搭建Jellyfin&启用视频硬解
date: 2026-02-09
categories: 技术教程
tags: 
 - 网心云
 - 网心云OECT
 - NAS
 - Armbian
excerpt_type: html
---
> 本文记录的比较匆忙，内容可能存在错误，还请见谅






## 准备
- 网心云OECT（Armbian系统）  
> 本文使用的系统为 [ Flash_Armbian_25.05.0_rockchip_efused-wxy-oec_bookworm_6.1.99_server_2025.03.20 - 123云盘](https://www.123865.com/s/BOa8Vv-TDf7A)  
- Jellyfin的Docker镜像  






## 正文
> 如果需要 `网心云OECT` 刷机教程，请查看 [网心云OEC/OECT刷入Armbian](https://blog.dmoe.top/posts/course-OECT-armbian)  

### 安装1Panel
您也可以在 [1Panel官网](https://1panel.cn/) 获取安装方法  

以下是一键安装指令：  
```Shell
bash -c "$(curl -sSL https://resource.fit2cloud.com/1panel/package/v2/quick_start.sh)"
```



### 安装Jellyfin
> Tips：  
> 官方镜像 [jellyfin/jellyfin - Docker Image](https://hub.docker.com/r/jellyfin/jellyfin) 目前并不支持调用网心云OECT的GPU，可使用 [nyanmisaka/jellyfin - Docker Image](https://hub.docker.com/r/nyanmisaka/jellyfin) 的 `latest-rockchip` 分支

将 `docker-compose.yml` 文件中的 `devices` & `image` 部分修改为以下内容：
```docker-compose.yml [Docker ~vscode-icons:file-type-docker2~]
    devices:
      - /dev/dri:/dev/dri
      - /dev/dma_heap:/dev/dma_heap
      - /dev/mpp_service:/dev/mpp_service
      - /dev/rga:/dev/rga
    image: nyanmisaka/jellyfin:latest-rockchip
```



### Jellyfin配置
在 `Jellyfin` 首页通过侧边栏进入 `控制台`  ，找到 `播放` - `转码`  

将 `硬件加速` 修改为 `Rockchip MPP (RKMPP)`  

`启用硬件编码` 部分可全部勾选，然后保存  
> `AV1` 可不勾选（?）  

是否配置成功请自行寻找视频资源测试  
> Tips：可通过 `WEB端` / `客户端` 的视频播放器的视频信息来查看  






## 参考资料
- [Orange 3B Jellyfin使用RK3566硬解4K视频 - Astarry技术日记](https://blog.astarry.cn/archives/822eb31f-cda3-4805-8a70-51879b9a96ec)
- [不到70块的NAS能硬解4K？RK3566jellyfin的安装和GPU调用 - Bilibili](https://www.bilibili.com/video/BV1W236zYEHU)






## 后记
~~新年的第二文章居然是水出来的（~~  

有两个令我疑惑的问题：  

- 网心云OEC和OECT这两个型号的芯片不同吗？目前我能查到的资料无法解答我的疑惑Orz  

- 不同的支持RK3566视频硬解的Armbian系统镜像，`docker-compose.yml` 文件中的 `devices` 配置不一样吗？~~（这对吗？）~~  

最后，提前祝各位春节快乐~  