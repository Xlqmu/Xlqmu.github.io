---
layout:     post
title:      "Win11 WSL2 安装教程"
subtitle:   "Win11 WSL2 Installation Tutorial"
date:       2024-05-02 13:40:00
author:     "陈立憨"
tags:
    - Ubuntu
    - WSL2
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[Win11 WSL2 安装教程](https://flowus.cn/lihanchen/share/ecfd58ff-e166-4214-8ac5-bf06d069048d?code=4PP1RS)

官方文档：[安装 WSL](https://learn.microsoft.com/zh-cn/windows/wsl/install)

## Step1 启用适用于 Linux 的 Windows 子系统

![image1.png](/img/in-post/About_Ubuntu/Win11-WSL2-Installation-Tutorial/image1.png)

以管理员身份打开 PowerShell，然后输入以下命令：

```Shell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

![image2.png](/img/in-post/About_Ubuntu/Win11-WSL2-Installation-Tutorial/image2.png)

**重新启动计算机**，然后继续执行下一步。

## Step2 启用虚拟机功能

安装 WSL 2 之前，必须启用“虚拟机平台”可选功能。 计算机需要[虚拟化功能](https://learn.microsoft.com/zh-cn/windows/wsl/troubleshooting#error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed)才能使用此功能。

以管理员身份打开 PowerShell 并运行：

```Shell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**重新启动**计算机，以完成 WSL 安装并更新到 WSL 2。

## Step3 下载 Linux 内核更新包

1. 下载最新包：

    [适用于 x64 计算机的 WSL2 Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

1. 运行上一步中下载的更新包。 （双击以运行 - 系统将提示你提供提升的权限，选择“是”以批准此安装。）

## Step4 将 WSL 2 设置为默认版本

打开 PowerShell，然后在安装新的 Linux 发行版时运行以下命令，将 WSL 2 设置为默认版本：

```Shell
wsl --set-default-version 2
```

## Step5 安装所选的 Linux 分发

1. 打开 [Microsoft Store](https://aka.ms/wslstore)，并选择你偏好的 Linux 分发版。

    ![image3.png](/img/in-post/About_Ubuntu/Win11-WSL2-Installation-Tutorial/image3.png)

1. 首次启动新安装的 Linux 分发版时，将打开一个控制台窗口，系统会要求你等待一分钟或两分钟，以便文件解压缩并存储到电脑上。 未来的所有启动时间应不到一秒。

    ![image4.png](/img/in-post/About_Ubuntu/Win11-WSL2-Installation-Tutorial/image4.png)

1. 然后，需要[为新的 Linux 分发版创建用户帐户和密码](https://learn.microsoft.com/zh-cn/windows/wsl/setup/environment#set-up-your-linux-username-and-password)。

    - 此**用户名**和**密码**特定于安装的每个单独的 Linux 分发版，与 Windows 用户名无关。

    - 请注意，输入**密码**时，屏幕上不会显示任何内容。 这称为**盲人键入**。 你**不会看到你正在键入的内容**，这是完全正常的。

    - 创建**用户名**和**密码**后，该帐户将是分发版的默认用户，并将在启动时自动登录。

    - 此帐户将被视为 Linux 管理员，能够运行 `sudo` (Super User Do) 管理命令。

    - 在 WSL 上运行的每个 Linux 发行版都有其自己的 Linux 用户帐户和密码。 每当添加分发版、重新安装或重置时，都必须配置一个 Linux 用户帐户。

**祝贺你！ 现已成功安装并设置了与 Windows 操作系统完全集成的 Linux 分发！**