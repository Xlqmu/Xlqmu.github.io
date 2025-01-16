---
layout:     post
title:      "在 minipc 中安装 Ubuntu 系统"
subtitle:   "Install Ubuntu System on Minipc"
date:       2025-01-16 23:16:03
author:     "Xlqmu"
tags:
    - Ubuntu
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[在 minipc 中安装 Ubuntu 系统](https://flowus.cn/lihanchen/share/14e45e2b-c824-4ef1-a689-a373de834cde?code=4PP1RS)

**官方文档链接：[在minipc中安装Ubuntu系统](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview)**

## 1. 概述

在本教程中，我们将指导您完成在笔记本电脑或 PC 上安装 Ubuntu 桌面所需的步骤。

### 硬件需求

- 具有至少 25GB 存储空间的笔记本电脑或 PC。

- 闪存驱动器（建议使用 12GB 或以上）。

虽然 Ubuntu 适用于各种设备，但建议您使用 [Ubuntu 认证硬件](https://ubuntu.com/certified?q=&limit=20&category=Desktop&category=Laptop) 页面上列出的设备。这些设备已经过测试并确认可以与 Ubuntu 很好地配合使用。

如果您在以前使用的 PC 或笔记本电脑上安装 Ubuntu，始终建议在安装之前备份数据。

## 2. 下载 Ubuntu 镜像

您可以[在此](https://ubuntu.com/download/desktop)下载 Ubuntu 镜像。请确保将其保存到计算机上易记的位置！在本教程中，我们将使用 Ubuntu 23.04 版本，该版本使用新的 Ubuntu 桌面安装程序，该安装程序将包含在所有未来的 Ubuntu 发行版中。

如果您正在安装旧版本的 Ubuntu，例如 Ubuntu 22.04 LTS，则会发现安装程序的视觉呈现方式不同，但总体流程应该保持相同。

![image1.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img1.jpeg)

## 3. 创建可启动的 U 盘

要安装 Ubuntu 桌面，您需要将下载的 ISO 写入 U 盘以创建安装介质。这与复制ISO不同，需要一些定制软件。

[balenaEtcher - Flash OS images to SD cards & USB drives](https://etcher.balena.io/#download-etcher)

![image2.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img2.png)

选择您下载的 ISO，选择您的 USB 闪存驱动器，然后单击 **Flash！** 以安装您的映像。

![image3.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img3.png)

> **从 DVD 安装 Ubuntu** 
> 也可以从 DVD
> 按照这些指南在[Windows](https://ubuntu.com/tutorials/burn-a-dvd-on-windows)，[MacOS](https://ubuntu.com/tutorials/burn-a-dvd-on-macos)或Ubuntu上刻录[Ubuntu](https://ubuntu.com/tutorials/burn-a-dvd-on-ubuntu)安装DVD，然后在以下步骤的启动选项屏幕上选择CD驱动器而不是USB设备。

## 4. 从 U 盘启动

将 USB 闪存驱动器插入要用于安装 Ubuntu 的笔记本电脑或 PC，然后启动或重新启动设备。它应该自动识别安装介质。如果没有，请尝试在启动过程中按住 F12，然后从系统特定的启动菜单中选择 USB 设备。

CLH：**Intel NUC中，按 F10 键！**

> F12 是调出系统启动菜单的最常见键，但 Escape、F2 和 F10 是常见的替代方案。如果您不确定，请在系统启动时查找一条简短的消息 - 这通常会通知您按哪个键来调出启动菜单。

安装程序初始化后，选择您的语言

CLH：建议用**English**，防止中文路径招来虫子

![image4.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img4.png)

![image5.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img5.png)

系统将要求您选择键盘布局。选择一个后，单击**继续**。

![image6.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img6.png)

接下来，您将被要求连接到 Wi-Fi，这将允许 Ubuntu 在安装过程中下载更新和第三方驱动程序（如 NVIDIA 显卡驱动程序）。一旦您连接到 Wi-Fi（或选择离线进行），我们就可以继续进行安装设置。

### （警报）RST 已启用

**CLH：实测，Intel NUC 未出现这种情况，跳过本小节即可**

一些电脑使用英特尔 RST（快速存储技术），这种技术不受 Ubuntu 支持。如果是这种情况，您将无法继续进行，除非在计算机的 BIOS 菜单中禁用 RST。如果遇到此弹出窗口，请访问 [help.ubuntu.com/rst](https://help.ubuntu.com/rst/) 以获取更多信息。

![image7.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img7.png)

## 5. 安装设置

系统将提示您在**“普通安装”**和**“最小安装”**选项之间进行选择。最小安装对于那些具有较小硬盘驱动器或不需要那么多预安装应用程序的用户很有用。

在**其他选项**中，您将被提示在安装过程中下载更新以及第三方软件，这些软件可能会提高设备的支持和性能（例如，Nvidia 显卡驱动程序）。**建议勾选这两个复选框**。

![image8.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img8.png)

## 6. 安装类型

此屏幕允许您配置安装。如果您希望 Ubuntu 成为硬盘驱动器上唯一的操作系统，请选择擦除**磁盘并安装 Ubuntu**。

如果您的设备当前安装了其他操作系统，您将收到其他选项，用于在该操作系统旁边安装 Ubuntu，而不是替换它。

![image9.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img9.png)

### 将 Ubuntu 与另一个操作系统一起安装

如果您选择此选项，您将获得一个简单的界面，允许您选择要安装 Ubuntu 的驱动器和一个滑块来确定您希望 Ubuntu 使用的磁盘空间量。可用空间受磁盘现有内容的限制，旨在避免覆盖现有文件。

此视图自动选择驱动器上最大的分区。要进行更精细的控制，您可以切换到下面详述的*手动分区*选项。

![image11.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img11.png)

### 擦除磁盘并安装 Ubuntu

如果选择此选项，Ubuntu 将占用所选驱动器上的整个磁盘空间。

![image12.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img12.png)

如果您的 PC 有多个硬盘驱动器，那么此选项允许您将 Ubuntu 与现有操作系统一起安装，只要它们都有自己的驱动器。请注意确保您在这种情况下选择了正确的驱动器！

此选项还允许您使用 LVM 加密整个驱动器。为此，请在进入上述屏幕之前打开“高级功能”选项，然后选择“加密新的 Ubuntu 安装以确保安全”

![image13.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img13.png)

> LVM 代表 逻辑卷管理。通过在安装过程中使用 LVM，可以更轻松地在安装后创建和管理分区。

在以下步骤中，系统将提示您创建一个安全密钥，您需要在使用用户凭据登录之前在启动时输入该密钥。

![image14.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img14.png)

如果您选择加密，重要的是不要丢失安全密钥！将其写下来并存储在本地系统之外的安全位置。**没有它，您将无法恢复数据！**

### 手动分区

手动分区专为希望为其用例创建特定配置的高级用户而设计。因此，我们假设这些用户将熟悉此界面，并且不会在本教程中详细介绍特定设置。

在这里，用户可以查看所有现有的驱动器和分区，并创建和管理新的分区表和配置。

![image15.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img15.png)

### (Warn) Windows BitLocker 已启用

如果您的设备启用了Windows BitLocker驱动器加密，则Ubuntu将无法收集与Windows一起安全安装Ubuntu所需的驱动器信息。

如果是这种情况，在重新启动 Ubuntu 安装程序之前，您将收到在 Windows 中禁用 BitLocker 的提示。

![image16.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img16.png)

当完全擦除Windows或有单独的未加密驱动器可用于Ubuntu时，不需要禁用Windows BitLocker。有关详细信息，请参阅本教程末尾的最后一部分。

## 7. 准备安装

无论选择哪个选项，单击“**下一步**”都会转到安装配置的摘要，以便您有机会在单击“**安装**”之前确认设置

![image17.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img17.png)

继续后，Ubuntu 将在后台开始安装过程，您将无法返回这一点。

## 8. 选择您的位置

从地图屏幕中选择您的位置和时区，然后单击**继续**。如果您连接到互联网，则会自动检测到此信息。

![image18.jpeg](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img18.jpeg)

## 9. 创建您的登录详细信息

在此屏幕上，系统将提示您输入您的姓名和计算机的名称，因为它将显示在网络上。最后，您将创建一个用户名和一个强密码。

您可以选择自动登录或要求输入密码。如果您在旅行时使用设备，建议您启用“需要我的密码才能登录”。

![image19.png](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img19.png)

## 10. **马上就好**

重新启动时，系统将提示您从设备中删除 USB 闪存驱动器。完成此操作后，按 **ENTER。**

就是这样，欢迎来到您的新 Ubuntu 桌面！

![image20.jpeg](/img/in-post/About_Ubuntu/Install-Ubuntu-System-on-Minipc/img20.jpeg)

# 恢复你的U盘

使用 [balenaEtcher](https://www.balena.io/etcher/) 配置启动U盘，导致你的U盘似乎“废了”，可通过以下步骤还原你的U盘

[Etcher 似乎把我的 U 盘搞废了，该怎么办？](https://zhuanlan.zhihu.com/p/335090328)



**本文fork自** [在 minipc 中安装 Ubuntu 系统 - 陈立憨（派大星）的博客 | LihanChen Blog](https://lihanchen2004.github.io/2024/05/01/Install-Ubuntu-System-on-Minipc/)
