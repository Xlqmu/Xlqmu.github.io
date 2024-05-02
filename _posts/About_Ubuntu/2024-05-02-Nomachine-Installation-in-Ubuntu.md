---
layout:     post
title:      "Ubuntu 中安装 Nomachine"
subtitle:   "Nomachine Installation in Ubuntu"
date:       2024-05-02 15:10:00
author:     "陈立憨"
tags:
    - Ubuntu
    - 常用软件安装
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[远程桌面-NoMachine](https://flowus.cn/lihanchen/share/8918e0e3-0371-496f-88d9-5b373d509fa1?code=4PP1RS)

上次更新：@2024/05/02 14:57

相较于 Todesk，Nomachine 可以在本地局域网中直接链接远程桌面

比赛现场 4G/5G 热点干扰极大，可在现场使用本工具连接minipc调试

**NoMachine**是一款**远程桌面软件**。适用于Linux、windows、ARM、Android等几乎全系统。常见的远程桌面软件还有向日葵、ToDesk等。选择NoMachine是因为它**支持ARM32位、ARM64位处理器**。

## 一. 下载并安装 NoMachine

1. 输入 `uname -a` 查看系统架构

    ![截图 2023-11-11 23-03-12.png](/img/in-post/About_Ubuntu/Nomachine-Installation-in-Ubuntu/截图+2023-11-11+23-03-12.png)

2. 前往官网下载对应系统架构的 deb 包

    - [x86_64, amd64](https://downloads.nomachine.com/linux/?id=1)[架构](https://downloads.nomachine.com/linux/?id=1)

    - [arm架构](https://downloads.nomachine.com/linux/?id=30&distro=Arm)

3. 安装

    ```Shell
    cd ~/Downloads
    sudo dpkg -i nomachine*.deb
    ```

## 二. 启动 NoMachine

1. 点击图标 NoMachine 即可，不需要启动 NoMachine Server

    ![Screenshot from 2023-09-29 12-36-15.png](/img/in-post/About_Ubuntu/Nomachine-Installation-in-Ubuntu/Screenshot+from+2023-09-29+12-36-15.png)

2. 此时软件自动搜索到局域网下可连接的设备（被控端也需要安装 NoMachine ）

    ![https://img-blog.csdnimg.cn/img_convert/da9205fd2dfe5a71ebe1f91978b0a233.png](/img/in-post/About_Ubuntu/Nomachine-Installation-in-Ubuntu/da9205fd2dfe5a71ebe1f91978b0a233.png)

3. 双击进行连接。输入要连接的设备的**用户名和密码**

    ![https://img-blog.csdnimg.cn/img_convert/732fece445074a8c68ca8cd340751a20.png](/img/in-post/About_Ubuntu/Nomachine-Installation-in-Ubuntu/732fece445074a8c68ca8cd340751a20.png)

## 三. 常见问题

### 3.1 被控主机能显示在界面，但无法连接

可能是被控主机在局域网内的 IP 地址变了，但是 Nomachine 记录的仍是旧的 IP 地址。

解决方法：在 Nomachine 主界面单击被控主机后，点击 `Edit` ，更新 IP 地址