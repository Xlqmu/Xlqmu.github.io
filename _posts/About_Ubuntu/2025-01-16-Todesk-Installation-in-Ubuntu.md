---
layout:     post
title:      "Ubuntu 中安装 Todesk"
subtitle:   "Todesk Installation in Ubuntu"
date:       2025-01-16 16:16:00
author:     "Xlqmu"
tags:
    - Ubuntu
    - 常用软件安装
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[远程桌面-Todesk](https://flowus.cn/lihanchen/share/cdc79eb7-2a19-4bd9-9c38-09e4ec86eb7e?code=4PP1RS)

上次更新：@2023/12/25 20:38

## 一. 安装 Todesk

浏览器搜索 [Todesk](https://www.todesk.com/linux.html) 官网，按照官网步骤安装即可

但配置完成后尝试远程控制，会出现：

*当前系统并无桌面环境、或无显示器，无法显示远程桌面，您需要自行安装 X11 桌面环境，或者您仍然可以使用终端、文件传输功能*

需要将 Ubuntu 桌面转换为 X11 ，具体步骤如下：

### 1.1 修改配置文件，关闭 wayland

```Shell
sudo nano /etc/gdm3/custom.conf
```

将 `WaylandeEnable=false` 前的 `#` 号 **删除**

![image1.png](/img/in-post/About_Ubuntu/Todesk-Installation-in-Ubuntu/image1.png)

Tips: `Ctrl + X` 离开；`Y` 保存

### 1.2 重启

```Shell
sudo reboot
```

重启完成后，Todesk 就可以远程连接了

### 1.3 番外

CLH：我怎么人一离开 501，这B Todesk 就连不上 minipc ？
所以，记得配置一下**虚拟显示器**！
否则 minipc 外接显示器关闭后，远程桌面将无法正常显示

- 参考博客
  
    [Ubuntu20.04 虚拟显示器配置，解决Ubuntu无显示器时nomachine/vnc/Teamviwer等远程终端桌面卡顿问题_ubuntu虚拟显示器_鳄鱼儿的博客-CSDN博客](https://blog.csdn.net/Ber_Bai/article/details/127768374)

#### 1.3.1 配置虚拟显示屏

1. 安装 xserver-xorg
   
   ```Shell
   sudo apt-get install xserver-xorg-core-hwe-18.04
   sudo apt-get install xserver-xorg-video-dummy
   ```

2. 增加 xorg 配置文件
   
    通过指令 `sudo vim /usr/share/X11/xorg.conf.d/xorg.conf` ，添加以下内容。
   
   ```Shell
   Section "Monitor"
       Identifier "Monitor0"
       HorizSync 28.0-80.0
       VertRefresh 48.0-75.0
       Modeline "1920x1080_60.00" 172.80 1920 2040 2248 2576 1080 1081 1084 1118 -HSync +Vsync
   EndSection
   Section "Device"
       Identifier "Card0"
       Driver "dummy"
       VideoRam 256000
   EndSection
   Section "Screen"
       DefaultDepth 24
       Identifier "Screen0"
       Device "Card0"
       Monitor "Monitor0"
       SubSection "Display"
       Depth 24
       Modes "1920x1080_60.00"
       EndSubSection
   EndSection
   ```
   
    `Ctrl+Shift+V` 粘贴后，连续按两次 `Esc` ，输入 `:wq` 即可**存盘并退出**
   
    教程里涉及到 vim 编辑器的使用，可以查阅 **[vim编辑器的基本使用](https://blog.csdn.net/hsforpyp/article/details/113833465)**

3. 创建一个文件夹，**当不需要使用虚拟屏幕时**，可以将配置文件放到 `no_use_conf` 文件夹中，从而关闭虚拟屏幕
   
   ```Shell
   cd /usr/share/X11/xorg.conf.d/
   sudo mkdir no_use_conf
   ```

#### 1.3.2 **重启**

    重启后将自动启用虚拟显示屏。

#### 1.3.3 恢复真实显示器

如果之后需要启用真实外置屏幕，
将 `/usr/share/X11/xorg.conf.d/` 中的 `xorg.conf` 文件移除，再重启机器即可。

- 法一：命令行操作方式：
  
  ```Shell
  sudo mv /usr/share/X11/xorg.conf.d/xorg.conf /usr/share/X11/xorg.conf.d/no_use_conf
  ```
  
  ```Shell
  sudo mv /usr/share/X11/xorg.conf.d/no_use_conf/xorg.conf /usr/share/X11/xorg.conf.d/xorg.conf 
  ```

- 法二：图形化界面操作方式：
  
    由于文件存于系统目录下，需要使用管理员权限才能删除
  
    输入以下命令，将以管理员身份打开文件窗口，找到并删除对应的文件即可
  
  ```Shell
  sudo nautilus
  ```

## 二. 一种非常坏的情况

假如，已经设置了虚拟屏幕，某天 minipc 没网了，无法远程桌面也无法连接外置屏幕。

> 别问，问就是踩坑过...

- **解决方法：** 在 U 盘安装 Ubuntu 系统，用 U 盘作为启动盘读取并修改 minipc 中的文件

### 2.1 制作U盘启动系统

下载软件 [Rufus](https://rufus.akeo.ie)

按照如图设置后，软件会把 `ubuntu-20.04.2-desktop-amd64.iso` 文件，写入U盘，制作系统启动盘。（注：最好是空 U 盘，否则会被格式化）

![image2.png](/img/in-post/About_Ubuntu/Todesk-Installation-in-Ubuntu/image2.png)

用推荐方式就行，直接ok

![https://img-blog.csdnimg.cn/3770f5ba04524b16b0f40d6b6fd9adcd.png](/img/in-post/About_Ubuntu/Todesk-Installation-in-Ubuntu/3770f5ba04524b16b0f40d6b6fd9adcd.png)

选是就好

![https://img-blog.csdnimg.cn/8d761d327e714bf1a483fe4e26c13029.png](/img/in-post/About_Ubuntu/Todesk-Installation-in-Ubuntu/8d761d327e714bf1a483fe4e26c13029.png)

点击确定，开始烧录

![https://img-blog.csdnimg.cn/b8dc9a27020f43fd84868a4082efcbfa.png](/img/in-post/About_Ubuntu/Todesk-Installation-in-Ubuntu/b8dc9a27020f43fd84868a4082efcbfa.png)

### 2.2 启动U盘Ubuntu系统

启动 minipc ，进入bios ，选择你的启动盘（例如 Kingston... ）

**Intel NUC中，按F10键**

U 盘启动后会弹出 Ubuntu 的配置页面，不要 `Install` ，**选择 `Try Ubuntu`** 

### 2.3 删除虚拟屏幕配置文件

注意，文件管理中有两个磁盘，**选择较大的磁盘**，才是 minipc 的存储盘

由于文件存于系统目录下，需要使用管理员权限才能删除

```Shell
sudo nautilus
```

在 `/usr/share/X11/xorg.conf.d/` 目录中，**删除 / 移动** `xorg.conf` 文件即可

Tips:  在文件管理页面中，快捷键 `Ctrl+L` 输入文件路径



**本文fork自** [Ubuntu 中安装 Todesk - 陈立憨（派大星）的博客 | LihanChen Blog](https://lihanchen2004.github.io/2024/05/02/Todesk-Installation-in-Ubuntu/)