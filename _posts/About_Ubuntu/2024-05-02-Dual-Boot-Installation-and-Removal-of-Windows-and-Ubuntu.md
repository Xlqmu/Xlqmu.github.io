---
layout:     post
title:      "Window+Ubuntu 双系统安装及删除"
subtitle:   "Dual Boot Installation and Removal of Windows and Ubuntu"
date:       2024-05-02 13:55:00
author:     "陈立憨"
tags:
    - Ubuntu
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[Window+Ubuntu 双系统安装及删除](https://flowus.cn/lihanchen/share/e6735ca6-92fb-4db0-ad6c-54837d87c510?code=4PP1RS)

## 一. 制作Ubuntu安装盘

### 1.1 需要准备的东西

1. 在官网上下载对应的 Ubuntu 镜像文件
2. 找一个闲置且空白的 U 盘或者硬盘（ 4G 及以上）
3. 在官网下载 [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)

### 1.2 操作

打开 [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)，选择镜像文件和设备，之后点击写入即可完成安装盘制作

-  *注意！！！在选择文件类型一栏设置成这样才能找到镜像文件

    ![注意！！！在选择文件类型一栏设置成这样才能找到镜像文件](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/屏幕截图+2023-09-29+152624.png)

- Win32的操作页面

    ![Win32的操作页面](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/屏幕截图+2023-09-29+152702.png)

## 二. Windows 磁盘分区

> 食用视频教程更佳~：[Windows 和 Ubuntu 双系统的安装和卸载](https://www.bilibili.com/video/BV1554y1n7zv/?p=5&share_source=copy_web&vd_source=fdbeaf912252824f68963fa058b7ba54&t=267)


在 Windows 系统，搜索栏输入“磁盘管理”并进入

找到空闲的磁盘，点击压缩卷 **（可以利用删除卷来获取更多空间！！！注意该磁盘内所有内容将清空）**

删除后你将获得一些空闲空间来安装 Ubuntu 系统，这个时候那些空间会变为灰色

建议为 Ubuntu 配置 100GB 的分区，避免后续因 Ubuntu 空间不足而重装系统

![image.png](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/image.png)

## 三. GPT分区形式安装方式

**（注意：还有MBR分区形式的安装方式，在安装前务必查看自己电脑磁盘的分区形式）**

### 2.1 进入BIOS

1. 关机后开机（重启）

2. 插入 Ubuntu 安装盘（之前制作好啦）

3. 进入 BIOS 

    拯救者按 F2 键进入

4. 寻找 `Security Boot` 选项，设置为 `False`

    非常重要！若保持默认为 True ，将导致**无法安装 CUDA 和使用外接显示屏**

5. 在启动栏选择 Windows UEFI 操作系统类型

6. 同时在启动设置中将 U 盘作为第一启动选项

7. 点击退出

### 2.2 选择启动项

1. 在启动选项页面选择U盘安装

    （注意！有的主板需要按动特殊按键才能进入启动选项页面【拯救者不需要】）

    ![这里有一张各个品牌电脑进入启动选项的图](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/18693d99ef00adb796a60084f02b775.jpg)

2. 之后系统会开始自动自检，然后开始安装流程

3. 选择 Install Ubuntu

4. 语言选择**英文**（这样以后的路径都是英文，减少编码阻碍）

5. 之后按照指令一步步连接 WiFi......（亲测不连也影响不大）

    ![Screenshot_20231011_123000.jpg](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/Screenshot_20231011_123000.jpg)

6. **然后来到安装类型界面！（非常重要）**

### 2.3 Ubuntu 分区

安装类型选择“其他选项”，如下图

![你会来到这样一个界面](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/cb00df755bdb7436e3b9c3b9b95b253.jpg)


![进来之后就长这个样子](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/569bdadaf6712df8810b0fd6d8f44ef.jpg)

1. 开始分区

    2. 配置500MB的 EFI 引导区

    3. 配置10G（10000MB）的交换空间

    4. 配置20G+（建议80G以上）的根分区选择根挂载点

    **【这个类似启动盘，一般的软件安装都在这里】**

    Tips: 1GB = 1024MB

2. 选择安装启动引导器 **（找到后缀是 efi 的设备，并把其设置为启动引导器）**

    - 分配500MB的EFI引导区

        ![a. 分配500MB的EFI引导区](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/fd64c3e0f8871395501ce2da760fe20.jpg)
        
    - 分配10G的交换空间（这个可以根据电脑运存决定）8G运存分配10G的交换空间较好

        ![b. 分配10G的交换空间（这个可以根据电脑运存决定）8G运存分配10G的交换空间较好](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/577b82e73117e651a99d5136d2ade29.jpg)

    - 给根挂载点分配内存（非常重要）建议 **80G+ (81920MB+)**，否则以后容量不足需重装系统盘

        ![c. 给根挂载点分配内存（非常重要）建议80G+ (81920MB+)，否则以后容量不足需重装系统盘](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/eb81233c070280b94c4886f1ac41a99.jpg)

    - 选择安装启动引导器（很重要！直接关系到你能否开机！）

        ![d. 选择安装启动引导器（很重要！直接关系到你能否开机！）](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/f5ec220d4d07fde47e79a72275318cb.jpg)

## 四. 其他后续操作

点击现在安装然后按流程选择时间和设置用户账号
**（重启Windows，会发现时间比标准时间慢8小时，可以通过 Windows 同步时间恢复标准时间）**

安装完成以后系统会重启，这个时候拔出安装盘即可完成安装（别忘记按ENTER键！）

恭喜拥有 Windows+Ubuntu 双系统~

## 五. 删除 Ubuntu 系统（UEFI引导）

它这么好你怎么不要它了！呜呜呜......

（有的电脑是 Legancy 引导方式，这里不做讲解）

### 5.1 需要准备的东西

下载 DiskGenius

### 5.2 操作

1. 进入软件找到Linux分区然后删除（选中分区，单击右键，点击彻底删除当前分区）

2. 然后按照上方一样的步骤删除其他Ubuntu分区 （FAT32（Ubuntu）引导区和EXT4 和 Linux标示分区）

    **不要把 Windows 的盘删了！！！**

1. **完成之后一定要点击保存更改（在左上角）【非常重要】**
    
    - Linux分区

        ![Linux分区](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/屏幕截图+2023-09-29+150348.png)

    - EXT4分区

        ![EXT4分区](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/屏幕截图+2023-09-29+150651.png)

### 5.3 回收磁盘空间

点击空闲相邻的磁盘，单击右键，选择扩容磁盘空间（按照指示操作后即可完成）

![大概就是如图这样的界面](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/屏幕截图+2023-09-29+151016.png)

### 5.4 移除 Ubuntu 的引导项

1. 展开左侧系统盘下的EFI分区，找到 Ubuntu 子目录

2. 进入后删除所有的文件 **（单击右键选择彻底删除）**

    **左边有一排目录，找到EFI，进入就可以看见Ubuntu的子目录啦**

    ![左边有一排目录，找到EFI，进入就可以看见Ubuntu的子目录啦](/img/in-post/About_Ubuntu/Dual-Boot-Installation-and-Removal-of-Windows-and-Ubuntu/屏幕截图+2023-09-29+151343.png)

---

- 参考资料：[Windows 和 Ubuntu 双系统的安装和卸载](https://www.bilibili.com/video/BV1554y1n7zv/?p=5&share_source=copy_web&vd_source=fdbeaf912252824f68963fa058b7ba54)