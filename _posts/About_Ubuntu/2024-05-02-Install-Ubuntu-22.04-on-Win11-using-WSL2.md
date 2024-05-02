---
layout:     post
title:      "Win11 使用 WSL2 安装 Ubuntu22.04"
subtitle:   "Install Ubuntu 22.04 on Win11 using WSL2"
date:       2024-05-02 13:30:00
author:     "陈立憨"
tags:
    - Ubuntu
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[Win11 使用 WSL2 安装 Ubuntu22.04](https://flowus.cn/lihanchen/share/8f7b8faf-da59-4df9-8013-dff334c4038b?code=4PP1RS)

开发人员可以在 Windows 计算机上同时访问 Windows 和 Linux 的强大功能。 通过适用于 Linux 的 Windows 子系统 (WSL)，开发人员可以安装 Linux 发行版（例如 Ubuntu、OpenSUSE、Kali、Debian、Arch Linux 等），并直接在 Windows 上使用 Linux 应用程序、实用程序和 Bash 命令行工具，不用进行任何修改，也无需承担传统虚拟机或双启动设置的麻烦。

官方文档：[安装 WSL](https://learn.microsoft.com/zh-cn/windows/wsl/install)


# 一. WSL2 安装教程

[Win11 WSL2 安装教程](https://lihanchen2004.github.io/2024/05/02/Win11-WSL2-Installation-Tutorial/)

# 二. 将 WSL2 从 C 盘迁移至其他盘

[将 WSL2 从 C 盘迁移至其他盘](https://lihanchen2004.github.io/2024/05/02/Move-WSL2-from-C-Drive-to-Another-Drive/)


# 三. 搭建舒适的开发环境

## 3.1 VScode 插件

WSL扩展允许你在Windows上使用VS Code来构建运行在Windows子系统(WSL)上的Linux应用程序。在使用基于linux的工具、运行时和实用程序进行开发时，您可以获得Windows的所有生产力。

WSL扩展允许你在WSL中使用VS Code，就像你在Windows中使用一样。

1. 安装 WSL VScode 插件

    ![image1.png](/img/in-post/About_Ubuntu/Install-Ubuntu-22.04-on-Win11-using-WSL2/image1.png)

1. 使用插件连接到 WSL

    ![image2.png](/img/in-post/About_Ubuntu/Install-Ubuntu-22.04-on-Win11-using-WSL2/image2.png)

## 3.2 安装 WSLg （在 WSL2 运行 Linux GUI 应用）

[learn.microsoft.com](https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/gui-apps)


Windows Subsystem for Linux GUI 是在 WSL 中使用 Linux 图形界面程序的一种方式，可以在 WSL 中任意使用 Linux 的图形界面程序。

WSLg 需要电脑已经安装了 WSL 2 内核组件。

设置完成后，就可以在 Windows 中弹出 Rviz2，文本编辑器...... 的图形化界面啦

在 **Windows** 中，使用**管理员 / Administrator 身份**打开 cmd 或 powershell，运行：

```Shell
wsl --update
```

```Shell
wsl --shutdown
```

## 3.3 一键安装ROS、Docker、换源等

```Shell
wget http://fishros.com/install -O fishros && . fishros
```

然后就可以愉快地开始 Windows 下的 Ubuntu 开发工作啦

# 四. 番外（选修篇）

## 4.1 在 WSL2 下连接 Livox 雷达

[在 WSL2 下连接 Livox 雷达](https://lihanchen2004.github.io/2024/05/02/Connect-Livox-Lidar-under-WSL2/)

## 4.2 安装 gnome-terminal

在 **WSL2** 中输入命令：

```Shell
sudo apt install gnome-terminal
```

安装后，你可以使用类似以下的脚本启动命令：

```sh
cmds=(  "ros2 launch pb_rm_simulation rm_simulation.launch.py world:=RMUC"
    "ros2 launch linefit_ground_segmentation_ros segmentation.launch.py" 
    "ros2 launch fast_lio mapping_mid360.launch.py rviz:=false"
    "ros2 launch pointcloud_to_laserscan pointcloud_to_laserscan_launch.py"
    "ros2 launch icp_localization_ros2 bringup.launch.py"
    "ros2 launch rm_navigation bringup_launch.py")

for cmd in "${cmds[@]}";
do
    echo Current CMD : "$cmd"
    gnome-terminal -- bash -c "cd $(pwd);source install/setup.bash;$cmd;exec bash;"
    sleep 0.2
done
```

